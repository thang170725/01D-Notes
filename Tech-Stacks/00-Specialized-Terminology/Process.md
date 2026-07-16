- [Domain](#domain)
  - [Domain website (Trong mảng website)](#domain-website-trong-mảng-website)
- [DNS (Domain Name System - domain → IP)](#dns-domain-name-system---domain--ip)
- [Subdomain](#subdomain)
- [ERP (Enterprise Resource Planning)](#erp-enterprise-resource-planning)
  - [Các luồng nghiệp vụ cơ bản trong ERP](#các-luồng-nghiệp-vụ-cơ-bản-trong-erp)
    - [CRM (Customer Relationship Management)](#crm-customer-relationship-management)
    - [HRM (Human Resource Management)](#hrm-human-resource-management)
    - [Quy trình tạo Ticket / Công việc](#quy-trình-tạo-ticket--công-việc)
- [Work items (công việc cụ thể)](#work-items-công-việc-cụ-thể)
---
# Domain
Các rủi ro liên quan domain

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
## Domain website (Trong mảng website)
```bash
Được hiểu là một tên miền (url - trỏ tới website)
```
**Cấu trúc một domain**
```bash
www.sub.example.com

- .com      : TLD (Top-Level Domain). Miền cấp cao
- example   : SLD. Tên chính
- sub       : Subdomain. Phân nhánh
- www       : Hostname. Máy/ứng dụng cụ thể
```
**Các loại domain (TLD)**
```bash
TLD – Generic TLD
  Ví dụ:
    - .com	: Commercial
    - .org	: Organization
    - .net	: Network
    - .info	: Information

ccTLD – Country Code
  Ví dụ	Quốc gia
    - .vn	: Việt Nam
    - .jp	: Nhật
    - .us	: Mỹ

New gTLD (mới)
  Ví dụ
    - .ai
    - .dev
    - .cloud
    - .app
```
# DNS (Domain Name System - domain → IP)
**Ex**
```bash
google.com A → 142.250.190.78
```
# Subdomain
```bash
📌 Trong thực tế:
  - 90% lỗi bảo mật nằm ở subdomain
  - Dev quên xóa:
    + test.example.com
    + old.example.com
    + staging.example.com
```
# ERP (Enterprise Resource Planning)
- Là hệ thống phần mềm quản lý toàn bộ hoạt động của một công ty trên một chỗ duy nhất
→ thay vì mỗi phòng ban dùng một file / phần mềm riêng.
- Không có ERP: → dữ liệu lệch nhau
  - Sale dùng Excel
  - HR dùng phần mềm khác
  - Kế toán dùng phần mềm khác
- Có ERP: Tất cả dùng một hệ thống, Thay đổi ở chỗ này → chỗ khác cập nhật theo

## Các luồng nghiệp vụ cơ bản trong ERP
### CRM (Customer Relationship Management)
- Quản lý khách hàng.
- Theo dõi khách từ lúc chưa mua → đã mua → chăm sóc sau bán
- Ví dụ đơn giản:
  - Lưu thông tin khách hàng (tên, SĐT, email)
  - Ghi lại khách đã hỏi gì, mua gì
  - Nhân viên sale gọi cho khách → cập nhật kết quả
Mục tiêu: không quên khách, bán hàng hiệu quả hơn

### HRM (Human Resource Management)
- Quản lý nhân sự, Quản lý con người trong công ty
- Ví dụ:
  - Thông tin nhân viên
  - Chấm công, nghỉ phép
  - Lương, thưởng
  - Phân quyền ai làm gì
- Mục tiêu: quản lý nhân sự rõ ràng, minh bạch

### Quy trình tạo Ticket / Công việc
- Tạo việc → giao người làm → theo dõi → hoàn thành
- Ví dụ:
  - Khách báo lỗi → tạo ticket
  - Giao cho nhân viên xử lý
  - Theo dõi trạng thái: Đang làm → Chờ → Hoàn thành
- Mục tiêu: không sót việc, ai làm gì đều rõ
# Work items (công việc cụ thể)
```text
Với các work items cần tuân thủ Cycles (Chu kỳ giống sprint).
```
**Cycles**
```text
- Là khoảng thời gian để  hoàn thành 1 work item (Ví dụ: 5 ngày, 1 tuần).
- Cycles có các trạng thái (đang hoạt động - work item sắp tới - hoàn thành)
```
**Timeline dependencies**
```text
- Là liện hệ giữa các task với nhau.
```
1. PRD (Product Requirements Document)

PRD là tài liệu mô tả yêu cầu của sản phẩm.

Nó trả lời các câu hỏi:

Sản phẩm này dùng để làm gì?
Đối tượng người dùng là ai?
Có những tính năng nào?
Luồng sử dụng ra sao?
Tiêu chí nào để coi là hoàn thành?

Ví dụ bạn đang làm web quản lý dinh dưỡng và tập luyện.

Một PRD đơn giản có thể là:

Tên sản phẩm
Smart Recipe

Mục tiêu
Giúp người dùng lên kế hoạch tập luyện và ăn uống.

Đối tượng
Người muốn giảm cân, tăng cơ.

Chức năng

- Đăng nhập
- Xem bài tập
- Tạo kế hoạch tập
- Theo dõi calories
- AI gợi ý thực đơn

Tiêu chí thành công

- Người dùng tạo được workout plan.
- AI trả lời dưới 3 giây.

PRD không chứa code, mà là tài liệu để Product Manager, Designer và Developer cùng hiểu sản phẩm.

2. MVP (Minimum Viable Product)

MVP là phiên bản nhỏ nhất của sản phẩm nhưng vẫn sử dụng được.

Ví dụ bạn muốn xây một ứng dụng giống MyFitnessPal.

Ý tưởng đầy đủ:

✓ AI Chat
✓ Workout
✓ Calories
✓ Barcode
✓ Camera nhận diện món ăn
✓ Đồng bộ đồng hồ
✓ Thống kê
✓ Social
✓ Chat
✓ Ranking

Nếu làm hết ngay sẽ mất rất lâu.

Thay vào đó, bạn tạo MVP:

✓ Đăng ký
✓ Đăng nhập
✓ Thêm món ăn
✓ Xem calories
✓ Workout đơn giản

Đưa cho người dùng dùng thử.

Nếu họ thích, bạn mới phát triển thêm.

MVP = phiên bản tối thiểu nhưng có giá trị sử dụng.

3. Cloudflare

Cloudflare là một công ty cung cấp các dịch vụ hạ tầng mạng và bảo mật.

Nó đứng giữa người dùng và server của bạn.

User

↓

Cloudflare

↓

Server của bạn

Cloudflare có rất nhiều chức năng.

CDN

Cache ảnh, CSS, JS ở nhiều quốc gia.

Ví dụ:

Người dùng Việt Nam truy cập.

Không cần lấy ảnh từ Mỹ.

Cloudflare sẽ trả ảnh từ server gần Việt Nam hơn.

=> Website nhanh hơn.

Chống DDoS

Nếu hacker gửi:

10 triệu request

Cloudflare sẽ chặn trước khi request tới server.

SSL

Cloudflare giúp website có:

https://

mà không cần tự cấu hình quá nhiều.

DNS

Bạn mua domain:

abc.com

Cloudflare quản lý DNS:

abc.com

↓

123.45.67.89
WAF (Web Application Firewall)

Chặn các request nguy hiểm như:

SQL Injection

XSS

Bot
Worker

Đây là tính năng rất nổi tiếng.

Bạn có thể chạy JavaScript hoặc TypeScript ngay trên hệ thống của Cloudflare.

Ví dụ:

export default {
  async fetch(request) {
    return new Response("Hello");
  }
}

Không cần VPS.

Không cần Docker.

Không cần Nginx.

Cloudflare sẽ chạy luôn đoạn code đó.

R2

Cloud Storage giống S3.

Bạn lưu:

ảnh
video
file
D1

Database SQLite trên Cloudflare.

KV

Lưu key-value.

Ví dụ:

user:123

↓

{
 name:"Thắng"
}
Durable Object

Lưu trạng thái theo thời gian thực.

Ví dụ:

Chat
Game
Multiplayer
Nếu áp dụng vào dự án của bạn

Bạn đang làm:

React
FastAPI
AI Agent
MariaDB

Có thể dùng Cloudflare như sau:

User

↓

Cloudflare
    ↓
- CDN
- SSL
- DNS
- DDoS Protection

↓

Nginx

↓

FastAPI

↓

MariaDB

Hoặc nếu có những API nhỏ (ví dụ xác thực token, chuyển hướng, xử lý nhẹ), bạn có thể viết bằng Cloudflare Workers thay vì chạy trên server riêng.

Tóm tắt
Khái niệm	Là gì?	Dùng để làm gì?
PRD	Tài liệu yêu cầu sản phẩm	Mô tả mục tiêu, tính năng, phạm vi của sản phẩm trước khi phát triển
MVP	Phiên bản tối thiểu của sản phẩm	Ra mắt sớm để kiểm chứng ý tưởng với người dùng trước khi phát triển đầy đủ
Cloudflare	Nền tảng hạ tầng mạng và bảo mật	Cung cấp CDN, DNS, SSL, chống DDoS, firewall, serverless (Workers), lưu trữ (R2), cơ sở dữ liệu (D1),...

Với dự án AI dinh dưỡng của bạn, PRD là bước lên kế hoạch, MVP là phiên bản đầu tiên để người dùng trải nghiệm, còn Cloudflare là dịch vụ giúp triển khai và vận hành ứng dụng nhanh, an toàn và ổn định hơn.