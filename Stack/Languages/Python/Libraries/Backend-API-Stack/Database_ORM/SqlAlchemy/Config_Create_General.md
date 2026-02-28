- [Config \& Create](#config--create)
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
# Config & Create
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