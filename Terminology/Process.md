- [Specialized Terminology Introduction (Thuật ngữ chuyên ngành và nghiệp vụ)](#specialized-terminology-introduction-thuật-ngữ-chuyên-ngành-và-nghiệp-vụ)
- [Domain](#domain)
  - [Subdomain takeover](#subdomain-takeover)
  - [DNS hijacking](#dns-hijacking)
  - [Typosquatting (gooogle.com)](#typosquatting-goooglecom)
  - [Phishing domain](#phishing-domain)
  - [Expired domain reuse](#expired-domain-reuse)
  - [Phòng thủ cơ bản](#phòng-thủ-cơ-bản)
- [Website Terminology (thuật ngữ mảng website)](#website-terminology-thuật-ngữ-mảng-website)
  - [Domain website (Được hiểu là một tên miền (url) trỏ tới website)](#domain-website-được-hiểu-là-một-tên-miền-url-trỏ-tới-website)
- [DNS (Domain Name System - domain → IP)](#dns-domain-name-system---domain--ip)
- [Subdomain](#subdomain)
- [ERP (Enterprise Resource Planning)](#erp-enterprise-resource-planning)
  - [Các luồng nghiệp vụ cơ bản trong ERP](#các-luồng-nghiệp-vụ-cơ-bản-trong-erp)
    - [CRM (Customer Relationship Management)](#crm-customer-relationship-management)
    - [HRM (Human Resource Management)](#hrm-human-resource-management)
    - [Quy trình tạo Ticket / Công việc](#quy-trình-tạo-ticket--công-việc)
- [Work items (công việc cụ thể)](#work-items-công-việc-cụ-thể)
- [PRD (Product Requirements Document - tài liệu mô tả yêu cầu của sản phẩm)](#prd-product-requirements-document---tài-liệu-mô-tả-yêu-cầu-của-sản-phẩm)
- [MVP (Minimum Viable Product - là phiên bản nhỏ nhất của sản phẩm nhưng vẫn sử dụng được)](#mvp-minimum-viable-product---là-phiên-bản-nhỏ-nhất-của-sản-phẩm-nhưng-vẫn-sử-dụng-được)
- [TPA Bảo hiểm (nghiệp vụ trong ngành bảo hiểm)](#tpa-bảo-hiểm-nghiệp-vụ-trong-ngành-bảo-hiểm)
  - [Phân loại giấy tờ](#phân-loại-giấy-tờ)
---
# Specialized Terminology Introduction (Thuật ngữ chuyên ngành và nghiệp vụ)
# Domain
## Subdomain takeover
## DNS hijacking
## Typosquatting (gooogle.com)
## Phishing domain
## Expired domain reuse
## Phòng thủ cơ bản
```bash
- Khóa domain (Registrar Lock)
- Bật DNSSEC
- Kiểm tra subdomain định kỳ
- Không public subdomain dev
- HTTPS + HSTS
```
# Website Terminology (thuật ngữ mảng website)
## Domain website (Được hiểu là một tên miền (url) trỏ tới website)
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
```bash
- Là hệ thống phần mềm quản lý toàn bộ hoạt động của một công ty trên một chỗ duy nhất
→ thay vì mỗi phòng ban dùng một file / phần mềm riêng.
- Không có ERP: → dữ liệu lệch nhau
  - Sale dùng Excel
  - HR dùng phần mềm khác
  - Kế toán dùng phần mềm khác
- Có ERP: Tất cả dùng một hệ thống, Thay đổi ở chỗ này → chỗ khác cập nhật theo
```
## Các luồng nghiệp vụ cơ bản trong ERP
### CRM (Customer Relationship Management)
```bash
- Quản lý khách hàng.
- Theo dõi khách từ lúc chưa mua → đã mua → chăm sóc sau bán
- Ví dụ đơn giản:
  - Lưu thông tin khách hàng (tên, SĐT, email)
  - Ghi lại khách đã hỏi gì, mua gì
  - Nhân viên sale gọi cho khách → cập nhật kết quả
Mục tiêu: không quên khách, bán hàng hiệu quả hơn
```
### HRM (Human Resource Management)
```bash
- Quản lý nhân sự, Quản lý con người trong công ty
- Ví dụ:
  - Thông tin nhân viên
  - Chấm công, nghỉ phép
  - Lương, thưởng
  - Phân quyền ai làm gì
- Mục tiêu: quản lý nhân sự rõ ràng, minh bạch
```
### Quy trình tạo Ticket / Công việc
```bash
- Tạo việc → giao người làm → theo dõi → hoàn thành
- Ví dụ:
  - Khách báo lỗi → tạo ticket
  - Giao cho nhân viên xử lý
  - Theo dõi trạng thái: Đang làm → Chờ → Hoàn thành
- Mục tiêu: không sót việc, ai làm gì đều rõ
```
# Work items (công việc cụ thể)
```bash
Với các work items cần tuân thủ Cycles (Chu kỳ giống sprint).
```
**Cycles**
```bash
- Là khoảng thời gian để  hoàn thành 1 work item (Ví dụ: 5 ngày, 1 tuần).
- Cycles có các trạng thái (đang hoạt động - work item sắp tới - hoàn thành)
```
**Timeline dependencies**
```bash
- Là liện hệ giữa các task với nhau.
```
# PRD (Product Requirements Document - tài liệu mô tả yêu cầu của sản phẩm)
```bash
Nó trả lời các câu hỏi:
  - Sản phẩm này dùng để làm gì?
  - Đối tượng người dùng là ai?
  - Có những tính năng nào?
  - Luồng sử dụng ra sao?
  - Tiêu chí nào để coi là hoàn thành?
```
**Ex: web quản lý dinh dưỡng và tập luyện**
```bash
Một PRD đơn giản có thể là:
  - Tên sản phẩm: Smart Recipe
  - Mục tiêu: Giúp người dùng lên kế hoạch tập luyện và ăn uống.
  - Đối tượng: Người muốn giảm cân, tăng cơ.
  - Chức năng
    + Đăng nhập
    + Xem bài tập
    + Tạo kế hoạch tập
    + Theo dõi calories
    + AI gợi ý thực đơn
  - Tiêu chí thành công
    + Người dùng tạo được workout plan.
    + AI trả lời dưới 3 giây.
=> PRD không chứa code, mà là tài liệu để Product Manager, Designer và Developer cùng hiểu sản phẩm.
```
# MVP (Minimum Viable Product - là phiên bản nhỏ nhất của sản phẩm nhưng vẫn sử dụng được)
```bash
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

Nếu làm hết ngay sẽ mất rất lâu. Thay vào đó, bạn tạo MVP:
  ✓ Đăng ký
  ✓ Đăng nhập
  ✓ Thêm món ăn
  ✓ Xem calories
  ✓ Workout đơn giản

Đưa cho người dùng dùng thử. Nếu họ thích, bạn mới phát triển thêm.
=> MVP = phiên bản tối thiểu nhưng có giá trị sử dụng.
```
# TPA Bảo hiểm (nghiệp vụ trong ngành bảo hiểm)
## Phân loại giấy tờ
```bash
Trong ngành bảo hiểm cần hiểu các loại giấy tờ.
```
**Giải thích các loại giấy tờ**
```bash
1. GRV                          # giấy ra viện
2. bảng kê                      # thường là bảng kê chi phí
3. hóa đơn                      # thường là hóa đơn giá trị gia tăng
4. đơn thuốc                    # thường là đơn thuốc 
5. chuẩn đoán hình ảnh          # thường là phiếu chuẩn đoán kết quả bệnh
6. lab_test                     # thường là phiếu kết quả cuối cùng
7. tóm tắt bệnh án              # thường là bản tóm tắt hồ sơ bệnh án
8. claimform                    # thường là giấy yêu cầu bồi thường
9. báo cáo y tế                 # thường là phiếu báo cáo y tế
10. bản tt tai nạn              # thường là bản tường trình tại nạn hoặc bản tường trình vụ việc
11. bảo hiểm y tế               # thường là thẻ bảo hiểm y tế
12. giấy chứng nhận phẫu thuật  # thường là giấy chứng nhận phẫu thuật
13. bảng kê type 2              # thường là phiếu thu tiền
14. hóa đơn type 2              # thường là hóa đơn bán hàng
```