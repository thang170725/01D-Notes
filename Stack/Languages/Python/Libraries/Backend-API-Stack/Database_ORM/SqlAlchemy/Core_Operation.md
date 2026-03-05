- [text()](#text)
- [.connect()](#connect)
- [.begin()](#begin)
- [insert](#insert)
  - [.values()](#values)
    - [Demo Insert 2 bảng trong 1 transaction (chuẩn)](#demo-insert-2-bảng-trong-1-transaction-chuẩn)
---
# text()
```bash
Để bao quanh query
```
**Syn**
```bash
from sqlalchemy import text

query = text("SELECT * FROM users")
```
# .connect()
```bash
- create_engine chưa thật sự mở kết nối ngay lập tức nó chỉ là factory nên cần dùng .connect()
- Mở một connection (kết nối vật lý) tới database.
**Syn**
```bash
from sqlalchemy import create_engine

engine = create_engine(
    url='mysql+pymysql://ai_user:ai123@localhost:3306/SmartRecipe'
)

with engine.connect() as conn:
    print('DB CONNECT OK')

Lúc này SQLAlchemy:
    1. Lấy 1 connection từ connection pool
    2. Mở kết nối thật tới DB
    3. Trả về object conn
    4. Sau khi thoát khỏi with, connection sẽ: Được trả về pool, Không bị leak
```
# .begin()
# insert
## .values()
**Ex**
```python
from sqlalchemy import insert

stmt = insert(districts).values(
    name="Ba Đình",
    city="Hà Nội"
)

with engine.begin() as conn:
    result = conn.execute(stmt)
```
### Demo Insert 2 bảng trong 1 transaction (chuẩn)
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
