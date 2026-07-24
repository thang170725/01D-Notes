- [context mới → cookie trống → chưa login](#context-mới--cookie-trống--chưa-login)
- [Chuẩn giao tiếp](#chuẩn-giao-tiếp)
  - [ASGI](#asgi)
- [Framework](#framework)
  - [Starlette](#starlette)
---
# Cookie (tờ giấy ghi chú mà website gửi cho trình duyệt giữ hộ)
```bash
Website dùng cookie để nhớ bạn là ai, bạn đã làm gì trước đó.

Ví dụ đời thường (quán cà phê)
    Bạn vào quán cà phê ☕
        - Lần đầu: nhân viên hỏi tên → ghi vào phiếu
        - Lần sau bạn quay lại, đưa phiếu → họ biết bạn là khách quen

Ví dụ trên website
    Bạn đăng nhập Facebook
        - Bạn đóng trình duyệt
        - Mở lại vẫn đăng nhập 👉 Vì: Facebook đã lưu cookie đăng nhập trong trình duyệt
```
## Session (hồ sơ tạm thời của bạn trên server)
```bash
- Cookie: nằm ở trình duyệt
- Session: nằm ở server

Ví dụ đời thường:
    Bạn vào quán
        - Nhân viên tạo 1 hồ sơ cho bạn:
            Khách A
                - Gọi cà phê sữa
                - Đang ngồi bàn số 3
            => Hồ sơ đó = session

        - Nhân viên đưa bạn 1 thẻ số
            Thẻ số = session_id (được lưu trong cookie)
```
**Ex: web thực tế**
```bash
Bạn login
    Server tạo session:
        - user = thang
        - role = admin

    Server gửi cookie:
        - session_id = xyz123

    Mỗi request sau:
        Trình duyệt gửi cookie. Server tìm session → OK
```
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
# Nginx (là một Web Server và Reverse Proxy)
**Không có Nginx**
```bash
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


Nhưng production thì sao? Một website có thể có 1000 request/s Hoặc 100000 request/s -> FastAPI không nên trực tiếp nhận toàn bộ Internet.
    Người ta đặt thêm.
        Internet
        ↓
        Nginx
        ↓
        FastAPI
```