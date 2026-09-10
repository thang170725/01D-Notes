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
- [Computer Network (mạng máy tính)](#computer-network-mạng-máy-tính)
  - [DNS (Domain Name System dùng để phân giải tên miền)](#dns-domain-name-system-dùng-để-phân-giải-tên-miền)
  - [proxy](#proxy)
  - [nslookup ...](#nslookup-)
  - [Test-NetConnection -ComputerName 123.123.123.123 -Port 80](#test-netconnection--computername-123123123123--port-80)
  - [gRPC](#grpc)
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
  - [Ask](#ask)
    - [Claim trong lĩnh vực bảo hiểm là gì?](#claim-trong-lĩnh-vực-bảo-hiểm-là-gì)
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
# Computer Network (mạng máy tính)
## DNS (Domain Name System dùng để phân giải tên miền)
**Ex**
```bash
google.com A → 142.250.190.78
```
## proxy
## nslookup ...
**Ex**
```bash
PS C:\Users\thang.ld> nslookup sv.haui.edu.vn
Server:  HO-ADC-01.insmart.com.vn
Address:  192.168.1.2

Non-authoritative answer:
Name:    sv.haui.edu.vn
Address:  103.140.39.111
```
## Test-NetConnection -ComputerName 123.123.123.123 -Port 80
## gRPC 
gRPC là một framework/protocol dùng để cho các service giao tiếp với nhau qua mạng.

Nếu nói đơn giản:

gRPC = một cách để Backend A gọi hàm của Backend B qua network, gần giống như gọi một function bình thường.

Nó đặc biệt phổ biến trong microservices.

1. Ví dụ thực tế

Giả sử hệ thống của bạn có:

                    ┌──────────────┐
                    │   Frontend   │
                    └──────┬───────┘
                           │ HTTP
                           ▼
                    ┌──────────────┐
                    │  API Server  │
                    └──────┬───────┘
                           │
                    gRPC   │
                           ▼
              ┌──────────────────────┐
              │  User Service       │
              └──────────────────────┘

API Server muốn lấy thông tin user.

Nếu dùng REST:

GET /users/123

Nếu dùng gRPC, bạn có thể định nghĩa một function:

GetUser(user_id)

Sau đó API Server gọi:

user = user_service.GetUser(user_id=123)

Nhưng User Service thực tế nằm trên một server khác.

gRPC sẽ lo phần:

API Server
    │
    │ serialize request
    ▼
   Network
    │
    ▼
User Service
    │
    │ deserialize
    ▼
GetUser(...)
    │
    ▼
response

Tức là bạn có cảm giác như đang gọi function, nhưng thực chất function đó chạy ở service khác.

2. gRPC viết tắt của gì?

gRPC ban đầu được hiểu là:

Google Remote Procedure Call

Trong đó quan trọng nhất là:

RPC = Remote Procedure Call

Tức là:

Gọi một procedure/function ở một máy khác thông qua network.

Ví dụ bình thường:

result = add(10, 20)

Function add() chạy trong process của bạn.

RPC:

result = remote_add(10, 20)

Function thực tế chạy ở:

Server B

Bạn đang ở:

Server A

gRPC chính là một framework rất phổ biến để thực hiện kiểu giao tiếp này.

3. gRPC khác REST API như thế nào?

Đây là phần rất đáng hiểu.

REST thường:

Client
   │
   │ HTTP
   │ GET /users/123
   ▼
Server

Response thường là JSON:

{
  "id": 123,
  "name": "Thang"
}

gRPC thường:

Client
   │
   │ HTTP/2
   │
   │ binary data
   ▼
Server

Dữ liệu thường được serialize bằng:

Protocol Buffers (Protobuf)

Ví dụ định nghĩa service:

service UserService {
    rpc GetUser(GetUserRequest)
        returns (User);
}

Request:

message GetUserRequest {
    int32 user_id = 1;
}

Response:

message User {
    int32 id = 1;
    string name = 2;
}

Sau đó gRPC có thể generate code cho Python, Go, Java, C#, C++...

4. Tại sao phải dùng .proto?

Đây là điểm khác REST rất rõ.

Bạn có thể coi .proto là hợp đồng (contract) giữa hai service.

Ví dụ:

syntax = "proto3";

service UserService {
    rpc GetUser(GetUserRequest)
        returns (User);
}

message GetUserRequest {
    int32 user_id = 1;
}

message User {
    int32 id = 2;
    string name = 3;
}

Nó nói rõ:

UserService
    │
    └── GetUser()
          │
          ├── Input: GetUserRequest
          │
          └── Output: User

Service A và Service B đều dựa trên contract này.

5. REST giống gọi URL

REST:

POST /api/users

body:

{
    "name": "Thang"
}

Bạn phải biết:

URL
HTTP method
headers
JSON format
status code

gRPC:

UserService.CreateUser(...)

Contract đã định nghĩa sẵn:

rpc CreateUser(CreateUserRequest)
    returns (User);

Client có thể gọi như một method:

response = stub.CreateUser(
    CreateUserRequest(name="Thang")
)

Đây là lý do RPC có cảm giác rất giống function call.

6. Tại sao gRPC nhanh?

Một lý do quan trọng là Protobuf + binary serialization.

REST thường:

{
    "id": 123,
    "name": "Thang"
}

Đây là text.

gRPC thường serialize thành binary:

01001001 00101010 ...

Binary thường:

nhỏ hơn JSON
serialize/deserialize nhanh
truyền qua network hiệu quả

Ngoài ra gRPC sử dụng HTTP/2, có các tính năng như multiplexing và streaming.

7. gRPC rất mạnh ở Streaming

REST thường kiểu:

Request
   ↓
Response

gRPC hỗ trợ nhiều kiểu:

Unary

Giống REST:

Client ───── Request ─────> Server
Client <──── Response ───── Server
Server streaming
Client ───── Request ─────> Server

Client <──── Response 1 ─── Server
Client <──── Response 2 ─── Server
Client <──── Response 3 ─── Server
Client <──── Response 4 ─── Server

Ví dụ:

Server liên tục gửi dữ liệu về client.

Client streaming
Client ── data 1 ──>
Client ── data 2 ──>
Client ── data 3 ──>
Client ── data 4 ──>

              Server
                 │
                 ▼
              Response
Bidirectional streaming

Cả hai bên cùng stream:

Client                 Server

  ───── data ─────────>
  <───── data ─────────
  ───── data ─────────>
  <───── data ─────────
  ───── data ─────────>
  <───── data ─────────

Cái này rất hữu ích cho những hệ thống realtime hoặc xử lý stream.

8. gRPC thường được dùng ở đâu?

Đặc biệt là:

Microservices

Ví dụ một công ty có:

                  API Gateway
                       │
          ┌────────────┼────────────┐
          │            │            │
          ▼            ▼            ▼
      User Service  Payment      Order
          │          Service     Service
          │            │            │
          └────── gRPC ─────────────┘

Các service giao tiếp nội bộ với nhau bằng gRPC.

Ví dụ:

Order Service
      │
      │ GetUser(user_id)
      ▼
User Service

rồi:

Order Service
      │
      │ CheckPayment(...)
      ▼
Payment Service
9. Tại sao không dùng REST hết?

REST hoàn toàn có thể dùng cho microservices.

Nhưng khi hệ thống lớn:

Service A
    ↓
Service B
    ↓
Service C
    ↓
Service D

có rất nhiều request nội bộ.

gRPC có lợi thế:

✓ nhanh
✓ binary
✓ HTTP/2
✓ strongly typed
✓ contract rõ ràng
✓ code generation
✓ streaming

Nên nhiều hệ thống chọn:

                    Internet
                       │
                       ▼
                REST / GraphQL
                       │
                       ▼
                 API Gateway
                       │
                ┌──────┴──────┐
                │             │
              gRPC          gRPC
                │             │
                ▼             ▼
             Service A     Service B
10. Một kiến trúc rất thực tế

Ví dụ hệ thống bán hàng:

Frontend
   │
   │ HTTPS / REST
   ▼
API Gateway
   │
   ├──── gRPC ────> User Service
   │
   ├──── gRPC ────> Product Service
   │
   ├──── gRPC ────> Order Service
   │
   └──── gRPC ────> Payment Service

Frontend không nhất thiết phải biết gRPC.

Frontend chỉ cần:

GET /api/products/123

Gateway nhận request:

GET /api/products/123

rồi bên trong gọi:

ProductService.GetProduct(123)

bằng gRPC.

11. Liên hệ với project Backend của bạn

Nếu backend của bạn hiện tại kiểu:

Frontend
    │
    │ HTTP
    ▼
FastAPI
    │
    ├── PostgreSQL
    ├── AI Agent
    ├── Redis
    └── ...

thì bạn chưa nhất thiết cần gRPC.

Nhưng nếu sau này tách thành:

                FastAPI
                   │
       ┌───────────┼────────────┐
       │           │            │
       ▼           ▼            ▼
 User Service   AI Service   Tool Service
       │           │            │
       └───── gRPC ┴────── gRPC ┘

thì gRPC bắt đầu rất có ý nghĩa.

Ví dụ:

FastAPI
   │
   │ "Hãy chạy AI Agent này"
   ▼
AI Service
   │
   │
   └── xử lý LangGraph

Thay vì AI Service phải expose REST endpoint như:

POST /run-agent

thì có thể định nghĩa:

rpc RunAgent(RunAgentRequest)
    returns (RunAgentResponse);

và service khác gọi:

response = ai_stub.RunAgent(request)
12. Một câu cực kỳ quan trọng

Bạn có thể phân biệt thế này:

REST
↓
"Gửi HTTP request tới URL"

gRPC
↓
"Gọi một method/function của remote service"

Nhưng gRPC vẫn truyền qua network.

Nó không phải là gọi function thần kỳ không cần network.

Bên dưới vẫn là:

Client
   │
   │ serialize
   ▼
Network
   │
   ▼
Server
   │
   │ deserialize
   ▼
Function
   │
   ▼
Response
Tóm lại
	REST	gRPC
Giao tiếp	HTTP	HTTP/2
Data phổ biến	JSON	Protobuf
Kiểu gọi	URL/API	Method/RPC
Type safety	Thường lỏng hơn	Rất mạnh
Performance	Tốt	Thường rất tốt
Streaming	Có nhưng không phải trọng tâm	Rất mạnh
Microservices	Có	Rất phổ biến
Browser gọi trực tiếp	Rất thuận tiện	Không thuận tiện bằng
Internal service-to-service	Tốt	Rất phù hợp

Mental model nên nhớ:

                    API bên ngoài
                         │
                    REST/GraphQL
                         │
                         ▼
                   API Gateway
                         │
               ┌─────────┴─────────┐
               │                   │
             gRPC                 gRPC
               │                   │
               ▼                   ▼
         User Service        AI Service
                                   │
                                   ▼
                              LangGraph

Nếu bạn đang học Backend + Microservices, sau Dijkstra thì mình khuyên hiểu tiếp HTTP → REST → RPC → gRPC → Protobuf → Microservices, vì chúng liên kết với nhau khá chặt.
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
**Luồng nghiệp vụ**
```bash
                                      ┌───────────────────────────────┐
                                      │      ĐẠI HỘI CỔ ĐÔNG         │
                                      │       Shareholders            │
                                      └───────────────┬───────────────┘
                                                      │
                                                      ▼
                                      ┌───────────────────────────────┐
                                      │       HỘI ĐỒNG QUẢN TRỊ      │
                                      │     Board of Directors        │
                                      │ - Định hướng chiến lược       │
                                      │ - Giám sát                    │
                                      │ - Bổ nhiệm lãnh đạo           │
                                      └───────────────┬───────────────┘
                                                      │
                                                      ▼
                                      ┌───────────────────────────────┐
                                      │       TỔNG GIÁM ĐỐC / CEO     │
                                      │ - Điều hành toàn công ty      │
                                      └───────────────┬───────────────┘
                                                      │
          ┌───────────────────────────────────────────┼───────────────────────────────────────────┐
          │                                           │                                           │
          ▼                                           ▼                                           ▼
┌──────────────────────┐                   ┌──────────────────────┐                   ┌──────────────────────┐
│ KHỐI KINH DOANH      │                   │ KHỐI NGHIỆP VỤ BH    │                   │ KHỐI HỖ TRỢ          │
│ Business             │                   │ Insurance Operations │                   │ Corporate Support    │
└──────────┬───────────┘                   └──────────┬───────────┘                   └──────────┬───────────┘
           │                                          │                                          │
           │                                          │                                          │
   ┌───────┼────────┐                   ┌─────────────┼─────────────────┐              ┌──────────┼───────────┐
   │       │        │                   │             │                 │              │          │           │
   ▼       ▼        ▼                   ▼             ▼                 ▼              ▼          ▼           ▼
Marketing Sales  Customer            Product      Underwriting     Servicing          HR        Admin      Legal
         /Agent  Service                                           /Policy Admin                              │
                                                                                                              │
                                                                                                              ▼
                                                                                                         Compliance


================================================================================================================
                                      QUY TRÌNH KINH DOANH CHÍNH
================================================================================================================


[1] MARKETING / TIẾP CẬN KHÁCH HÀNG
            │
            │ quảng cáo, campaign, giới thiệu sản phẩm
            ▼
┌──────────────────────────────┐
│       KHÁCH HÀNG TIỀM NĂNG   │
│          Prospect             │
└───────────────┬──────────────┘
                │
                │ quan tâm sản phẩm
                ▼
┌──────────────────────────────┐
│       SALES / AGENT          │
│ - Tư vấn                     │
│ - Giải thích quyền lợi       │
│ - Báo phí                    │
│ - Thu thập thông tin         │
└───────────────┬──────────────┘
                │
                ▼


[2] THẨM ĐỊNH TRƯỚC KHI CẤP BẢO HIỂM

┌──────────────────────────────┐
│        UNDERWRITING          │
│ - Đánh giá rủi ro            │
│ - Kiểm tra sức khỏe          │
│ - Kiểm tra nghề nghiệp       │
│ - Xem lịch sử bảo hiểm       │
│ - Quyết định điều kiện BH    │
└───────────────┬──────────────┘
                │
                ├──────────────► Reject
                │
                ├──────────────► Accept with conditions
                │
                ▼
             Accept
                │
                ▼


[3] PHÁT HÀNH HỢP ĐỒNG

┌──────────────────────────────┐
│       POLICY ADMIN           │
│ - Tạo hợp đồng               │
│ - Cấp policy number          │
│ - Ghi nhận quyền lợi         │
│ - Ghi nhận phí               │
│ - Ghi nhận người thụ hưởng   │
└───────────────┬──────────────┘
                │
                ▼
┌──────────────────────────────┐
│      INSURANCE POLICY        │
│      HỢP ĐỒNG BẢO HIỂM       │
└───────────────┬──────────────┘
                │
                ▼


[4] QUẢN LÝ HỢP ĐỒNG / SERVICING

┌──────────────────────────────┐
│          SERVICING           │
│ - Đổi thông tin khách hàng   │
│ - Gia hạn                    │
│ - Thu phí                    │
│ - Thay đổi quyền lợi         │
│ - Đổi người thụ hưởng        │
│ - Cấp lại hợp đồng           │
│ - Tra cứu quyền lợi          │
└───────────────┬──────────────┘
                │
                │
                │ hợp đồng còn hiệu lực
                ▼


================================================================================================================
                                        KHI CÓ SỰ KIỆN BẢO HIỂM
================================================================================================================


                         ┌──────────────────────────────┐
                         │         KHÁCH HÀNG           │
                         │ - Người được bảo hiểm        │
                         │ - Người thụ hưởng            │
                         └───────────────┬──────────────┘
                                         │
                                         │ xảy ra sự kiện
                                         │
                                         │ VD:
                                         │ - Nằm viện
                                         │ - Tai nạn
                                         │ - Phẫu thuật
                                         │ - Bệnh hiểm nghèo
                                         │ - Tử vong
                                         ▼


[5] CLAIM SUBMISSION

┌──────────────────────────────┐
│       CLAIM FORM             │
│ - Điền yêu cầu bồi thường    │
│ - Policy number              │
│ - Thông tin người BH         │
│ - Sự kiện bảo hiểm           │
│ - Số tiền yêu cầu            │
└───────────────┬──────────────┘
                │
                │ kèm tài liệu
                ▼

┌─────────────────────────────────────────┐
│          CLAIM DOCUMENTS                │
│                                         │
│ - Claim Form                            │
│ - CCCD / thông tin KH                   │
│ - Giấy ra viện                          │
│ - Hóa đơn viện phí                      │
│ - Đơn thuốc                             │
│ - Kết quả xét nghiệm                    │
│ - Chẩn đoán                             │
│ - Hồ sơ bệnh án                         │
│ - Giấy chứng tử                         │
│ - Chứng từ khác                         │
└──────────────────┬──────────────────────┘
                   │
                   ▼


[6] CUSTOMER SERVICE / CLAIM INTAKE

┌──────────────────────────────┐
│      CUSTOMER SERVICE        │
│ - Hướng dẫn khách hàng       │
│ - Tiếp nhận yêu cầu          │
│ - Giải đáp thắc mắc          │
│ - Kiểm tra sơ bộ             │
└───────────────┬──────────────┘
                │
                ▼

┌──────────────────────────────┐
│        CLAIM INTAKE          │
│ - Tạo Claim ID               │
│ - Gom giấy tờ                │
│ - Scan hồ sơ                 │
│ - Kiểm tra số lượng tài liệu │
│ - Đóng thành bộ hồ sơ        │
└───────────────┬──────────────┘
                │
                ▼


[7] DOCUMENT PROCESSING / AI / OCR

┌──────────────────────────────────────┐
│              AI / OCR                │
│                                      │
│ 1. OCR                              │
│    PDF/Image ───────────► Text        │
│                                      │
│ 2. Document Classification           │
│    ├─ Invoice                        │
│    ├─ Prescription                   │
│    ├─ Discharge Summary              │
│    ├─ Lab Result                     │
│    ├─ Claim Form                     │
│    └─ Other                          │
│                                      │
│ 3. Data Extraction                   │
│    ├─ Patient name                   │
│    ├─ Hospital                       │
│    ├─ Diagnosis                      │
│    ├─ Amount                         │
│    ├─ Admission date                 │
│    └─ Discharge date                 │
│                                      │
│ 4. Table Extraction                  │
│                                      │
│ 5. Validation / Normalization        │
│                                      │
│ 6. Structured Output                 │
│    JSON / Database record            │
└──────────────────┬───────────────────┘
                   │
                   │ structured data
                   ▼

┌──────────────────────────────┐
│       CLAIM DATABASE         │
│ / Claim Management System    │
└───────────────┬──────────────┘
                │
                ▼


[8] CLAIM PROCESSING

┌──────────────────────────────────────┐
│          CLAIM PROCESSOR             │
│                                      │
│ - Kiểm tra đủ hồ sơ                  │
│ - Kiểm tra thông tin OCR             │
│ - Kiểm tra policy                    │
│ - Kiểm tra người được BH             │
│ - Kiểm tra thời hạn hợp đồng         │
│ - Kiểm tra quyền lợi                 │
│ - Kiểm tra điều khoản loại trừ       │
│ - Kiểm tra lịch sử claim             │
│ - Tính quyền lợi có thể được hưởng   │
└──────────────────┬───────────────────┘
                   │
                   ├──────────────► Thiếu hồ sơ
                   │                    │
                   │                    ▼
                   │          Customer Service
                   │                    │
                   │                    ▼
                   │             yêu cầu bổ sung
                   │                    │
                   │                    ▼
                   │                Customer
                   │
                   ▼


[9] CLAIM ASSESSMENT

                  ┌──────────────────────────────┐
                  │       CLAIM ASSESSOR         │
                  │ - Đánh giá hồ sơ             │
                  │ - Xác minh bệnh / sự kiện    │
                  │ - Kiểm tra điều khoản        │
                  │ - Tính số tiền chi trả       │
                  └──────────────┬───────────────┘
                                 │
             ┌───────────────────┼────────────────────┐
             │                   │                    │
             ▼                   ▼                    ▼
       Policy Check        Benefit Check        Document Check
             │                   │                    │
             └───────────────────┼────────────────────┘
                                 │
                                 ▼


[10] FRAUD / RISK CHECK

                         ┌──────────────────────────────┐
                         │        FRAUD CHECK           │
                         │ - Claim bất thường           │
                         │ - Claim trùng                │
                         │ - Hóa đơn bất thường         │
                         │ - Hospital pattern           │
                         │ - Lịch sử claim đáng ngờ     │
                         └──────────────┬───────────────┘
                                        │
                         ┌──────────────┴──────────────┐
                         │                             │
                         ▼                             ▼
                    Normal Case                  Suspicious
                         │                             │
                         │                             ▼
                         │                  Fraud Investigation
                         │                             │
                         └──────────────┬──────────────┘
                                        ▼


[11] CLAIM DECISION

                         ┌──────────────────────────────┐
                         │          DECISION            │
                         └──────────────┬───────────────┘
                                        │
                     ┌──────────────────┼──────────────────┐
                     │                  │                  │
                     ▼                  ▼                  ▼
                  Approve            Reject         Request Info
                     │                  │                  │
                     │                  │                  └────► Customer
                     │                  │
                     │                  └────► Customer Service
                     │                           │
                     │                           ▼
                     │                     Thông báo từ chối
                     ▼


[12] APPROVAL HIERARCHY

                ┌──────────────────────────────┐
                │     CLAIM SUPERVISOR         │
                │     Level 1 Approval         │
                └──────────────┬───────────────┘
                               │
                     số tiền lớn hơn limit
                               │
                               ▼
                ┌──────────────────────────────┐
                │       CLAIM MANAGER          │
                │       Level 2 Approval       │
                └──────────────┬───────────────┘
                               │
                     số tiền rất lớn
                               │
                               ▼
                ┌──────────────────────────────┐
                │ HEAD OF CLAIMS / DIRECTOR    │
                │ Level 3 Approval             │
                └──────────────┬───────────────┘
                               │
                               ▼


[13] FINANCE / ACCOUNTING

┌──────────────────────────────┐
│          FINANCE             │
│ - Nhận lệnh chi trả          │
│ - Kiểm tra thông tin bank    │
│ - Chuẩn bị payment           │
└───────────────┬──────────────┘
                │
                ▼
┌──────────────────────────────┐
│         ACCOUNTING           │
│ - Hạch toán                  │
│ - Ghi nhận chi phí claim     │
│ - Đối soát                   │
│ - Báo cáo                    │
└───────────────┬──────────────┘
                │
                ▼
┌──────────────────────────────┐
│            BANK              │
│      Chuyển khoản tiền       │
└───────────────┬──────────────┘
                │
                ▼


[14] KHÁCH HÀNG NHẬN TIỀN

┌──────────────────────────────┐
│          CUSTOMER            │
│                              │
│       Nhận tiền bảo hiểm     │
└───────────────┬──────────────┘
                │
                ▼
┌──────────────────────────────┐
│      CUSTOMER SERVICE        │
│ - Thông báo kết quả          │
│ - Giải thích quyết định      │
│ - Hỗ trợ khiếu nại           │
└──────────────────────────────┘


================================================================================================================
                                         CÁC PHÒNG BAN HỖ TRỢ
================================================================================================================


CEO
 │
 ├── IT / TECHNOLOGY
 │     │
 │     ├── Infrastructure
 │     │     ├── Server
 │     │     ├── Network
 │     │     ├── Cloud
 │     │     └── Storage
 │     │
 │     ├── Application Development
 │     │     ├── Claim System
 │     │     ├── Policy System
 │     │     ├── CRM
 │     │     └── Internal Apps
 │     │
 │     ├── Helpdesk
 │     │
 │     ├── Database Administration
 │     │
 │     └── Cyber Security
 │
 ├── DATA
 │     │
 │     ├── Data Engineering
 │     ├── Data Warehouse
 │     ├── BI / Reporting
 │     ├── Analytics
 │     ├── Data Governance
 │     └── AI / ML / OCR
 │
 ├── FINANCE
 │     │
 │     ├── Accounting
 │     ├── Treasury
 │     ├── Payment
 │     ├── Budget
 │     ├── Tax
 │     └── Financial Reporting
 │
 ├── LEGAL
 │     │
 │     ├── Hợp đồng
 │     ├── Tư vấn pháp lý
 │     └── Tranh chấp
 │
 ├── COMPLIANCE
 │     │
 │     ├── Tuân thủ pháp luật
 │     ├── Quy định bảo hiểm
 │     ├── AML / KYC nếu áp dụng
 │     └── Internal policy
 │
 ├── RISK MANAGEMENT
 │     │
 │     ├── Insurance Risk
 │     ├── Operational Risk
 │     ├── Financial Risk
 │     ├── Cyber Risk
 │     └── Fraud Risk
 │
 ├── INTERNAL AUDIT
 │     │
 │     ├── Kiểm tra quy trình
 │     ├── Kiểm soát nội bộ
 │     └── Báo cáo HĐQT
 │
 ├── HR
 │     │
 │     ├── Recruitment
 │     ├── Payroll
 │     ├── Training
 │     ├── Performance
 │     └── Employee Benefits
 │
 ├── ADMIN
 │     │
 │     ├── Reception
 │     ├── Văn phòng
 │     ├── Tài sản
 │     └── Hậu cần
 │
 ├── PROCUREMENT
 │     │
 │     ├── Mua laptop
 │     ├── Mua server
 │     ├── License phần mềm
 │     ├── Vendor
 │     └── Contract mua sắm
 │
 └── CORPORATE COMMUNICATION
       │
       ├── PR
       ├── Truyền thông nội bộ
       ├── Thương hiệu
       └── Quan hệ công chúng


================================================================================================================
                                       CÁC BÊN NGOÀI CÔNG TY
================================================================================================================


                              INSURANCE COMPANY
                                      │
       ┌──────────────────────────────┼───────────────────────────────┐
       │                              │                               │
       ▼                              ▼                               ▼
┌───────────────┐             ┌───────────────┐               ┌───────────────┐
│   CUSTOMER    │             │   HOSPITAL    │               │     BANK      │
│ Khách hàng    │             │ Bệnh viện     │               │ Ngân hàng     │
└───────────────┘             └───────────────┘               └───────────────┘
                                      │
                                      │ hồ sơ y tế
                                      ▼
                                    Claim

       ┌──────────────────────────────┼───────────────────────────────┐
       │                              │                               │
       ▼                              ▼                               ▼
┌───────────────┐             ┌───────────────┐               ┌───────────────┐
│   REGULATOR   │             │ REINSURANCE   │               │    VENDOR     │
│ Cơ quan QL    │             │ Tái bảo hiểm  │               │ Nhà cung cấp  │
└───────────────┘             └───────────────┘               └───────────────┘


================================================================================================================
                                   TÓM TẮT LUỒNG TOÀN CÔNG TY
================================================================================================================


Marketing
   │
   ▼
Sales / Agent
   │
   ▼
Customer
   │
   ▼
Underwriting
   │
   ▼
Policy Issuance
   │
   ▼
Servicing
   │
   ▼
Insurance Event
   │
   ▼
Claim Form
   │
   ▼
Claim Documents
   │
   ▼
Customer Service / Claim Intake
   │
   ▼
AI / OCR
   │
   ▼
Structured Data / Database
   │
   ▼
Claim Processor
   │
   ▼
Claim Assessor
   │
   ├────────► Fraud / Risk
   │
   ▼
Decision
   │
   ├────────► Reject ───────► Customer
   │
   └────────► Approve
                  │
                  ▼
            Supervisor
                  │
                  ▼
            Claim Manager
                  │
                  ▼
               Finance
                  │
                  ▼
             Accounting
                  │
                  ▼
                Bank
                  │
                  ▼
              Customer
```
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
## Ask 
### Claim trong lĩnh vực bảo hiểm là gì?
```bash
Claim = yêu cầu bồi thường / yêu cầu giải quyết quyền lợi bảo hiểm.

Ví dụ khách hàng mua bảo hiểm sức khỏe, đi bệnh viện và phát sinh viện phí. Sau đó khách gửi hồ sơ cho công ty bảo hiểm để yêu cầu thanh toán.

Quy trình có thể hình dung:

Khách hàng → gửi claim → công ty bảo hiểm thẩm định → duyệt/từ chối → chi trả

Ví dụ:

Customer submits a claim for medical expenses.
→ Khách hàng gửi yêu cầu bồi thường chi phí y tế.

Trong hệ thống bảo hiểm, claim thường không chỉ là một tờ giấy mà có thể là một hồ sơ/case gồm:

Claim ID
Thông tin khách hàng
Hợp đồng bảo hiểm
Ngày xảy ra sự kiện
Loại tổn thất/quyền lợi
Số tiền yêu cầu
Chứng từ
Kết quả thẩm định
Số tiền được chi trả
2. Claim Form là gì?

Claim Form = mẫu đơn yêu cầu bồi thường / mẫu khai yêu cầu giải quyết quyền lợi bảo hiểm.

Đây là form mà khách hàng hoặc bên liên quan điền để tạo một claim.

Ví dụ Claim Form có các trường:

Claim Form

Policy Number:     POL123456
Customer Name:     Nguyen Van A
Date of Incident:  01/09/2026
Claim Type:        Medical
Amount Claimed:    10,000,000 VND

Description:
...

Attachments:
- Hospital bill
- Medical report
- Prescription

Sau khi submit Claim Form → hệ thống tạo Claim.

Nói đơn giản:

Claim Form = cái form để khai báo
Claim = hồ sơ/yêu cầu bồi thường được tạo ra từ đó

3. "Bên/phòng Claim" là gì?

Nếu trong công ty bảo hiểm người ta nói:

"Chuyển hồ sơ sang bên Claim."

thì bên Claim thường là bộ phận giải quyết bồi thường/quyền lợi bảo hiểm.

Họ có thể phụ trách:

Receive claim → Check documents → Assess → Approve/Reject → Calculate payout → Payment

Ví dụ:

Sales: bán bảo hiểm
Underwriting: thẩm định/risk trước khi cấp hợp đồng
Policy/Operations: quản lý hợp đồng
Claim: xử lý yêu cầu bồi thường
Finance: xử lý tài chính/chi trả

Một điểm dễ nhầm là Claim không nhất thiết chỉ là "bồi thường". Trong bảo hiểm nhân thọ/sức khỏe, nó còn có thể bao gồm giải quyết quyền lợi bảo hiểm như tử vong, nằm viện, phẫu thuật, bệnh hiểm nghèo, đáo hạn... tùy sản phẩm.

Nếu bạn đang làm hệ thống/phần mềm bảo hiểm, mình có thể giải thích tiếp cho bạn Claim → Claim Form → Claim Assessment → Claim Decision → Payment và 
database của từng phần thường thiết kế như thế nào.
```