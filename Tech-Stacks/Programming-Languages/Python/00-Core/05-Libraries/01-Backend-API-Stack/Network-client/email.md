- [Introduction email (Thư viện email giúp tạo lá thư)](#introduction-email-thư-viện-email-giúp-tạo-lá-thư)
- [mime](#mime)
  - [text](#text)
    - [MIMETEXT()](#mimetext)
  - [multipart](#multipart)
    - [MIMEMulipart (đối tượng đại diện cho một email hoàn chỉnh)](#mimemulipart-đối-tượng-đại-diện-cho-một-email-hoàn-chỉnh)
      - [.attach (thêm nội dung vào email)](#attach-thêm-nội-dung-vào-email)
---
# Introduction email (Thư viện email giúp tạo lá thư)
```bash
Nếu không có thư viện này thì server không biết email gồm:
    - Tiêu đề
    - Người gửi
    - Người nhận
    - Nội dung
```
# mime
## text
### MIMETEXT()
**Syn**
```bash
MIMEText(body, "plain")

- "plain"   : là văn bản thuần (plain text)
- "html"    : là văn bản html
```
**Ex**
```python
from email.mime.text import MIMEText

msg = MIMEText("Xin chào")
```
## multipart
### MIMEMulipart (đối tượng đại diện cho một email hoàn chỉnh)
```bash
Có thể chứa:
    - nội dung text
    - HTML
    - hình ảnh
    - file đính kèm
```
**Ex**
```python
from email.mime.multipart import MIMEMultipart
from email.mime.text import MIMEText

EMAIL = "shop@gmail.com"

msg = MIMEMultipart()
msg["From"] = EMAIL
msg["To"] = "abc@gmail.com"
msg["Subject"] = "OTP Reset Password"

body = "Your OTP is: 123456"
msg.attach(MIMEText(body, "plain"))

print(msg)
# Content-Type: multipart/mixed; boundary="===============123456789=="
# MIME-Version: 1.0
# From: shop@gmail.com
# To: abc@gmail.com
# Subject: OTP Reset Password

# --===============123456789==
# Content-Type: text/plain; charset="us-ascii"
# MIME-Version: 1.0
# Content-Transfer-Encoding: 7bit

# Your OTP is: 123456
# --===============123456789==--
```
#### .attach (thêm nội dung vào email)
**Syn**
```bash
msg.attach(MIMEText(body, "plain"))
```