# Description
- Khác với Reflected tấn công trực tiếp vào một số nạn nhân mà hacker nhắm đến, Stored XSS hướng đến nhiều nạn  nhân hơn. Lỗi này xảy ra khi ứng dụng web không kiểm tra kỹ các dữ liệu đầu vào trước khi lưu vào cơ sở dữ liệu. Do đó, dữ liệu độc hại sẽ xuất hiện là một phần của trang web và chạy trong trình duyệt của người dùng theo các đặc quyền của ứng dụng web.
- Lỗ hổng này có thể được sử dụng để tiến hành một số cuộc tấn công dựa trên trình duyệt bao gồm:
* Đánh cắp thông tin, theo dõi người dùng
* Quét cổng của máy chủ nội bộ ("nội bộ" liên quan đến người dùng ứng dụng web)
* Cướp phiên làm việc của nạn nhân, quản trị viên
* Chuyển hướng người dùng đến các trang web nhằm mục đích khác nhau
* ...
- Kịch bản khai thác:
* Kẻ tấn công lưu trữ mã độc vào trang dễ bị tấn công
* Người dùng truy cập trang dễ bị tổn thương
* Mã độc hại được thực thi bởi trình duyệt của người dùng  

![](https://github.com/huyenlamchiton/owasp/blob/master/Input%20Validation%20Testing/image/002-1.png)  

# Reason
- Server không kiểm soát giá trị input người dùng nhập vào trước khi trả về cho trình duyệt
# Exploit
- Detect : Giống với Reflected cross stire scripting
Thực hiện kiểm tra xem đầu vào của người dùng được ứng dụng xử lý như thế nào trước khi được lưu trữ vào hệ thống back-end bằng các bước sau đây (Graybox):
- Sử dụng ứng dụng front-end và nhập dữ liệu với các ký tự đặc biệt / không hợp lệ
- Phân tích response
- Xác định sự hiện diện của đầu vào
- Truy cập hệ thống back-end và kiểm tra xem đầu vào được lưu trữ và cách nó được lưu trữ
- Phân tích mã nguồn và hiểu cách ứng dụng được lưu trữ, hiển thị nội dung   
# Prevent
- Lọc input và ouput bằng các hàm như replace(), addslashes(), pre_match(), htmlspecialchars(), htmlentities(),stripslashes(),strip_tags(),...

# Example
### Example 1:
![](https://github.com/huyenlamchiton/owasp/blob/master/Input%20Validation%20Testing/image/002-2.png)  

- Ta có trang web như trên
Bây giờ ta nhập "a" vào ô 'Name' input ```<script>alert(document.cookie)<script>``` vào ô 'Message' input  
Kết quả: 

![](https://github.com/huyenlamchiton/owasp/blob/master/Input%20Validation%20Testing/image/002-3.png)  

- Như vậy mỗi lần người dùng vào trang web ,đoạn mã độc được tiêm sẽ được thực thi.  
- Kiểm tra raw response body:

![](https://github.com/huyenlamchiton/owasp/blob/master/Input%20Validation%20Testing/image/002-5.png)

Kiểm tra database:  

![](https://github.com/huyenlamchiton/owasp/blob/master/Input%20Validation%20Testing/image/002-4.png)

Như ta thấy các kí tự đặc biệt nhập vào đã không được encode,filter đúng cách trước khi lưu vào trong database đồng thời dữ liệu trả về cho người dùng cũng không được encode, dẫn đến đoạn mã độc tiêm vào đã được thực thi.  
### Example 2:
Trong ví dụ 2 này 'name' input và 'Message' input đều được filter.  

![](https://github.com/huyenlamchiton/owasp/blob/master/Input%20Validation%20Testing/image/002-6.png)  

Ta thấy 'Message' đã được filter rất chặt chẽ nhưng 'Name' thì không, nên đây sẽ là vector để tấn công.

![](https://github.com/huyenlamchiton/owasp/blob/master/Input%20Validation%20Testing/image/002-7.png)  

![](https://github.com/huyenlamchiton/owasp/blob/master/Input%20Validation%20Testing/image/002-8.png)  

![](https://github.com/huyenlamchiton/owasp/blob/master/Input%20Validation%20Testing/image/002-9.png)  

-Kiểm tra database:

![](https://github.com/huyenlamchiton/owasp/blob/master/Input%20Validation%20Testing/image/002-10.png)

# References  
- [XSS Filter Evasion Cheat Sheet](https://www.owasp.org/index.php/XSS_Filter_Evasion_Cheat_Sheet)