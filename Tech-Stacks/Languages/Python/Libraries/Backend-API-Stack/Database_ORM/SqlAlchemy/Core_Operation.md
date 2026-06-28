- [text()](#text)
- [.connect()](#connect)
- [.begin()](#begin)
- [insert](#insert)
  - [.values()](#values)
    - [Demo Insert 2 bảng trong 1 transaction (chuẩn)](#demo-insert-2-bảng-trong-1-transaction-chuẩn)
- [Delete (Nhóm xóa)](#delete-nhóm-xóa)
  - [delete()](#delete)
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
# Delete (Nhóm xóa)
## delete()
**Ex1**
```python
from sqlalchemy import delete
from sqlalchemy.engine import Engine
from models import User

def delete_user_core(engine: Engine, user_id: int):
    with engine.begin() as conn:  # auto commit/rollback
        stmt = delete(User).where(User.id == user_id)

        result = conn.execute(stmt)

        return result.rowcount > 0
```
**Ex2**
```python
from sqlalchemy import delete

stmt = delete(listings).where(listings.c.id == 1)

with engine.begin() as conn:
    conn.execute(stmt)
```