# Description
- SQL injection là một kỹ thuật cho phép những kẻ tấn công lợi dụng lỗ hổng của việc kiểm tra dữ liệu đầu vào trong các ứng dụng web và các thông báo lỗi của hệ quản trị cơ sở dữ liệu trả về để dữ liệu và thi hành các câu lệnh SQL bất hợp pháp.  
- Tấn công có thể đọc dữ liệu nhạy cảm từ cơ sở dữ liệu, sửa đổi dữ liệu cơ sở dữ liệu (chèn / cập nhật / xóa), thực thi các thao tác quản trị trên cơ sở dữ liệu.  

![](https://github.com/huyenlamchiton/owasp/blob/master/Input%20Validation%20Testing/image/005-1.png)  

### Ví dụ minh họa
```sql
$query = "SELECT * FROM users WHERE uname = '" + $userName + "' AND password='"+$password+"';";
```
- Câu lệnh này được thiết kế để kiểm tra đăng nhập hoặc thông tin người dùng cụ thể từ bảng những người dùng.
- Tuy nhiên, nếu biến "userName" được nhập chính xác theo một cách nào đó bởi người dùng ác ý, nó có thể trở thành một câu truy vấn SQL với mục đích khác hẳn so với mong muốn của tác giả đoạn mã trên.
- Ví dụ, ta nhập vào giá trị của biến userName như sau: 
```sql
admin' OR 1=1#
```
- Câu truy vấn trở thành:
```sql
SELECT * FROM users WHERE uname = 'admin' OR 1=1 # AND password='';
```
- Câu truy vấn trên sẽ lấy dữ liệu của admin. Điều này vô cùng nguy hiểm!!!
### Có năm kỹ thuật chung để khai thác SQL. Ngoài ra, các kỹ thuật này đôi khi có thể được sử dụng theo cách kết hợp :
- Union query based
- Boolean base
- Error based
- Out-of-band
- Time based
# How to test
#### 1. Phát hiện
- Thêm vào câu truy vấn các meta character trong các hệ quản trị cơ sở dữ liệu, chẳng hạn như dấu nháy đơn (single quote), dấu nháy kép (double quote), dấu chấm phẩy (semi colon) và các ký tự comment (--, ##, /**/)…

![](https://github.com/huyenlamchiton/owasp/blob/master/Input%20Validation%20Testing/image/005-2.png)  



#### 2. Thu thập thông tin về hệ quản trị cơ sở dữ liệu
- Khi phát hiện ứng dụng bị dính lỗi SQL injection, công việc cần làm tiếp theo là thu thập thông tin về hệ quản trị cơ sở dữ liệu mà ứng dụng đang dùng, thông tin này bao gồm loại cơ sở dữ liệu (mysql, mssql, oracle…) và phiên bản của nó.

![](https://github.com/huyenlamchiton/owasp/blob/master/Input%20Validation%20Testing/image/005-3.png)  

#### 3. Xác định số lượng cột trong mệnh đề select
- Ta có thể sử dụng mệnh đề ```order by``` hoặc dùng ```UNION SELECT```  

![](https://github.com/huyenlamchiton/owasp/blob/master/Input%20Validation%20Testing/image/005-4.png)  

- Kết quả trả về lỗi do số lượng cột của 2 mệnh đề select khác nhau. Tăng thêm số lượng cột :

![](https://github.com/huyenlamchiton/owasp/blob/master/Input%20Validation%20Testing/image/005-5.png)  

#### 4. Xác định thông tin
- Sau khi lấy được các thông tin cơ bản, chúng ta sẽ tiến hành khai thác SQL injection để lấy cơ sở dữ liệu hay thực hiện những hành vi khác thông qua lỗ hổng này.
- Ở đây chúng ta sử dụng kĩ thuật UNION BASED.

![](https://github.com/huyenlamchiton/owasp/blob/master/Input%20Validation%20Testing/image/005-6.png)  

- Tiếp tục, lấy tên các bảng trong cơ sở dữ liệu bằng cách sử dụng database information_schema:
```sql
1' union select 1,CONCAT(TABLE_NAME),3 FROM information_schema.TABLES where TABLE_SCHEMA='leettime_761wHole'-- -
```

![](https://github.com/huyenlamchiton/owasp/blob/master/Input%20Validation%20Testing/image/005-7.png)  

- Lấy tên cột:

```sql
-1' union select 1,CONCAT(COLUMN_NAME),3 FROM information_schema.COLUMNS where TABLE_NAME='users'-- -
```

![](https://github.com/huyenlamchiton/owasp/blob/master/Input%20Validation%20Testing/image/005-8.png)  

- Lấy dữ liệu từ bảng:
```sql
-1' union select 1,CONCAT(username,'+',password,'-'),3 FROM users-- -
```

![](https://github.com/huyenlamchiton/owasp/blob/master/Input%20Validation%20Testing/image/005-9.png) 

# Các kĩ thuật khai thác sql
### SQL boolean base
- Boolean based: Cơ sở của kỹ thuật này là việc so sánh đúng sai để tìm ra từng ký tự của những thông tin như tên bảng, tên cột… Khi mà chúng ta không thể sử dụng kĩ thuật UNION BASE


##### Example:
- Trang web sau kiểm tra tham số id. Nếu id tồn tại thì thông báo đăng nhập thành công, ngược lại thì thất bại.  

![](https://github.com/huyenlamchiton/owasp/blob/master/Input%20Validation%20Testing/image/005-10.png) 
![](https://github.com/huyenlamchiton/owasp/blob/master/Input%20Validation%20Testing/image/005-11.png) 

- Bây giờ ta sẽ chèn vào câu truy vấn một mệnh đề true-false.
```sql
-1' OR 1=1 -- -
```
- Như ta đã biết 'flase' OR 'true' eq 'true',  'flase' OR 'false' eq 'false'. Hoặc ta có thể sử dụng AND.

![](https://github.com/huyenlamchiton/owasp/blob/master/Input%20Validation%20Testing/image/005-12.png) 
![](https://github.com/huyenlamchiton/owasp/blob/master/Input%20Validation%20Testing/image/005-13.png)  

- Tiến hành lấy tên cơ sở dữ liệu:

![](https://github.com/huyenlamchiton/owasp/blob/master/Input%20Validation%20Testing/image/005-14.png)  

- Do tên cơ sở dữ liệu rất dài nên chúng ta cần viết một đoạn script để lấy tên cơ sở dữ liệu.

![](https://github.com/huyenlamchiton/owasp/blob/master/Input%20Validation%20Testing/image/005-15.png) 

##### Tối ưu hóa tấn công sql blind
1. Sử dụng thuật toán tìm kiếm nhị phân.
    Việc sử dụng sqlblind truyền thống là đang sử dụng việc tìm kiếm tuần tự. Tức là sẽ tìm kiếm kí tự lần lượt theo bảng chữ cái. Như vậy việc tìm kiếm sẽ rất là tốn thời gian nếu kí tự cần tìm ở cuối danh sách. Ở đây ta sẽ sử dụng thuật toán tìm kiếm nhị phân để tối ưu hóa thời gian tấn công.
    Xét ví dụ trên, ta có payload:
    ```sql
    1' AND ascii(SUBSTR(database(),1,1))<100 -- -
    ```
    payload trên lấy number ascii của chữ cái đầu tiên trong tên của database và so sánh với 100.

    ![](https://github.com/huyenlamchiton/owasp/blob/master/Input%20Validation%20Testing/image/005-16.png)
    ![](https://github.com/huyenlamchiton/owasp/blob/master/Input%20Validation%20Testing/image/005-17.png)

    Như chúng ta thấy chữ cái đầu tiên trong tên của database là "l" tương ứng với number 108 trong bảng mã ascii. Cho nên nếu chúng ta so sánh nó nhỏ hơn 100 thì sẽ nhận được thông báo dạng false, ngược lại ta sẽ nhận được thông báo dạng true.

    ![](https://github.com/huyenlamchiton/owasp/blob/master/Input%20Validation%20Testing/image/005-18.png)
2. Tối ưu hóa bằng cách sử dụng kỹ thuật dịch bit (Bit Shifing)
    Mỗi ký tự đều tương ứng với một giá trị trong bảng mã ASCII. Giá trị này từ 0 đến 127 đối với hệ cơ số thập phân, nếu chuyển sang hệ nhị phân thì giá trị này sẽ được biểu diễn bằng 7 bit
    
