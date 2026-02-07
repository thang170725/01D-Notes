- [Cấu trúc file cho toàn bộ hệ thống](#cấu-trúc-file-cho-toàn-bộ-hệ-thống)
---
# Cấu trúc file cho toàn bộ hệ thống
**ROOT LEVEL**
```bash
.
├── backend/              # toàn bộ backend services
├── frontend/             # toàn bộ frontend (html, react, next…)
├── gateway/              # API Gateway / BFF
├── shared/               # code / schema / utils dùng chung
├── data/                 # dữ liệu runtime
├── dataset/              # dữ liệu huấn luyện (AI)
├── database/              # dữ liệu huấn luyện (AI)
├── infra/                # hạ tầng (docker, k8s, terraform)
├── scripts/              # script dev / deploy / migrate
├── docs/                 # tài liệu
├── tests/                # test integration / e2e
├── .env.example
└── README.md
```
**BACKEND - cấu trúc CHUẨN 100% (1 service)**
```bash
Áp dụng cho:
- Python
- Java
- Node
- Go
```
```bash
backend/
└── user-service/
    ├── app/
    │   ├── main.py              # entry point (start server)
    │   │
    │   ├── config/              # cấu hình hệ thống
    │   │   ├── settings.py
    │   │   └── logging.py
    │   │
    │   ├── api/                 # controller / router (HTTP layer)
    │   │   └── v1/
    │   │       └── user_api.py
    │   │
    │   ├── schemas/             # định nghĩa request/response
    │   │   └── user_schema.py
    │   │
    │   ├── domain/              # entity, business model
    │   │   └── user.py
    │   │
    │   ├── services/            # business logic
    │   │   └── user_service.py
    │   │
    │   ├── repositories/        # DB access layer
    │   │   └── user_repo.py
    │   │
    │   ├── core/                # logic cốt lõi của service, thuật toán nặng / AI / ML
    │   │   └── id3.py
    │   │
    │   ├── workers/             # background jobs (queue, cron)
    │   │   └── email_worker.py
    │   │
    │   ├── integrations/        # gọi service bên ngoài
    │   │   └── payment_client.py
    │   │
    │   ├── utils/               # helper, logger, constants
    │   │   └── time.py
    │   │ 
    │   ├── usecases/              
    │   │   └ 
    │   │
    │   └── exceptions/          # custom error
    │       └── user_error.py
    │
    ├── tests/
    │   ├── unit/
    │   ├── integration/
    │   └── e2e/
    │
    ├── migrations/              # DB migration
    ├── requirements.txt
    ├── Dockerfile
    └── README.md
```
**FRONTEND - kết hợp HTML + CSS + JS + React + Next**
```text
❗ Nguyên tắc:
- Next.js = framework chính
- HTML/CSS/JS thuần = static / legacy
- React component nằm trong Next
```
```bash
frontend/
└── web-cra/                     # web tạo bằng react
    ├── public/                  # static thuần (html, image)
    │   ├── legacy/
    │   │   └── landing.html
    │   └── assets/
    │
    ├── src/
    │   │
    │   ├── pages/               # nếu cần Pages Router
    │   │   └── HomePage.jsx
    │   │
    ├── components/          # React components
    │   │   └── Hello.jsx
    │   │    
    │   ├── hooks/               # custom hooks
    │   │
    │   ├── services/            # gọi API
    │   │   └── user.service.js
    │   │
    │   ├── store/               # state management
    │   │
    │   ├── styles/              # css / scss / tailwind
    │   │
    │   ├── utils/               # helper frontend
    │   │
    │   └── constants/
    │   └── App.jsx
    │   └── index.js
    │
    ├── package.json
    └── README.md
└── web-ssr/                     # Next.js
```

Ok, mình dừng lý thuyết, không nói thuật ngữ cao siêu nữa.
Mình giải thích bằng ví dụ đời thực + map thẳng vào project của BẠN.

Bạn chỉ cần nhớ 1 câu duy nhất trước:

Core = đồ nghề
Repository = người đi lấy đồ
Usecase = người quyết định làm món gì
Utils = đồ lặt vặt hỗ trợ

Giờ đi từng cái.

1️⃣ Ví dụ đời thực: QUÁN PHỞ 🍜

Giả sử bạn mở quán phở.

🔧 CORE = ĐỒ NGHỀ TRONG BẾP

Core KHÔNG tự nấu, KHÔNG bán

Nó chỉ là:

Dao

Nồi

Bếp gas

Công thức cơ bản

Map vào project của bạn
core/
├── db.py        → kết nối DB (ổ cắm điện)
├── tables.py   → biết DB có bảng gì (danh sách nguyên liệu)
├── queries.py  → viết SQL (cách thái thịt, hầm xương)


👉 Core KHÔNG biết:

ai gọi

làm để ML hay API

dữ liệu dùng để làm gì

📌 Core chỉ biết: “Làm sao query cho đúng”

2️⃣ REPOSITORY = NGƯỜI ĐI CHỢ 🧺

Repository:

dùng dao, nồi (core)

đi lấy nguyên liệu đúng yêu cầu

Ví dụ đời thực

“Đi chợ mua:

thịt bò

hành

giá”

Repository KHÔNG nấu, chỉ mua về.

Map vào project của bạn
repositories/
└── listings_repository.py

def get_listings_with_district(engine, params):
    # dùng core.query
    # fetch raw data
    return rows


👉 Repository:

gọi query

gọi DB

trả về data thô

❌ Repository KHÔNG:

pandas

ML

business logic

📌 Repository = data access

3️⃣ USECASE = ĐẦU BẾP 👨‍🍳

Usecase:

quyết định nấu món gì

gọi nhiều repository

xử lý dữ liệu

Ví dụ đời thực

“Hôm nay nấu:

phở bò tái

thêm gầu

ít hành”

Map vào project của bạn (RẤT QUAN TRỌNG)
usecases/
└── prepare_training_dataset.py

def prepare_training_dataset(engine):
    rows = listings_repo.get_listings_with_district(engine)
    df = pd.DataFrame(rows)
    df["price_per_m2"] = df["price_total"] / df["area"]
    return df


👉 Usecase:

dùng repository

dùng pandas

xử lý data

phục vụ ML / API

📌 Usecase = logic thật của hệ thống

4️⃣ UTILS = ĐỒ LẶT VẶT 🧂

Utils:

không thuộc bếp

không thuộc món ăn

dùng ở nhiều nơi

Ví dụ đời thực

cân điện tử

muỗng đong

khăn lau

Map vào project của bạn
utils/
├── logger.py
├── validators.py
├── converters.py


Ví dụ:

def snake_to_camel(s: str) -> str:
    ...


📌 Utils KHÔNG được import core / repository / usecase

5️⃣ Toàn bộ flow thực tế (rất quan trọng)
Khi bạn chạy ML:
Usecase
  ↓
Repository
  ↓
Core (query, db)
  ↓
MySQL

KHÔNG BAO GIỜ ngược lại

❌ Core gọi usecase
❌ Repository gọi usecase

6️⃣ Áp thẳng vào project của bạn (ngắn gọn)
app/
├── core/            # đồ nghề DB
│
├── repositories/   # lấy dữ liệu
│
├── usecases/       # xử lý nghiệp vụ / ML
│
├── utils/          # helper
│
├── schemas/        # input/output

7️⃣ Trả lời câu hỏi gốc của bạn (dứt khoát)

executor cao hơn queries, tables, db → để đâu?

✅ executor = usecase

❌ KHÔNG để chung với core
❌ KHÔNG để trong repository

8️⃣ Chốt 1 câu cho khỏi rối

Core: làm sao query
Repository: lấy data
Usecase: dùng data để làm việc thật
Utils: đồ phụ

Nếu bạn muốn, bước tiếp theo mình có thể:

vẽ flow đúng 1 file ML chạy thế nào

refactor 1 file thật của bạn sang đúng tầng

giúp bạn viết usecase đầu tiên hoàn chỉnh

👉 Bạn muốn mình refactor trực tiếp file nào của bạn không?