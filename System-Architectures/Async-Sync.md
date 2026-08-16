- [Sync (synchronous) (làm tuần tự, việc A xong mới làm B)](#sync-synchronous-làm-tuần-tự-việc-a-xong-mới-làm-b)
- [Async (asynchronous) (có thể bắt đầu việc khác trong lúc chờ A)](#async-asynchronous-có-thể-bắt-đầu-việc-khác-trong-lúc-chờ-a)
---
# Sync (synchronous) (làm tuần tự, việc A xong mới làm B)
# Async (asynchronous) (có thể bắt đầu việc khác trong lúc chờ A)
1. Sync là gì?

Ví dụ bạn gọi API:

data = requests.get(url)   # chờ server trả về
print(data)
print("Done")

Luồng chạy:

Gọi API
   ↓
CHỜ API trả về
   ↓
Nhận data
   ↓
print
   ↓
Done

Nếu API mất 5 giây thì chương trình đứng chờ 5 giây ở đó.

Đây là sync.

2. Async là gì?

Với async, trong lúc đang chờ một tác vụ I/O, chương trình có thể xử lý việc khác.

Ví dụ:

async def get_data():
    data = await fetch_data()
    print(data)

Điểm quan trọng là:

await fetch_data()

await có ý nghĩa gần như:

"Việc này đang chờ kết quả. Trong lúc chờ, nếu có việc khác thì cứ làm đi."

Ví dụ có 3 API:

API A ──────── 5s
API B ── 2s
API C ─── 3s

Sync:

A █████ 5s
          B ██ 2s
                C ███ 3s


Tổng ≈ 10s

Async:

A █████
B ██
C ███


Tổng ≈ 5s

Vì A, B, C có thể chờ đồng thời.

3. Khi nào dùng Sync?

Dùng sync khi công việc của bạn chủ yếu đơn giản hoặc không cần chạy đồng thời.

Ví dụ:

Đọc một file
Xử lý một JSON
Tính toán
Chạy pipeline tuần tự
Code script nhỏ
Các bước phụ thuộc nhau

Ví dụ project json_service của bạn:

load JSON
   ↓
build mapping
   ↓
create table
   ↓
save result

Nếu mỗi bước cần kết quả của bước trước thì sync hoàn toàn hợp lý.

data = load_json()
mapping = build_mapping(data)
table = create_table(mapping)
save(table)

Không cần async chỉ vì "async hiện đại hơn".

4. Khi nào dùng Async?

Async đặc biệt hữu ích khi chương trình phải chờ I/O nhiều.

Ví dụ:

Gọi API
Gọi API
Gọi API
Đọc network
Đợi database
Đợi database

Các tác vụ này thường có thời gian:

CPU:      █
Network:     █████████████
Database:       ███████

CPU không thực sự bận trong thời gian chờ network/database.

Async tận dụng khoảng thời gian chờ đó.

Ví dụ:

async def main():
    result1 = await call_api_1()
    result2 = await call_api_2()

Nếu muốn chạy hai API đồng thời:

result1, result2 = await asyncio.gather(
    call_api_1(),
    call_api_2()
)
5. Một hiểu lầm rất quan trọng

Async không có nghĩa là chạy nhiều CPU task cùng lúc.

Ví dụ:

async def calculate():
    for i in range(10_000_000):
        ...

Đây là CPU-bound.

Async không giúp nhiều trong trường hợp này.

Phân biệt:

Công việc	Nên dùng
Đọc file nhỏ	Sync
Xử lý JSON	Sync
Tính toán nặng	multiprocessing / tối ưu CPU
Gọi 100 API	Async
Query nhiều database	Async
Web server nhiều request	Async thường phù hợp
Download nhiều file	Async
Pipeline đơn giản	Sync
Pipeline có nhiều API/network	Có thể Async
6. Hãy nhớ bằng một ví dụ đời thường

Sync:

Bạn đi pha cà phê:

Cho nước vào máy
↓
Đứng chờ
↓
Cà phê xong
↓
Uống

Bạn không làm gì khác trong lúc chờ.

Async:

Bật máy pha cà phê
↓
Trong lúc máy pha
→ rửa cốc
→ lấy bánh
→ kiểm tra điện thoại
↓
Cà phê xong
↓
Uống

await giống như:

"Tôi đang chờ việc này, nhưng bạn cứ cho tôi làm việc khác trong lúc chờ."

7. Nếu bạn đang học Python thì nên hiểu 3 thứ này
async def
await
asyncio.gather()

Ví dụ quan trọng nhất:

import asyncio


async def task(name, seconds):
    print(f"{name} started")
    await asyncio.sleep(seconds)
    print(f"{name} finished")


async def main():
    await asyncio.gather(
        task("A", 3),
        task("B", 2),
        task("C", 1),
    )


asyncio.run(main())

Ba task có thể chạy đồng thời theo kiểu async, nên tổng thời gian khoảng 3 giây, thay vì 6 giây nếu chạy tuần tự.

Tóm lại:

Sync = làm → chờ xong → làm tiếp.
Async = làm → gặp lúc phải chờ → tranh thủ làm việc khác → quay lại.

Nếu bạn đang học Python để làm backend/pipeline, 
mình có thể giải thích tiếp async/await thực sự hoạt động bên trong event loop như thế nào — đây là phần quan trọng để không chỉ biết dùng mà còn hiểu bản chất.

vậy thì các luồng post thì có phải thường là sync không ví dụ đăng nhập, đăng ký. 2 - làm sao để nhận dạn được lúc nào dùng cái nào, về lý thuyết thì tôi hiểu rồi nhưng áp dùng vào thực tế để khi nào biết lên dùng cái nào thì khó
Đúng, nhưng có một điểm cần sửa trong cách nghĩ:

Không nên quyết định Sync/Async dựa vào "POST hay GET".
Quyết định dựa vào bên trong request đó có phải chờ I/O hay không và có cần xử lý nhiều request đồng thời hay không.

Ví dụ đăng nhập / đăng ký vẫn hoàn toàn có thể dùng async.

1. Login không phải cứ POST là Sync

Ví dụ:

POST /login
      ↓
Nhận username/password
      ↓
Query database  ← CHỜ I/O
      ↓
Kiểm tra password
      ↓
Tạo JWT
      ↓
Trả response

Nếu database/network là async thì endpoint có thể là:

async def login(...):
    user = await db.get_user(...)
    ...

Nó vẫn là POST, nhưng code xử lý là async.

Ngược lại, một POST đơn giản:

POST /calculate
       ↓
Nhận dữ liệu
       ↓
Tính toán
       ↓
Trả kết quả

thì có thể chẳng cần async.

Cách nhận biết trong thực tế

Đây mới là cách mình khuyên bạn dùng:

Hãy hỏi 3 câu
Câu 1: "Trong lúc xử lý, tôi có phải CHỜ thứ gì không?"

Nếu không:

request
  ↓
tính toán
  ↓
response

→ Sync thường đủ.

Nếu có:

request
  ↓
đợi DB
  ↓
đợi API
  ↓
đợi file
  ↓
response

→ Async có thể hữu ích.

Câu 2: "Tôi phải chờ cái gì?"

Đây là câu quan trọng nhất.

Nếu chờ:

Database
HTTP API
Redis
File/network
Message queue
Upload/download
WebSocket

→ I/O-bound → nghĩ đến Async.

Ví dụ login:

POST /login


password
   ↓
query DB
   ↓
await ← chờ DB
   ↓
check password
   ↓
return

Async rất hợp lý.

Câu 3: "Tôi có nhiều việc phải chờ cùng lúc không?"

Ví dụ một request:

GET /profile


        ┌── DB user
        │
request ├── API payment
        │
        └── API notification

Nếu 3 việc độc lập:

user, payment, notification = await asyncio.gather(
    get_user(),
    get_payment(),
    get_notification()
)

Async càng có giá trị.

Nhưng có một điều rất quan trọng

Đừng nghĩ:

"Có database → phải async."

Không phải.

Ví dụ bạn dùng FastAPI + SQLAlchemy:

def login():
    user = db.query(...)

vẫn hoàn toàn hợp lệ.

Async chỉ thực sự đáng cân nhắc khi concurrency quan trọng.

Một quy tắc thực chiến tôi khuyên bạn nhớ

Khi viết một function, hãy nhìn vào nó:

def xxx():
    ...

và hỏi:

"Function này có thời gian bị đứng chờ bên ngoài CPU không?"

Nếu:

CPU → CPU → CPU → CPU

→ Sync

Nếu:

CPU → WAIT → CPU → WAIT → CPU
          ↑
       DB/API/File

→ Async có thể phù hợp.

Ví dụ rất thực tế

Giả sử bạn làm API:

A. Tính tổng
def calculate(a, b):
    return a + b

→ Sync.

Không có gì để chờ.

B. Login
async def login(username, password):
    user = await db.find_user(username)
    ...

→ Async có thể phù hợp.

Vì phải chờ DB.

C. Lấy thông tin user
async def get_profile(user_id):
    user = await db.get_user(user_id)
    return user

→ Async có thể phù hợp.

D. Resize ảnh bằng CPU
def resize_image(image):
    # xử lý ảnh rất nặng
    ...

→ Không phải cứ API thì async.

Đây là CPU-bound.

Async không giải quyết tốt vấn đề này.

Có thể cần:

multiprocessing
worker
Celery
task queue
GPU

tùy trường hợp.

Một cách tư duy rất hữu ích

Khi thiết kế API, đừng nhìn HTTP method trước.

Đừng nghĩ:

GET → async?
POST → sync?
PUT → sync?
DELETE → sync?

Hãy nghĩ:

Request
   ↓
Business logic
   ↓
Có I/O không?
   ↓
Có phải chờ không?
   ↓
Có nhiều request đồng thời không?

Ví dụ:

POST /register
       ↓
validate data
       ↓
DB: kiểm tra email     ← I/O
       ↓
DB: insert user        ← I/O
       ↓
Email service          ← I/O
       ↓
response

→ Async khá tự nhiên.

Trong khi:

POST /calculate-tax
       ↓
validate
       ↓
tính toán
       ↓
response

→ Sync có thể đơn giản hơn.

Và đây là điểm tôi nghĩ bạn đang thiếu

Bạn nói:

"Lý thuyết thì tôi hiểu nhưng áp dụng thực tế khó."

Điều này rất bình thường.

Bạn không cần cố nhớ một đống rule.

Hãy tập một thói quen:

Viết code sync trước, sau đó tìm những chỗ phải WAIT.

Ví dụ ban đầu:

def create_order():
    user = get_user()
    product = get_product()
    save_order()
    send_email()

Sau đó nhìn:

get_user()      → DB
get_product()   → DB
save_order()    → DB
send_email()    → API

Bạn sẽ nhận ra:

        WAIT
         ↓
get_user()
         ↓
        WAIT
         ↓
get_product()
         ↓
        WAIT
         ↓
save_order()
         ↓
        WAIT
         ↓
send_email()

Lúc này mới bắt đầu nghĩ:

"Có đáng chuyển sang async không?"

Đây là cách từ code thực tế suy ra async, chứ không phải học thuộc "trường hợp nào dùng async".

Một mental model cực ngắn

Bạn có thể nhớ:

SYNC
│
├── CPU work
├── logic đơn giản
├── tuần tự
└── không cần concurrency đặc biệt


ASYNC
│
├── phải WAIT
│   ├── DB
│   ├── API
│   ├── network
│   ├── file I/O
│   └── queue
│
└── nhiều request/task cùng chờ

Và POST/GET không quyết định sync/async.

Nếu bạn đang học backend Python, bước tiếp theo rất đáng học là "I/O-bound vs CPU-bound". Khi hiểu thật rõ hai khái niệm này, việc quyết định sync / async / threading / multiprocessing sẽ dễ hơn rất nhiều.

Tiếp tục đào sâu:

Phân biệt I/O-bound và CPU-bound bằng ví dụ backend
Phân tích một endpoint đăng ký thực tế