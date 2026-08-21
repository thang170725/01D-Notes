- [SQLAlchemy Model](#sqlalchemy-model)
- [Create \& Config (tạo \& cấu hình hệ thống)](#create--config-tạo--cấu-hình-hệ-thống)
  - [Connection Setup (Thiết lập kết nối)](#connection-setup-thiết-lập-kết-nối)
    - [sessionmaker() (Tạo "nhà máy" sinh ra các session, nơi bạn làm việc với db bằng ORM)](#sessionmaker-tạo-nhà-máy-sinh-ra-các-session-nơi-bạn-làm-việc-với-db-bằng-orm)
    - [Session (Nó giống như “phiên làm việc” giữa app và database)](#session-nó-giống-như-phiên-làm-việc-giữa-app-và-database)
      - [refresh() (Load lại dữ liệu từ DB vào object)](#refresh-load-lại-dữ-liệu-từ-db-vào-object)
  - [Model Definition](#model-definition)
    - [declarative\_base() (tạo một base class để các model class kế thừa - cách cũ)](#declarative_base-tạo-một-base-class-để-các-model-class-kế-thừa---cách-cũ)
    - [DeclarativeBase (tạo một base class để các model class kế thừa - cách mới)](#declarativebase-tạo-một-base-class-để-các-model-class-kế-thừa---cách-mới)
      - [__table\_args__ (là một thuộc tính đặc biệt của SQLAlchemy ORM, dùng để cấu hình các tùy chọn ở mức bảng (table-level), thay vì mức column)](#table_args-là-một-thuộc-tính-đặc-biệt-của-sqlalchemy-orm-dùng-để-cấu-hình-các-tùy-chọn-ở-mức-bảng-table-level-thay-vì-mức-column)
    - [Constraints (Ràng buộc)](#constraints-ràng-buộc)
    - [Index (chỉ mục)](#index-chỉ-mục)
    - [UniqueConstraint](#uniqueconstraint)
    - [Index](#index)
    - [ForeignKey (dùng để tạo ràng buộc khóa ngoại (foreign key constraint) giữa các bảng)](#foreignkey-dùng-để-tạo-ràng-buộc-khóa-ngoại-foreign-key-constraint-giữa-các-bảng)
    - [ForeignKeyConstraint](#foreignkeyconstraint)
    - [relationship (lấy dữ liệu liên quan giữa các bảng bằng object, không cần viết JOIN)](#relationship-lấy-dữ-liệu-liên-quan-giữa-các-bảng-bằng-object-không-cần-viết-join)
  - [Data Types](#data-types)
    - [Integer](#integer)
    - [String \& DateTime](#string--datetime)
    - [Enum](#enum)
    - [Date \& TIMESTAMP](#date--timestamp)
    - [JSON](#json)
    - [Identity (dùng để tạo cột ID tự động tăng ở phía PostgreSQL)](#identity-dùng-để-tạo-cột-id-tự-động-tăng-ở-phía-postgresql)
    - [Mapped (type annotation ORM)](#mapped-type-annotation-orm)
      - [mapped\_column() (Nó giống như Column() nhưng dành cho ORM mới)](#mapped_column-nó-giống-như-column-nhưng-dành-cho-orm-mới)
- [Search (tìm kiếm đôi tượng)](#search-tìm-kiếm-đôi-tượng)
  - [.query() (lấy ra đối tượng = select \* from ...)](#query-lấy-ra-đối-tượng--select--from-)
  - [.get()](#get)
- [Filtering (Bộ lọc)](#filtering-bộ-lọc)
  - [.filter() (Lọc theo điều kiện)](#filter-lọc-theo-điều-kiện)
    - [like()](#like)
    - [filter\_by() (lọc theo tên thuộc tính của model)](#filter_by-lọc-theo-tên-thuộc-tính-của-model)
  - [Logic Healers](#logic-healers)
- [sa](#sa)
- [Insert (thêm mới vào db)](#insert-thêm-mới-vào-db)
  - [.add() (đưa object vào session chưa ghi xuống db)](#add-đưa-object-vào-session-chưa-ghi-xuống-db)
- [add\_all()](#add_all)
- [Update (Nhóm cập nhật)](#update-nhóm-cập-nhật)
  - [.flush() (Dùng để đẩy các thay đổi từ bộ nhớ session xuống database nhưng chưa commit transaction)](#flush-dùng-để-đẩy-các-thay-đổi-từ-bộ-nhớ-session-xuống-database-nhưng-chưa-commit-transaction)
- [Delete (Nhóm xóa)](#delete-nhóm-xóa)
  - [Session.delete()](#sessiondelete)
---
# SQLAlchemy Model
**Ex**
```bash
class Document(Base):
    __tablename__ = "documents"

    id = Column(Integer, primary_key=True)
    OCR_DOC_ID = Column(String)
# Đây là SQLAlchemy Model. Nó là cách Python của bạn mô tả database/table.
# Có thể hiểu:
# SQLAlchemy Model
#   ↓
# "Database mà tôi mong muốn có cấu trúc như thế này"
```
# Create & Config (tạo & cấu hình hệ thống)
## Connection Setup (Thiết lập kết nối)
### sessionmaker() (Tạo "nhà máy" sinh ra các session, nơi bạn làm việc với db bằng ORM)
```bash
Không thể làm việc trực tiếp db bằng ORM nếu không có Session
```
**Syn**
```bash
from sqlalchemy.orm import sessionmaker

SessionLocal = sessionmaker(
    bind=engine,
    autocommit=False,
    autoflush=False,
)

- Input:
    + bind=engine	    : gắn session với DB
    + autocommit=False	: không tự commit
    + autoflush=False	: không tự đẩy dữ liệu
- Output: 
    + SessionLocal()	: tạo 1 session mới
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
### Session (Nó giống như “phiên làm việc” giữa app và database)
```bash
Bạn không thao tác trực tiếp với DB → Bạn thao tác qua Session

Dùng để:
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
#### refresh() (Load lại dữ liệu từ DB vào object)
```bash
Thuộc ORM không dùng cho CORE.

Mục đích:
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
### declarative_base() (tạo một base class để các model class kế thừa - cách cũ) 
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
### DeclarativeBase (tạo một base class để các model class kế thừa - cách mới) 
```bash
- Nó giúp:
    + Map class → table
    + Tự động quản lý metadata
    + Tạo schema bằng Base.metadata.create_all()
```
**Syn**
```bash
from sqlalchemy.orm import DeclarativeBase

class Base(DeclarativeBase):
    pass
```
#### __table_args__ (là một thuộc tính đặc biệt của SQLAlchemy ORM, dùng để cấu hình các tùy chọn ở mức bảng (table-level), thay vì mức column)
```bash
- Có thể chứa:
    + UniqueConstraint
    + Index
    + ForeignKeyConstraint
    + CheckConstraint
    + Engine options (MySQL, Postgres…)
```
**Ex**
```python
class User(Base):
    __tablename__ = "users"
    __table_args__ = {"schema": "test"} # Bảng users nằm trong schema test

    id = Column(Integer, primary_key=True)
    name = Column(String)

# SQLAlchemy sẽ hiểu tương đương với:
# CREATE TABLE test.users (
#     id INTEGER PRIMARY KEY,
#     name VARCHAR
# );
```
**Ex2: Tuple. Dùng khi muốn khai báo constraint / index / table option**
```python
class User(Base):
    __tablename__ = "users"


    __table_args__ = (
        UniqueConstraint("email"),
    )


    id = Column(Integer, primary_key=True)
    email = Column(String)

# SQL sẽ tương đương ý tưởng:
# CREATE TABLE users (
#     id INTEGER PRIMARY KEY,
#     email VARCHAR,
#     UNIQUE (email)
# );
```
**Ex3: Tuple + Dictionary. Đây là dạng rất quan trọng vì bạn có thể vừa khai báo constraint/index vừa cấu hình table**
```python
class User(Base):
    __tablename__ = "users"
    __table_args__ = (
        UniqueConstraint("email"),
        {"schema": "test"}
    )

    id = Column(Integer, primary_key=True)
    email = Column(String)
```
### Constraints (Ràng buộc)
### Index (chỉ mục)
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
### ForeignKey (dùng để tạo ràng buộc khóa ngoại (foreign key constraint) giữa các bảng)
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
### relationship (lấy dữ liệu liên quan giữa các bảng bằng object, không cần viết JOIN)
**Syn**
```bash
relationship("TenModel", back_populates="ten_field")

- Input
    + 'TenModel'        : tên class model liên kết, dạng str
    + back_populates    : tên field ở model bên kia, dùng để liên kết 2 chiều
    + lazy              : cách load data
    + cascade           : xóa dây chuyền
        - 'all, delete-orphan'  : 
        - 'save-update'         : Lưu/cập nhật object con khi lưu object cha
        - merge	                : Session.merge() thì object con cũng được merge
        - refresh-expire	    : Refresh hoặc expire object cha thì object con cũng vậy
        - expunge	            : Xóa object cha khỏi Session thì object con cũng bị xóa khỏi Session
        - delete	            : Xóa object cha thì object con cũng bị DELETE trong database
        - delete-orphan	        : Nếu object con không còn thuộc cha nào thì tự động DELETE
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
### Identity (dùng để tạo cột ID tự động tăng ở phía PostgreSQL)
```bash
Nó tương đương với ý tưởng:

id INTEGER GENERATED BY DEFAULT AS IDENTITY
1. Ví dụ đơn giản
from sqlalchemy import Integer, Identity
from sqlalchemy.orm import DeclarativeBase, Mapped, mapped_column




class Base(DeclarativeBase):
    pass




class User(Base):
    __tablename__ = "users"


    id: Mapped[int] = mapped_column(
        Integer,
        Identity(),
        primary_key=True,
    )


    name: Mapped[str]

Khi insert:

user = User(name="Thang")


session.add(user)
session.commit()

Bạn không cần tự truyền id:

User(name="Thang")

PostgreSQL tự tạo:

id = 1

Record tiếp theo:

id = 2
2. Vì sao cần Identity()?

Nếu bạn viết:

id: Mapped[int] = mapped_column(
    Integer,
    primary_key=True
)

SQLAlchemy/PostgreSQL cũng có thể cấu hình cơ chế sinh ID tùy dialect/version/config, nhưng Identity() làm cho ý định rất rõ:

Đây là một cột mà database chịu trách nhiệm generate giá trị.

Ví dụ:

id: Mapped[int] = mapped_column(
    Integer,
    Identity(),
    primary_key=True
)

Database sẽ đảm nhiệm việc sinh ID.

3. Có thể cấu hình Identity

Ví dụ:

id: Mapped[int] = mapped_column(
    Integer,
    Identity(
        start=1000,
        increment=1
    ),
    primary_key=True,
)

Khi đó:

1000
1001
1002
1003
...

SQL tương ứng về ý tưởng:

GENERATED BY DEFAULT AS IDENTITY
(START WITH 1000 INCREMENT BY 1)
4. Identity khác gì Sequence?

Đây là chỗ dễ nhầm.

Identity
id = mapped_column(
    Integer,
    Identity(),
    primary_key=True
)

Bạn nói với DB:

"DB tự quản lý việc generate ID cho column này."

Đây thường là lựa chọn mình khuyên dùng cho ID thông thường.

Sequence
from sqlalchemy import Sequence


id = mapped_column(
    Integer,
    Sequence("user_id_seq"),
    primary_key=True
)

Bạn tạo một sequence riêng:

user_id_seq

và dùng sequence đó để sinh ID.

Sequence hữu ích khi bạn cần kiểm soát sequence riêng hoặc có logic đặc biệt.

5. Một điểm rất quan trọng: Identity không phải UUID

Ví dụ:

id: Mapped[int] = mapped_column(
    Integer,
    Identity(),
    primary_key=True,
)

sẽ tạo:

1
2
3
4
5

Còn UUID:

id: Mapped[UUID] = mapped_column(
    UUID(as_uuid=True),
    primary_key=True,
    server_default=text("gen_random_uuid()")
)

sẽ tạo kiểu:

550e8400-e29b-41d4-a716-446655440000

Hai cách này phục vụ những mục đích khác nhau.

6. Với project Python + PostgreSQL của bạn

Nếu bạn có bảng kiểu:

documents
----------------
id
name
status
created_at

thì mình sẽ thường viết:

from datetime import datetime


from sqlalchemy import DateTime, Identity, Integer, String
from sqlalchemy.orm import DeclarativeBase, Mapped, mapped_column




class Base(DeclarativeBase):
    pass




class Document(Base):
    __tablename__ = "documents"


    id: Mapped[int] = mapped_column(
        Integer,
        Identity(),
        primary_key=True,
    )


    name: Mapped[str] = mapped_column(String(255))


    status: Mapped[str] = mapped_column(String(50))


    created_at: Mapped[datetime] = mapped_column(
        DateTime,
    )

Sau đó:

document = Document(
    name="abc.json",
    status="pending",
)


session.add(document)
session.commit()

Không cần:

document.id = 123

Sau commit, SQLAlchemy sẽ biết ID mà PostgreSQL vừa sinh:

print(document.id)

Ví dụ:

1
Tóm lại
Identity()
    ↓
PostgreSQL tự sinh ID
    ↓
Python không cần tự tạo ID
    ↓
SQLAlchemy lấy ID vừa sinh về object

Nếu bạn đang xây luồng DB bằng SQLAlchemy + PostgreSQL, mình khuyên bạn hiểu kỹ thêm 4 thứ ngay sau Identity: primary_key, server_default, default, và autoincrement. Đây là 4 thứ rất dễ bị nhầm khi thiết kế model.
```
### Mapped (type annotation ORM)
```bash
ORM mới (2.0) SQLAlchemy giới thiệu
    - Mapped
    - mapped_column
=> để hỗ trợ type hint.
```
**Syn**
```bash
id: Mapped[int] # thuộc tính id khi lấy ra sẽ có kiểu int.
```
#### mapped_column() (Nó giống như Column() nhưng dành cho ORM mới)
**Kiểu cũ**
```bash
id = Column(Integer, primary_key=True)
```
**Kiểu mới**
```bash
id: Mapped[int] = mapped_column(primary_key=True)
```
**Ex**
```python
from sqlalchemy.orm import DeclarativeBase
from sqlalchemy.orm import Mapped
from sqlalchemy.orm import mapped_column

class Base(DeclarativeBase):
    pass

class User(Base):
    __tablename__ = "users"

    id: Mapped[int] = mapped_column(primary_key=True)
    name: Mapped[str] = mapped_column(nullable=False)
    age: Mapped[int]
```
# Search (tìm kiếm đôi tượng)
## .query() (lấy ra đối tượng = select * from ...)
```bash
query chỉ dùng cho ORM không dùng cho Core.
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
## .get()
# Filtering (Bộ lọc)
## .filter() (Lọc theo điều kiện)
```bash
- filter có cần import không?
    + filter không cần import vì nó là phương thức của class
- filter thường dùng cho ORM. Đây là style ORM cũ. where được recommanded
```
**Syn**
```bash
query = session.query(User).filter(User.email == email)

- Output: Nó trả về một query/statement đã được thêm điều kiện lọc # WHERE username = 'admin'
```
**Syn2**
```bash
stmt = select(User).filter(User.email == email)
```
**Ex**
```python
class User(Base):
    __tablename__ = "users"

    id = Column(Integer, primary_key=True)
    username = Column(String)
    age = Column(Integer)

query = db.query(User).filter(User.username == "thang").first() # SELECT * FROM users WHERE username = 'thang' LIMIT 1;
query.first()
# user là object User
# Hoặc None
```
**Ex2**
Với SQLAlchemy 2.x

Nếu bạn đang dùng kiểu mới:

stmt = select(User).filter(User.email == email)

thì filter() trả về Select statement, chưa query DB.

Sau đó:

result = await session.execute(stmt)


user = result.scalar_one_or_none()

→ user mới là User hoặc None.
### like()
### filter_by() (lọc theo tên thuộc tính của model)
```bash
filter_by() là API của ORM, không dùng cho SQLAlchemy Core.
```
**Syn**
```bash
session.query(User).filter_by(name="Thắng") # SELECT *FROM usersWHERE name = 'Thắng';
```
**Ex1: tìm user theo tên**
```bash
user = session.query(User).filter_by(name="Thắng").first() # SELECT *FROM usersWHERE name = 'Thắng'LIMIT 1;
```
**Ex2: nhiều điều kiện**
```python
users = session.query(User).filter_by(
    name="Thắng",
    age=20
).all() # SELECT *FROM usersWHERE name='Thắng'AND age=20;
```
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
## .add() (đưa object vào session chưa ghi xuống db)
```bash
add chỉ dùng cho ORM, không dùng cho Core

Để insert data vào database bằng ORM của SQLAlchemy, bạn làm theo flow chuẩn: tạo model → tạo session → add → commit.
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
# add_all() 
```bash
Được sử dụng trong SQLAlchemy ORM, không phải Core.
```
**Ex**
```python
instances = [
    BangKeCPKB(...),
    BangKeCPKB(...),
    BangKeCPKB(...),
]


db.add_all(instances)
db.commit()

# Ở đây BangKeCPKB là ORM Model:
# class BangKeCPKB(Base):
#    __tablename__ = "BANGKE_CPKB"
```
# Update (Nhóm cập nhật)
## .flush() (Dùng để đẩy các thay đổi từ bộ nhớ session xuống database nhưng chưa commit transaction)
```bash
flush chỉ dùng cho ORM, không dùng cho Core.

Hiểu đơn giản:
    + Bạn thêm/sửa/xóa object trong Session
    + → flush() sẽ generate và execute SQL (INSERT/UPDATE/DELETE)
    + → nhưng chưa COMMIT, nên vẫn có thể rollback
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