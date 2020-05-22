# Summary
- Một máy chủ web thường lưu trữ một số ứng dụng web trên cùng một địa chỉ IP, tham chiếu đến từng ứng dụng thông qua máy chủ ảo. Trong một yêu cầu HTTP đến, các máy chủ web thường gửi yêu cầu đến máy chủ ảo đích dựa trên giá trị được cung cấp trong tiêu đề Máy chủ. Nếu không xác thực hợp lệ giá trị tiêu đề, kẻ tấn công có thể cung cấp đầu vào không hợp lệ để khiến máy chủ web:
  - Gửi yêu cầu đến máy chủ ảo đầu tiên trong danh sách
  - Gây ra chuyển hướng đến một miền do kẻ tấn công kiểm soát
  - Thực hiện ngộ độc bộ đệm web
  - Thao tác chức năng đặt lại mật khẩu
# How to Test 
- Chỉnh sủa tiêu đề "Host" trong header của request. Cuộc tấn công có hiệu lực khi máy chủ web xử lý đầu vào để gửi yêu cầu đến máy chủ do kẻ tấn công kiểm soát và không gửi đến máy chủ ảo nội bộ nằm trên máy chủ web.
VD: Chỉnh sửa tiêu đề "host"
```
GET / HTTP/1.1
Host: www.attacker.com
[...]
```
Request gửi về
```
HTTP/1.1 302 Found
[...]
Location: http://www.attacker.com/login.php
```
## X-Forwarded Host Header Bypass
- Một cách khác nữa có thể tiêm qua tiêu đề "X-Forwarded-Host" 
```
GET / HTTP/1.1
Host: www.example.com
X-Forwarded-Host: www.attacker.com
...
```
## Web Cache Poisoning
- Sử dụng kỹ thuật này, kẻ tấn công có thể thao tác bộ đệm web để cung cấp nội dung độc cho bất kỳ ai yêu cầu. Điều này phụ thuộc vào khả năng đầu độc proxy lưu trữ được chạy bởi chính ứng dụng, CDN hoặc các nhà cung cấp tuyến dưới khác. Do đó, nạn nhân sẽ không có quyền kiểm soát việc nhận nội dung độc hại khi yêu cầu ứng dụng dễ bị tấn công.
```
GET / HTTP/1.1
Host: www.attacker.com
...
```
```
...
<link src="http://www.attacker.com/link" />
...
```
## Reset password poisoning
- Thông thường chức năng đặt lại mật khẩu sẽ bao gồm giá trị tiêu đề Máy chủ khi tạo liên kết đặt lại mật khẩu sử dụng mã thông báo bí mật được tạo. Nếu ứng dụng xử lý miền do kẻ tấn công kiểm soát để tạo liên kết đặt lại mật khẩu, nạn nhân có thể nhấp vào liên kết trong email và cho phép kẻ tấn công lấy mã thông báo đặt lại, do đó đặt lại mật khẩu của nạn nhân.
```
... Email snippet ...

Click on the following link to reset your password:

http://www.attacker.com/index.php?module=Login&action=resetPassword&token=<SECRET_TOKEN>

... Email snippet ...
```
