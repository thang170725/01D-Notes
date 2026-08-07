- [.drop\_table()](#drop_table)
- [.add\_column()](#add_column)
- [drop\_column()](#drop_column)
- [alter\_column()](#alter_column)
- [.create\_foreign\_key()](#create_foreign_key)
- [.drop\_constraint()](#drop_constraint)
- [.create\_index()](#create_index)
- [.drop\_index()](#drop_index)
- [.create\_unique\_constraint()](#create_unique_constraint)
- [.execute()](#execute)
---
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
# op (operation object)
## .create_table()
```bash
dùng để tạo bảng
```
**Ex**
```python
from alembic import op
import sqlalchemy as sa

op.create_table(
    "table_name",
    sa.Column("id", sa.Integer, primary_key=True),
    sa.Column("name", sa.String(100), nullable=False),
    sa.Column("created_at", sa.DateTime),
)
```
## .drop_table()
```bash
Để xóa bảng.
```
**Syn**
```bash
op.drop_table("table_name")
```
## .add_column()
```bash
Để thêm cột.
```
**Syn**
```bash
op.add_column(
    "table_name",
    sa.Column("age", sa.Integer, nullable=True)
)
```
## drop_column()
```bash
Xóa cột
```
**Syn**
```bash
op.drop_column("table_name", "age")
```
## alter_column()
```bash
Để sửa cột.
```
**Ex**
```python
op.alter_column(
    "users",
    "email",
    existing_type=sa.String(255),
    nullable=False
)
```
## .create_foreign_key()
```bash
Tạo khóa ngoài
```
**Syn**
```bash
op.create_foreign_key(
    "fk_name",
    "child_table",
    "parent_table",
    ["child_column"],
    ["parent_column"],
    ondelete="CASCADE"
)
```
## .drop_constraint()
```bash
Xóa khóa ngoài
```
**Syn**
```bash
op.create_foreign_key(
    "fk_name",
    "child_table",
    "parent_table",
    ["child_column"],
    ["parent_column"],
    ondelete="CASCADE"
)
```
## .create_index()
```bash
Tạo index.
```
**Syn**
```bash
op.create_index(
    "ix_name",
    "table_name",
    ["column_name"],
    unique=False
)
```
## .drop_index()
```bash
Xóa index
```
**Syn**
```bash
op.drop_index("ix_name", table_name="table_name")
```
## .create_unique_constraint()
```bash
Tạo Unique Constraint
```
**Syn**
```bash
op.create_unique_constraint(
    "uq_name",
    "table_name",
    ["column_name"]
)
```
## .execute()
```bash
Thực thi raw SQL
```
**Syn**
```bash
op.execute("UPDATE users SET active = 1")
```