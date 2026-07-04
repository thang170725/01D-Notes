- [Itroduction smtplib (tạo kết nối với máy chủ email (Gmail, Outlook,...), đăng nhập và gửi email)](#itroduction-smtplib-tạo-kết-nối-với-máy-chủ-email-gmail-outlook-đăng-nhập-và-gửi-email)
- [SMTP() (tạo kết nối SMTP)](#smtp-tạo-kết-nối-smtp)
  - [.starttls (Bật mã hóa TLS)](#starttls-bật-mã-hóa-tls)
  - [.login (đăng nhập)](#login-đăng-nhập)
  - [.send\_message() (gửi email)](#send_message-gửi-email)
  - [.quit() (đóng kết nối)](#quit-đóng-kết-nối)
---
# Itroduction smtplib (tạo kết nối với máy chủ email (Gmail, Outlook,...), đăng nhập và gửi email)
```bash
smtplib là thư viện chuẩn của Python dùng giao thức SMTP (Simple Mail Transfer Protocol) để gửi email
```
# SMTP() (tạo kết nối SMTP)
**Ex**
```python
import smtplib

server = smtplib.SMTP("smtp.gmail.com", 587)
# Kết nối tới server Gmail.
# Port 587 là cổng dành cho TLS.
# Python ------> SMTP Server ------> Người nhận
```
## .starttls (Bật mã hóa TLS)
```bash
Nếu không:
    Python ----password----> Server
=> Có thể bị nghe lén.

Sau khi dùng TLS
    Python === dữ liệu mã hóa ===> Server
=> An toàn hơn.
```
## .login (đăng nhập)
## .send_message() (gửi email)
## .quit() (đóng kết nối)