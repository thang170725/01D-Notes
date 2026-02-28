- [Create \& Config](#create--config)
  - [sessionmaker()](#sessionmaker)
- [declarative\_base() \& DeclarativeBase](#declarative_base--declarativebase)
- [Session](#session)
  - [Column()](#column)
- [DataType](#datatype)
  - [Integer](#integer)
  - [String \& DateTime](#string--datetime)
  - [Enum](#enum)
  - [Date \& TIMESTAMP](#date--timestamp)
- [Table](#table)
- [.add() \& .commit() \& refresh()](#add--commit--refresh)
- [.query() \& .first() \& .filter() \& .all()](#query--first--filter--all)
- [like()](#like)
- [filter\_by()](#filter_by)
- [sa](#sa)
---
# Create & Config
## sessionmaker()
```bash
- Tạo "nhà máy" sinh ra các session, nơi bạn làm việc với db bằng ORM
- Không thể làm việc trực tiếp db bằng ORM nếu không có Session
**Syn**
```bash
from sqlalchemy.orm import sessionmaker

SessionLocal = sessionmaker(
    bind=engine,
    autocommit=False,
    autoflush=False,
)

- bind=engine	    : gắn session với DB
- autocommit=False	: không tự commit
- autoflush=False	: không tự đẩy dữ liệu
- SessionLocal()	: tạo 1 session mới
```
**Ex**
```python
from sqlalchemy import create_engine
from sqlalchemy.orm import sessionmaker

DATABASE_URL = "mysql+pymysql://user:pass@localhost/dbname"

engine = create_engine(DATABASE_URL)

SessionLocal = sessionmaker(
    bind=engine,
    autocommit=False,
    autoflush=False,
)

def get_db():
    db = SessionLocal()
    try:
        yield db
    finally:
        db.close()

# mỗi lần gọi SessionLocal() là tạo một session mới
```
# declarative_base() & DeclarativeBase
```bash
- Tạo một Base class để các model (class) kế thừa.
- Nó giúp:
    + Map class → table
    + Tự động quản lý metadata
    + Tạo schema bằng Base.metadata.create_all()
```
**Syn: Cách cũ**
```python
from sqlalchemy.orm import declarative_base
from sqlalchemy import Column, Integer, String

Base = declarative_base()

class User(Base):
    __tablename__ = "users"

    id = Column(Integer, primary_key=True)
    name = Column(String)
```
**Syn: Cách mới**
```bash
from sqlalchemy.orm import DeclarativeBase

class Base(DeclarativeBase):
    pass
```
# Session
```bash
- Nó giống như “phiên làm việc” giữa app và database
- Bạn không thao tác trực tiếp với DB → Bạn thao tác qua Session
- Dùng để:
    + Làm việc với database thông qua ORM
    + Quản lý transaction (commit / rollback)
    + Thêm, sửa, xóa, query dữ liệu
```
**Syn**
```bash
from sqlalchemy.orm import Session
```
**Ex: thêm dữ liệu bằng Session**
```bash
def create_user(db: Session):
    user = User(name="Thang")
    db.add(user)
    db.commit()
    db.refresh(user)
    return user
```
## Column()
```bash
Định nghĩa cột trong bảng
```
**Syn: Column**
```bash
Column(
    name,
    type_,
    primary_key=False,
    nullable=True,
    unique=False,
    default=None,
    index=False,
    foreign_key=...
)
```
# DataType
## Integer
## String & DateTime
## Enum
**Ex**
```python
Enum('sedentary', 'light', "moderate", name='activity_level_role')
```
## Date & TIMESTAMP
```bash
- Date: Chỉ lưu ngày (không lưu giờ)
    + Format chuẩn: YYYY-MM-DD
    + Ví dụ: 2026-02-25
    + Nếu bạn query bằng SQLAlchemy DATE → trả về kiểu: datetime.date
- TIMESTAMP: Chỉ lưu ngày + giờ
    + Format chuẩn: YYYY-MM-DD HH:MM:SS
    + Ví dụ: 2026-02-25 14:30:45
    + TIMESTAMP → trả về kiểu: datetime.datetime
```
# Table
```bash
- Table là biểu diễn Python cho một bảng SQL cụ thể trong db.
- Nó KHÔNG:
    + Tạo bảng (trừ khi bạn create_all)
    + Không chạy query
    + Không chứa dữ liệu
- Nó CHỈ:
    + Mô tả schema của bảng
    + Là nguyên liệu để build SQL thuần
- Dùng khi:
    + Viết query thuần
    + Không cần ORM Model
    + DB có sẵn
    + Viết tool, admin, ETL, report
- Không nên dùng Table khi:
    + Domain logic phức tạp
    + Cần relationship
    + App CRUD lớn (lúc đó dùng ORM)
```
**Syn**
```bash
Table(
    table_name,
    metadata,
    Column(...),
    Column(...),
    autoload_with=engine # dùng khi db đã có bảng
)

- SQLAlchemy sẽ:
    + Connect DB
    + Read schema
    + Tự tạo Column objects
-> Đây gọi là: Table reflection
```
**Ex1: MetaData chứa Table (cách bạn đang dùng)**
```python
from sqlalchemy import MetaData, Table

metadata = MetaData()

users = Table(
    "users",
    metadata,
    autoload_with=engine
)

orders = Table(
    "orders",
    metadata,
    autoload_with=engine
)

Lúc này: metadata.tables
Output (dict-like):
{
  'users': <sqlalchemy.Table users>,
  'orders': <sqlalchemy.Table orders>
}

```
**Ex2: Vì sao dùng chung MetaData là QUAN TRỌNG**
```python
Table("users", MetaData(), autoload_with=engine)
Table("orders", MetaData(), autoload_with=engine)

# Hậu quả:
# Sai cách (mỗi bảng một metadata)
# SQLAlchemy không biết 2 bảng liên quan gì
# Không join được chuẩn
# Không quản lý được schema

metadata = MetaData()

users = Table("users", metadata, autoload_with=engine)
orders = Table("orders", metadata, autoload_with=engine)
```

6. Demo 3: Join 2 bảng nhờ MetaData

Giả sử:

orders.user_id → users.id

from sqlalchemy import select

stmt = (
    select(
        users.c.email,
        orders.c.total_amount
    )
    .select_from(
        users.join(
            orders,
            users.c.id == orders.c.user_id
        )
    )
)


👉 Join KHÔNG cần ORM, chỉ cần:

Table

MetaData dùng chung

7. Demo 4: MetaData + create_all (ít dùng khi DB có sẵn)
metadata = MetaData()

Table(
    "logs",
    metadata,
    Column("id", Integer, primary_key=True),
    Column("message", String(255))
)

metadata.create_all(engine)


👉 SQLAlchemy sẽ:

Đọc metadata.tables

Tạo bảng tương ứng

8. Demo 5: Reflect toàn bộ DB bằng MetaData
metadata = MetaData()
metadata.reflect(bind=engine)

print(metadata.tables.keys())


👉 Output:

dict_keys(['users', 'orders', 'products'])


➡️ MetaData lúc này là “ảnh chụp” toàn bộ DB

9. Liên hệ với TableFactory của bạn

Class bạn viết:

self.metadata = MetaData()


👉 Ý nghĩa:

Tất cả bảng load từ TableFactory

Đều nằm trong 1 registry

Join, reuse, cache đều OK

👉 Đây là cách làm đúng.

10. Khi nào nên có NHIỀU MetaData?

Hiếm, nhưng có:

Multi-database

Multi-tenant

Migrate schema độc lập

Ví dụ:

user_metadata = MetaData()
log_metadata = MetaData()

# .add() & .commit() & refresh()
```bash
- add       : đưa object vào session chưa ghi xuống db.
- commit    : thực sự insert vào db. nếu lỗi -> rollback
- refresh   : lấy dữ liệu mới nhất từ db
```
**Ex**
```python
@router.post("/register")
def register(
    payload: UserSchema,
    db: Session = Depends(get_db)
):
    user = User(
        **payload.model_dump(exclude_unset=True)
    )

    db.add(user)
    db.commit()
    db.refresh(user)

    return {
        "id": user.id,
        "username": user.username
    }
```
# .query() & .first() & .filter() & .all()
```bash
- query     : Nghĩa là: “Tôi muốn lấy dữ liệu từ bảng users”
- first     : Nghĩa là: “Lấy 1 dòng đầu tiên hoặc None”
- all       : Lấy tất cả dòng.
- filter    : Nghĩa là: “Lọc theo điều kiện”
```
**Syn: query**
```bash
db.query(User) # SELECT * FROM users
```
**Syn: filter**
```bash
.filter(User.username == "admin") # WHERE username = 'admin'
```
**Ex**
**Model**
```python
class User(Base):
    __tablename__ = "users"

    id = Column(Integer, primary_key=True)
    username = Column(String)
    age = Column(Integer)

user = db.query(User).filter(User.username == "thang").first() # SELECT * FROM users WHERE username = 'thang' LIMIT 1;

# user là object User
# Hoặc None
```
# like()
# filter_by()
# sa
sa = alias của SQLAlchemy

import sqlalchemy as sa
1️⃣ Kiểu dữ liệu (Data Types)
sa.Integer
sa.String(length)
sa.Text
sa.Boolean
sa.Date
sa.DateTime
sa.Float
sa.Numeric(10, 2)
sa.JSON
sa.Enum("A", "B", name="enum_name")

Ví dụ:

sa.Column("price", sa.Numeric(10, 2))
2️⃣ Column
sa.Column(
    "name",
    sa.String(100),
    nullable=False,
    unique=True,
    default="abc"
)
3️⃣ ForeignKey (khi create_table)
sa.Column(
    "user_id",
    sa.Integer,
    sa.ForeignKey("users.id", ondelete="CASCADE")
)
4️⃣ Primary Key
sa.Column("id", sa.Integer, primary_key=True)

Hoặc:

sa.PrimaryKeyConstraint("id")
5️⃣ Unique Constraint
sa.UniqueConstraint("email")
6️⃣ Check Constraint
sa.CheckConstraint("age > 0", name="check_age_positive")
7️⃣ Index (khi define table)
sa.Index("ix_name", table.c.column_name)
8️⃣ Server Default
sa.Column(
    "created_at",
    sa.DateTime,
    server_default=sa.func.now()
)
9️⃣ func (SQL functions)
sa.func.now()
sa.func.count()
sa.func.sum()
III. Ví dụ hoàn chỉnh một migration
def upgrade():
    op.create_table(
        "users",
        sa.Column("id", sa.Integer, primary_key=True),
        sa.Column("email", sa.String(255), nullable=False, unique=True),
        sa.Column("age", sa.Integer),
        sa.Column("created_at", sa.DateTime, server_default=sa.func.now())
    )

def downgrade():
    op.drop_table("users")