# Summary
- Phần này mô tả cách giám sát tất cả các yêu cầu HTTP đến / đi ở cả phía máy khách hoặc máy chủ web. Mục đích của thử nghiệm này là để xác minh xem có yêu cầu HTTP không cần thiết hoặc đáng ngờ gửi trong nền không.
# How to Test
## Reverse proxy
- Để có thể theo dõi tất cả các request dến máy chủ ta có thể cấu hình reverse proxy 
- The testing step:
  - Configure the Fiddler or Charles as Reverse Proxy
  - Capture the HTTP traffic
  - Inspect HTTP traffic
  - Modify HTTP requests and replay the modified requests for testing
# Port Forwarding
- Port forwarding là một cách khác cho phép chúng ta chặn HTTP requets mà không cần thay đổi cấu hình client
- The testing flow will be:
  - Install the Charles or port forwarding on another machine or web Server
  - Configure the Charles as Socks proxy as port forwarding.
# TCP-level Network Traffic Capture
 - Kĩ thuật này cho phép bắt tất cả các lưu lượng TCP. Các công cụ như TCP dump hoặc wireshark có thể được sử dụng. Tuy nhiên các công cụ này không thể cho phép chúng ta gửi các yêu cầu HTTP đã sửa đổi để kiểm tra.
 - The testing steps will be:
    - Activate TCPDump or WireShark on Web Server side to capture network traffic
    - Monitor the captured files (PCAP)
    - Edit PCAP files by Ostinato tool based on need
    - Reply the HTTP requests

