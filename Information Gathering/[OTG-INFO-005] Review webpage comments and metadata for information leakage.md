# Description
- Các comment và metadata giúp các lập trình viên code dễ dàng hơn.Tuy nhiên khi chúng được bao gồm trong HTML code có thể tiết lộ thông tin nội bộ cho những kẻ tấn công.Vì vậy đánh giá, kiểm tra xem có bất cứ thông tin nào bị dò rỉ không
# Exploit
- HTML comment thường được sử dụng bởi các devoloper, trong đó có chứa các thông tin debug chương trình. Đôi khi họ quên mất không xóa đi.  
VD:  

![](https://github.com/huyenlamchiton/owasp/blob/master/Information%20Gathering/image/005-1.png)  

OR:  

![](https://github.com/huyenlamchiton/owasp/blob/master/Information%20Gathering/image/005-2.png)  

- Kiểm tra phiên bản của HTML và DTD:  

![](https://github.com/huyenlamchiton/owasp/blob/master/Information%20Gathering/image/005-3.png)  

- Thẻ ```<Meta>``` cũng có thể quản lí robot:  

![](https://github.com/huyenlamchiton/owasp/blob/master/Information%20Gathering/image/005-4.png) 