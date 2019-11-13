# Description  
- Xác định Web framework là một bước rất quan trọng trong quá trình thu thập thông tin. Nó giúp chúng ta xác định các lỗ hổng trong phiên bản hiện tại chưa được vá và các cấu hình sai.  
# How to Test
- Có một số vị trí phổ biến nhất để xem xét để xác định framework hiện tại:  
    * HTTP headers
    * Cookies
    * HTML source code
    * Specific files and folders
    * File Extensions
    * Error Message
### HTTP headers  

![](https://github.com/huyenlamchiton/owasp/blob/master/Information%20Gathering/image/008-1.png)  

Từ trường **X-Powered-By:** ta có thể đoán được ứng dụng sử dụng framework Mono. Tuy nhiên,nó không đúng trong tất cả các trường hợp. Để che dấu thông tin về máy chủ, quản trị viên có thể thêm dòng code:  

```header('x-powered-by: ZendServer 8.5.0,ASP.NET');```  

### Cookies

![](https://github.com/huyenlamchiton/owasp/blob/master/Information%20Gathering/image/008-2.png)  

- Như hình trên ta có thể đoán được ứng dụng sử dụng laravel framwork.  

![](https://github.com/huyenlamchiton/owasp/blob/master/Information%20Gathering/image/008-3.png) 

### HTML source code  
- Từ cách xác định các đường dẫn đến thư mục css,js,image,... hay comment ta có thể xác định được framework  

![](https://github.com/huyenlamchiton/owasp/blob/master/Information%20Gathering/image/008-3.png)  

![](https://github.com/huyenlamchiton/owasp/blob/master/Information%20Gathering/image/008-5.png)  

### File Extensions
- Dựa vào file extension, ta có thể xác định được nền tảng của web. VD laravel framework thường không có extension.

### Specific files and folders
- Các framework thường có một số file hoặc thư mục đặc biệt.
VD: laravel farme có file web.config  

# Remediation
- Làm xáo trộn các header
- Thay đổi cookie mặc định
- Ẩn, thay đổi quyền truy cập với các file, folder đặc biệt