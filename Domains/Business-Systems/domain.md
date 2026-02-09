Domain (tên miền) là tên định danh dùng để trỏ tới một tài nguyên trên Internet, thường là:
- Website
- Server
- Dịch vụ mạng
- Thay vì nhớ IP như: 142.250.190.78. Con người dùng: google.com
- Domain chỉ là “tên”, còn DNS mới là thứ dịch tên → IP

# Cấu trúc một domain
**Ex**
```text
www.sub.example.com
- .com      : TLD (Top-Level Domain). Miền cấp cao
- example   : SLD. Tên chính
- sub       : Subdomain. Phân nhánh
- www       : Hostname. Máy/ứng dụng cụ thể
```
**Thực tế**
```text
www.facebook.com
- facebook.com là domain
- www là subdomain
```

# Các loại domain (TLD)
🔹 3.1. gTLD – Generic TLD
Ví dụ	Ý nghĩa
.com	Commercial
.org	Organization
.net	Network
.info	Information
🔹 3.2. ccTLD – Country Code
Ví dụ	Quốc gia
.vn	Việt Nam
.jp	Nhật
.us	Mỹ
🔹 3.3. New gTLD (mới)
Ví dụ
.ai
.dev
.cloud
.app

📌 Lưu ý bảo mật:
.dev và .app bắt buộc HTTPS

4️⃣ Domain ≠ Website ≠ Hosting

Rất nhiều người nhầm 👇

Khái niệm	Là gì
Domain	Tên
Hosting	Nơi lưu code
Website	Code chạy trên hosting

Ví dụ:

domain → trỏ tới → IP server → server trả HTML

5️⃣ DNS – Trái tim của domain
🔹 5.1. DNS là gì?

DNS (Domain Name System) là hệ thống:

domain → IP

🔹 5.2. Các bản ghi DNS quan trọng
Record	Dùng làm gì
A	Domain → IPv4
AAAA	Domain → IPv6
CNAME	Domain → domain khác
MX	Mail server
TXT	SPF, DKIM, verify
NS	Name server

Ví dụ:

google.com A → 142.250.190.78

6️⃣ Subdomain – Cực kỳ quan trọng trong bảo mật

Ví dụ:

api.example.com
admin.example.com
dev.example.com


📌 Trong thực tế:

90% lỗi bảo mật nằm ở subdomain

Dev quên xóa:

test.example.com
old.example.com
staging.example.com


👉 Đây là điểm tấn công phổ biến

7️⃣ Domain trong tấn công & phòng thủ (high-level)

⚠️ Chỉ nói ở mức kiến thức & phòng thủ

🔹 7.1. Các rủi ro liên quan domain

Subdomain takeover

DNS hijacking

Typosquatting (gooogle.com)

Phishing domain

Expired domain reuse

🔹 7.2. Phòng thủ cơ bản

Khóa domain (Registrar Lock)

Bật DNSSEC

Kiểm tra subdomain định kỳ

Không public subdomain dev

HTTPS + HSTS

8️⃣ Domain & AI / CNTT (liên quan trực tiếp bạn)
🔹 AI / Web

Model API thường nằm ở:

api.domain.com

🔹 Bảo mật dữ liệu

Domain mail quyết định:

Spam

Spoofing

Email giả mạo

🔹 DevOps / Cloud

Load balancer gắn domain

Microservice → mỗi service 1 subdomain

9️⃣ Domain ≠ Active Directory Domain (đừng nhầm)

Trong Windows / Enterprise:

Internet Domain	AD Domain
example.com	corp.local
DNS public	DNS nội bộ
Internet	Mạng nội bộ

📌 Hacker/defender rất quan tâm AD Domain