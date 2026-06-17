- [](#)
- [Quản lý người dùng](#quản-lý-người-dùng)
---
# 
# Quản lý người dùng
```bash
1. Tạo db có bảng users (id, name, email, created_at)
2. Thêm 2 user
    + Alice - alice@example.com
    + Bob   - bob@example.com
3. In ra tất cả user
4. In ra user có email là alice@example.com
5. Đổi tên Bob -> Robert
6. Xóa user có email alice@example.com
```
```python
from sqlalchemy import (
    create_engine,
    MetaData,
    Table,
    Column,
    Integer,
    String,
    DateTime,
    insert,
    select,
    update,
    delete,
)
from datetime import datetime, timezone

# =====================
# 1. CREATE ENGINE
# =====================
engine = create_engine(
    "mysql+pymysql://ai_user:ai123@localhost:3306/ManageUser",
    echo=True
)

metadata = MetaData()

# =====================
# 2. DEFINE TABLE
# =====================
users = Table(
    "users",
    metadata,
    Column("id", Integer, primary_key=True),
    Column("name", String(100), nullable=False),
    Column("email", String(100), unique=True, nullable=False),
    Column(
        "created_at",
        DateTime(timezone=True),
        default=lambda: datetime.now(timezone.utc),
    ),
)

# =====================
# 3. CREATE TABLE
# =====================
metadata.create_all(engine)

# =====================
# 4. CRUD OPERATIONS
# =====================
with engine.begin() as conn:

    # 2. Thêm 2 user
    conn.execute(
        insert(users),
        [
            {"name": "Alice", "email": "alice@example.com"},
            {"name": "Bob", "email": "bob@example.com"},
        ],
    )

    # 3. In ra tất cả user
    print("\n--- ALL USERS ---")
    result = conn.execute(select(users))
    for row in result:
        print(row.id, row.name, row.email, row.created_at)

    # 4. In user có email = alice@example.com
    print("\n--- USER ALICE ---")
    alice = conn.execute(
        select(users).where(users.c.email == "alice@example.com")
    ).first()
    print(alice.id, alice.name, alice.email)

    # 5. Đổi tên Bob -> Robert
    conn.execute(
        update(users)
        .where(users.c.name == "Bob")
        .values(name="Robert")
    )

    # 6. Xoá user có email alice@example.com
    conn.execute(
        delete(users)
        .where(users.c.email == "alice@example.com")
    )

    # Kiểm tra lại dữ liệu
    print("\n--- AFTER UPDATE & DELETE ---")
    result = conn.execute(select(users))
    for row in result:
        print(row.id, row.name, row.email, row.created_at)
```