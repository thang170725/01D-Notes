Chương 1
Vì sao SQL không đủ?

Ví dụ bạn có bảng

exercise

id

name

description

Có dữ liệu

1
Bench Press
Chest exercise using barbell

2
Push Up
Bodyweight chest workout

3
Squat
Leg exercise

4
Deadlift
Back and leg movement

Người dùng hỏi

"I want exercises to build my chest."

SQL truyền thống

SELECT *
FROM exercise
WHERE description LIKE '%chest%'

Được.

Nhưng người dùng hỏi

"I want bigger pecs."

SQL

LIKE '%chest%'

Không ra.

Hoặc

Upper body pushing workout

SQL

Không biết.

Hoặc

Exercises similar to Bench Press

SQL cũng không biết.

Đây chính là lúc Vector Database xuất hiện.

Ý tưởng

Thay vì lưu

Bench Press

ta biến nó thành

[-0.22,
 0.41,
 0.11,
...
768 numbers]

Người dùng

build chest

cũng biến thành

[-0.20,
0.42,
0.10,
...
768 numbers]

Hai vector rất gần nhau.

Máy tính sẽ biết

=> giống nghĩa
Chương 2
Embedding là gì?

Embedding là

chuyển dữ liệu thành vector số.

Ví dụ

Bench Press

↓

Embedding Model

↓

[
0.12,
0.44,
-0.55,
...
]

Đây gọi là

Embedding Vector

Ví dụ

Bench Press

và

Barbell Chest Press

sẽ tạo ra

Vector A

↓

[0.12,
0.44,
...]
Vector B

↓

[0.13,
0.42,
...]

Rất gần nhau.

Trong khi

Pizza
[-0.8,
0.1,
...]

Rất xa.

Đó là toàn bộ ý tưởng.

Chương 3
Vector là gì?

Giả sử chỉ có 2 chiều

Dog

(1,1)
Cat

(2,2)
Pizza

(100,100)

Nhìn trên mặt phẳng

Cat

●

Dog

●













Pizza

●

Dog gần Cat.

Pizza rất xa.

Embedding thực tế

Không phải

2 chiều.

Mà

384 chiều

768 chiều

1024 chiều

1536 chiều

3072 chiều

Ví dụ

OpenAI

1536 dimensions

Gemini

768 hoặc 3072

BGE

1024
Chương 4

Similarity Search

Thay vì

WHERE name='Bench Press'

ta hỏi

Vector nào gần nhất?

Có 3 cách đo.

Euclidean Distance
A ●

     ● B

Khoảng cách.

Dot Product
A·B
Cosine Similarity

Đây là cái dùng nhiều nhất.

0

Không giống
1

Giống hoàn toàn

Ví dụ

Bench Press

0.98
Push Up

0.91
Squat

0.12
Chương 5

Tại sao cần Vector Database?

Giả sử có

100 vector

Muốn tìm gần nhất.

Duyệt

Không sao.

Nếu

100 triệu vector

Mỗi query

100 triệu phép tính

Không thể.

Vector DB dùng

ANN

Approximate Nearest Neighbor

Ý tưởng

Không tìm toàn bộ.

Chỉ tìm vùng gần.

xxxxxxxxxxxxxxxx

xxxxxxx

xx

Query

●

xxxxxx

xxxx


Nhanh hơn hàng nghìn lần.

Chương 6

Vector Index

Giống B-tree của SQL.

Nhưng dành cho vector.

Các thuật toán phổ biến.

HNSW
IVF
PQ

Hiện nay

HNSW

được dùng nhiều nhất.

Qdrant

pgvector

Milvus

đều hỗ trợ.

Chương 7

pgvector

Đây là extension của PostgreSQL.

Tức là

PostgreSQL

+

Vector

Bạn vẫn có

JOIN

WHERE

GROUP BY

JSONB

và thêm

Embedding

Ví dụ

exercise

id

name

embedding
1

Bench Press

[....]

Query

SELECT *

FROM exercise

ORDER BY embedding <=> query_vector

LIMIT 5;
<=>

là cosine distance.

Ưu điểm

✅ Không cần DB mới

✅ SQL đầy đủ

✅ Transaction

✅ ACID

Nhược điểm

100 triệu vector

↓

Không nhanh bằng Qdrant.

Chương 8

Qdrant

Qdrant sinh ra chỉ để lưu vector.

Không phải SQL.

Kiểu

Collection

↓

Points

↓

Embedding

Một Point

id

vector

payload

Ví dụ

