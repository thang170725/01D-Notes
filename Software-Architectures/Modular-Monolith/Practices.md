- [Architecture](#architecture)
---
# Kiến trúc mẫu Python + ReactJS
**Backend: Python**
```bash
backend/
├── modules/
│   ├── recipes/            # Module Công thức    
│   │   ├── service.py      # Logic xử lý recipe
│   │   ├── models.py       # DB model của recipe
│   │   ├── routes.py       # Endpoint cho recipe
│   │   ├── dependencies.py # database connection, redis client, http client
│   │   ├── repository.py   # DB access
│   │   └── schemas.py      # Pydantic schemas cho recipe
│   │
│   ├── ai_assistant/       # Module Trợ lý AI (Cái bạn đang làm)
│   │   ├── chain.py        # Logic LangChain
│   │   ├── service.py      # Xử lý prompt, context
│   │   └── prompts.py      # Các template câu lệnh cho AI
│   │
│   └── inventory/          # Module Kho nguyên liệu
│       └── service.py
│
├── core/                   # Những thứ dùng chung cho toàn hệ thống
│   ├── database.py         # Kết nối DB chung
│   ├── config.py           # Biến môi trường
│   └── security.py         # JWT, Hash password
└── app.py                  # File chính để "cắm" các module vào
```
**Frontend**
```bash
frontend/
├── src/
│   ├── components/            # Module Công thức    
│   │   ├── service.py      # Logic xử lý recipe
│   │   ├── models.py       # DB model của recipe
│   │   ├── routes.py       # Endpoint cho recipe
│   │   ├── dependencies.py # database connection, redis client, http client
│   │   ├── repository.py   # DB access
│   │   └── schemas.py      # Pydantic schemas cho recipe
│   │
│   ├── features/       # Module Trợ lý AI (Cái bạn đang làm)
│   │   ├── chain.py        # Logic LangChain
│   │   ├── service.py      # Xử lý prompt, context
│   │   └── prompts.py      # Các template câu lệnh cho AI
│   │
│   ├── layout/       # Module Trợ lý AI (Cái bạn đang làm)
│   │   ├── chain.py        # Logic LangChain
│   │   ├── service.py      # Xử lý prompt, context
│   │   └── prompts.py      # Các template câu lệnh cho AI
│   │
│   ├── pages/       # Module Trợ lý AI (Cái bạn đang làm)
│   │   ├── chain.py        # Logic LangChain
│   │   ├── service.py      # Xử lý prompt, context
│   │   └── prompts.py      # Các template câu lệnh cho AI
│   │
│   ├── routes/             # Bộ điều khiển URL (link pages)
│   │
│   └── services/          # Module Kho nguyên liệu
│       └── service.py
│
├── core/                   # Những thứ dùng chung cho toàn hệ thống
│   ├── database.py         # Kết nối DB chung
│   ├── config.py           # Biến môi trường
│   └── security.py         # JWT, Hash password
└── app.py                  # File chính để "cắm" các module vào
```