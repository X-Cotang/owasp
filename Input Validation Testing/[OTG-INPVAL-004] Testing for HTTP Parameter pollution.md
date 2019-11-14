# Description
- HTTP parameter pollution (HPP) là một kỹ thuật tấn công web mà kẻ tấn công sẽ tạo ra các tham số trùng nhau trong HTTP request. Lợi dụng các phản ứng khác nhau của các công nghệ web khi xử lý các tham số trùng nhau này để inject những đoạn mã độc hại nhằm tấn công server và người sử dụng.

- Đây là một kỹ thuật đơn giản nhưng khá hiệu quả. Kẻ tấn công có thể lợi dụng kỹ thuật này để:

    * Sửa đổi các tham số HTTP
    * Thay đổi các hành vi của ứng dụng web
    * Truy cập và khai thác các biến không được kiểm soát chặt chẽ
    * Bypass WAF và các cơ chế kiểm tra dữ liệu đầu vào

- Do đó, nếu một ứng dụng web tồn tại lỗ hổng để thực hiện cuộc tấn công HPP, kẻ tấn công có thể dễ dàng chèn các đoạn mã độc hại để tấn công web server cũng như người sử dụng.
- RFC-3986 không quy định cách xử lý tiêu chuẩn cho trường hợp này. Do đó, mỗi công nghệ web khác nhau đưa ra cách xử lý khác nhau cho riêng nó trong trường hợp này.

![](https://github.com/huyenlamchiton/owasp/blob/master/Input%20Validation%20Testing/image/004-1.png)  

VD với xss:

![](https://github.com/huyenlamchiton/owasp/blob/master/Input%20Validation%20Testing/image/adv-5.png)  

![](https://github.com/huyenlamchiton/owasp/blob/master/Input%20Validation%20Testing/image/adv-3.png)  

### Input Validation and filters bypass
```
/index.aspx?page=select 1&page=2,3
```

### Authentication bypass
- Một lỗ hổng HPP thậm chí còn nghiêm trọng hơn đã được phát hiện trong Blogger, nền tảng viết blog phổ biến. Lỗi này cho phép người dùng độc hại chiếm quyền sở hữu blog nạn nhân bằng cách sử dụng yêu cầu HTTP sau:
```
 POST /add-authors.do HTTP/1.1

security_token=attackertoken&blogID=attackerblogidvalue&blogID=victimblogidvalue&authorsList=goldshlager19test%40gmail.com(attacker email)&ok=Invite 
```
# How to test
- Thực hiện kiểm tra đối với các tham số của phương thức GET và POST
### Server-side HPP
1. Gửi yêu cầu HTTP chứa tên và giá trị tham số tiêu chuẩn và ghi lại phản hồi HTTP.
2. Thay thế giá trị tham số bằng giá trị giả mạo, gửi và ghi lại phản hồi HTTP.
3. Gửi yêu cầu mới kết hợp bước (1) và (2). Một lần nữa, lưu phản hồi HTTP  
4. So sánh các câu trả lời thu được trong tất cả các bước trước đó. Nếu phản hồi từ (3) khác với (1) và phản hồi từ (3) cũng khác với (2) có thể kích hoạt các lỗ hổng HPP.  
### Client-side HPP
- Để kiểm tra các lỗ hổng HPP phía máy khách, cần xác định bất kỳ form hoặc hành động nào cho phép người dùng nhập và hiển thị kết quả của đầu vào đó cho người dùng.
- Cách test giống với sever-side HPP