Point

id=1

vector=[...]

payload

{

"name":"Bench Press",

"muscle":"Chest"

}

Query

Query Vector

↓

Qdrant

↓

Top 10 nearest

Không cần SQL.

Ưu điểm

Rất nhanh

RAM tối ưu

HNSW

Filtering

Payload

Distributed

Nhược điểm

Không JOIN

Không Transaction như PostgreSQL
pgvector vs Qdrant
Tiêu chí	pgvector	Qdrant
Dựa trên	PostgreSQL	Vector DB chuyên dụng
SQL	✅	❌
JOIN	✅	❌
Transaction	✅	Hạn chế hơn
Vector Search	✅	✅
Tốc độ	Tốt	Rất nhanh
>10 triệu vector	Có thể	Phù hợp hơn
Metadata Filter	✅	✅
Scale ngang	Hạn chế	Tốt
Khi nào dùng pgvector?

Ví dụ

Workout AI

Exercise

Recipe

Food

Coach

Có khoảng

50.000 exercise

100.000 recipe

20.000 food

=> pgvector là quá đủ.

Khi nào dùng Qdrant?

Ví dụ

ChatGPT

Wikipedia

100 triệu document

PDF

Images

Logs

Lúc này

Qdrant

hoặc

Milvus

Weaviate

là hợp lý.

Hybrid Search

Production gần như không chỉ dùng Vector Search.

Ví dụ

Người dùng hỏi

Chest exercise

Pipeline

User

↓

Embedding

↓

Vector Search

↓

Top 100

↓

SQL Filter

↓

Business Logic

↓

LLM

Hoặc

User

↓

Keyword Search (BM25)

+

Vector Search

↓

Merge Ranking

↓

Top K

↓

LLM

Đây gọi là Hybrid Search, giúp vừa bắt được từ khóa chính xác vừa hiểu ngữ nghĩa.

AI Agent Pipeline Production

Đây là kiến trúc mà hầu hết các hệ thống AI hiện đại sử dụng.

User Question
      │
      ▼
Embedding Model
      │
      ▼
Vector Database (Qdrant / pgvector)
      │
      ▼
Top-K Similar Documents
      │
      ▼
Metadata Filter
(muscle=Chest, difficulty=Beginner...)
      │
      ▼
Business Logic
      │
      ▼
LLM (Gemini/OpenAI)
      │
      ▼
Final Response
Áp dụng vào dự án AI Workout của bạn

Với dự án hiện tại của bạn (FastAPI + MariaDB + AI Agent + Tool Calling), mình sẽ không dùng Vector DB để thay thế database chính.

Kiến trúc phù hợp sẽ là:

MariaDB
│
├── workout_plan
├── exercise
├── food
├── recipe
└── user
        │
        ├── Dữ liệu nghiệp vụ (source of truth)
        ▼

Embedding Service
        │
        ├── Sinh embedding cho:
        │     • exercise.name
        │     • exercise.description
        │     • recipe
        │     • tool descriptions
        ▼

Qdrant (hoặc pgvector nếu chuyển sang PostgreSQL)
        │
        ├── Lưu:
        │     vector
        │     exercise_id
        │     metadata
        ▼

AI Agent
        │
        ├── Embed câu hỏi người dùng
        ├── Semantic Search Top-K
        ├── Lấy ID phù hợp
        ├── Truy vấn chi tiết từ MariaDB
        ▼
Gemini
        │
        ▼
Câu trả lời cuối cùng

Đây là mô hình phổ biến trong production vì:

MariaDB/PostgreSQL vẫn là nguồn dữ liệu chính (ACID, transaction, quan hệ).
Qdrant/pgvector chỉ chịu trách nhiệm tìm kiếm ngữ nghĩa cực nhanh.
LLM chỉ nhận những tài liệu liên quan nhất thay vì toàn bộ cơ sở dữ liệu.

Nếu quy mô dữ liệu của bạn dưới vài triệu vector và bạn đã dùng PostgreSQL, pgvector rất tiện. Nếu hướng đến hệ thống RAG hoặc AI Agent với hàng chục triệu embedding và cần hiệu năng cao, Qdrant là lựa chọn chuyên dụng hơn.
Đây là một trong những phần quan trọng nhất của AI Agent production. Mình sẽ giải thích theo cách dễ hình dung nhất.

Đầu tiên phải hiểu:

Redis là RAM.

Nó không phải database chính như MariaDB.

Nó giống như một cuốn sổ ghi chú siêu nhanh.

