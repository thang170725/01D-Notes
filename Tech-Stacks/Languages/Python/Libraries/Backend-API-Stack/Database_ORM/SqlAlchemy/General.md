- [Create](#create)
  - [create\_engine()](#create_engine)
  - [MetaData](#metadata)
    - [.create\_all()](#create_all)
  - [Table](#table)
    - [Column()](#column)
- [Search (Nhóm tìm kiếm để lấy dữ liệu)](#search-nhóm-tìm-kiếm-để-lấy-dữ-liệu)
  - [select() (Là các mới của query)](#select-là-các-mới-của-query)
  - [select\_from()](#select_from)
  - [.where() (lấy đôi tượng có điều kiện)](#where-lấy-đôi-tượng-có-điều-kiện)
  - [.join()](#join)
- [Display](#display)
  - [.columns](#columns)
  - [.name \& .type](#name--type)
  - [.label() (Dùng để đặt tên alias cho cột trong kết quả query)](#label-dùng-để-đặt-tên-alias-cho-cột-trong-kết-quả-query)
- [Insert](#insert)
  - [commit (Thực sự insert vào db. nếu lỗi -\> rollback)](#commit-thực-sự-insert-vào-db-nếu-lỗi---rollback)
- [Process (Các thao tác liên qua đến xử  lý)](#process-các-thao-tác-liên-qua-đến-xử--lý)
  - [.execute() (Gửi câu SQL xuống database để thực thi)](#execute-gửi-câu-sql-xuống-database-để-thực-thi)
    - [.all() (lấy tất cả các dòng dữ liệu)](#all-lấy-tất-cả-các-dòng-dữ-liệu)
    - [.fetchall() (Lấy mọi dòng có kết quả trùng)](#fetchall-lấy-mọi-dòng-có-kết-quả-trùng)
    - [.mappings()](#mappings)
    - [.first() (Lấy 1 dòng đầu tiên hoặc None)](#first-lấy-1-dòng-đầu-tiên-hoặc-none)
    - [scalars() (dùng để lấy ra giá trị đầu tiên của mỗi hàng (row) trong kết quả truy vấn)](#scalars-dùng-để-lấy-ra-giá-trị-đầu-tiên-của-mỗi-hàng-row-trong-kết-quả-truy-vấn)
    - [scalar\_one\_or\_none() (dùng để lấy một giá trị duy nhất từ kết quả query)](#scalar_one_or_none-dùng-để-lấy-một-giá-trị-duy-nhất-từ-kết-quả-query)
  - [.update()](#update)
  - [func](#func)
    - [.sum()](#sum)
    - [.count()](#count)
    - [.now()](#now)
    - [.coalesce() (Trả về giá trị đầu tiên khác NULL trong danh sách các giá trị)](#coalesce-trả-về-giá-trị-đầu-tiên-khác-null-trong-danh-sách-các-giá-trị)
    - [round()](#round)
    - [case()](#case)
- [ext](#ext)
  - [asyncio](#asyncio)
    - [create\_async\_engine (tạo Engine kết nối Database)](#create_async_engine-tạo-engine-kết-nối-database)
    - [async\_sessionmaker (tạo ra Session Factory)](#async_sessionmaker-tạo-ra-session-factory)
    - [AsyncSession](#asyncsession)
---
# Create
```bash
Nhóm khởi tạo và cấu hình
```
## create_engine()
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

- "dialect+driver://username:password@host:port/database"
    + dialect	: mysql, postgresql, sqlite, oracle
    + driver	: pymysql, psycopg2, cx_oracle
    + username	: root
    + password	: 123456
    + host	    : localhost
    + port	    : 3306, 5432
    + database	: test_db
- echo      : True là bất chế độ log in ra các cấu SQL
```
## MetaData
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
### .create_all()
```bash
Tạo bảng trong db.
```
**Syn**
```bash
metadata = MetaData()
metadata.create_all(engine)
```
## Table
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
### Column()
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
# Search (Nhóm tìm kiếm để lấy dữ liệu)
## select() (Là các mới của query)
```bash
Dùng được cho cả CORE + ORM
```
**Ex1: sử dụng select cho CORE**
```python
from sqlalchemy import select

stmt = select(districts) # print(stmt) chỉ in ra SQL string (query), Không có dữ liệu, Muốn xem dữ liệu → phải execute()

with engine.connect() as conn:
    rows = conn.execute(stmt).fetchall()

for row in rows:
    print(row.id, row.name, row.city)
```
**Ex2: select một vài cột**
```python
stmt = select(User.id, User.name)
result = session.execute(stmt)

result.all() # [(1, 'Alice'), (2, 'Bob')]
```
**Ex3: Muốn lấy dạng dict**
```python
result = session.execute(stmt).mappings().all()

[{'id': 1, 'name': 'Alice'}, {'id': 2, 'name': 'Bob'}]
```
## select_from()
## .where() (lấy đôi tượng có điều kiện)
```bash
- where() dùng được cho cả Core và ORM trong SQLAlchemy mới (2.0 style).
- Thực tế hiện nay:
    + where() = style chuẩn mới
    + filter() = style ORM cũ (session.query())
```
**Syn**
```bash
select(TableOrModel).where(condition, ...)
```
**Ex: Ví dụ về or**
```python
from sqlalchemy import or_

stmt = select(User).where(
    or_(
        User.age < 18,
        User.age > 60
    )
)
```
## .join()
**Ex**
```python
stmt = (
    select(
        listings.c.id,
        listings.c.price_total,
        districts.c.name,
        districts.c.city
    )
    .join(districts, listings.c.id_districts == districts.c.id)
)

with engine.connect() as conn:
    for row in conn.execute(stmt):
        print(row)
```
# Display
```bash
nhóm hàm để cung cấp thông tin (nhóm hiển thị thông tin).
```
## .columns
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
## .name & .type
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
## .label() (Dùng để đặt tên alias cho cột trong kết quả query)
```bash
Dùng được cho cả Core & ORM.
```
**Ex**
```python
Meal.name.label("name")
Category.name.label("category_name")

# Nó tương đương SQL: SELECT meal.name AS name, category.name AS category_name
```
# Insert
## commit (Thực sự insert vào db. nếu lỗi -> rollback)
```bash
Dùng cho cả CORE và ORM.
```
**Ex1: commit bằng ORM**
```python
def create_user(db: Session):
    user = User(name="Thang")

    db.add(user)      # thêm vào session
    db.commit()       # flush + commit

    return user

# Luồng xảy ra:
# add() → đưa object vào session
# commit(): tự gọi flush() → chạy INSERT rồi commit transaction
```
**Ex2: commit bằng Core (Connection.commit())**
```python
from sqlalchemy import insert

def create_user_core(conn):
    stmt = insert(users).values(name="Thang")

    conn.execute(stmt)  # chạy SQL
    conn.commit()       # commit transaction

# Cách viết Core chuẩn hơn (hay dùng)
from sqlalchemy import insert

def create_user_core(engine):
    with engine.begin() as conn:
        conn.execute(
            insert(users).values(name="Thang")
        )

#  engine.begin() sẽ:
# tự BEGIN
# tự COMMIT khi không lỗi
# tự ROLLBACK nếu lỗi
```
# Process (Các thao tác liên qua đến xử  lý)
## .execute() (Gửi câu SQL xuống database để thực thi)
```bash
execute() dùng được cho cả SQLAlchemy Core và ORM, nhưng cách dùng hơi khác tùy phiên bản SQLAlchemy.
```
**Ex1: SQLAlchemy Core**
```python
from sqlalchemy import create_engine, text

engine = create_engine(DATABASE_URL)

with engine.connect() as conn:
    result = conn.execute(text("SELECT * FROM users"))

    for row in result:
        print(row)

Hoặc:

from sqlalchemy import select

stmt = select(user_table)

with engine.connect() as conn:
    result = conn.execute(stmt)

# Ở đây execute() thuộc về Connection.
```
**SQLAlchemy ORM**
```python
from sqlalchemy import select

db = SessionLocal()

stmt = select(User)

result = db.execute(stmt)

print(result.all())

db.close()

# Ở đây execute() thuộc về Session.
```
### .all() (lấy tất cả các dòng dữ liệu)
```bash
Dùng được cho cả CORE & ORM.
```
### .fetchall() (Lấy mọi dòng có kết quả trùng)
```bash
dữ liệu trả về là list[obj]
```
**Ex**
```python
result = conn.execute(text("SELECT * FROM users"))
rows = result.fetchall()
print(rows) # [(1, 'Thang', 25), (2, 'An', 30)]

# Nhìn giống tuple, nhưng thực ra mỗi phần tử là: sqlalchemy.engine.row.Row
```
### .mappings()
```bash
SQLAlchemy sẽ trả về:

[
    {
        "plan_date": datetime.date(2025, 2, 17),
        "day_of_week": 2,
        "meal_type": "breakfast",
        "name": "Bánh mì trứng",
        "image_url": "https://...",
        "calories": 350
    },
    {
        "plan_date": datetime.date(2025, 2, 17),
        "day_of_week": 2,
        "meal_type": "lunch",
        "name": "Cơm gà",
        "image_url": "https://...",
        "calories": 600
    }
]

Kiểu dữ liệu thực tế
type(result)
# list

type(result[0])
# sqlalchemy.engine.row.RowMapping

Nhưng bạn có thể dùng như dict bình thường:
row["name"]
row["meal_type"]
```
### .first() (Lấy 1 dòng đầu tiên hoặc None)
### scalars() (dùng để lấy ra giá trị đầu tiên của mỗi hàng (row) trong kết quả truy vấn)
**Không dùng scalars()**
```python
stmt = select(User)

result = db.execute(stmt)

print(result.all())
# Kết quả:
# [
#     (<User id=1>,),
#     (<User id=2>,),
#     (<User id=3>,)
# ]

# execute() luôn trả về các Row. Mỗi Row giống như một tuple:

# nên muốn lấy User phải:
for row in result:
    user = row[0]
```
**Dùng scalars()**
```python
users = db.execute(select(User)).scalars().all()

print(users)
# Kết quả:
# [
#     <User id=1>,
#     <User id=2>,
#     <User id=3>
# ]

Nó tự lấy phần tử đầu tiên của mỗi row.
```
**Ex**
```python
stmt = select(User.username)

result = db.execute(stmt).all()
print(result)
# [
#     ('alice',),
#     ('bob',),
#     ('charlie',)
# ]

Nếu dùng:
names = db.execute(stmt).scalars().all()
print(names)
# ['alice', 'bob', 'charlie']
```
**Ex2: Nhưng phải cẩn thận. Nếu truy vấn nhiều cột**
```python
stmt = select(User.id, User.username)

result = db.execute(stmt).all()
# [(1, 'alice'), (2, 'bob')]

# Nếu dùng:
db.execute(stmt).scalars().all() # thì chỉ lấy cột đầu tiên:
# [1, 2]
# vì scalars() luôn lấy cột đầu tiên của mỗi row.
```
### scalar_one_or_none() (dùng để lấy một giá trị duy nhất từ kết quả query)
```bash
Nó có ý nghĩa như sau:
    "Tôi kỳ vọng query này trả về đúng 1 dòng hoặc không có dòng nào."
```
## .update()
**Ex**
```python
from sqlalchemy import update

stmt = (
    update(listings)
    .where(listings.c.id == 1)
    .values(price_total=58000000000)
)

with engine.begin() as conn:
    conn.execute(stmt)
```
## func
```bash
- func trong SQLAlchemy dùng để gọi SQL functions (hàm của database) 
    + COUNT()
    + SUM()
    + NOW()
    + MAX()
    + DATE_TRUNC()
    + hoặc bất kỳ function custom nào trong DB
```
### .sum()
```python
stmt = (
    select(
        Product.category_id,
        func.sum(Product.price).label("total")
    )
    .group_by(Product.category_id)
)
```
### .count()
**Ex: COUNT**
**SQL thuần**
```sql
SELECT COUNT(id) FROM users;
```
```python
from sqlalchemy import func

stmt = select(func.count(User.id))
```
### .now()
```bash
dùng để gọi hàm NOW() của database
```
**Ex: Lấy thời gian hiện tại từ DB**
```python
from sqlalchemy import create_engine, select, func
from sqlalchemy.orm import Session

engine = create_engine("sqlite:///test.db")

with Session(engine) as session:
    stmt = select(func.now())
    result = session.execute(stmt).scalar()
    print(result)

# 2026-03-01 10:42:15
```
### .coalesce() (Trả về giá trị đầu tiên khác NULL trong danh sách các giá trị)
**Syn**
```bash
from sqlalchemy import func

func.coalesce(column, 0)
```
**Ex**
```sql
stmt = select(
    func.coalesce(User.nickname, "Anonymous")
)
```
### round()
```python
from sqlalchemy import func

stmt = select(
    Product.name,
    func.round(Product.price, 2).label("price")
)

# SELECT
#     product.name,
#     ROUND(product.price, 2) AS price
# FROM product;
```
### case()
**Ex**
```python
from sqlalchemy import case

stmt = select(
    Student.name,
    case(
        (Student.score >= 8, "Giỏi"),
        (Student.score >= 5, "Đạt"),
        else_="Trượt"
    ).label("rank")
)
```
# ext
## asyncio
### create_async_engine (tạo Engine kết nối Database)
**Syn**
```bash
engine = create_async_engine(
    url,
    echo=False
)

- url: # url = "postgresql+asyncpg://..." hoặc url = "mysql+aiomysql://..."
- echo:
    True: SQL được sinh ra tiện cho debug
```
### async_sessionmaker (tạo ra Session Factory)
**Syn**
```bash
from sqlalchemy.ext.asyncio import async_sessionmaker

SessionLocal = async_sessionmaker(
    bind=engine
)
```
### AsyncSession 