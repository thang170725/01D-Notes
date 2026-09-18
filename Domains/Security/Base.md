- [Cookie (tờ giấy ghi chú mà website gửi cho trình duyệt giữ hộ)](#cookie-tờ-giấy-ghi-chú-mà-website-gửi-cho-trình-duyệt-giữ-hộ)
  - [Ask](#ask)
    - [output của cookie là gì?](#output-của-cookie-là-gì)
- [Session (hồ sơ tạm thời của bạn trên server)](#session-hồ-sơ-tạm-thời-của-bạn-trên-server)
- [Session Cookie](#session-cookie)
- [JWT (JSON Web Token là một dạng token thường dùng để xác thực người dùng giữa client và server)](#jwt-json-web-token-là-một-dạng-token-thường-dùng-để-xác-thực-người-dùng-giữa-client-và-server)
  - [Ask](#ask-1)
    - [JWT khác cookie thế nào?](#jwt-khác-cookie-thế-nào)
---
# Cookie (tờ giấy ghi chú mà website gửi cho trình duyệt giữ hộ)
```bash
Website dùng cookie để nhớ bạn là ai, bạn đã làm gì trước đó.
```
**Ex: Ví dụ quán cà phê**
```bash
Bạn vào quán cà phê ☕
    1. Lần đầu: nhân viên hỏi tên → ghi vào phiếu
    2. Lần sau bạn quay lại, đưa phiếu → họ biết bạn là khách quen
```
**Ex: Đăng nhập trên facebook**
```bash
Bạn đăng nhập Facebook
    1. Bạn đóng trình duyệt
    2. Mở lại vẫn đăng nhập 👉 Vì: Facebook đã lưu cookie đăng nhập trong trình duyệt
```
## Ask
### output của cookie là gì?
```bash
Cookie là các cặp name=value mà trình duyệt lưu lại.

Ví dụ:
    - session_id=abc123xyz789
    - auth_token=eyJhbGciOiJIUzI1NiIs...
```
không hiểu gì cả nó kiểu _ga=;OGPC=;OGP, SID; APISID; SAPISID; _ga_WC57KJ50ZZ, __Secure-STRP; SIDCC là gì

À, nhìn danh sách của bạn thì phần lớn đây là cookie của Google, chứ chưa chắc cookie nào cũng là "session đăng nhập" theo nghĩa bạn đang học.

Có thể hiểu từng cái đơn giản như sau:

Cookie	Hiểu đơn giản
_ga	Google Analytics → nhận diện/tracking trình duyệt để thống kê
_ga_WC57KJ50ZZ	Cookie của Google Analytics 4 cho một property cụ thể
OGPC	Cookie liên quan đến các dịch vụ Google
OGP	Cookie của Google, thường liên quan đến trạng thái/tương tác dịch vụ
SID	Cookie xác thực Google
APISID	Cookie liên quan đến xác thực/tương tác Google API/dịch vụ
SAPISID	Cookie xác thực/liên quan đến các dịch vụ Google
__Secure-STRP	Cookie Google có tiền tố __Secure-, được đặt với các yêu cầu bảo mật nhất định
SIDCC	Cookie liên quan đến trạng thái/bảo vệ phiên của Google
Cái quan trọng nhất để bạn hiểu

Trong danh sách của bạn:

_ga
OGPC
OGP
SID
APISID
SAPISID
_ga_WC57KJ50ZZ
__Secure-STRP
SIDCC

Không nên hiểu rằng mỗi cookie = một session.

Ví dụ:

Browser
│
├── _ga              → Analytics
├── _ga_xxxxx        → Analytics
├── SID              → authentication/session-related
├── SAPISID          → authentication-related
├── APISID           → authentication-related
└── SIDCC            → session/security-related

Một website có thể có hàng chục cookie phục vụ những mục đích hoàn toàn khác nhau.

Đặc biệt: SID

Đây là cái đáng chú ý khi bạn đang học authentication.

Mô hình khái niệm có thể hình dung:

Bạn login Google
       │
       ▼
Google xác thực
       │
       ▼
Browser nhận authentication cookies
       │
       ├── SID
       ├── SAPISID
       ├── APISID
       └── ...
       │
       ▼
Các request tiếp theo
       │
       ▼
Google biết request này thuộc phiên
đã xác thực

Nhưng đừng copy/paste giá trị thực của SID, SAPISID, APISID lên chat hoặc gửi cho người khác. Các cookie xác thực có thể có giá trị tương đương thông tin đăng nhập phiên.

Và đây là chỗ dễ nhầm với Session

Bạn đang học:

Session
Cookie
Session Cookie
JWT

thì cần phân biệt:

Cookie
  │
  ├── Analytics cookie
  ├── Preference cookie
  ├── Authentication cookie
  └── Session cookie

Cookie chỉ là cơ chế browser lưu và gửi dữ liệu.

Còn Session là khái niệm về trạng thái xác thực/phiên của user.

Ví dụ backend Python của bạn có thể tạo:

session_id = "abc123"

rồi gửi:

Set-Cookie: session_id=abc123; HttpOnly; Secure

Khi đó:

Cookie trên Browser
        │
        │ session_id=abc123
        ▼
Backend
        │
        │ tìm abc123
        ▼
Session
{
    "user_id": 123,
    "logged_in": true
}

Đây mới là ví dụ session-based authentication kinh điển.

Còn Google sử dụng một hệ thống authentication phức tạp hơn nhiều, nên đừng lấy danh sách cookie của Google làm ví dụ đơn giản để học Session.

Nếu mục tiêu của bạn là hiểu tận gốc Cookie → Session → JWT, mình có thể 
giải thích bằng một ví dụ React + FastAPI login hoàn chỉnh, từ lúc bấm Login → Set-Cookie → browser lưu → request /me → backend xác định user, nhìn sẽ rất dễ hiểu.

tôi có một website đang đang nhập mà tôi muốn xem cookie của nó hình dạng như nào thì bấm f5 vào console rồi viết code gì để xem được

Nếu là website bạn đang đăng nhập và bạn muốn xem các cookie mà JavaScript được phép đọc, mở DevTools → Console rồi chạy:

document.cookie

Ví dụ có thể ra:

"theme=dark; language=vi; session_id=abc123"

Muốn dễ đọc hơn:

document.cookie.split('; ').forEach(c => console.log(c))

Hoặc chuyển thành object:

Object.fromEntries(
  document.cookie.split('; ').map(c => c.trim().split('='))
)
Nhưng có một điểm rất quan trọng

Nếu bạn thấy:

"theme=dark; language=vi"

thì không có nghĩa website không có cookie đăng nhập.

Cookie đăng nhập thường được cấu hình:

HttpOnly

Cookie HttpOnly không thể đọc bằng document.cookie. Đây là chủ ý bảo mật để JavaScript (ví dụ XSS) không dễ lấy session cookie.

Để xem tất cả cookie của website, kể cả HttpOnly:

F12 → Application → Storage → Cookies → chọn domain

Bạn sẽ thấy các cột kiểu:

Name          Value          Domain       Path    HttpOnly    Secure    SameSite
session_id    abc123...      example.com  /       ✓           ✓         Lax
theme         dark           example.com  /                   ✓         Lax

Đây cũng là cách tốt nhất để học Cookie + Session vì bạn sẽ nhìn được trực tiếp Name, Value, HttpOnly, Secure, SameSite, Expires...
# Session (hồ sơ tạm thời của bạn trên server)
```bash
Session khác với Cookie ở chỗ:
    - Cookie: nằm ở trình duyệt
    - Session: nằm ở server
```
**Ex**
```bash
Bạn vào quán

Nhân viên tạo 1 hồ sơ cho bạn: 
    Khách A
        - Gọi cà phê sữa
        - Đang ngồi bàn số 3
    => Hồ sơ đó = session

Nhân viên đưa bạn 1 thẻ số: Thẻ số = session_id (được lưu trong cookie)
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
# Session Cookie
# JWT (JSON Web Token là một dạng token thường dùng để xác thực người dùng giữa client và server)
**Ex**
```bash
Bạn đăng nhập: Username + Password -> Backend -> Tạo JWT -> Client nhận token
```
**Structure**
```bash
HEADER.PAYLOAD.SIGNATURE

- Header: Nó mô tả đại khái token dùng thuật toán ký nào.
- Payload: chứa thông tin gọi là claims
- Signature: Server dùng secret/private key để tạo chữ ký
```
**Ex: Login**
```bash
Bước 1: Login
    Frontend gửi: POST /login # {"username": "thang", "password": "123456"}
Bước 2: Backend xác thực
    Username/password đúng -> Backend tạo JWT -> {"access_token": "eyJhbGciOi..."}
Bước 3: Client gọi API khác
    Client gửi JWT cùng request, thường trong header:
        - GET /api/profile
        - Authorization: Bearer eyJhbGciOi...
        - Bearer có thể hiểu đơn giản là: Ai đang cầm token hợp lệ thì được dùng nó.
Bước 4: Backend kiểm tra JWT
    Request
       │
       ▼
    Có JWT không?
       │
       ├── Không → 401 Unauthorized
       │
       ▼
    Kiểm tra signature
       │
       ├── Sai → 401
       │
       ▼
    Kiểm tra hết hạn
       │
       ├── Hết hạn → 401
       │
       ▼
    Token hợp lệ
       │
       ▼
    Cho phép xử lý request
```
## Ask
### JWT khác cookie thế nào?
```bash
JWT và Cookie không phải hai thứ cùng loại để so sánh trực tiếp.
    Giống như:
        - Cookie = cái ví/túi chứa
        - JWT = một loại thẻ có thể đặt vào đó
```