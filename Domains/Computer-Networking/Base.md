- [Cookie (tờ giấy ghi chú mà website gửi cho trình duyệt giữ hộ)](#cookie-tờ-giấy-ghi-chú-mà-website-gửi-cho-trình-duyệt-giữ-hộ)
- [Session (hồ sơ tạm thời của bạn trên server)](#session-hồ-sơ-tạm-thời-của-bạn-trên-server)
- [JWT](#jwt)
- [Paseto](#paseto)
- [Domain](#domain)
- [Chuẩn giao tiếp](#chuẩn-giao-tiếp)
  - [ASGI](#asgi)
- [Framework](#framework)
  - [Starlette](#starlette)
- [Nginx (là một Web Server và Reverse Proxy)](#nginx-là-một-web-server-và-reverse-proxy)
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
cookies thì output là gì dãy kí tự à. 2 - nếu lộ cookie giả sử facebook thì người ta dùng cookie có vào được mà không cần mật khẩu hay tài khoản không 

Đúng, nhưng cần phân biệt cookie nói chung và cookie đăng nhập/session cookie.

1. Cookie output có phải một dãy ký tự không?

Thường là có. Cookie là các cặp name=value mà trình duyệt lưu lại.

Ví dụ minh họa:

session_id=abc123xyz789

Hoặc một cookie có thể trông như:

auth_token=eyJhbGciOiJIUzI1NiIs...

Nhưng không phải cookie nào cũng là thông tin đăng nhập. Có cookie chỉ lưu:

language=vi
theme=dark

Cookie cũng có thể chứa ID/token ngẫu nhiên thay vì trực tiếp chứa username/password.

2. Nếu lộ cookie đăng nhập Facebook thì có thể vào mà không cần password không?

Có thể, nếu đó là cookie/session token còn hiệu lực và hệ thống chấp nhận nó.

Cơ chế đại khái là:

Lần đầu đăng nhập:

Email + Password
       ↓
Facebook xác thực
       ↓
Tạo session
       ↓
Browser lưu session cookie

Những request sau có thể giống:

Browser
   │
   │ Cookie: session=XYZ...
   ▼
Facebook
   │
   └── "Session này đã được xác thực"

Do đó server không nhất thiết phải yêu cầu gửi lại password ở mỗi request.

Vì vậy nếu một session cookie nhạy cảm bị đánh cắp:

Password ❌ không biết
Email     ❌ không biết

Session cookie ✅

thì trong một số tình huống, kẻ khác có thể sử dụng session đó để truy cập tài khoản như phiên đăng nhập của nạn nhân.

Đây là lý do người ta gọi việc đánh cắp session cookie là một dạng session hijacking.

Nhưng có một điểm rất quan trọng

Không phải cứ lấy được bất kỳ cookie nào là đăng nhập được.

Ví dụ:

theme=dark
language=vi
tracking_id=abc

→ gần như không có giá trị để đăng nhập.

Cái nguy hiểm là các cookie/token liên quan đến:

authentication
session
login

Ngoài ra, các hệ thống lớn có thể có thêm cơ chế bảo vệ như:

cookie hết hạn
session bị revoke
phát hiện thiết bị/vị trí bất thường
yêu cầu xác minh lại
2FA/step-up authentication
ràng buộc hoặc kiểm tra session ở phía server

Nên lộ cookie không đồng nghĩa chắc chắn tài khoản bị chiếm, nhưng nếu lộ một authentication/session cookie còn hiệu lực thì đó là sự cố bảo mật nghiêm trọng.

Một cách hình dung rất dễ nhớ
Password
   ↓
"Chứng minh bạn là ai"
   ↓
Server cấp
   ↓
Session Cookie
   ↓
"Vé vào cửa" cho các request tiếp theo

Nếu bạn đang học cybersecurity, đây là một khái niệm rất quan trọng: password authentication → session → cookie → authenticated request.
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
# JWT 
JWT (JSON Web Token) là một dạng token thường dùng để xác thực người dùng giữa client và server.

Liên hệ với câu bạn vừa hỏi về cookie:

Cookie là nơi/cách trình duyệt gửi dữ liệu, còn JWT là một loại dữ liệu/token có thể được lưu và truyền đi.

1. Luồng dễ hiểu nhất

Bạn đăng nhập:

Username + Password
        │
        ▼
     Backend
        │
        │ kiểm tra đúng
        ▼
     Tạo JWT
        │
        ▼
Client nhận token

Ví dụ JWT trông như một chuỗi dài:

eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9
.
eyJ1c2VyX2lkIjoxMjMsInJvbGUiOiJ1c2VyIn0
.
abcXYZ_signature_here

Thường viết liền:

xxxxx.yyyyy.zzzzz

JWT có 3 phần, ngăn cách bởi dấu chấm:

HEADER.PAYLOAD.SIGNATURE
2. Ba phần đó là gì?
Header

Ví dụ:

{
  "alg": "HS256",
  "typ": "JWT"
}

Nó mô tả đại khái token dùng thuật toán ký nào.

Payload

Có thể chứa thông tin như:

{
  "user_id": 123,
  "username": "thang",
  "role": "user"
}

Đây gọi là claims.

⚠️ Quan trọng: JWT thông thường không mã hóa payload. Nó chỉ được encode, nên không nên đặt password hoặc dữ liệu bí mật vào đó.

Signature

Server dùng secret/private key để tạo chữ ký:

HEADER + PAYLOAD
       │
       ▼
Ký bằng secret/private key
       │
       ▼
SIGNATURE

Nhờ đó nếu ai sửa payload, server có thể phát hiện token không còn hợp lệ.

3. JWT dùng như thế nào?

Giả sử bạn login vào backend.

Bước 1: Login

Frontend gửi:

POST /login

{
  "username": "thang",
  "password": "123456"
}
Bước 2: Backend xác thực
Username/password đúng
          │
          ▼
Backend tạo JWT

Ví dụ payload:

{
    "sub": "123",
    "role": "user",
    "exp": 9999999999
}

Backend trả:

{
    "access_token": "eyJhbGciOi..."
}
Bước 3: Client gọi API khác

Client gửi JWT cùng request, thường trong header:

GET /api/profile

Authorization: Bearer eyJhbGciOi...

Bearer có thể hiểu đơn giản là:

Ai đang cầm token hợp lệ thì được dùng nó.

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
4. JWT khác cookie thế nào?

Đây là chỗ rất nhiều người nhầm.

Cookie

Cookie là cơ chế trình duyệt lưu/gửi dữ liệu:

Browser
  │
  ├── lưu cookie
  │
  └── tự động gửi cookie tới website phù hợp

Ví dụ:

Cookie: session_id=abc123
JWT

JWT là format của token:

xxxxx.yyyyy.zzzzz

Nó có thể được gửi qua:

Cách 1: Authorization Header
Authorization: Bearer <JWT>
Cách 2: Cookie
Cookie: access_token=<JWT>

Nên hoàn toàn có thể:

Cookie chứa JWT

Hoặc:

Authorization Header chứa JWT

Đây là điểm cần nhớ:

JWT và Cookie không phải hai thứ cùng loại để so sánh trực tiếp.

Giống như:

Cookie = cái ví/túi chứa
JWT = một loại thẻ có thể đặt vào đó
5. JWT và Session Cookie khác nhau thế nào?

Đây là so sánh sát nhất.

Session truyền thống
Client                    Server

session_id=ABC
──────────────►

                         Server tra DB/Redis:
                         ABC → user_id=123

Cookie chỉ chứa:

session_id=ABC

Thông tin session nằm phía server.

JWT
Client
JWT:
{
  user_id: 123,
  role: user,
  exp: ...
}
     │
     ▼
Server kiểm tra signature

JWT có thể tự chứa claims cần thiết để server xác minh, nên thường được gọi là stateless token theo nghĩa server không nhất thiết phải tra session store cho mỗi request.

So sánh nhanh
	Session ID	JWT
Client giữ gì?	ID ngẫu nhiên	Token có cấu trúc
Server cần lưu session?	Thường có	Không nhất thiết
Server kiểm tra	Tra session store	Verify chữ ký + claims
Có thể hết hạn	Có	Có (exp)
Có thể bị đánh cắp	Có	Có
Có thể lưu trong Cookie	Có	Có
6. Ví dụ nguy hiểm: sửa JWT có được không?

Giả sử payload là:

{
  "user_id": 123,
  "role": "user"
}

Ai đó nhìn thấy rồi sửa thành:

{
  "user_id": 123,
  "role": "admin"
}

Không đơn giản là họ sẽ thành admin.

Vì khi payload thay đổi:

Payload bị sửa
     ↓
Signature cũ không còn khớp
     ↓
Server verify
     ↓
❌ Token không hợp lệ

Đó là vai trò của chữ ký.

7. Liên hệ với backend của bạn

Bạn có thể gặp flow:

Frontend
    │
    │ POST /login
    ▼
FastAPI
    │
    │ verify username/password
    ▼
Generate JWT
    │
    ▼
Frontend
    │
    │ Authorization: Bearer JWT
    ▼
FastAPI
    │
    │ verify JWT
    ▼
Biết user_id / quyền
    │
    ▼
Xử lý API

Ví dụ FastAPI có dependency kiểm tra token:

/api/me
   │
   ▼
verify JWT
   │
   ▼
lấy user_id
   │
   ▼
truy vấn thông tin user
Câu quan trọng nhất

Hãy nhớ:

Password
   ↓
Đăng nhập lần đầu

JWT / Session
   ↓
Chứng minh phiên đăng nhập ở các request sau

Và:

Cookie ≠ JWT

Cookie = cách lưu/gửi dữ liệu
JWT = format token

JWT có thể nằm trong cookie, hoặc được gửi trong Authorization: Bearer ....
# Paseto
PASETO là viết tắt của Platform-Agnostic Security Tokens — một chuẩn token dùng để xác thực và truyền thông tin có tính bảo mật giữa client và server, tương tự mục đích của JWT.

Nếu vừa học JWT thì bạn có thể hiểu:

PASETO là một lựa chọn thay thế JWT, được thiết kế với mục tiêu giảm các lựa chọn nguy hiểm/cấu hình sai trong JWT.

1. Đặt JWT và PASETO cạnh nhau

JWT:

Client
  │
  │ JWT
  ▼
Server

PASETO:

Client
  │
  │ PASETO
  ▼
Server

Cả hai đều có thể được dùng để:

Login
  ↓
Server xác thực
  ↓
Tạo token
  ↓
Client giữ token
  ↓
Client gửi token trong các request
  ↓
Server xác minh token
2. Vấn đề của JWT là gì?

JWT rất phổ biến và không phải là một công nghệ "không an toàn".

Vấn đề là JWT cho phép khá nhiều lựa chọn về thuật toán và cách sử dụng.

Ví dụ JWT có:

alg = HS256
alg = RS256
alg = ES256
...

Nếu developer cấu hình sai thuật toán, key, validation, expiration... thì có thể tạo ra lỗ hổng.

PASETO cố gắng đưa ra một API/format có ít lựa chọn nguy hiểm hơn.

Mental model:

JWT:

"Bạn có rất nhiều option.
Hãy cấu hình đúng."

PASETO:

"Tôi giới hạn các option
để khó cấu hình sai hơn."
3. PASETO có 2 kiểu rất quan trọng

PASETO có hai mục đích chính:

PASETO
├── Local
└── Public
Local

Dùng khi muốn token có tính bí mật + xác thực.

Nói đơn giản:

Server
   │
   │ encrypt
   ▼
PASETO Local Token

Nội dung bên trong được mã hóa.

Public

Dùng khi muốn token có thể được đọc nhưng cần đảm bảo:

Token thực sự được ký bởi server và không bị sửa.

Server
   │
   │ sign
   ▼
PASETO Public Token

Nó tương tự ý tưởng JWT ký bằng public/private key.

4. Ví dụ

Giả sử server muốn nói:

{
    "user_id": 123,
    "role": "admin",
    "exp": 1789000000
}

Server tạo token.

Với JWT:

eyJhbGciOiJIUzI1NiJ9
.
eyJ1c2VyX2lkIjoxMjMsInJvbGUiOiJhZG1pbiJ9
.
signature

Với PASETO, token có format khác, ví dụ dạng:

v4.public.eyJ1c2VyX2lkIjoxMjN9.signature...

hoặc với local:

v4.local.......

Điểm cần nhớ là:

JWT ≠ PASETO

Chúng là hai chuẩn token khác nhau.

5. PASETO khác JWT ở đâu?
	JWT	PASETO
Mục đích	Authentication / authorization / data transport	Tương tự
Format	header.payload.signature	version.purpose.payload...
Có encryption	Có thể dùng JWE	Có Local
Có signing	Có JWS	Có Public
Nhiều algorithm option	Có	Ít hơn
Khả năng cấu hình sai	Tương đối nhiều	Thiết kế giảm bớt
Độ phổ biến	Rất cao	Thấp hơn
Ecosystem	Rất lớn	Nhỏ hơn
6. Một điểm cực kỳ quan trọng

Đừng hiểu:

PASETO = JWT nhưng an toàn hơn tuyệt đối

Không chính xác.

Bảo mật còn phụ thuộc vào:

Token
 +
Key management
 +
Expiration
 +
Storage
 +
Transport HTTPS
 +
Authorization
 +
Server implementation

Ví dụ bạn dùng PASETO nhưng để token vào nơi không an toàn hoặc để token sống quá lâu thì vẫn có vấn đề.

7. Liên hệ với câu hỏi Cookie → JWT lúc nãy

Bạn đang đi đúng một chuỗi kiến thức:

HTTP
 │
 ▼
Cookie
 │
 ▼
Session
 │
 ▼
JWT
 │
 ▼
PASETO

Nhưng thực tế chúng không phải các phiên bản nối tiếp nhau.

Đúng hơn:

                Authentication
                      │
          ┌───────────┴───────────┐
          │                       │
       Session                 Token
          │                       │
          ▼                ┌──────┴──────┐
    Session Cookie          JWT         PASETO
8. Vậy tại sao người ta dùng PASETO?

Một backend có thể quyết định:

Login
  ↓
Tạo PASETO
  ↓
Client
  ↓
Authorization: Bearer <PASETO>
  ↓
API
  ↓
Verify PASETO
  ↓
user_id
  ↓
Authorization

Mục tiêu là có một token mechanism đơn giản hơn về mặt lựa chọn cryptographic primitives và khó cấu hình sai hơn so với một số cách dùng JWT.

9. Nếu bạn đang học Backend, nhớ thế này

Cookie:

Cơ chế lưu/gửi dữ liệu của browser.

Session:

Trạng thái đăng nhập được server quản lý.

JWT:

Một chuẩn token có cấu trúc, thường được ký.

PASETO:

Một chuẩn security token khác, thiết kế với các lựa chọn cryptographic hạn chế hơn để giảm khả năng dùng sai.

Và cả JWT/PASETO đều có thể được đặt bên trong Cookie:

Cookie:
    access_token=<JWT>

hoặc:

Cookie:
    access_token=<PASETO>

Đây là điểm rất quan trọng: Cookie là "container/cơ chế truyền", còn JWT/PASETO là "loại token".
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