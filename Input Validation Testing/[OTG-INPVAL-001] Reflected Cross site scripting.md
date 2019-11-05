## Description
- Kỹ thuật XSS được thực hiện dựa trên việc chèn các đoạn script nguy hiểm vào trong source code ứng dụng web. Nhằm thực thi các đoạn mã độc Javascript để chiếm phiên đăng nhập của người dùng
- Mã độc được tiêm vào url và gửi đến cho nạn nhân, nạn nhân ấn vào đường link có chứa mã độc và sẽ bị đánh cắp phiên làm việc
![](https://github.com/huyenlamchiton/owasp/blob/master/Input%20Validation%20Testing/image/1%20o_asKsD_JqunhqggHoxodw.png)
##### Example:
```http://example.com/?search=<script>alert(1)</script>```
## Reason
- Server không kiểm soát giá trị input người dùng nhập vào trước khi trả về cho trình duyệt
- Người dùng sử dụng các trình duyệt đã lỗi thời
- Nạn nhân bị lừa ấn vào đường link có chứa mã độc
## Exploit
1. Phát hiện input vector  
    * Đối với mỗi trang web, người kiểm tra phải xác định tất cả các input do người dùng định nghĩa và cách nhập chúng
    * **Các input dễ bị tấn công:** ?search=,?page=,?document=,?user=,...
2. Phân tích từng vector 
    * Người kiểm tra fuzz các kí tự và các từ khóa nhạy cảm,vô hại để phát hiện lỗ hổng trong ứng dụng web.
    * **Các kí tự nhạy cảm:** <,>,/,script,alert,...

```
<script>alert(123)</script>
```