Đặc điểm:

Đọc: khoảng vài trăm micro giây đến vài mili giây.
Ghi: rất nhanh.
Có thể tự xóa dữ liệu sau một thời gian (TTL).
Không dùng để lưu dữ liệu quan trọng lâu dài.
So sánh

MariaDB

User

↓

SELECT

↓

Đọc từ ổ cứng

Redis

User

↓

GET

↓

Đọc trực tiếp từ RAM

RAM nhanh hơn SSD rất nhiều.

Redis dùng để làm gì?

Trong AI Agent, thường có 4 mục đích lớn.

Session

Conversation State

Pending Actions

Cache
1. Session

Ví dụ

User đăng nhập.

MariaDB

user

id = 15

email

password

Sau khi login thành công.

Server tạo

session_id

abc123xyz

Redis lưu

Key

session:abc123xyz

↓

Value

{

user_id:15,

role:"premium",

expire:30 phút

}

Lần request tiếp theo.

Browser gửi

Cookie

abc123xyz

Server

↓

Redis

↓

Lấy được

user_id=15

Không cần query MariaDB.

Nhanh hơn.

Session Pipeline
Login

↓

MariaDB

↓

Password đúng

↓

Redis

session:abc123

↓

Browser lưu Cookie

↓

Request mới

↓

Redis

↓

User
2. Cache

Ví dụ

Có API

GET

/exercises

Trong DB

10000 bài tập

Mỗi request

SELECT *

FROM exercise

Tốn.

Thay vào đó.

Lần đầu

Client

↓

MariaDB

↓

10000 exercise

↓

Redis Cache

Lần sau

Client

↓

Redis

↓

Trả luôn

Không cần query SQL.

Ví dụ

Redis

Key

exercise:list

↓

Value

JSON
Cache Pipeline
Request

↓

Redis

↓

Có

↓

Return

Nếu không có

Redis

↓

MariaDB

↓

Redis

↓

Return
3. Conversation State

Đây là phần AI Agent dùng rất nhiều.

Ví dụ.

Bạn chat

User

Tôi muốn giảm cân.

AI

Được.

Sau đó

User

Nam.

25 tuổi.

70kg.


Rồi

Tôi nên ăn gì?

Nếu AI không nhớ.

Nó sẽ hỏi lại.

Redis sẽ lưu.

conversation:abc

{

goal:"lose weight",

gender:"male",

age:25,

weight:70

}

Lần prompt sau.

AI đọc.

↓

Biết ngay.

Pipeline

Prompt

↓

Redis

↓

Conversation State

↓

LLM

↓

Update State

↓

Redis
4. Pending Actions

Đây là phần rất nhiều AI Agent production sử dụng.

Ví dụ.

User

Đặt lịch tập cho ngày mai.

AI

↓

Bạn có chắc không?

User

Chưa trả lời.

Redis lưu

pending_action

{

type:"create_workout",

date:"tomorrow"

}

5 phút sau.

User

Đồng ý.

AI

↓

Redis

↓

Ồ

Đang chờ action

↓

Thực hiện luôn.

Nếu không có Redis.

AI sẽ quên.

Pipeline

User

↓

AI

↓

Pending Action

↓

Redis

↓

Sau

User

OK

↓

Redis

↓

Action

↓

Database

Ví dụ khác

AI

Bạn có muốn xóa lịch tập không?

Redis

pending

delete_workout

id=15

User

Có.

↓

AI

↓

Redis

↓

Biết đang xác nhận việc gì.

↓

Delete.

Trong AI Agent của bạn

Giả sử pipeline.

Gemini

↓

Tool Calling

↓

Workout Tool

↓

MariaDB

Redis sẽ nằm ở đâu?

User

↓

Redis

(Session)

↓

Redis

(Conversation)

↓

Gemini

↓

Tool Calling

↓

MariaDB

↓

Redis

(Cache)

↓

Response
Ví dụ thực tế

User

Tôi muốn tăng cơ.

Redis

goal

↓

gain muscle

User

Tôi chỉ có tạ đơn.

Redis

equipment

↓

dumbbell

User

Lập lịch tập giúp tôi.

Gemini

↓

Đọc Redis

↓

Biết

goal

gain muscle

equipment

dumbbell

↓

Gọi Tool

↓

Sinh Workout.

Không cần người dùng nhập lại.

