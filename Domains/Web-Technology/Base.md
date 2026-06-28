- [context mới → cookie trống → chưa login](#context-mới--cookie-trống--chưa-login)
- [Chuẩn giao tiếp](#chuẩn-giao-tiếp)
  - [ASGI](#asgi)
- [Framework](#framework)
  - [Starlette](#starlette)
---
1. Cookie là gì? 🍪
Hiểu đơn giản:

Cookie = tờ giấy ghi chú mà website gửi cho trình duyệt giữ hộ

Website dùng cookie để nhớ bạn là ai, bạn đã làm gì trước đó.

Ví dụ đời thường (quán cà phê)

Bạn vào quán cà phê ☕

Lần đầu: nhân viên hỏi tên → ghi vào phiếu

Lần sau bạn quay lại, đưa phiếu → họ biết bạn là khách quen

📌 Tờ phiếu = cookie

Ví dụ trên website

Bạn đăng nhập Facebook

Bạn đóng trình duyệt

Mở lại vẫn đăng nhập

👉 Vì:

Facebook đã lưu cookie đăng nhập trong trình duyệt

Cookie dùng để làm gì?
Dùng cho	Ví dụ
Nhớ đăng nhập	Facebook, Gmail
Nhớ giỏ hàng	Shopee, Lazada
Nhớ ngôn ngữ	Tiếng Việt / English
Tracking	Quảng cáo bạn từng xem
Cookie trông như thế nào (không cần nhớ kỹ)
user_id=12345
session_token=abcxyz

2. Session là gì? (không phải section) 🧠

⚠️ Bạn đang hỏi session, không phải section
(Section = mục, chương → khác hoàn toàn)

Session là gì?
Hiểu đơn giản:

Session = hồ sơ tạm thời của bạn trên server

Cookie: nằm ở trình duyệt

Session: nằm ở server

Ví dụ đời thường (quán cà phê tiếp)

Bạn vào quán

Nhân viên tạo 1 hồ sơ cho bạn:

Khách A

Gọi cà phê sữa

Đang ngồi bàn số 3

📌 Hồ sơ đó = session

Nhân viên đưa bạn 1 thẻ số
📌 Thẻ số = session_id (được lưu trong cookie)

Khi bạn gọi thêm nước?

Bạn đưa thẻ số

Nhân viên nhìn hồ sơ → biết bạn là ai

➡️ Cookie chỉ chứa mã
➡️ Session chứa thông tin thật

3. Cookie & Session hoạt động cùng nhau thế nào?
Trình duyệt ----(cookie: session_id)---> Server
Server ----(dựa vào session_id tìm session)---> Biết bạn là ai

Ví dụ web thực tế

Bạn login

Server tạo session:

user = thang
role = admin


Server gửi cookie:

session_id = xyz123


Mỗi request sau:

Trình duyệt gửi cookie

Server tìm session → OK

4. So sánh dễ nhớ
Tiêu chí	Cookie	Session
Lưu ở đâu	Trình duyệt	Server
Ai tạo	Server	Server
Dung lượng	Nhỏ	Lớn
Bảo mật	Thấp hơn	Cao hơn
Mất khi	Xóa cookie	Server restart / timeout
5. Ví dụ cực dễ nhớ
❌ Không có cookie

Mỗi lần refresh → web hỏi: “Bạn là ai?”

❌ Có cookie nhưng không có session

Có thẻ số nhưng không có hồ sơ

✅ Có cả 2

Web chạy mượt

Nhớ trạng thái người dùng

6. Liên hệ với Playwright (cho bạn dễ hình dung)

Context ≈ trình duyệt ẩn danh

Cookie ≈ thông tin đăng nhập

Session ≈ trạng thái user trên server

context = await browser.new_context()
# context mới → cookie trống → chưa login

Tóm lại 1 câu cho dễ nhớ

🍪 Cookie = thẻ gửi xe
🧠 Session = hồ sơ trong bãi x
```bash
- Web hiện đại KHÔNG load 1 lần
- Có 3 tầng:
    + HTML khung (load ngay)
    + JS render DOM
    + JS fetch data khi có event (scroll, focus, viewport xuất hiện)


🧪 BÀI TEST 1 (BẮT BUỘC)

👉 Không viết crawler, chỉ debug:

Mở devtools

Reload page detail

KHÔNG scroll

Gõ trong console:

document.querySelectorAll('.re__pr-specs-content-item').length


👉 Sau đó scroll xuống → gõ lại

❓ Câu hỏi bạn phải trả lời được:

Trước scroll là bao nhiêu?

Sau scroll là bao nhiêu?

Vậy lỗi nằm ở Python hay JS?

📌 Khi bạn trả lời được → sang phần 2
# Domain 
```bash 
- Là địa chỉ website trên Internet để người dùng truy cập.
- Ví dụ:
    + google.com
    + facebook.com
    + myapi.com
- Thay vì phải nhớ địa chỉ IP như 142.250.190.78, ta dùng domain cho dễ nhớ.
```
**Ex: cấu trúc domain**
```bash
api.mywebsite.com

- com → top-level domain (TLD)
- mywebsite → tên chính
- api → subdomain
```
# Chuẩn giao tiếp
## ASGI
```bash
- ASGI (Asynchronous Server Gateway Interface) là chuẩn giao tiếp giữa:
    + Web server (uvicorn, daphne…)
    + Và ứng dụng Python (FastAPI, Django…)
- Nó cho phép xử lý bất đồng bộ (async/await)
- Hỗ trợ WebSocket, HTTP, background task
- Hiểu đơn giản: ASGI = phiên bản nâng cấp của WSGI để chạy async.
-> ASGI → chuẩn async cho web Python 
```
# Framework
## Starlette
```bash
- Starlette là một ASGI framework siêu nhẹ dùng để xây dựng web app async.
- FastAPI thực chất được xây dựng trên Starlette.
- Starlette cung cấp:
    + Routing
    + Middleware
    + WebSocket
    + Background tasks
    + ASGI support
- FastAPI chỉ bổ sung thêm:
Validation bằng Pydantic
Dependency Injection
Tự động sinh OpenAPI
```
Đây là một câu hỏi rất hay vì Nginx gần như xuất hiện trong mọi hệ thống backend production.

Nếu bạn học FastAPI, AI Agent, Docker, Kubernetes..., sớm muộn gì cũng sẽ gặp Nginx.

Nói ngắn gọn

Nginx là một Web Server và Reverse Proxy.

Nhưng câu này rất khó hiểu.

Hãy hiểu bằng ví dụ.

Không có Nginx

Giả sử bạn có FastAPI.

Internet

↓

FastAPI

↓

MariaDB

Người dùng

https://abc.com

↓

FastAPI

↓

Trả dữ liệu.

Đơn giản.

Nhưng production thì sao?

Một website có thể có

1000 request/s

Hoặc

100000 request/s

FastAPI không nên trực tiếp nhận toàn bộ Internet.

Người ta đặt thêm.

Internet

↓

Nginx

↓

FastAPI

Nginx đứng trước.

FastAPI đứng sau.

Hãy tưởng tượng

Một nhà hàng.

Không có lễ tân.

Khách

↓

Đầu bếp

Khách.

Cho tôi bàn.

Cho tôi nước.

Thanh toán.

Đầu bếp phải làm tất.

Rất mệt.

Có lễ tân.

Khách

↓

Lễ tân

↓

Đầu bếp

Lễ tân.

tiếp khách
hướng dẫn
phân luồng
trả lời những việc đơn giản

Đầu bếp.

Chỉ nấu ăn.

Nginx chính là

Lễ tân.
Reverse Proxy là gì?

Giả sử.

Bạn có.

FastAPI

Port 8000

Người dùng.

Không nên biết.

http://1.2.3.4:8000

Thay vào đó.

Người dùng.

https://abc.com

↓

Nginx.

↓

FastAPI.

Người dùng.

Không hề biết.

FastAPI ở đâu.

Pipeline.

Client

↓

Nginx

↓

FastAPI

↓

MariaDB
Reverse Proxy làm gì?

Ví dụ.

Bạn có.

/api

Nginx.

↓

FastAPI.

Bạn có.

/images

Nginx.

↓

Static File.

Bạn có.

/admin

Nginx.

↓

Admin Service.

Nginx giống.

Điều phối viên.
Load Balancer

Giả sử.

Bạn có.

1 FastAPI.

Nginx

↓

FastAPI

Một ngày.

Server quá tải.

Bạn tạo.

3 FastAPI.

          FastAPI 1

         /

Nginx

         \

          FastAPI 2

           \

            FastAPI 3

Nginx.

Tự chia.

Request.

Ví dụ.

100 request.

↓

FastAPI1

33

↓

FastAPI2

33

↓

FastAPI3

34

Đây gọi là.

Load Balancing.
SSL

Nếu không có Nginx.

FastAPI.

Phải xử lý.

HTTPS.

Khá phiền.

Có Nginx.

HTTPS

↓

Nginx

↓

HTTP

↓

FastAPI

SSL.

Dừng ở.

Nginx.

FastAPI.

Không cần biết.

Static File

Ví dụ.

Bạn có.

logo.png

Nếu.

FastAPI.

Trả.

↓

Không tối ưu.

Nginx.

Được sinh ra.

Để phục vụ.

Ảnh

CSS

JS

Video

PDF

Rất nhanh.

Gzip

FastAPI.

Trả.

{
...
}

500KB.

Nginx.

↓

Nén.

↓

100KB.

↓

Internet.

Nhanh hơn.

Cache

Ví dụ.

/logo.png

100000 người.

Đều tải.

Không cần.

FastAPI.

Nginx.

Lưu cache.

↓

Trả luôn.

Rate Limit

Ví dụ.

Một hacker.

Spam.

100000 request

Nginx.

Chặn.

429 Too Many Requests

FastAPI.

Không bị ảnh hưởng.

Routing

Ví dụ.

Bạn có.

/api

↓

FastAPI.

/chat

↓

AI Service.

/admin

↓

Admin.

Nginx.

Biết.

Đường nào.

Đi đâu.

Docker

Production.

Thường.

Docker

↓

Nginx Container

↓

FastAPI Container
Kubernetes
Internet

↓

Ingress

↓

Nginx

↓

Pod

↓

FastAPI
AI Agent

Ví dụ.

Bạn có.

Gemini

Qdrant

Redis

MariaDB

FastAPI

Production.

Internet

↓

Nginx

↓

FastAPI

↓

Gemini

↓

Qdrant

↓

Redis

↓

MariaDB
Nginx có thay FastAPI không?

Không.

FastAPI.

Viết API.

Nginx.

Không biết.

Business Logic.

Ví dụ.

FastAPI.

@app.get("/user")

Nginx.

Không thể.

Thay.

Nginx có thay Redis không?

Không.

Redis.

Lưu.

RAM.

Nginx.

Chỉ.

Proxy.

Nginx có thay Docker không?

Không.

Docker.

Là.

Container.

Nginx.

Là.

Application.

Pipeline Production chuẩn

Đây là kiến trúc rất phổ biến cho một hệ thống FastAPI + AI Agent:

                    Internet
                        │
                        ▼
                     Nginx
        ┌───────────────┼────────────────┐
        │               │                │
        ▼               ▼                ▼
   /api/*          /static/*        /admin/*
        │               │                │
        ▼               ▼                ▼
     FastAPI       File tĩnh      Admin Service
        │
        ▼
     Service Layer
        │
        ├───────────────┐
        ▼               ▼
    MariaDB         Redis
        │
        ├───────────────┐
        ▼               ▼
    Qdrant          Gemini/OpenAI
Bạn cần học Nginx đến mức nào?

Với mục tiêu trở thành Backend AI Engineer, mình khuyên theo thứ tự:

Reverse Proxy ⭐⭐⭐⭐⭐
HTTPS (SSL/TLS) ⭐⭐⭐⭐⭐
Load Balancing ⭐⭐⭐⭐⭐
Static File ⭐⭐⭐⭐☆
Rate Limiting ⭐⭐⭐⭐☆
Caching ⭐⭐⭐⭐☆
Docker + Nginx ⭐⭐⭐⭐⭐
Kubernetes Ingress (Nginx Ingress Controller) ⭐⭐⭐⭐☆
Tóm tắt dễ nhớ

Hãy nhớ một câu:

FastAPI là người nấu ăn, Nginx là lễ tân.

FastAPI xử lý nghiệp vụ: đăng nhập, tạo workout, gọi Gemini, truy vấn MariaDB...
Nginx đứng trước FastAPI để:
nhận request từ Internet,
chuyển request đến đúng service,
cân bằng tải giữa nhiều instance FastAPI,
xử lý HTTPS,
phục vụ file tĩnh,
cache và giới hạn tốc độ truy cập.

Vì vậy, trong hầu hết các hệ thống production, người dùng gần như không bao giờ truy cập trực tiếp vào FastAPI. Họ luôn đi qua Nginx (hoặc một reverse proxy/load balancer tương tự như HAProxy, Envoy, Traefik hay dịch vụ cân bằng tải trên cloud).