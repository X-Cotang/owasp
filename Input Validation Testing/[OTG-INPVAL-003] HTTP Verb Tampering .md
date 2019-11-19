# Description
- Đặc tả HTTP 1.1 đầy đủ xác định các phương thức hoặc động từ yêu cầu HTTP hợp lệ sau:
    * OPTIONS
    * GET
    * HEAD
    * POST
    * PUT
    * DELETE
    * TRACE
    * CONNECT
- Nếu được bật, các tiện ích mở rộng Web Distributed Authoring and Version (WebDAV) cho phép thêm một số phương thức HTTP:  
    * PROPFIND
    * PROPPATCH
    * MKCOL
    * COPY
    * MOVE
    * LOCK
    * UNLOCK
# How to test
- Vì tiêu chuẩn HTML không hỗ trợ các phương thức yêu cầu ngoài GET hoặc POST, chúng tôi sẽ cần tạo các yêu cầu HTTP tùy chỉnh để kiểm tra các phương thức khác
### Manual HTTP verb tampering testing
1. Crafting custom HTTP requests  
Mỗi yêu cầu HTTP 1.1 tuân theo định dạng và cú pháp cơ bản sau. Các yếu tố được bao quanh bởi dấu ngoặc [] là theo ngữ cảnh cho ứng dụng của bạn. Dòng mới trống ở cuối là bắt buộc.  
![](https://github.com/huyenlamchiton/owasp/blob/master/Input%20Validation%20Testing/image/003-0.png)

    1.1 OPTIONS  

    ![](https://github.com/huyenlamchiton/owasp/blob/master/Input%20Validation%20Testing/image/003-1.png)  

    1.2 GET 

    ![](https://github.com/huyenlamchiton/owasp/blob/master/Input%20Validation%20Testing/image/003-2.png)   
    1.3 HEAD

    ![](https://github.com/huyenlamchiton/owasp/blob/master/Input%20Validation%20Testing/image/003-3.png)

    1.4 POST

    ![](https://github.com/huyenlamchiton/owasp/blob/master/Input%20Validation%20Testing/image/003-4.png)

    1.5 PUT

    ![](https://github.com/huyenlamchiton/owasp/blob/master/Input%20Validation%20Testing/image/003-5.png)

    1.6 DELETE

    ![](https://github.com/huyenlamchiton/owasp/blob/master/Input%20Validation%20Testing/image/003-6.png)

    1.7 TRACE  

    ![](https://github.com/huyenlamchiton/owasp/blob/master/Input%20Validation%20Testing/image/003-7.png)

    1.8 CONNECT 

    ![](https://github.com/huyenlamchiton/owasp/blob/master/Input%20Validation%20Testing/image/003-8.png)
2. Sending HTTP requests 
    * Sử dụng netcat hoặc các công cụ tương tự gửi request lên server 
    ```nc www.example.com 80 < OPTIONS.http.txt```
3. Parsing HTTP responses 
    * Mặc dù mỗi phương thức HTTP có thể có khả năng trả về các kết quả khác nhau, nhưng chỉ có một kết quả hợp lệ duy nhất cho tất cả các phương thức khác ngoài GET và POST.
    * Một ví dụ về thử nghiệm thất bại (nghĩa là, máy chủ hỗ trợ ```OPTION``` mặc dù không cần nó):  

![](https://github.com/huyenlamchiton/owasp/blob/master/Input%20Validation%20Testing/image/003-9.png)