Tóm tắt
Redis dùng để lưu	Có lưu lâu dài không?	Ví dụ
Session	❌ Không (TTL)	Người dùng đã đăng nhập
Cache	❌ Không (TTL)	Danh sách bài tập phổ biến
Conversation State	❌ Thường không (TTL)	Mục tiêu, tuổi, cân nặng trong cuộc trò chuyện
Pending Actions	❌ Không (TTL)	"Đang chờ xác nhận xóa lịch tập"
Phân biệt Redis và MariaDB trong AI Agent

Hãy nhớ một quy tắc rất dễ:

MariaDB = "Sự thật" (Source of Truth): lưu user, workout, recipe, exercise, lịch sử... Những dữ liệu này phải bền vững và không được mất.
Redis = "Bộ nhớ ngắn hạn" (Working Memory): lưu những gì AI hoặc ứng dụng cần nhớ trong vài phút đến vài giờ để xử lý nhanh.

Có thể hình dung như một người làm việc:

MariaDB giống tủ hồ sơ: mọi tài liệu chính thức đều được cất ở đó.
Redis giống tờ giấy ghi chú trên bàn: ghi những việc đang làm, thông tin cần dùng ngay. Làm xong thì bỏ đi.

Đó cũng chính là cách hầu hết các AI Agent production hiện nay sử dụng Redis.
Câu trả lời ngắn:

LangSmith không phải là framework. Nó là một nền tảng (platform) để quan sát, debug, đánh giá và kiểm thử ứng dụng LLM/AI Agent.

Nó giống như:

Với Backend → có Grafana, Prometheus, Jaeger
Với AI Agent → có LangSmith
Hệ sinh thái LangChain

Rất nhiều người nhầm các thành phần này.

LangChain
│
├── LangChain
│     Framework viết AI Agent
│
├── LangGraph
│     Framework xây AI Workflow/Agent phức tạp
│
└── LangSmith
      Monitoring + Debug + Evaluation

Nó giống như

FastAPI

↓

Application

↓

Prometheus

↓

Grafana

LangSmith đóng vai trò giống

Prometheus

+

Grafana

+

Jaeger

cho AI.

LangSmith làm gì?

Giả sử AI Agent của bạn.

User

↓

Gemini

↓

Tool Calling

↓

MariaDB

↓

Gemini

↓

Response

Một ngày AI trả lời sai.

Bạn sẽ hỏi

Sai ở đâu?

Nếu không có LangSmith.

Bạn chỉ có

print(prompt)

hoặc

logger.info(...)

Khá cực.

Có LangSmith.

Bạn mở dashboard.

Thấy toàn bộ.

Request

↓

System Prompt

↓

User Prompt

↓

LLM Response

↓

Tool Calling

↓

SQL

↓

Output

↓

Final Answer

Toàn bộ pipeline hiện ra.

Ví dụ

User

Lập lịch tập cho tôi.

LangSmith hiển thị

Trace

Request

↓

Prompt

↓

Gemini

↓

Tool

get_user_profile()

↓

Tool

search_exercise()

↓

Gemini

↓

Final Response

Bạn click từng bước.

Biết ngay.

Nó lưu gì?

Ví dụ.

Prompt

You are workout assistant...

↓

Model

gemini-2.5-pro

↓

Input

I want bigger chest

↓

Output

Bench Press...

↓

Latency

2.3 seconds

↓

Cost

$0.003

↓

Token

Input

1230

Output

420

Tất cả đều có.

Trace

Đây là tính năng mạnh nhất.

Ví dụ

AI Agent.

User

↓

Gemini

↓

Tool A

↓

Tool B

↓

Tool C

↓

Gemini

LangSmith sẽ vẽ

Run

│

├── Prompt

├── LLM

├── Tool A

├── Tool B

├── Tool C

└── Response

Giống Jaeger Trace.

Evaluation

Ví dụ.

Bạn có

100 prompt

Muốn biết.

AI mới có tốt hơn AI cũ không.

LangSmith chạy

100 Prompt

↓

Gemini

↓

Score

↓

Accuracy

↓

Hallucination

↓

Latency

Đây gọi là

Evaluation
Dataset

Ví dụ.

Prompt

↓

Expected Answer
Tăng cơ

↓

Workout A
Giảm cân

↓

Workout B

LangSmith lưu.

Sau này test.

AI mới.

↓

So sánh.

Playground

Bạn sửa Prompt.

You are fitness coach...

↓

Run.

↓

Đổi Prompt.

↓

Run.

↓

So sánh.

Không cần sửa code.

Monitoring

Production.

10000 request/ngày

LangSmith biết.

Average latency

