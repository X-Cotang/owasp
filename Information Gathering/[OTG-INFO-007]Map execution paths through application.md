# Description
- Trước khi bắt đầu thử nghiệm bảo mật, hiểu cấu trúc của ứng dụng là điều tối quan trọng. Nếu không có sự hiểu biết kỹ lưỡng về cách bố trí của ứng dụng, chắc chắn nó sẽ được kiểm tra kỹ lưỡng.
# How to Test
### Có một số cách để tiếp cận kiểm tra và đo lường mức độ bao phủ của mã:

- Đường dẫn - kiểm tra từng đường dẫn thông qua một ứng dụng thử nghiệm phân tích giá trị kết hợp cho từng đường dẫn quyết định. Trong khi phương pháp này cung cấp tính kỹ lưỡng, số lượng đường dẫn kiểm tra có thể tăng theo cấp số nhân với mỗi nhánh.
- Luồng dữ liệu (hoặc phân tích mờ) - kiểm tra việc gán biến thông qua tương tác bên ngoài (người dùng thông thường). Tập trung vào việc ánh xạ luồng, chuyển đổi và sử dụng dữ liệu trong toàn bộ ứng dụng.
- Race - Kiểm tra nhiều phiên bản đồng thời của ứng dụng thao tác cùng một dữ liệu.
### Blackbox 
- Người kiểm tra có thể bắt đầu bằng bảng tính và ghi lại tất cả các liên kết được phát hiện bằng cách quét ứng dụng (bằng tay hoặc tự động). Sau đó, người kiểm tra có thể xem xét kỹ hơn các điểm quan trọng trong ứng dụng và điều tra xem có bao nhiêu đường dẫn mã quan trọng được phát hiện. Những điều này sau đó nên được ghi lại trong bảng tính với các mô tả URL, văn xuôi và ảnh chụp màn hình của các đường dẫn được phát hiện.  
# Example
### Automatic Spidering 
VD vs burp-suite:  

![](https://github.com/huyenlamchiton/owasp/blob/master/Information%20Gathering/image/007-1.png)  