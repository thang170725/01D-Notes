+ [<<Back](../Base.md)
- [Paseto](#paseto)
- [Domain](#domain)
- [Chuẩn giao tiếp](#chuẩn-giao-tiếp)
  - [ASGI (Asynchronous Server Gateway Interface là chuẩn giao tiếp giữa Web server Và ứng dụng Python)](#asgi-asynchronous-server-gateway-interface-là-chuẩn-giao-tiếp-giữa-web-server-và-ứng-dụng-python)
- [Framework](#framework)
  - [Starlette](#starlette)
- [Nginx (là một Web Server và Reverse Proxy)](#nginx-là-một-web-server-và-reverse-proxy)
- [SSE (cơ chế để server chủ động gửi dữ liệu liên tục về client qua một HTTP connection đang mở)](#sse-cơ-chế-để-server-chủ-động-gửi-dữ-liệu-liên-tục-về-client-qua-một-http-connection-đang-mở)
- [WebSocket (Các để Frontend và backend giữ kết nối liên tục, từ đó hai bên có thể gửi dữ liệu cho nhau ngày lập tức)](#websocket-các-để-frontend-và-backend-giữ-kết-nối-liên-tục-từ-đó-hai-bên-có-thể-gửi-dữ-liệu-cho-nhau-ngày-lập-tức)
---
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
## ASGI (Asynchronous Server Gateway Interface là chuẩn giao tiếp giữa Web server Và ứng dụng Python)
```bash
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
# SSE (cơ chế để server chủ động gửi dữ liệu liên tục về client qua một HTTP connection đang mở)
**SSE khác API bình thường thế nào?**  
*API bình thường*
```bash
FE ───── request ─────> BE
FE <──── toàn bộ JSON ── BE
```
*Ex*
```bash
{
  "answer": "Xin chào, tôi có thể giúp gì?"
}
```
*SSE*
```bash
FE ───── request ─────> BE
       connection giữ mở
FE <──── "Xin"
FE <──── " chào"
FE <──── " bạn"
FE <──── [DONE]
```
# WebSocket (Các để Frontend và backend giữ kết nối liên tục, từ đó hai bên có thể gửi dữ liệu cho nhau ngày lập tức)
Hiểu đơn giản:

HTTP bình thường
Frontend ────── Request ──────> Backend
Frontend <───── Response ────── Backend

        kết thúc kết nối

Muốn biết Backend có dữ liệu mới không, Frontend phải hỏi lại:

FE → "Có gì mới không?"
BE → "Chưa"

FE → "Có gì mới không?"
BE → "Chưa"

FE → "Có gì mới không?"
BE → "Có rồi!"

Đây gọi là polling.

WebSocket

WebSocket mở một kết nối và giữ kết nối đó:

Frontend ═════════════════ Backend
          kết nối liên tục

FE  ───────────────→  BE
FE  ←───────────────  BE
FE  ←───────────────  BE
FE  ───────────────→  BE

Backend có dữ liệu mới thì chủ động đẩy xuống Frontend ngay.

Không cần Frontend hỏi liên tục.

Ví dụ dễ hiểu

Bạn có game Tetris.

Khi người chơi đang chơi:

Python Backend
     │
     │ WebSocket
     ↓
React Frontend

Backend có thể gửi:

{
  "score": 1200,
  "level": 3,
  "next_piece": "T",
  "status": "running"
}

Frontend nhận được ngay và cập nhật UI.

WebSocket thường dùng để làm gì?

Rất phù hợp với những hệ thống cần real-time:

1. Chat
A gửi:
"Hello"

        ↓ WebSocket

B nhận ngay:
"Hello"

Không cần B refresh trang.

2. Notification

Ví dụ:

Backend
   ↓
"Có email mới"
   ↓ WebSocket
Frontend
   ↓
🔔 Email mới
3. Theo dõi tiến trình

Đặc biệt liên quan đến AI Agent/LangGraph của bạn.

Ví dụ workflow:

START
 ↓
REWRITE
 ↓
RETRIEVE
 ↓
AGENT
 ↓
EXECUTE
 ↓
RESULT EVALUATOR
 ↓
FINAL

Frontend có thể nhận từng trạng thái:

WebSocket

Backend ──→ "rewrite: running"
Backend ──→ "rewrite: completed"
Backend ──→ "retrieve: running"
Backend ──→ "retrieve: completed"
Backend ──→ "agent: running"
Backend ──→ "agent: completed"
Backend ──→ "done"

React sau đó hiển thị:

✓ Phân tích câu hỏi
✓ Tìm công cụ phù hợp
✓ AI suy luận
✓ Thực thi công cụ
✓ Kiểm tra kết quả
✓ Hoàn thành

Đây chính là kiểu UI WorkflowProgress mà bạn đang làm.

WebSocket khác SSE thế nào?

Bạn trước đó cũng hỏi về SSE, nên đây là điểm rất đáng phân biệt:

	WebSocket	SSE
Kết nối liên tục	✅	✅
Backend → Frontend	✅	✅
Frontend → Backend	✅	❌*
2 chiều	✅	❌
Chat realtime	⭐⭐⭐⭐⭐	⭐⭐⭐⭐
AI streaming	⭐⭐⭐⭐⭐	⭐⭐⭐⭐⭐
Workflow progress	⭐⭐⭐⭐⭐	⭐⭐⭐⭐⭐
Đơn giản	⭐⭐⭐	⭐⭐⭐⭐⭐

* Với SSE, Frontend vẫn gửi request HTTP bình thường; chỉ riêng kênh SSE là server → client.

Hình dung:

SSE:

Frontend ─────── Request ──────→ Backend

Frontend ←══════════════════════ Backend
              STREAM

WebSocket:

Frontend ═══════════════════════ Backend
            2 chiều
Với hệ thống AI Agent của bạn

Nếu mục đích chỉ là:

Backend
  ↓
gửi tiến trình Agent
  ↓
React WorkflowProgress

thì SSE thường đơn giản và phù hợp hơn WebSocket.

Ví dụ:

LangGraph
   ↓
rewrite completed
   ↓
SSE
   ↓
React
   ↓
✓ Phân tích câu hỏi

Còn nếu sau này bạn muốn Frontend gửi lệnh realtime ngược lại trong cùng connection, ví dụ:

React
 ↓
"Pause Agent"

      ↕ WebSocket

Backend
 ↓
Agent paused

thì WebSocket có lợi thế hơn.

Tóm lại: WebSocket = một đường kết nối realtime 2 chiều giữa client và server. Nó rất hữu ích cho chat, game, notification, live dashboard và các hệ thống cần cập nhật trạng thái ngay lập tức.

có websocket rồi thì còn cần sse làm gì 2 cái này đều dùng để giữ kết nối be và fe mà

Đúng là WebSocket và SSE đều giúp giữ một kết nối lâu dài giữa FE ↔ BE, nhưng điểm khác biệt quan trọng là hướng truyền dữ liệu.

1. Khác nhau cốt lõi
SSE
FE ──────────────── HTTP connection ────────────────> BE
                       ↑
                       │ data
                       │
                       └──────────────────────────── BE → FE

SSE chủ yếu là:

BE → FE liên tục

FE gửi request ban đầu, sau đó BE có thể liên tục push event xuống FE.

Ví dụ workflow AI của bạn:

FE ── POST /chat ──> BE

BE:
  rewrite ────────> FE  "Đang phân tích..."
  retrieve ───────> FE  "Đang tìm tool..."
  agent ──────────> FE  "AI đang suy luận..."
  execute ────────> FE  "Đang thực thi..."
  final ──────────> FE  "Hoàn thành"

SSE rất hợp với trường hợp này.

2. WebSocket thì khác

WebSocket tạo một connection 2 chiều:

             WebSocket
FE <────────────────────────> BE
       ↑                  ↑
       │                  │
       └── gửi/nhận ──────┘

Cả FE và BE đều có thể chủ động gửi message bất cứ lúc nào.

Ví dụ ứng dụng chat realtime:

FE ── "Hello" ─────────────> BE
FE <── "Typing..." ───────── BE

BE ── "New message" ───────> FE
FE ── "Seen" ──────────────> BE
3. Vậy tại sao có WebSocket rồi còn cần SSE?

Vì không phải lúc nào bạn cần giao tiếp 2 chiều.

Ví dụ chính workflow LangGraph của bạn:

                    LangGraph
                        │
                        │ progress events
                        ↓
FE <────────────────── BE

FE chủ yếu muốn:

"BE ơi, có tiến trình gì mới thì báo cho tôi."

FE không cần liên tục gửi message ngược lại trên connection đó.

SSE lúc này đơn giản hơn WebSocket.

4. So sánh nhanh
	SSE	WebSocket
Connection	Giữ lâu	Giữ lâu
BE → FE	✅	✅
FE → BE	⚠️ Không phải mục đích chính	✅
Giao thức	HTTP	WebSocket
FE API	EventSource	WebSocket
Reconnect	Có cơ chế built-in	Tự xử lý thường nhiều hơn
Streaming AI	⭐⭐⭐⭐⭐	⭐⭐⭐⭐⭐
Chat realtime	⭐⭐	⭐⭐⭐⭐⭐
Game realtime	❌	⭐⭐⭐⭐⭐
Notification	⭐⭐⭐⭐⭐	⭐⭐⭐⭐
Workflow progress	⭐⭐⭐⭐⭐	⭐⭐⭐⭐
5. Một điểm rất quan trọng

SSE không có nghĩa là FE bị "khóa", không thể gửi request nữa.

Ví dụ:

FE                         BE

POST /chat ───────────────> bắt đầu AI

GET /chat/stream ─────────> mở SSE

<────────────────────────── rewrite
<────────────────────────── retrieve
<────────────────────────── agent
<────────────────────────── execute
<────────────────────────── final

POST /feedback ───────────> gửi feedback

FE vẫn có thể gửi các HTTP request bình thường.

Chỉ là connection SSE cụ thể đó chủ yếu dùng cho BE → FE.

6. Với project LangGraph của bạn

Kiến trúc của bạn khá hợp với SSE:

                    ┌───────────────┐
                    │   LangGraph  │
                    └───────┬───────┘
                            │
             events/progress│
                            ↓
┌──────────┐         ┌──────────────┐
│ React FE │ <───────│ Python BE    │
└──────────┘   SSE   └──────────────┘
      │                     │
      │ POST /chat          │
      ├────────────────────>│
      │                     │
      │<──── SSE ───────────│ rewrite
      │<──── SSE ───────────│ retrieve
      │<──── SSE ───────────│ agent
      │<──── SSE ───────────│ execute
      │<──── SSE ───────────│ evaluator
      │<──── SSE ───────────│ final

Đặc biệt component WorkflowProgress của bạn:

rewrite
   ↓
retrieve
   ↓
agent
   ↓
execute
   ↓
result_evaluator
   ↓
final

SSE rất phù hợp để stream từng node progress về React.

7. Có thể hiểu cực ngắn như này
SSE:
"BE có gì mới thì báo cho FE."

WebSocket:
"FE và BE cứ nói chuyện 2 chiều realtime với nhau."

Vì vậy WebSocket không làm SSE trở nên vô dụng. Nếu hệ thống chỉ cần server streaming → client, SSE thường đơn giản và đúng mục đích hơn.

Còn nếu bạn muốn kiểu:

FE ↔ BE
FE ↔ BE
FE ↔ BE

liên tục và realtime hai chiều → WebSocket phù hợp hơn.