# CSP 
- Ta có ví dụ như sau:
Trang web cho ta nhập vào một chuỗi plaint text và in ra cipher text của mã ceasar.

![](https://github.com/huyenlamchiton/owasp/blob/master/Input%20Validation%20Testing/image/adv2-1.png)

## Idea
Ta sẽ chuyển đổi chuỗi cipher text ```<script>alert(1)</script>``` về plaint text và inject vào trang web đã cho.

![](https://github.com/huyenlamchiton/owasp/blob/master/Input%20Validation%20Testing/image/adv2-2.png)

# Exploit

![](https://github.com/huyenlamchiton/owasp/blob/master/Input%20Validation%20Testing/image/adv2-3.png)

- Oh! Như ta đã thấy không có chuyện gì xảy ra cả.why??? Kiểm tra source ta có:

![](https://github.com/huyenlamchiton/owasp/blob/master/Input%20Validation%20Testing/image/adv2-4.png)  

- Tab ```<script>``` bị đỏ. Xem bảng console:  

![](https://github.com/huyenlamchiton/owasp/blob/master/Input%20Validation%20Testing/image/adv2-5.png)   

- CSP đã chặn tài nguyên ở inline!!! :(

![](https://github.com/huyenlamchiton/owasp/blob/master/Input%20Validation%20Testing/image/adv2-6.png)  

- Giá trị ```default-src: 'self'``` chỉ cho phép nạp script từ các file có cùng URL nhưng không cho phép nạp code inline.  
