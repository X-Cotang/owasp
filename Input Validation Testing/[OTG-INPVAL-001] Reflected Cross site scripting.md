## Description
- Kỹ thuật XSS được thực hiện dựa trên việc chèn các đoạn script nguy hiểm vào trong source code ứng dụng web. Nhằm thực thi các đoạn mã độc Javascript để chiếm phiên đăng nhập của người dùng
- Mã độc được tiêm vào url và gửi đến cho nạn nhân, nạn nhân ấn vào đường link có chứa mã độc và hacker sẽ nhận được response chứa kết quả mong muốn.
![](https://github.com/huyenlamchiton/owasp/blob/master/Input%20Validation%20Testing/image/1%20o_asKsD_JqunhqggHoxodw.png)  

##### Example:
```http://example.com/?search=<script>alert(1)</script>```
## Reason
- Server không kiểm soát giá trị input người dùng nhập vào trước khi trả về cho trình duyệt
- Người dùng sử dụng các trình duyệt đã lỗi thời
- Sự chủ quan, thiếu kiến thức và sự đề phòng của nạn nhân
## Exploit
1. Phát hiện input vector  
    * Đối với mỗi trang web, người kiểm tra phải xác định tất cả các input do người dùng định nghĩa và cách nhập chúng
    * **Các input dễ bị tấn công:** ?search=,?page=,?document=,?user=,...
2. Phân tích từng vector 
    * Người kiểm tra fuzz các kí tự và các từ khóa nhạy cảm,vô hại để phát hiện lỗ hổng trong ứng dụng web.
    * Phát hiện các input cho phép hiển thị kết quả được nhập vào!
    * **Các kí tự nhạy cảm:** <,>,/,script,alert,',...
Example: Input
```
<script>alert(document.cookie)</script>
```
3. Phân tích kết quả
    * Người kiểm tra xác định bất kỳ ký tự đặc biệt nào không được mã hóa, thay thế hoặc lọc đúng
    * Các kí tự HTML đặc biệt cần phải được thay thế bằng HTML entities hoặc replace,encode,...
## Example
### Example 1:
![](https://github.com/huyenlamchiton/owasp/blob/master/Input%20Validation%20Testing/image/001-1.png)  

- Ta có trang web như trên.Trang web cho phép người dùng nhập vào tên và in ra kết quả ra màn hình. Dữ liệu input được gửi lên server bằng phương thức **GET**.Đối với người sử dụng bình thường có thể thấy trang web hoàn toàn hoạt động bình thường.Bây giờ ta sẽ tiến hành nhập thử đoạn javascript đơn giản vào input:```<script>alert(1);</script>```.Kết quả:  

![](https://github.com/huyenlamchiton/owasp/blob/master/Input%20Validation%20Testing/image/001-2.png)  

- Qua hình ảnh trên ta có thể thấy đoạn script ta nhập đã được thực thi.Tiến hành phân tức dữ liệu trả về ta thấy như sau:  

![](https://github.com/huyenlamchiton/owasp/blob/master/Input%20Validation%20Testing/image/001-3.png)  

- Trong quá trình xử lí dữ liệu người dùng nhập vào không dược filter nên dữ liệu server trả về sẽ làm thay đổi DOM của trang Web và đoạn script được thực thi.  

![](https://github.com/huyenlamchiton/owasp/blob/master/Input%20Validation%20Testing/image/001-4.png "dữ liệu xử lí không được filter")
### Example 2:
- Chúng ta sẽ tiếp tục ví dụ trên nhưng ở mức độ nâng cao hơn một chút  

![](https://github.com/huyenlamchiton/owasp/blob/master/Input%20Validation%20Testing/image/001-5.png)  

* Ta sử dụng payload ```<script>alert(1)</script>``` để kiểm tra. Nhưng lần này đoạn code ta inject đã không được thực thi. Thay vào đó kết quả trả về là **Hello alert(1);**. Ấn **ctrl+u** hoặc **f12** kiểm tra raw response:  

![](https://github.com/huyenlamchiton/owasp/blob/master/Input%20Validation%20Testing/image/001-6.png)

* Oh!!! Ta thấy ngay từ khóa ```<script>``` đã bị filter  

![](https://github.com/huyenlamchiton/owasp/blob/master/Input%20Validation%20Testing/image/001-7.png)  

* Đối với dạng filter lỏng lẻo như thế này chúng ta có thể bypass bằng payload có dạng như sau: ```<scr<script>ipt>alert(1);</script>```  

![](https://github.com/huyenlamchiton/owasp/blob/master/Input%20Validation%20Testing/image/001-8.png)
