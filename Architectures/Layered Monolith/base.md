```bash
backend/
│
├── app.py
│   # File khởi động ứng dụng
│   # Chạy server, load config, wire các module lại với nhau
│
├── config/
│   ├── settings.py
│   # Cấu hình chung: DB, path model, env (dev/prod)
│   │
│   └── logging.py
│       # Log toàn hệ thống
│
├── data/
│   # MỌI THỨ LIÊN QUAN ĐẾN DỮ LIỆU THÔ
│   # (DB, CSV, parquet, raw data...)
│   │
│   ├── db/
│   │   ├── connection.py
│   │   # Kết nối database
│   │   │
│   │   └── repositories.py
│   │       # Query dữ liệu thô (KHÔNG business logic)
│   │
│   ├── csv/
│   │   ├── csv_reader.py
│   │   # Đọc file CSV
│   │   │
│   │   └── csv_exporter.py
│   │       # Xuất dữ liệu ra CSV (phục vụ train AI)
│   │
│   └── dataset_builder.py
│       # Ghép + clean dữ liệu
│       # DB → dataset dùng cho AI
│
├── ai/
│   # LÕI AI – KHÔNG BIẾT DB, KHÔNG BIẾT API
│   │
│   ├── model/
│   │   ├── model.py
│   │   # Định nghĩa model (ML / DL / LLM wrapper)
│   │   │
│   │   └── load_model.py
│   │       # Load model từ file
│   │
│   ├── training/
│   │   ├── train.py
│   │   # Code train model (offline)
│   │   │
│   │   └── evaluate.py
│   │       # Đánh giá model
│   │
│   ├── inference/
│   │   └── predict.py
│   │       # Nhận input → gọi model → trả output
│   │
│   └── features.py
│       # Xử lý feature (vector hoá, normalize...)
│
├── api/
│   # LỚP GIAO TIẾP VỚI FRONTEND
│   │
│   ├── routes.py
│   # Định nghĩa endpoint (REST / GraphQL)
│   │
│   └── schemas.py
│       # Validate input / output (DTO)
│
├── jobs/
│   # CÁC TASK CHẠY NỀN
│   │
│   ├── train_model_job.py
│   # Job train model theo lịch
│   │
│   └── export_dataset_job.py
│       # Job xuất dataset từ DB → CSV
│
├── shared/
│   # CODE DÙNG CHUNG (RẤT ÍT)
│   │
│   ├── utils.py
│   # Hàm nhỏ: format, time, hash...
│   │
│   └── exceptions.py
│       # Exception dùng chung
│
└── tests/
    # Test từng phần riêng
```