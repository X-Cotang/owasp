# Description
- Với số lượng lớn các dự án phần mềm nguồn mở và miễn phí đang tích cực phát triển và triển khai trên toàn thế giới, rất có thể một thử nghiệm bảo mật ứng dụng sẽ phải đối mặt với một trang đích hoàn toàn phụ thuộc hoặc một phần vào các ứng dụng nổi tiếng này (ví dụ Wordpress, phpBB, Mediawiki, v.v.)
- Biết các thành phần ứng dụng web đang được thử nghiệm sẽ giúp ích đáng kể trong quá trình thử nghiệm và cũng sẽ giảm đáng kể nỗ lực không cần thiết trong quá trình thử nghiệm. 
- Các ứng dụng web nổi tiếng này có các tiêu đề HTML, cookie và cấu trúc thư mục đã biết có thể được liệt kê để xác định ứng dụng.

# How to Test
### Cookies
![](https://github.com/huyenlamchiton/owasp/blob/master/Information%20Gathering/image/009-1.png)  

### HTML source code
![](https://github.com/huyenlamchiton/owasp/blob/master/Information%20Gathering/image/009-2.png)  

### Specific files and folders
VD với wordpress:  

![](https://github.com/huyenlamchiton/owasp/blob/master/Information%20Gathering/image/009-3.png)  

# Remediation
- Thay đổi các cookie mặc định
- Làm xáo trộn các HTTP header tiết lộ thông tin về hệ thống
- Xóa, thay đổi các thẻ, comment không cần thiết
- Giới hạn truy cập, thay đổi đường dẫn hoặc xóa các thư mục, file không cần thiết.
- ...