- [Alembic Introduction (dùng để quản lý migration (di trú) cơ sở dữ liệu, thường được sử dụng cùng với SQLAlchemy)](#alembic-introduction-dùng-để-quản-lý-migration-di-trú-cơ-sở-dữ-liệu-thường-được-sử-dụng-cùng-với-sqlalchemy)
- [Installation](#installation)
- [Ask](#ask)
  - [Alembic có thật sự được dùng nhiều trong production không?](#alembic-có-thật-sự-được-dùng-nhiều-trong-production-không)
---
# Alembic Introduction (dùng để quản lý migration (di trú) cơ sở dữ liệu, thường được sử dụng cùng với SQLAlchemy)
```bash
Khi bạn thay đổi cấu trúc database (thêm cột, xóa bảng, đổi kiểu dữ liệu, ...), bạn cần cập nhật database mà không làm mất dữ liệu cũ. Alembic giúp bạn:
    + Quản lý thay đổi schema database
    + Tạo bảng mới
    + Thêm / sửa / xóa cột
    + Tạo hoặc xóa index, constraint
    + Đổi tên bảng
    + Tạo migration script

Alembic sinh ra các file migration (Python script) mô tả thay đổi database.
```
# Installation 
```bash
1. pip install alembic
```
# Ask
## Alembic có thật sự được dùng nhiều trong production không?
```bash
Có. Alembic được dùng rất nhiều trong production, đặc biệt trong hệ thống Python dùng SQLAlchemy. 
    Điểm quan trọng là: Alembic không phải công cụ dành riêng cho senior, nhưng để dùng nó thực sự tốt trong production thì thường cần hiểu khá chắc về database.

1. Vì sao Alembic có cảm giác khó?
    Vì nó không đơn thuần là: “Tôi sửa model Python → Alembic tự sửa database.”

    Nó đang giải quyết một bài toán lớn hơn: Database đã tồn tại ở version nào, và làm thế nào đưa nó sang version mới một cách an toàn?

    Ví dụ ban đầu:
        Database v1
            users
            ├── id
            └── name

        Sau đó bạn sửa SQLAlchemy model:
            class User(Base):
                id = Column(Integer, primary_key=True)
                name = Column(String)
                email = Column(String)

        Alembic cần tạo migration:
            v1
             ↓
            migration 001
             ↓
            v2

        và migration có thể chứa:
            def upgrade():
                op.add_column(
                    "users",
                    sa.Column("email", sa.String())
                )


            def downgrade():
                op.drop_column("users", "email")

        Đây chính là lý do có những thứ như:
            - alembic revision
            - alembic upgrade
            - alembic downgrade
            - alembic current
            - alembic history

        và các file:
            alembic/
            ├── env.py
            ├── script.py.mako
            └── versions/
                ├── xxx_create_user.py
                ├── yyy_add_email.py
                └── zzz_add_index.py

        Nhìn ban đầu khá rối.

2. Nhưng trong production thì đây lại là điểm mạnh
    Hãy tưởng tượng bạn có production database:
        - 10 tables
        - 500GB data
        - 20 developers
        - 100 migration changes

    Nếu mỗi lần thay đổi model lại chạy kiểu:
        ALTER TABLE ...
    
        thủ công thì rất nguy hiểm.
        
        Alembic giúp team biết chính xác:
            Database hiện đang ở migration nào?
                    ↓
            Migration tiếp theo là gì?
                    ↓
            Migration tiếp theo nữa là gì?
```