# Description
- Khám phá ứng dụng web là một quá trình nhằm xác định các ứng dụng web trên một cơ sở hạ tầng nhất định
# Exploit
- Có ba yếu tố ảnh hưởng đến số lượng ứng dụng có liên quan một DNS name đã cho hoặc là địa chỉ ip:
    1. Different base URL
    2. Non-standard ports
    Mặc dù các ứng dụng web thường sống trên cổng 80 (http) và 443 (https), nhưng không có gì kỳ diệu về các số cổng này. Trong thực tế, các ứng dụng web có thể được liên kết với các cổng TCP tùy ý và có thể được tham chiếu bằng cách chỉ định số cổng như sau: http://www.example.com:20000/. 
    3. Virtual hosts 
    DNS cho phép một địa chỉ IP duy nhất được liên kết với một hoặc nhiều tên tượng trưng (subdomain).
    Mối quan hệ 1-N này có thể được phản ánh để phục vụ các nội dung khác nhau bằng cách sử dụng virtual hosts.  

**Approaches to address issue 1 - non-standard URLs**
Không có cách nào để xác định các ứng dụng nếu không có các chuẩn. Nếu máy chủ web được cấu hình sai và cho phép duyệt thư mục, thì có thể phát hiện ra các ứng dụng này. Hoặc các ứng dụng này có thể được tham chiếu bởi các ứng dụng khác,website khác.
VD:
```
Stite: shop.vn
Trang đăng nhập của quản trị viên bị ẩn: login.shop.vn
```

**Approaches to address issue 2 - non-standard ports**
![](https://github.com/huyenlamchiton/owasp/blob/master/Information%20Gathering/image/004-1.png)  

- Theo ví dụ trên ta có :
    * Apache server với giao thức http chạy ở cổng 80
    * Giao thức https chạy ở công 443
    * SSH cổng 22
    * FTP cổng 21
    * Cổng 8083 chạy một giao thức http khác
- Truy cập cổng 8083 ta được:

![](https://github.com/huyenlamchiton/owasp/blob/master/Information%20Gathering/image/004-2.png)  
**Approaches to address issue 3 - virtual hosts**