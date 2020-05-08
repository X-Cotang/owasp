# Summary
- Khi tài nguyên được cung cấp cài đặt quyền cung cấp quyền truy cập vào phạm vi tác nhân rộng hơn mức yêu cầu, điều đó có thể dẫn đến việc lộ thông tin nhạy cảm hoặc sửa đổi tài nguyên đó bởi các bên vô ý. Điều này đặc biệt nguy hiểm khi tài nguyên có liên quan đến cấu hình chương trình, thực thi hoặc dữ liệu người dùng nhạy cảm.
VD: Các thư mục nhạy cảm như hình ảnh hay các file back up không được set quyền đúng cách,...
# How to Test
- Sử dụng các lệnh liệt kê thư mục để kiểm tra permission như ```ls```, ```Windows AccessEnum```,...
- Các file và thư mục cần kiểm tra:
    - Web files/directory
    - Configuration files/directory
    - Sensitive files (encrypted data, password, key)/directory
    - Log files (security logs, operation logs, admin logs)/directory
    - Executables (scripts, EXE, JAR, class, PHP, ASP)/directory
    - Database files/directory
    - Temp files /directory
    - Upload files/directory
