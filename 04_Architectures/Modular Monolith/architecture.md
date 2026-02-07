**Ex**
```bash
- Giả sử bạn có 1 app AI rất đơn giản:
    + Có frontend (web)
    + Có backend
    + Có database
    + Có AI (ví dụ: dự đoán / gợi ý)
```
# Kiến trúc chuẩn
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