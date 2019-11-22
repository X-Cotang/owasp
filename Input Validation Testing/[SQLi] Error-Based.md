# Summary
- Kĩ thuật SQLi Error-based dựa trên việc chủ quan, không tắt thông báo lỗi ứng dụng của các lập trình viên trong việc phát triển ứng dụng
# Exploit
1. Detect attack vector  
- Ta có website như sau:

![](https://github.com/X-Cotang/owasp/blob/master/Input%20Validation%20Testing/image/sqli-error-1.png)  

- Lướt một vòng quanh trang web, ta thấy có một input vector duy nhất :"search". Đây là vector hay được sử dụng để tấn công xss. Nhưng trang web này lại không hề có phần đăng nhập hay lưu lại các input người dùng nhập vào, nên việc xss là vô nghĩa.
- Fuzz input ```search``` ta phát hiện được có lỗi xảy ra với dấu ```"```:

![](https://github.com/X-Cotang/owasp/blob/master/Input%20Validation%20Testing/image/sqli-error-2.png)

- Trang thông báo lỗi về sql query hiện ra. Nhìn vào giao diện thông báo lỗi,ta thấy ngay trang web sử dụng framework CodeIgniter. Tới đây ta liền nghĩ ngay tới việc sử dụng kĩ thuật Error-based để tấn công. Tiến hành khai thác:
**Payload**
```sql
-1") and (select 1 from (Select count(*),Concat((select table_name from information_schema.tables where table_schema=database() limit 1,1),0x3a,floor(rand(0)*2))y from information_schema.tables group by y) x) -- -
```  

![](https://github.com/X-Cotang/owasp/blob/master/Input%20Validation%20Testing/image/sqli-error-3.png)


![](https://github.com/X-Cotang/owasp/blob/master/Input%20Validation%20Testing/image/sqli-error-1.gif)
