# Description
- Khám phá ứng dụng web là một quá trình nhằm xác định các ứng dụng web trên một cơ sở hạ tầng nhất định
# Exploit
- Có ba yếu tố ảnh hưởng đến số lượng ứng dụng có liên quan một DNS name đã cho hoặc là địa chỉ ip:
    1. Different base URL
    Giả sử có trang web có nguồn gốc tại "www.example.com". Không có điều gì bắt buộc ứng dụng phải bắt đầu tại "/" (root).
    Với cùng một tên tượng trưng như trên ta có thể có ba ứng dụng web như:
    ```
    www.example.com/url1
    www.example.com/url2
    www.example.com/url3
    ```
    Trong một số trường hợp các ứng dụng này bị ẩn bởi người chủ sở hữu trang web. Nghĩa là các ứng dụng web này không thể truy cập theo cách tiêu chuẩn.
    2. Non-standard ports
    Mặc dù các ứng dụng web thường sống trên cổng 80 (http) và 443 (https), nhưng không có gì kỳ diệu về các số cổng này. Trong thực tế, các ứng dụng web có thể được liên kết với các cổng TCP tùy ý và có thể được tham chiếu bằng cách chỉ định số cổng như sau: http://www.example.com:20000/. 
    3. Virtual hosts 
    DNS cho phép một địa chỉ IP duy nhất được liên kết với một hoặc nhiều tên tượng trưng (subdomain).
    Mối quan hệ 1-N này có thể được phản ánh để phục vụ các nội dung khác nhau bằng cách sử dụng virtual hosts.  

**Approaches to address issue 1 - non-standard URLs**
Không có cách nào để xác định các ứng dụng nếu không có các chuẩn. Nếu máy chủ web được cấu hình sai và cho phép duyệt thư mục, thì có thể phát hiện ra các ứng dụng này. Hoặc các ứng dụng này có thể được tham chiếu bởi các ứng dụng khác,website khác.

Người ta sẽ không nghi ngờ sự tồn tại của các ứng dụng web khác ngoài www.example.com rõ ràng, trừ khi họ biết về helpdesk.example.com và webmail.example.com.

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
Có một số kỹ thuật có thể được sử dụng để xác định tên DNS được liên kết với một địa chỉ IP nhất định x.y.z.t:  
- DNS zone transfers
Trước hết, người kiểm tra phải xác định máy chủ tên phục vụ x.y.z.t.Nếu một tên tượng trưng (example.com) được biết đến với x.y.z.t máy chủ của nó có thể được xác định bằng các công cụ như nslookup,host,dig,... bằng cách gửi yêu cầu DNS NS record.
Ví dụ sau đây cho thấy cách xác định name server cho www.owasp.org bằng cách sử dụng host command:  

![](https://github.com/huyenlamchiton/owasp/blob/master/Information%20Gathering/image/004-3.png)   

- DNS inverse queries  
Quá trình này tương tự như quy trình trước, nhưng phụ thuộc vào các bản ghi DNS (PTR). Thay vì yêu cầu chuyển vùng, hãy thử đặt loại bản ghi thành PTR và đưa ra truy vấn trên địa chỉ IP đã cho. Nếu người kiểm tra may mắn, họ có thể lấy lại mục nhập tên DNS. Kỹ thuật này dựa trên sự tồn tại của bản đồ tên từ IP đến biểu tượng, không được bảo đảm.  
- Web-based DNS searches  
Kiểu tìm kiếm này gần giống với DNS zone transfer
- Reverse-IP services  
Dịch vụ Reverse-IP tương tự như các truy vấn DNS-Reverse, với sự khác biệt là người kiểm tra truy vấn ứng dụng dựa trên web thay vì máy chủ tên. Có một số dịch vụ như vậy có sẵn. Vì họ có xu hướng trả về kết quả một phần (và thường khác nhau), tốt hơn là sử dụng nhiều dịch vụ để có được phân tích toàn diện hơn.
- Googling  
Sau khi thu thập thông tin từ các kỹ thuật trước đó, người kiểm tra có thể dựa vào các công cụ tìm kiếm để có thể tinh chỉnh và tăng phân tích của họ.
