- [Architecture](#architecture)
---
# Architecture
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
```bash
- Nguyên tắc:
  + Next.js = framework chính
  + HTML/CSS/JS thuần = static / legacy
  + React component nằm trong Next
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