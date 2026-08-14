- [Psycopg2 Introduction (Dùng để kết nối Python với CSDL PostgreSQL)](#psycopg2-introduction-dùng-để-kết-nối-python-với-csdl-postgresql)
- [Installation](#installation)
- [.connect() (tạo connection tới PostgreSQL)](#connect-tạo-connection-tới-postgresql)
  - [.cursor() (Sau khi có connection, bạn cần tạo cursor để thực thi SQL)](#cursor-sau-khi-có-connection-bạn-cần-tạo-cursor-để-thực-thi-sql)
    - [.execute() (Dùng để thực thi SQL)](#execute-dùng-để-thực-thi-sql)
  - [.fetchone() (Lấy một row từ kết quả query)](#fetchone-lấy-một-row-từ-kết-quả-query)
  - [.fetchmany() (Lấy nhiều row, nhưng giới hạn số lượng)](#fetchmany-lấy-nhiều-row-nhưng-giới-hạn-số-lượng)
  - [.fetchall() (Lấy toàn bộ kết quả còn lại)](#fetchall-lấy-toàn-bộ-kết-quả-còn-lại)
  - [.executemany() (Dùng khi muốn thực hiện cùng một SQL nhiều lần với nhiều parameters)](#executemany-dùng-khi-muốn-thực-hiện-cùng-một-sql-nhiều-lần-với-nhiều-parameters)
  - [.mogrify() (Cái này rất hữu ích để debug SQL + parameters)](#mogrify-cái-này-rất-hữu-ích-để-debug-sql--parameters)
  - [.rowcount (Property cho biết số row bị ảnh hưởng / returned tùy loại query)](#rowcount-property-cho-biết-số-row-bị-ảnh-hưởng--returned-tùy-loại-query)
  - [.description (Cái này cực hữu ích khi bạn muốn biết metadata của columns)](#description-cái-này-cực-hữu-ích-khi-bạn-muốn-biết-metadata-của-columns)
  - [.connection (Cursor có reference tới connection)](#connection-cursor-có-reference-tới-connection)
- [.commit() (Dùng để commit transaction)](#commit-dùng-để-commit-transaction)
- [.rollback() (Nếu transaction lỗi, dùng: conn.rollback())](#rollback-nếu-transaction-lỗi-dùng-connrollback)
- [.closed (0 nghĩa là đang mở. Khác 0 nghĩa là đã đóng)](#closed-0-nghĩa-là-đang-mở-khác-0-nghĩa-là-đã-đóng)
- [.status (Cho biết trạng thái connection)](#status-cho-biết-trạng-thái-connection)
- [.autocommit](#autocommit)
- [.close() (Đóng cursor/conn)](#close-đóng-cursorconn)
- [sql](#sql)
  - [.SQL()](#sql-1)
  - [.Literal()](#literal)
- [Transaction với with](#transaction-với-with)
- [extras (Cái này rất hữu ích nếu bạn làm API/service)](#extras-cái-này-rất-hữu-ích-nếu-bạn-làm-apiservice)
  - [RealDictCursor](#realdictcursor)
  - [.execute\_values() (Nếu cần insert nhiều records thì rất đáng học)](#execute_values-nếu-cần-insert-nhiều-records-thì-rất-đáng-học)
  - [.execute\_batch()](#execute_batch)
- [Context manager with conn (sử dụng trong code production)](#context-manager-with-conn-sử-dụng-trong-code-production)
- [Practices](#practices)
  - [Kết nối python với postgreSQL](#kết-nối-python-với-postgresql)
- [Ask](#ask)
  - [psycopg2 có mạnh hơn sqlalchemy không?](#psycopg2-có-mạnh-hơn-sqlalchemy-không)
  - [Demo một CRUD hoàn chỉnh](#demo-một-crud-hoàn-chỉnh)
---
# Psycopg2 Introduction (Dùng để kết nối Python với CSDL PostgreSQL)
# Installation
```bash
pip install psycopg2-binary
```
# .connect() (tạo connection tới PostgreSQL)
**Syn**
```bash
psycopg2.connect(
    dsn=None,
    connection_factory=None,
    cursor_factory=None,
    **kwargs
)

- Input
    + Các kwargs thường dùng:
        - host
        - port
        - database
        - user
        - password
- Output: Trả về một object psycopg2.extensions.connection
```
**Ex**
```python
conn = psycopg2.connect(
    host="49.213.89.136",
    port=5432,
    database="my_database",
    user="postgres",
    password="123456"
)

print(type(conn)) # <class 'psycopg2.extensions.connection'>
```
## .cursor() (Sau khi có connection, bạn cần tạo cursor để thực thi SQL)
**syn**
```bash
cursor = conn.cursor(
    cursor_factory=...
)

- Output: psycopg2.extensions.cursor
```
**Ex**
```python
conn = psycopg2.connect(...)
cursor = conn.cursor()


print(type(cursor))
```
### .execute() (Dùng để thực thi SQL)
**Syn**
```bash
cursor.execute(
    query, 
    vars=None
)
```
## .fetchone() (Lấy một row từ kết quả query)
**Syn**
```bash
row = cursor.fetchone()

- Input     : Không có
- Output    : tuple
```
**Ex**
```python
cursor.execute("SELECT id, name FROM users")


row = cursor.fetchone()


print(row) # (1, 'Thang')
```
## .fetchmany() (Lấy nhiều row, nhưng giới hạn số lượng)
**Syn**
```bash
cursor.fetchmany(size=None)
```
**Ex**
```python
cursor.execute("SELECT * FROM users")


rows = cursor.fetchmany(10)
# [
#     (1, "Thang"),
#     (2, "Nam"),
#     (3, "An"),
#     ...
# ]
```
## .fetchall() (Lấy toàn bộ kết quả còn lại)
**Syn**
```bash
rows = cursor.fetchall()

- Input     : Không có.
- Output    : list[tuple]
```
**Ex**
```python
cursor.execute("SELECT * FROM users")

rows = cursor.fetchall()
# [
#     (1, "Thang"),
#     (2, "Nam"),
#     (3, "An")
# ]
```
## .executemany() (Dùng khi muốn thực hiện cùng một SQL nhiều lần với nhiều parameters)
**Ex: insert nhiều user**
```python
users = [
    ("Thang", 25),
    ("Nam", 30),
    ("An", 22),
]

cursor.executemany(
    """
    INSERT INTO users(name, age)
    VALUES (%s, %s)
    """,
    users
)
```
## .mogrify() (Cái này rất hữu ích để debug SQL + parameters)
**Ex**
```python
query = """
SELECT *
FROM users
WHERE name = %s
AND age > %s
"""


sql = cursor.mogrify(
    query,
    ("Thang", 20)
)


print(sql) # b"\nSELECT *\nFROM users\nWHERE name = 'Thang'\nAND age > 20\n"
```
## .rowcount (Property cho biết số row bị ảnh hưởng / returned tùy loại query)
**Ex**
```python
cursor.execute(
    "DELETE FROM users WHERE age < %s",
    (18,)
)


print(cursor.rowcount) # 5, nghĩa là 5 rows bị delete.
```
## .description (Cái này cực hữu ích khi bạn muốn biết metadata của columns)
**Ex**
```python
cursor.execute(
    "SELECT id, name, age FROM users"
)


print(cursor.description) # Bạn sẽ nhận được metadata về các column.
```
## .connection (Cursor có reference tới connection)
# .commit() (Dùng để commit transaction)
**Syn**
```bash

- Input     : Không có.
- Output    : None
```
**Ex**
```python
cursor.execute(
    """
    INSERT INTO users(name)
    VALUES (%s)
    """,
    ("Thang",)
)

conn.commit() # Nếu không commit, transaction có thể không được lưu vĩnh viễn.
```
# .rollback() (Nếu transaction lỗi, dùng: conn.rollback())
**Ex**
```python
try:
    cursor.execute(...)
    conn.commit()


except Exception:
    conn.rollback()

# Nó đưa transaction về trạng thái trước transaction hiện tại.
```
# .closed (0 nghĩa là đang mở. Khác 0 nghĩa là đã đóng)
**Ex**
```python
if conn.closed == 0:
    print("Connection đang mở")
```
# .status (Cho biết trạng thái connection)
# .autocommit
# .close() (Đóng cursor/conn)
# sql
## .SQL()
## .Literal()
# Transaction với with
**Ex**
```python
with conn:
    with conn.cursor() as cursor:
        cursor.execute(...)
        cursor.execute(...)

# Nếu mọi thứ thành công → transaction được commit.
# Nếu exception → transaction được rollback.
```
**Ex2**
```python
try:
    with conn:
        with conn.cursor() as cursor:
            cursor.execute(
                "INSERT INTO users(name) VALUES (%s)",
                ("Thang",)
            )

            cursor.execute(
                "INSERT INTO users(name) VALUES (%s)",
                ("Nam",)
            )
except Exception as e:
    print(e)
```
# extras (Cái này rất hữu ích nếu bạn làm API/service)
## RealDictCursor
**Không dùng RealDicCursor**
```python
# Mặc định:
cursor.execute(
    "SELECT id, name FROM users"
)

row = cursor.fetchone()

print(row) # (1, "Thang")
```
**dùng RealDictCursor**
```python
# Muốn dạng dictionary
from psycopg2.extras import RealDictCursor

cursor = conn.cursor(
    cursor_factory=RealDictCursor
)

cursor.execute(
    "SELECT id, name FROM users"
)

row = cursor.fetchone()

print(row)
# {
#     "id": 1,
#     "name": "Thang"
# }
# Rất tiện khi trả JSON.
```
## .execute_values() (Nếu cần insert nhiều records thì rất đáng học)

from psycopg2.extras import execute_values


users = [
    ("Thang", 25),
    ("Nam", 30),
    ("An", 22),
]


execute_values(
    cursor,
    """
    INSERT INTO users(name, age)
    VALUES %s
    """,
    users
)


conn.commit()

Nó thường hiệu quả hơn việc:

executemany()

cho bulk insert.
## .execute_batch()

Một lựa chọn khác:

from psycopg2.extras import execute_batch


execute_batch(
    cursor,
    """
    INSERT INTO users(name, age)
    VALUES (%s, %s)
    """,
    users
)


conn.commit()
1.  copy_from() / copy_expert()

Nếu bạn cần import/export rất nhiều dữ liệu, PostgreSQL có cơ chế COPY.

Ví dụ:

cursor.copy_from(
    file_object,
    "users",
    sep=","
)

Hoặc:

cursor.copy_expert(
    "COPY users FROM STDIN WITH CSV",
    file_object
)

Đây là nhóm API bạn nên học nếu service của bạn sau này phải xử lý hàng triệu records.

30. connection.set_session()

Cho phép cấu hình session/transaction behavior.

Ví dụ:

conn.set_session(
    autocommit=False,
    readonly=False
)

Có thể cấu hình:

autocommit
readonly
deferrable
isolation_level
31. Isolation level

PostgreSQL hỗ trợ các isolation level.

Trong psycopg2 có thể dùng:

conn.set_isolation_level(...)

Ví dụ:

from psycopg2.extensions import ISOLATION_LEVEL_SERIALIZABLE


conn.set_isolation_level(
    ISOLATION_LEVEL_SERIALIZABLE
)

Các mức thường gặp:

READ COMMITTED
REPEATABLE READ
SERIALIZABLE

Đây là phần bạn nên học sau khi đã hiểu transaction.

32. Xử lý exception

psycopg2 có hệ thống exception khá đầy đủ.

Ví dụ:

import psycopg2


try:
    conn = psycopg2.connect(...)
except psycopg2.Error as e:
    print(e)

Một số exception thường gặp:

psycopg2.OperationalError
psycopg2.DatabaseError
psycopg2.IntegrityError
psycopg2.ProgrammingError
psycopg2.DataError

Ví dụ duplicate key:

try:
    cursor.execute(
        "INSERT INTO users(id, name) VALUES (%s, %s)",
        (1, "Thang")
    )


    conn.commit()


except psycopg2.IntegrityError:
    conn.rollback()
    print("Duplicate hoặc violation constraint")
Tổng hợp API bạn nên nhớ

Nếu học theo mức độ quan trọng:
# Context manager with conn (sử dụng trong code production)
**Ex**
```python
with psycopg2.connect(
    host="49.213.89.136",
    port=5432,
    database="my_database",
    user="postgres",
    password="xxx"
) as conn:
    with conn.cursor() as cursor:
        cursor.execute(
            "SELECT * FROM users"
        )

        rows = cursor.fetchall() # Ưu điểm là Python tự xử lý việc đóng resource.
```
# Practices
## Kết nối python với postgreSQL
```python
import psycopg2

conn = psycopg2.connect(
    host="49.213.89.136",
    port=3306,
    database="my_database",
    user="postgres",
    password="your_password",
)

print("Kết nối thành công!")

cursor = conn.cursor()
cursor.execute("SELECT version();")

print(cursor.fetchone())

cursor.close()
conn.close()
```
# Ask
## psycopg2 có mạnh hơn sqlalchemy không?
```bash
Không phải psycopg2 mạnh hơn SQLAlchemy. Hai cái này khác tầng.
    Bạn có thể hình dung:
        Python application
               ↓
           SQLAlchemy
               ↓
           psycopg2
               ↓
           PostgreSQL

psycopg2 là driver để Python nói chuyện trực tiếp với PostgreSQL.
    Bạn tự quản lý:
        - connection
        - cursor
        - SQL
        - transaction
        - commit / rollback
-> Nó khá thấp tầng và trực tiếp.

SQLAlchemy là một database toolkit + ORM.
    Nó thường vẫn cần một driver bên dưới.
```
## Demo một CRUD hoàn chỉnh
Một CRUD hoàn chỉnh

Nếu gom những thứ quan trọng nhất lại, một repository đơn giản có thể như sau:

import psycopg2
from psycopg2.extras import RealDictCursor




conn = psycopg2.connect(
    host="49.213.89.136",
    port=5432,
    database="my_database",
    user="postgres",
    password="xxx",
)




def get_user(user_id: int):
    with conn.cursor(cursor_factory=RealDictCursor) as cursor:
        cursor.execute(
            """
            SELECT id, name, age
            FROM users
            WHERE id = %s
            """,
            (user_id,)
        )


        return cursor.fetchone()




def get_users():
    with conn.cursor(cursor_factory=RealDictCursor) as cursor:
        cursor.execute(
            """
            SELECT id, name, age
            FROM users
            ORDER BY id
            """
        )


        return cursor.fetchall()




def create_user(name: str, age: int):
    with conn.cursor() as cursor:
        cursor.execute(
            """
            INSERT INTO users(name, age)
            VALUES (%s, %s)
            """,
            (name, age)
        )


    conn.commit()




def update_user(user_id: int, name: str):
    with conn.cursor() as cursor:
        cursor.execute(
            """
            UPDATE users
            SET name = %s
            WHERE id = %s
            """,
            (name, user_id)
        )


    conn.commit()




def delete_user(user_id: int):
    with conn.cursor() as cursor:
        cursor.execute(
            """
            DELETE FROM users
            WHERE id = %s
            """,
            (user_id,)
        )


    conn.commit()

Ở đây bạn có gần như toàn bộ flow cơ bản:

connect
   ↓
cursor
   ↓
execute
   ↓
fetch
   ↓
commit
   ↓
close
Nhưng có một thứ rất quan trọng với project của bạn

Nếu bạn đang xây database_manager_service, mình không khuyên bạn viết application bằng cách gọi psycopg2.connect() ở khắp nơi.

Nên tổ chức thành:

database_manager_service/
│
├── app/
│   ├── config/
│   │   └── settings.py
│   │
│   ├── database/
│   │   ├── connection.py
│   │   └── repository.py
│   │
│   ├── services/
│   │   └── user_service.py
│   │
│   └── main.py
│
└── .env

Sau đó:

Service
   ↓
Repository
   ↓
psycopg2
   ↓
PostgreSQL

Và nếu database manager của bạn sẽ có connection pool, nhiều worker, transaction phức tạp, CRUD nhiều bảng, lúc đó mình sẽ cân nhắc SQLAlchemy thay vì sử dụng psycopg2 trực tiếp.

Một điểm cuối: lúc trước bạn đưa 49.213.89.136:3306. Nếu đó thực sự là PostgreSQL thì port 3306 không vấn đề gì; nhưng 3306 thường là MySQL, còn PostgreSQL mặc định là 5432. Trước khi viết database.py, nên xác nhận server đó thực sự đang chạy PostgreSQL.

Tiếp tục đào sâu:

Viết repository psycopg2 an toàn
Giải thích connection pool psycopg2