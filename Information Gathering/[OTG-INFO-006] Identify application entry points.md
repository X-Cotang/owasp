# Description
- Phần này nhằm giúp xác định và vạch ra các khu vực, điểm yếu trong ứng dụng cần được điều tra sau khi hoàn thành việc liệt kê và lập bản đồ
# How to test
- Trước khi bắt đầu thử nghiệm, người kiểm tra phải luôn hiểu rõ về ứng dụng và cách hoạt động của các giao thức như GET, POST,...
- Để xem các parammeter của POST ta có thể sử dụng các công cụ devolop có sẵn của browser hoặc proxy như ZAP

### Requests:
* Xác định chỗ nào dùng GET, chỗ nào dùng POST
* Xác định tất cả tham số được sử dụng trong POST requet
* Trong yêu cầu POST cần chú ý tới tất cả tham số ẩn nào, các tham số này không được nhìn thấy trừ khi xem HTML source code
* Xác định tất cả tham số của GET
* Xác định tất cả tham số của chuỗi truy vấn 
* Một lưu ý đặc biệt, tester cần kiểm tra tất cả các tham số, đặc biệt là các tham số dễ bị tấn công, những tham số chưa được mã hóa, những tham số được ứng dụng xử lí.
* Ngoài ra cũng cần chú ý đến các tham số không nhìn thấy như: ?debug=True,...
### Responses:
* Xác định dòng nào trong reponse header set cookie, modifi, delete
* Xác định nơi có chuyển hướng
* Xác định status của response header
* Ngoài ra cần xác định các header đặc biệt. VD: Server: BIG-IP
# Example

![](https://github.com/huyenlamchiton/owasp/blob/master/Information%20Gathering/image/006-1.png)  