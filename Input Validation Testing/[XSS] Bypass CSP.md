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

- Tab ```<script>``` bị đỏ. Xem nguyên nhân trong tab console:  

![](https://github.com/huyenlamchiton/owasp/blob/master/Input%20Validation%20Testing/image/adv2-5.png)   

- Thì ra CSP đã chặn tài nguyên ở inline!!! :(

![](https://github.com/huyenlamchiton/owasp/blob/master/Input%20Validation%20Testing/image/adv2-6.png)  

- Giá trị ```default-src: 'self'``` chỉ cho phép nạp script từ các file có cùng URL nhưng không cho phép nạp code inline.  

- Bây giờ chúng ta sẽ lợi dụng chính trang này để tạo ra một nguồn script hợp lệ  

![](https://github.com/huyenlamchiton/owasp/blob/master/Input%20Validation%20Testing/image/adv2-7.png)  

![](https://github.com/huyenlamchiton/owasp/blob/master/Input%20Validation%20Testing/image/adv2-8.png)  

![](https://github.com/huyenlamchiton/owasp/blob/master/Input%20Validation%20Testing/image/adv2-9.png)  

- Tiến hành lấy cookie của admin:  

![](https://github.com/huyenlamchiton/owasp/blob/master/Input%20Validation%20Testing/image/adv2-10.png)  

![](https://github.com/huyenlamchiton/owasp/blob/master/Input%20Validation%20Testing/image/adv2-11.png)  

![](https://github.com/huyenlamchiton/owasp/blob/master/Input%20Validation%20Testing/image/adv2-13.png)  

![](https://github.com/huyenlamchiton/owasp/blob/master/Input%20Validation%20Testing/image/adv2-14.png)  

# References
- (google jsonp) https://github.com/jacopotediosi/Writeups/tree/master/CTF/CSAW-Quals-2019/Web/BabyCSP-50
- https://ctftime.org/task/7020
- https://ctftime.org/writeup/16642
- (google jsonp)https://corb3nik.github.io/blog/ins-hack-2019/bypasses-everywhere
- https://jbz.team/inshack2019/Bypasses_Everywhere