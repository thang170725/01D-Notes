- [Create \& Config (tạo \& cấu hình hệ thống)](#create--config-tạo--cấu-hình-hệ-thống)
  - [Connection Setup](#connection-setup)
    - [sessionmaker()](#sessionmaker)
    - [Session](#session)
      - [refresh()](#refresh)
  - [Model Definition](#model-definition)
    - [declarative\_base() \& DeclarativeBase](#declarative_base--declarativebase)
    - [__table\_args__](#table_args)
  - [Constraints \& Index](#constraints--index)
    - [UniqueConstraint](#uniqueconstraint)
    - [Index](#index)
    - [ForeignKey](#foreignkey)
    - [ForeignKeyConstraint](#foreignkeyconstraint)
    - [relationship](#relationship)
  - [Data Types](#data-types)
    - [Integer](#integer)
    - [String \& DateTime](#string--datetime)
    - [Enum](#enum)
    - [Date \& TIMESTAMP](#date--timestamp)
    - [JSON](#json)
- [Search](#search)
  - [.query()](#query)
- [Filtering (Bộ lọc)](#filtering-bộ-lọc)
  - [.filter() (Lọc theo điều kiện)](#filter-lọc-theo-điều-kiện)
    - [like()](#like)
    - [filter\_by()](#filter_by)
  - [Logic Healers](#logic-healers)
- [sa](#sa)
- [Insert (thêm mới vào db)](#insert-thêm-mới-vào-db)
  - [.add()](#add)
- [Update (Nhóm cập nhật)](#update-nhóm-cập-nhật)
  - [.flush()](#flush)
- [Delete (Nhóm xóa)](#delete-nhóm-xóa)
  - [Session.delete()](#sessiondelete)
---
# Create & Config (tạo & cấu hình hệ thống)
## Connection Setup
```bash
Thiết lập kết nối
```
### sessionmaker()
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
### Session
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
#### refresh()
```bash
- Thuộc ORM không dùng cho CORE.
- Mục đích:
    + Load lại dữ liệu từ DB vào object
    + Đồng bộ state sau khi:
        - commit
        - trigger DB
        - update từ nơi khác
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
## Model Definition
```bash
Định nghĩa thực thể
```
### declarative_base() & DeclarativeBase
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
### __table_args__
```bash
- Đây là biến đặc biệt trong ORM model. Dùng để cấu hình thêm cho table ngoài các Column.
- Có thể chứa:
    + UniqueConstraint
    + Index
    + ForeignKeyConstraint
    + CheckConstraint
    + Engine options (MySQL, Postgres…)
```
## Constraints & Index
```bash
Ràng buộc và chỉ mục
```
### UniqueConstraint
**Syn**
```bash
from sqlalchemy import UniqueConstraint

UniqueConstraint(
    column_name1,
    column_name2,
    ...
    name="constraint_name"
)
```
### Index
**Syn**
```bash
from sqlalchemy import Index

Index(
    "index_name",
    column1,
    column2,
    ...
)
```
### ForeignKey 
```bash
dùng để tạo ràng buộc khóa ngoại (foreign key constraint) giữa các bảng.
```
**Syn**
```bash
ForeignKey("users.id", ondelete="CASCADE")

- ondelete:
    + CASCADE: xóa user toàn bộ con bị xóa theo
```
**Ex**
```python
from sqlalchemy import Column, Integer, ForeignKey

user_id = Column(Integer, ForeignKey("users.id"))
```
### ForeignKeyConstraint
```bash
Khi cần foreign key nhiều cột
```
**Syn**
```bash
from sqlalchemy import ForeignKeyConstraint

__table_args__ = (
    ForeignKeyConstraint(
        ["user_id", "week_start"],
        ["users.id", "users.week_start"]
    ),
)
```
### relationship
```bash
relationship giúp bạn lấy dữ liệu liên quan giữa các bảng bằng object, không cần viết JOIN
```
**Syn**
```bash
relationship("TenModel", back_populates="ten_field")

- Input
    + 'TenModel'        : tên class model liên kết, dạng str
    + back_populates    : tên field ở model bên kia, dùng để liên kết 2 chiều
    + lazy              : cách load data
    + cascade           : xóa dây chuyền
- Output: trả về dạng Object
```
**Ex**
```python
class User(Base):
    __tablename__ = "user"
    id = Column(Integer, primary_key=True)

    posts = relationship("Post", back_populates="user")

class Post(Base):
    __tablename__ = "post"
    id = Column(Integer, primary_key=True)
    user_id = Column(Integer, ForeignKey("user.id"))

    user = relationship("User", back_populates="posts")

post = db.query(Post).first()

print(post.user)       # 👉 object User
print(post.user.id)    # 👉 truy cập bình thường

user = db.query(User).first()

print(user.posts)  # 👉 list các Post
```
## Data Types
### Integer
### String & DateTime
### Enum
**Ex**
```python
Enum('sedentary', 'light', "moderate", name='activity_level_role')
```
### Date & TIMESTAMP
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
### JSON
# Search
```bash
- tìm kiếm đôi tượng
```
## .query()
```bash
Là select kiểu cũ, giờ đổi thành select() - select là chuẩn mới dùng cho cả CORE + ORM.
```
**Syn: query**
```bash
db.query(User) # SELECT * FROM users
```
**Ex: query full model**
```python
users = session.query(User).all() # [User(...), User(...)] → List object ORM
```
**Ex2: query vài cột**
```python
rows = session.query(User.id, User.name).all() # [(1, 'Alice'), (2, 'Bob')] → List tuple
```
# Filtering (Bộ lọc)
## .filter() (Lọc theo điều kiện)
```bash
- filter có cần import không?
    + filter không cần import vì nó là phương thức của class
- filter thường dùng cho ORM. Đây là style ORM cũ. where được recommanded
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
### like()
### filter_by()
## Logic Healers
# sa
```bash
- Dùng để gọi các hàm logic
- sa = alias của SQLAlchemy
```
**Ex: hoàn chỉnh một migration**
```python
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
```
# Insert (thêm mới vào db)
## .add()
```bash
- add       : đưa object vào session chưa ghi xuống db.
- Để insert data vào database bằng ORM của SQLAlchemy, bạn làm theo flow chuẩn: tạo model → tạo session → add → commit.
```
**Ex: insert vào db bằng ORM**
```python
# 1. Định nghĩa model (table)
from sqlalchemy import Column, Integer, String, create_engine
from sqlalchemy.orm import declarative_base

Base = declarative_base()

class User(Base):
    __tablename__ = "users"

    id = Column(Integer, primary_key=True)
    name = Column(String)
    age = Column(Integer)

# 2. Kết nối DB + tạo bảng
engine = create_engine("sqlite:///example.db", echo=True)
Base.metadata.create_all(engine)

# 3. Tạo session
from sqlalchemy.orm import sessionmaker

Session = sessionmaker(bind=engine)
session = Session()

# 4. Insert 1 record
new_user = User(name="Thang", age=22)

session.add(new_user)
session.commit()

#  Sau commit() thì data mới thực sự được ghi xuống DB.
```
**Ex2: Insert nhiều record**
```python
users = [
    User(name="A", age=20),
    User(name="B", age=25),
    User(name="C", age=30),
]

session.add_all(users)
session.commit()
```
# Update (Nhóm cập nhật)
## .flush() 
```bash
- Dùng để đẩy (sync) các thay đổi từ bộ nhớ (session) xuống database nhưng chưa commit transaction.
- Hiểu đơn giản:
    + Bạn thêm/sửa/xóa object trong Session
    + → flush() sẽ generate và execute SQL (INSERT/UPDATE/DELETE)
    + → nhưng chưa COMMIT, nên vẫn có thể rollback
- ORM (chủ yếu dùng ở đây)
```
**Ex1: cần lấy id ngay sau khi insert**
```python
user = User(name="Thang")
session.add(user)

session.flush()  # gửi INSERT xuống DB

print(user.id)  # lúc này đã có id

# Nếu không flush(), user.id có thể vẫn là None
```
**Ex2: Đảm bảo dữ liệu đã tồn tại trong DB trước khi query tiếp**
```python
session.add(user)
session.flush()

result = session.query(User).filter_by(name="Thang").first()

# Nếu không flush, query có thể không thấy dữ liệu mới
```
# Delete (Nhóm xóa)
## Session.delete()
```python
from sqlalchemy.orm import Session
from models import User

def delete_user_orm(db: Session, user_id: int):
    # 1. Lấy object
    user = db.get(User, user_id)

    if not user:
        return False

    # 2. Đánh dấu xóa
    db.delete(user)

    # 3. Commit (flush + delete + commit)
    db.commit()

    return True
```