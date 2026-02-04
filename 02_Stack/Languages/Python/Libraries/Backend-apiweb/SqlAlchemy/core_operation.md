- [create\_engine() \& .connect()](#create_engine--connect)
- [insert](#insert)
  - [Demo Insert district](#demo-insert-district)
- [Demo Insert listing (FK)](#demo-insert-listing-fk)
- [Demo Insert 2 bảng trong 1 transaction (chuẩn)](#demo-insert-2-bảng-trong-1-transaction-chuẩn)
---
# create_engine() & .connect()
```bash
- Để kết nối database.
- create_engine() KHÔNG kết nối DB ngay, mà chỉ kết nối khi có query đầu tiên.
```
**Syn**
```bash
from sqlalchemy import create_engine

engine = create_engine(
    "dialect+driver://username:password@host:port/database",
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
**Ex**
```python
from sqlalchemy import create_engine

engine = create_engine(
    url='mysql+pymysql://ai_user:ai123@localhost:3306/SmartRecipe'
)

with engine.connect() as conn:
        print('DB CONNECT OK')
```
# insert
## Demo Insert district
```python
from sqlalchemy import insert

stmt = insert(districts).values(
    name="Ba Đình",
    city="Hà Nội"
)

with engine.begin() as conn:
    result = conn.execute(stmt)
    district_id = result.inserted_primary_key[0]

Tương đương LAST_INSERT_ID()
```

# Demo Insert listing (FK)
```python
stmt = insert(listings).values(
    id_districts=district_id,
    price_total=56000000000,
    area=96,
    property_type="nha_mat_pho"
)

with engine.begin() as conn:
    conn.execute(stmt)
```

# Demo Insert 2 bảng trong 1 transaction (chuẩn)
```bash
with engine.begin() as conn:
    result = conn.execute(
        insert(districts).values(name="Ba Đình", city="Hà Nội")
    )
    district_id = result.inserted_primary_key[0]

    conn.execute(
        insert(listings).values(
            id_districts=district_id,
            price_total=56000000000,
            area=96
        )
    )
```
SELECT – đọc dữ liệu
5.1 Select đơn giản
from sqlalchemy import select

stmt = select(districts)

with engine.connect() as conn:
    rows = conn.execute(stmt).fetchall()

for row in rows:
    print(row.id, row.name, row.city)

5.2 WHERE
stmt = select(districts).where(
    districts.c.name == "Ba Đình"
)

5.3 JOIN (rất quan trọng)
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

6️⃣ UPDATE
from sqlalchemy import update

stmt = (
    update(listings)
    .where(listings.c.id == 1)
    .values(price_total=58000000000)
)

with engine.begin() as conn:
    conn.execute(stmt)

7️⃣ DELETE
from sqlalchemy import delete

stmt = delete(listings).where(listings.c.id == 1)

with engine.begin() as conn:
    conn.execute(stmt)

8️⃣ SELECT + PAGINATION (crawler / API)
stmt = (
    select(listings)
    .order_by(listings.c.id.desc())
    .limit(20)
    .offset(0)
)

9️⃣ Dùng raw SQL khi cần (rất thực tế)
from sqlalchemy import text

stmt = text("""
SELECT l.id, l.price_total, d.name, d.city
FROM listings l
JOIN districts d ON l.id_districts = d.id
WHERE l.price_total > :price
""")

with engine.connect() as conn:
    result = conn.execute(stmt, {"price": 50000000000})