2.1s
Prompt lỗi

2%
Hallucination

...
Cost

Ví dụ.

Gemini.

Input Tokens

Output Tokens

Total Cost

Hiển thị luôn.

Có bắt buộc dùng LangChain không?

Không.

Đây là điểm nhiều người nhầm.

Bạn có thể dùng

FastAPI

+

Gemini SDK

+

Qdrant

+

SQLAlchemy

Không có LangChain.

Vẫn dùng LangSmith được.

Hoặc thậm chí chỉ gửi trace thủ công.

Trong dự án AI Agent của bạn

Pipeline hiện tại của bạn có dạng:

User
        │
        ▼
FastAPI
        │
        ▼
Gemini
        │
        ▼
Tool Calling
        │
        ├── MariaDB
        ├── Redis
        ├── Qdrant
        ▼
Gemini
        ▼
Response

Nếu tích hợp LangSmith.

User
        │
        ▼
LangSmith Trace  ← Ghi toàn bộ pipeline
        │
        ▼
FastAPI
        │
        ▼
Gemini
        │
        ▼
Tool Calling
        │
        ├── SQL
        ├── Redis
        ├── Qdrant
        ▼
Gemini
        ▼
Response

Sau này nếu AI trả lời sai.

Bạn mở dashboard sẽ biết ngay:

Prompt có đúng không?
Tool nào được gọi?
SQL chạy ra dữ liệu gì?
Qdrant trả về document nào?
Gemini nhận context gì?
Gemini sinh câu trả lời như thế nào?

Không cần đọc hàng nghìn dòng log.

LangSmith có nên học không?

Theo lộ trình của bạn (xây AI Agent production), mình đánh giá:

Công nghệ	Mức độ ưu tiên
FastAPI Async	⭐⭐⭐⭐⭐
SQLAlchemy Async	⭐⭐⭐⭐⭐
Redis	⭐⭐⭐⭐⭐
Qdrant / pgvector	⭐⭐⭐⭐⭐
Tool Calling	⭐⭐⭐⭐⭐
MCP	⭐⭐⭐⭐☆
LangGraph	⭐⭐⭐⭐☆ (nếu workflow phức tạp)
LangSmith	⭐⭐⭐⭐☆ (rất nên biết khi đưa AI Agent lên production)

Điểm mấu chốt là: LangSmith không giúp AI "thông minh hơn". Nó giúp bạn hiểu AI đang làm gì, debug nhanh hơn, đánh giá chất lượng, theo dõi chi phí và vận hành hệ thống AI Agent một cách chuyên nghiệp. Đây là lý do nó được nhiều đội ngũ sử dụng khi ứng dụng AI đã bước sang giai đoạn production.
Nếu phải chọn một công nghệ AI được nhắc đến nhiều nhất năm 2025–2026, thì đó là MCP (Model Context Protocol).

Nhưng có một điều nhiều người hiểu sai:

MCP không phải AI.

MCP không phải framework.

MCP là một giao thức (Protocol).

Nó giống như:

HTTP là giao thức để Browser nói chuyện với Server.
SQL là ngôn ngữ để nói chuyện với Database.
MCP là giao thức để AI nói chuyện với Tool.
Hiểu bằng ví dụ

Giả sử bạn có AI Agent.

User

↓

Gemini

↓

MariaDB

Gemini không biết cách kết nối MariaDB.

Bạn phải viết

get_user()

get_workout()

create_plan()

delete_plan()

rồi truyền cho Gemini.

Điều này ổn.

Nhưng nếu sau này.

Bạn có thêm

Google Calendar

Notion

Slack

GitHub

Qdrant

Redis

Stripe

Bạn sẽ phải viết rất nhiều Tool.

Không có MCP
Gemini

│

├── Tool A

├── Tool B

├── Tool C

├── Tool D

├── Tool E

├── Tool F

Mỗi Tool

Có format khác nhau.

Có auth khác nhau.

Có schema khác nhau.

AI phải học từng cái.

Có MCP
Gemini

↓

MCP

↓

Google Calendar

↓

Notion

↓

Slack

↓

MariaDB

↓

GitHub

AI chỉ cần biết

"Nói chuyện bằng MCP."

Không cần quan tâm Tool bên dưới viết bằng Python, NodeJS hay Go.

MCP giống USB

Đây là ví dụ dễ hiểu nhất.

Ngày xưa.

Chuột.

PS/2

Bàn phím.

PS/2

Máy in.

COM

Camera.

FireWire

Rất loạn.

