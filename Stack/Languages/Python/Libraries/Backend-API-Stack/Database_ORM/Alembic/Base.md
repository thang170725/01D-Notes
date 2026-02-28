# Installation & Setup
```bash
1. pip install alembic
2. alembic init migrations
    + Tạo các file setup migrations
    + alembic.ini → cấu hình database
    + env.py → nơi Alembic kết nối với project của bạn
    + versions/ → nơi chứa các file migration
3. alembic.ini
    + tìm dòng sqlalchemy.url = driver://user:pass@localhost/dbname và thay đường dẫn đến db
4. env.py
    + Tìm dòng: target_metadata = None
    + Sửa thành:
        from your_model_file import Base        
        target_metadata = Base.metadata
    + Ví dụ nếu model bạn nằm ở models.py:
        from models import Base
        target_metadata = Base.metadata
5. alembic stamp head
    + Nó chỉ đánh dấu: "DB này đang ở version mới nhất".
6. alembic revision -m "add email to users"
    + Tạo migration mới
    + Nó sẽ tạo file trong: migrations/versions/xxxxxxxx_add_email_to_users.py
7. Viết nội dung migration
    + Mở file đó và chỉnh:
        from alembic import op
        import sqlalchemy as sa

        def upgrade():
            op.add_column(
                "users",
                sa.Column("email", sa.String(50), nullable=True)
            )

        def downgrade():
            op.drop_column("users", "email")
8. alembic upgrade head --sql
    + test
9. alembic upgrade head
    + Chạy migration
    + Lúc này nó sẽ chỉ chạy:
    + ALTER TABLE users ADD COLUMN email VARCHAR(50);
    + Không đụng bảng khác.
```
# Introduction
```bash
- Alembic là một công cụ trong Python dùng để quản lý migration (di trú) cơ sở dữ liệu, thường được sử dụng cùng với SQLAlchemy.
- Khi bạn thay đổi cấu trúc database (thêm cột, xóa bảng, đổi kiểu dữ liệu…), bạn cần cập nhật database mà không làm mất dữ liệu cũ. Alembic giúp bạn:
    + Quản lý thay đổi schema database
    + Tạo bảng mới
    + Thêm / sửa / xóa cột
    + Tạo hoặc xóa index, constraint
    + Đổi tên bảng
    + Tạo migration script
- Alembic sinh ra các file migration (Python script) mô tả thay đổi database.
```