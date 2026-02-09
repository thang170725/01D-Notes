- [create\_engine()](#create_engine)
- [MetaData](#metadata)
  - [.create\_all()](#create_all)
- [Column()](#column)
- [Integer \& String \& DateTime](#integer--string--datetime)
- [Table](#table)
  - [So sánh giữa có và không có declarative\_base](#so-sánh-giữa-có-và-không-có-declarative_base)
- [columns](#columns)
- [name \& type](#name--type)
---
# create_engine()
```bash
- Để tạo hoặc kết nối database.
- create_engine kHÔNG kết nối DB ngay, mà chỉ kết nối khi có query đầu tiên.
```
**Syn**
```bash
from sqlalchemy import create_engine

engine = create_engine(
    "dialect+driver://username:password@host:port/database", # nếu chưa có thì tự động tạo db
    pool_recycle=,
    echo=
)

- dialect	mysql, postgresql, sqlite, oracle
- driver	pymysql, psycopg2, cx_oracle
- username	root
- password	123456
- host	    localhost
- port	    3306, 5432
- database	test_db
- echo      : True là bất chế độ log in ra các cấu SQL
```
# MetaData
```bash
- MetaData chứa toàn bộ thông tin schema của database trong SQLAlchemy Core.
- MetaData KHÔNG kết nối DB
- MetaData KHÔNG chứa dữ liệu. Nó chỉ ghi nhớ cấu trúc của các bảng.
- Nếu KHÔNG có MetaData thì sao?
    + Không làm được quan hệ giữa các bảng
```
**Syn**
```bash
from sqlalchemy import MetaData

metadata = MetaData()
```
## .create_all()
```bash
Tạo bảng trong db.
```
**Syn**
```bash
metadata = MetaData()
metadata.create_all(engine)
```
# Column()
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
# Integer & String & DateTime
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

**declarative_base**
## So sánh giữa có và không có declarative_base
**Không có declarative_base**
```python
class User:
    __tablename__ = "users"

# SQLAlchemy sẽ coi đây là class Python bình thường
```
**Có declarative_base**
```bash
backend/
├── base.py
├── user.py
```
**base.py**
```python
from sqlalchemy.orm import declarative_base

Base = declarative_base()
```
**user.py**
```python
from sqlalchemy import Column, Integer, String
from backend.db.base import Base

class User(Base):
    __tablename__ = "users"

    id = Column(Integer, primary_key=True)
    username = Column(String(50))
    password = Column(String(255))

# User class  <=>  users table
```
# columns
**Ex**
```python
from sqlalchemy import Table, MetaData

def load_table(engine, table_name: str):
    metadata = MetaData()
    return Table(table_name, metadata, autoload_with=engine)

if __name__ == '__main__':
    from backend.python_service.app.core.db import create_engine_dynamic
    engine = create_engine_dynamic({
        "driver": "mysql+pymysql",
        "user": "ai_user",
        "password": "ai123",
        "host": "localhost",
        "port": 3306,
        "database": "house_price_project"
    })
    
    table = load_table(engine, table_name='listings')
    print(table.columns)

# ReadOnlyColumnCollection(listings.id, listings.id_districts, listings.price_total, listings.price_m2, listings.area, listings.location_lat, listings.location_long, listings.dist_to_center, listings.property_type, listings.legal_status, listings.bedrooms, listings.bathrooms, listings.floors, listings.orientation, listings.frontage_width, listings.alley_width, listings.source_url, listings.posted_date, listings.scraped_date, listings.market_trend_idx)
```

# name & type
```python
from sqlalchemy import Table, MetaData

def load_table(engine, table_name: str):
    metadata = MetaData()
    return Table(table_name, metadata, autoload_with=engine)

if __name__ == '__main__':
    from backend.python_service.app.core.db import create_engine_dynamic
    engine = create_engine_dynamic({
        "driver": "mysql+pymysql",
        "user": "ai_user",
        "password": "ai123",
        "host": "localhost",
        "port": 3306,
        "database": "house_price_project"
    })
    
    table = load_table(engine, table_name='listings')
    for col in table.columns:
        print(col.name, col.type)

# id INTEGER
# id_districts INTEGER
# price_total DECIMAL(15, 0)
# price_m2 DECIMAL(15, 2)
# area DECIMAL(7, 2)
# location_lat FLOAT
# location_long FLOAT
# dist_to_center FLOAT
# property_type VARCHAR(30)
# legal_status VARCHAR(50)
# bedrooms TINYINT
# bathrooms TINYINT
# floors TINYINT
# orientation VARCHAR(20)
# frontage_width FLOAT
# alley_width FLOAT
# source_url VARCHAR(500)
# posted_date DATE
# scraped_date DATETIME
# market_trend_idx FLOAT
```