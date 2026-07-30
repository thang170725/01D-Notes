- [Cloudflare Introduction (là một công ty cung cấp các dịch vụ hạ tầng mạng và bảo mật)](#cloudflare-introduction-là-một-công-ty-cung-cấp-các-dịch-vụ-hạ-tầng-mạng-và-bảo-mật)
---
# Cloudflare Introduction (là một công ty cung cấp các dịch vụ hạ tầng mạng và bảo mật)
```bash
Nó đứng giữa người dùng và server của bạn.
  User
  ↓
  Cloudflare
  ↓
  Server của bạn

Cloudflare có rất nhiều chức năng.
  - CDN
  - Cache ảnh, CSS, JS ở nhiều quốc gia.

Ví dụ:
  Người dùng Việt Nam truy cập.
    Không cần lấy ảnh từ Mỹ.
    
    Cloudflare sẽ trả ảnh từ server gần Việt Nam hơn.
=> Website nhanh hơn.

Chống DDoS
  Nếu hacker gửi: 10 triệu request
    Cloudflare sẽ chặn trước khi request tới server.

SSL
  Cloudflare giúp website có: https:// mà không cần tự cấu hình quá nhiều.

DNS
  Bạn mua domain: abc.com

  Cloudflare quản lý DNS:
    abc.com
    ↓
    123.45.67.89

WAF (Web Application Firewall)
  Chặn các request nguy hiểm như:
    - SQL Injection
    - XSS
    - Bot
    - Worker
=> Đây là tính năng rất nổi tiếng.

Cloud Storage giống S3.
  Bạn lưu:
    - ảnh
    - video
    - file
    - D1

Database SQLite trên Cloudflare.
  KV: Lưu key-value.
    Ví dụ:
      user:123
      ↓
      {
       name:"Thắng"
      }

Durable Object
  Lưu trạng thái theo thời gian thực.

  Ví dụ:
    - Chat
    - Game
    - Multiplayer
```