# Description
- Biết phiên bản và loại máy chủ web đang chạy cho phép người kiểm tra xác định các lỗ hổng đã biết và các khai thác thích hợp để sử dụng trong quá trình thử nghiệm. 
# Expoit  
- Sử dụng netcat hoặc DevTool của trình duyệt để tìm kiếm phiên bản Web server thông qua response header:  

![](https://github.com/huyenlamchiton/owasp/blob/master/Information%20Gathering/image/002-1.png)

- Như ta thấy server sử dụng Apache phiên bản 1.3.3 chạy trên Red Hat distro  
- Một ví dụ khác:

![](https://github.com/huyenlamchiton/owasp/blob/master/Information%20Gathering/image/002-2.png)  

- Gửi yêu cầu không đúng định dạng:  

![](https://github.com/huyenlamchiton/owasp/blob/master/Information%20Gathering/image/002-3.png)

# Tool
- Online tool: Netcraft