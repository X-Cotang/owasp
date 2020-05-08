# Summary
- Tiêu đề HTTP Strict Transport Security (HSTS) là một cơ chế mà các trang web phải giao tiếp với các trình duyệt web mà tất cả lưu lượng truy cập được trao đổi với một tên miền nhất định phải luôn được gửi qua https, điều này sẽ giúp bảo vệ thông tin khỏi bị vượt qua các yêu cầu không được mã hóa.
- Tính năng HSTS cho phép ứng dụng web thông báo cho trình duyệt, thông qua việc sử dụng tiêu đề phản hồi đặc biệt, rằng nó sẽ không bao giờ thiết lập kết nối đến các máy chủ miền được chỉ định bằng HTTP. Thay vào đó, trình duyệt sẽ tự động thiết lập tất cả các yêu cầu kết nối để truy cập trang web thông qua HTTPS
- HTTP strict transport security header sử dụng 2 chỉ thị:
    - max-age: Số giây mà trình duyệt sẽ chuyển đổi HTTP request sang HTTPS requests
    - includeSubDomains: Để khai báo rằng tất cả sub-domains của ứng dụng phải sử dụng HTTPS.
VD:  
```
Strict-Transport-Security: max-age=60000; includeSubDomains
```
# How to Test
- Kiểm tra header có chứa ```Strict-Transport-Security``` hay không.
```
$ curl -s -D- https://owasp.org | grep Strict
Strict-Transport-Security: max-age=15768000
```