Sau đó.

USB ra đời.

Bây giờ.

Chuột

↓

USB
Bàn phím

↓

USB
Máy in

↓

USB

Máy tính chỉ cần biết

USB

Là dùng được.

MCP cũng vậy.

AI chỉ biết

MCP

Là gọi được mọi Tool.

MCP Server

Ví dụ.

Bạn có Database.

MariaDB

Bạn viết

MCP Server

Bên trong.

get_user()

create_workout()

delete_workout()

get_recipe()

Gemini không gọi Python trực tiếp.

Gemini

↓

MCP

↓

Tool.

Kiến trúc
Gemini

↓

MCP Client

↓

Internet

↓

MCP Server

↓

Tool

↓

MariaDB
Một MCP Server

Ví dụ.

Workout MCP Server

↓

get_user()

↓

search_exercise()

↓

create_workout()

↓

update_workout()

Gemini chỉ thấy.

4 Tool
Một MCP khác
Google Calendar MCP

↓

create_event()

↓

delete_event()

↓

list_events()

Gemini vẫn gọi giống hệt.

Vì sao MCP ra đời?

Ngày xưa.

OpenAI

Tool Calling.

Có format.

Gemini

Tool Calling.

Có format khác.

Anthropic

Tool Calling.

Khác nữa.

Rất rối.

MCP chuẩn hóa.

AI

↓

MCP

↓

Tool

AI nào cũng dùng được.

Ví dụ thực tế

User

Đặt lịch tập vào tối mai.

Gemini

↓

MCP

↓

Google Calendar MCP

↓

Tool

create_event()

↓

Google Calendar.

Hoặc.

Cho tôi lịch tập của tuần trước.

Gemini

↓

Workout MCP

↓

get_workout_plan()

↓

MariaDB.

MCP có thay thế FastAPI không?

Không.

FastAPI vẫn là API.

Ví dụ.

Browser

↓

FastAPI

↓

MariaDB

Không liên quan.

Nếu có AI.

Gemini

↓

MCP

↓

FastAPI

↓

MariaDB

Hoặc.

Gemini

↓

MCP

↓

Python Function

↓

MariaDB

Đều được.

MCP có thay Tool Calling không?

Không.

Thực ra.

Tool Calling

↓

MCP

↓

Tool

Tool Calling vẫn tồn tại.

MCP chỉ định nghĩa.

Tool trông như thế nào.
Input thế nào.
Output thế nào.
Discovery ra sao.
Authentication thế nào.
Trong dự án AI Workout của bạn

Hiện tại.

Gemini

↓

Function Calling

↓

search_exercise()

↓

create_workout()

↓

MariaDB

Hoàn toàn ổn.

Sau này.

Nếu muốn.

Bạn có thể chuyển.

Gemini

↓

MCP

↓

Workout MCP Server

↓

search_exercise()

↓

create_workout()

↓

update_workout()

↓

Redis

↓

Qdrant

↓

MariaDB

Gemini sẽ tự khám phá (discover) các tool mà MCP Server công bố thay vì bạn phải đăng ký từng function trong ứng dụng.

MCP có phải học ngay không?

Theo mình, với lộ trình hiện tại của bạn:

FastAPI Async
        ↓
SQLAlchemy Async
        ↓
Redis
        ↓
Qdrant
        ↓
Tool Calling
        ↓
AI Agent
        ↓
MCP
        ↓
LangGraph
        ↓
LangSmith

Đừng học MCP đầu tiên.

Lý do là MCP giải quyết bài toán tích hợp và chuẩn hóa giữa AI với nhiều công cụ, chứ không phải bài toán xây AI Agent cơ bản.

Nếu bạn đã có một AI Agent dùng Gemini Function Calling hoạt động tốt, thì chuyển sang MCP sẽ rất dễ. Ngược lại, nếu chưa hiểu Tool Calling, Repository, Service, hay pipeline Agent hoạt động ra sao, thì MCP sẽ chỉ là thêm một lớp trừu tượng khiến mọi thứ khó hiểu hơn.

Có thể xem MCP như "USB-C cho AI":

AI (Gemini, Claude, ChatGPT...) là máy tính.
Tool (Database, GitHub, Google Calendar, Redis...) là thiết bị ngoại vi.
MCP là chuẩn cắm chung để AI kết nối với mọi công cụ theo một giao thức thống nhất, thay vì mỗi công cụ dùng một kiểu giao tiếp riêng. Đây chính là giá trị lớn nhất của MCP.