# Description
- XSS auditor là một công cụ chạy trên trình duyệt nhân chromium giúp bảo vệ người dùng tránh khỏi các cuộc tấn công xss.
- XSS auditor có 2 chế độ là block mode và filter mode
# Exmaple 
- Ta có trang web sau giúp chúng ta tạo ra một chuỗi json thông qua các câu truy vấn GET.
![](https://github.com/huyenlamchiton/owasp/blob/master/Input%20Validation%20Testing/image/adv-5.png)  

- Lợi dụng việc không filter kết quả vào và kết quả ra chúng ta sẽ thực hiện xss.

![](https://github.com/huyenlamchiton/owasp/blob/master/Input%20Validation%20Testing/image/adv-1.png)  

- Đây là kết quả của trình duyệt không có xss auditor:

![](https://github.com/huyenlamchiton/owasp/blob/master/Input%20Validation%20Testing/image/adv-6.png) 

- Như ta đã thấy trang web đã bị xss-auditor chặn lại giúp bảo vệ người dùng tránh khỏi xss. Kiểm tra source code của trình duyệt nhân chromium:  

![](https://github.com/huyenlamchiton/owasp/blob/master/Input%20Validation%20Testing/image/adv-2.png) 

- Trình duyệt đã phát hiện đoạn code được inject. Đối với các trang web khác nhau xss auditor có các cách xử sự khác nhau, chính vì vậy để vượt qua xss auditor là một vấn đề nan giải:

![](https://github.com/huyenlamchiton/owasp/blob/master/Input%20Validation%20Testing/image/adv-3.png)  

![](https://github.com/huyenlamchiton/owasp/blob/master/Input%20Validation%20Testing/image/adv-4.png)  

# References
- https://medium.com/bugbountywriteup/xss-auditor-the-protector-of-unprotected-f900a5e15b7b  
- https://chromium-review.googlesource.com/c/chromium/src/+/1417872  
- (write-up:pwn2win) https://github.com/lbherrera/writeups/tree/master/pwn2win-2019/calc
- (csp+xss auditor+gg jsonp) https://corb3nik.github.io/blog/ins-hack-2019/bypasses-everywhere
- https://drx.home.blog/2019/07/31/xss-cross-site-scripting-part-3-xss-auditor/#more-1104
- (xs-search ggctf) https://github.com/fbsamples/fbctf-2019-challenges/tree/master/web/secret_note_keeper
# Note

-  Tính năng này đã bị vô hiệu hóa vĩnh viễn vào ngày 5 tháng 8 năm 2019 và được gỡ bỏ hoàn toàn cho Chrome 78 (source: https://www.chromium.org/developers/design-documents/xss-auditor)







