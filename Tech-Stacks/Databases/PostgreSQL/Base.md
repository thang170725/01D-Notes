+ [<<Back](../Base.md)

- [PostgreSQL Introduction](#postgresql-introduction)
- [Database](#database)
  - [CREATE DATABASE (tạo database)](#create-database-tạo-database)
  - [DROP DATABASE (xóa database)](#drop-database-xóa-database)
  - [ALTER DATABASE ... rename to ... (sửa tên database)](#alter-database--rename-to--sửa-tên-database)
- [Schema](#schema)
  - [information\_schema (PostgreSQL có một hệ thống các bảng đặc biệt gọi là Information Schema. Nó chứa thông tin về chính database của bạn)](#information_schema-postgresql-có-một-hệ-thống-các-bảng-đặc-biệt-gọi-là-information-schema-nó-chứa-thông-tin-về-chính-database-của-bạn)
    - [.tables (dùng để xem thông tin về các bảng trong database)](#tables-dùng-để-xem-thông-tin-về-các-bảng-trong-database)
      - [table\_name (Đây là column của information\_schema.tables)](#table_name-đây-là-column-của-information_schematables)
      - [table\_schema (là một column của information\_schema.tables)](#table_schema-là-một-column-của-information_schematables)
    - [.column (xem thông tin về cột của các bảng trong)](#column-xem-thông-tin-về-cột-của-các-bảng-trong)
  - [Ask](#ask)
    - [MySQL, SQL Server có schema không](#mysql-sql-server-có-schema-không)
    - [Vậy public là gì?](#vậy-public-là-gì)
    - [Tại sao lại cần Schema?](#tại-sao-lại-cần-schema)
- [Table](#table)
  - [CREATE TABLE (Tạo bảng)](#create-table-tạo-bảng)
- [Data](#data)
  - [Data types](#data-types)
  - [INSERT INTO ... VALUES ... (Thêm dữ liệu)](#insert-into--values--thêm-dữ-liệu)
  - [SELECT (đọc dữ liệu)](#select-đọc-dữ-liệu)
  - [WHERE (Lọc dữ liệu)](#where-lọc-dữ-liệu)
  - [ORDER BY (Sắp xếp)](#order-by-sắp-xếp)
  - [LIMIT (Giới hạn số record)](#limit-giới-hạn-số-record)
  - [OFFSET (Bỏ qua một số record)](#offset-bỏ-qua-một-số-record)
  - [DISTINCT (Loại bỏ giá trị trùng)](#distinct-loại-bỏ-giá-trị-trùng)
  - [UPDATE (Cập nhật dữ liệu)](#update-cập-nhật-dữ-liệu)
  - [DELETE (Xóa record)](#delete-xóa-record)
  - [COUNT (Đếm record)](#count-đếm-record)
  - [SUM (Tính tổng)](#sum-tính-tổng)
  - [AVG (Tính trung bình)](#avg-tính-trung-bình)
  - [MIN / MAX](#min--max)
  - [GROUP BY (Nhóm dữ liệu)](#group-by-nhóm-dữ-liệu)
  - [HAVING (Lọc sau GROUP BY)](#having-lọc-sau-group-by)
  - [JOIN (Đây là phần cực kỳ quan trọng khi làm backend)](#join-đây-là-phần-cực-kỳ-quan-trọng-khi-làm-backend)
  - [LEFT JOIN (Lấy tất cả users, kể cả user chưa có order)](#left-join-lấy-tất-cả-users-kể-cả-user-chưa-có-order)
  - [RIGHT JOIN (Ngược lại LEFT JOIN)](#right-join-ngược-lại-left-join)
  - [FULL OUTER JOIN (Lấy tất cả record của cả hai bảng)](#full-outer-join-lấy-tất-cả-record-của-cả-hai-bảng)
  - [CROSS JOIN (Cartesian product)](#cross-join-cartesian-product)
  - [Subquery (Query bên trong query)](#subquery-query-bên-trong-query)
  - [EXISTS (Kiểm tra có tồn tại record hay không)](#exists-kiểm-tra-có-tồn-tại-record-hay-không)
  - [ALTER TABLE ... add column ... (Thêm column)](#alter-table--add-column--thêm-column)
  - [alter table ... drop column ... (Xóa column)](#alter-table--drop-column--xóa-column)
  - [alter table ... rename column ... (Đổi tên column)](#alter-table--rename-column--đổi-tên-column)
  - [alter table ... rename to ... (Đổi tên table)](#alter-table--rename-to--đổi-tên-table)
  - [alter table ... alter column ... (Đổi kiểu dữ liệu)](#alter-table--alter-column--đổi-kiểu-dữ-liệu)
  - [alter table ... add constraint ... (Thêm constraint)](#alter-table--add-constraint--thêm-constraint)
  - [Index (Index giúp tăng tốc query)](#index-index-giúp-tăng-tốc-query)
  - [UNIQUE INDEX](#unique-index)
  - [View](#view)
  - [Sequence](#sequence)
  - [SERIAL](#serial)
  - [Transaction](#transaction)
  - [SAVEPOINT (Tạo điểm rollback trung gian)](#savepoint-tạo-điểm-rollback-trung-gian)
  - [CASE (Điều kiện trong query)](#case-điều-kiện-trong-query)
  - [COALESCE (Lấy giá trị đầu tiên khác NULL)](#coalesce-lấy-giá-trị-đầu-tiên-khác-null)
  - [NULLIF (Nếu hai giá trị bằng nhau thì trả về NULL)](#nullif-nếu-hai-giá-trị-bằng-nhau-thì-trả-về-null)
  - [concat](#concat)
  - [lower](#lower)
  - [upper](#upper)
  - [length](#length)
  - [NOW()](#now)
  - [CURRENT\_DATE;](#current_date)
  - [CURRENT\_TIME;](#current_time)
  - [generated ... as identity (Column này để PostgreSQL tự sinh giá trị)](#generated--as-identity-column-này-để-postgresql-tự-sinh-giá-trị)
- [Function](#function)
  - [CREATE FUNCTION (tạo một function)](#create-function-tạo-một-function)
  - [REPLACE (thay thế)](#replace-thay-thế)
  - [LANGUAGE](#language)
  - [AS $$ ... $$](#as---)
  - [BEGIN ... END (là block code)](#begin--end-là-block-code)
  - [Trigger (là một cơ chế để database tự động thực hiện một hành động khi một sự kiện xảy ra trên table)](#trigger-là-một-cơ-chế-để-database-tự-động-thực-hiện-một-hành-động-khi-một-sự-kiện-xảy-ra-trên-table)
    - [BEFORE và AFTER](#before-và-after)
    - [OLD và NEW](#old-và-new)
  - [Tại sao trigger function phải RETURN NEW?](#tại-sao-trigger-function-phải-return-new)
  - [Xem cấu trúc cột của 1 bảng](#xem-cấu-trúc-cột-của-1-bảng)
---
# PostgreSQL Introduction
# Database
## CREATE DATABASE (tạo database)
**Syn**
```bash
CREATE DATABASE database_name;
```
**Ex**
```sql
CREATE DATABASE shop_db;
```
## DROP DATABASE (xóa database)
**Syn**
```bash
DROP DATABASE database_name;
```
**Ex**
```sql
DROP DATABASE shop_db;
```
## ALTER DATABASE ... rename to ... (sửa tên database)
```bash
ALTER DATABASE database_name
RENAME TO new_name;
```
**Ex**
```sql
ALTER DATABASE shop_db RENAME TO ecommerce_db;
```
# Schema
```bash
Bạn có thể hình dung:
    Database
       └── Schema
            └── Table
-> schema giống như một cái folder để phân loại table trong database.

Database Schema là gì?

Schema là cấu trúc hiện tại của database.

Ví dụ PostgreSQL hiện tại có:

database: document_db


table: documents


+----+-------------+
| id | OCR_DOC_ID  |
+----+-------------+
| 1  | ABC001      |
| 2  | ABC002      |
+----+-------------+

Cấu trúc của bảng:

documents
├── id          INTEGER
└── OCR_DOC_ID  VARCHAR

Đây chính là database schema hiện tại.

Nó mô tả:

Có những table nào?
Table có những column nào?
Kiểu dữ liệu là gì?
Primary key là gì?
Foreign key là gì?
Index nào tồn tại?
Constraint nào tồn tại?

Ví dụ:

CREATE TABLE documents (
    id INTEGER PRIMARY KEY,
    OCR_DOC_ID VARCHAR
);

Đây là SQL tạo ra schema.
```
## information_schema (PostgreSQL có một hệ thống các bảng đặc biệt gọi là Information Schema. Nó chứa thông tin về chính database của bạn)
**Ex**
```bash
test
├── users
├── orders
├── products
└── logs

PostgreSQL cần lưu metadata kiểu:
    - Có những schema nào?
    - Có những table nào?
    - Table nào có column gì?
    - Column nào có datatype gì?
    - User nào có quyền gì?
    - ...
-> Bạn có thể truy vấn những thông tin đó thông qua information_schema.
```
### .tables (dùng để xem thông tin về các bảng trong database)
**Ex**
```sql
SELECT * FROM information_schema.tables;

-- Nó sẽ trả về rất nhiều column.
-- Một số column quan trọng:
-- table_catalog
-- table_schema
-- table_name
-- table_type
-- ...
```
#### table_name (Đây là column của information_schema.tables)
#### table_schema (là một column của information_schema.tables)
**Ex**
```sql
SELECT table_name
FROM information_schema.tables
WHERE table_schema = 'test';

-- Có thể tưởng tượng PostgreSQL làm:
-- information_schema.tables
-- ┌──────────────┬─────────────┐
-- │ table_schema │ table_name  │
-- ├──────────────┼─────────────┤
-- │ public       │ users       │
-- │ public       │ orders      │
-- │ test         │ products    │
-- │ test         │ logs        │
-- └──────────────┴─────────────┘
--   ↓
-- WHERE table_schema = 'test'
--   ↓
-- ┌──────────────┬─────────────┐
-- │ table_schema │ table_name  │
-- ├──────────────┼─────────────┤
-- │ test         │ products    │
-- │ test         │ logs        │
-- └──────────────┴─────────────┘
--   ↓
--    SELECT table_name
--   ↓
-- products
-- logs
```
### .column (xem thông tin về cột của các bảng trong)
**Ex: xem kiểu dữ liệu của các field trong tất cả table thuộc một schema PostgreSQL**
```sql
SELECT
    table_name,
    column_name,
    data_type
FROM information_schema.columns
WHERE table_schema = 'ten_schema'
ORDER BY table_name, ordinal_position;
```
## Ask
### MySQL, SQL Server có schema không
**MySQL**
```bash
MySQL làm cho chuyện này hơi "ẩn" đi.
    Bạn thường thấy:
        MySQL
        └── Database
            ├── users
            ├── orders
            └── products
-> Nhưng trong MySQL, database và schema gần như là synonym.
```
**SQL Server**
```bash
SQL Server thực ra cũng có schema, chỉ là có thể bạn chưa để ý.
    Ví dụ mặc định:
        Database
        └── dbo
            ├── Users
            ├── Orders
            └── Products
    -> dbo chính là schema.

    Khi bạn viết:
        SELECT * FROM dbo.Users;
            thì:
                - dbo     = schema
                - Users   = table
```
### Vậy public là gì?
```bash
Đây cũng là thứ bạn sẽ gặp rất nhiều trong PostgreSQL.

Một database PostgreSQL mới thường có schema mặc định tên: public

Nếu bạn tạo:
    CREATE TABLE users (
        id INT
    );
-> thì mặc định nó thường nằm ở: public.users
```
### Tại sao lại cần Schema?
```bash
Đây là điểm schema thực sự hữu ích.
    Bạn có thể có:
        insmart_medical_ocr
        │
        ├── production
        │   └── HOADON_TYPE2
        │
        ├── test
        │   └── HOADON_TYPE2
        │
        └── dev
            └── HOADON_TYPE2
    -> Cùng tên HOADON_TYPE2 nhưng nằm ở 3 schema khác nhau, hoàn toàn được.

    Bạn truy cập:
        - SELECT * FROM production.HOADON_TYPE2;
        - SELECT * FROM test.HOADON_TYPE2;
        - SELECT * FROM dev.HOADON_TYPE2;
    -> Đây chính là lý do schema rất tiện để tách dev / test / production mà không nhất thiết phải tạo 3 database riêng.
```
# Table
## CREATE TABLE (Tạo bảng)
**Ex**
```sql
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    email VARCHAR(255),
    age INTEGER
);
```
Xem danh sách table

Trong psql:

\dt

Xem cả schema:

\dt *.*
Xem cấu trúc table
\d users

Chi tiết hơn:

\d+ users
DROP TABLE

Xóa table:

DROP TABLE users;

Nếu table không tồn tại thì lỗi.

Có thể dùng:

DROP TABLE IF EXISTS users;
TRUNCATE

Xóa toàn bộ dữ liệu, nhưng giữ cấu trúc table.

TRUNCATE TABLE users;

Khác:

DROP TABLE users;

DROP → xóa cả table.

TRUNCATE → giữ table, chỉ xóa data.
# Data
## Data types
```bash
- Integer               : số nguyên
- DECIMAL(10,2)         :
- VARCHAR(100)          : chuỗi, Unicode được hỗ trợ mặc định, nên VARCHAR lưu tiếng Việt bình thường
- TEXT                  : chuỗi dài
- BOOLEAN       
- DATE                  : ngày
- TIMESTAMP             : thời gian (ngày giờ phút giây)
- CURRENT_TIMESTAMP     : thời gian hiện tại
- JSONB         : json
- UUID          : 
- Primary Key   : Xác định duy nhất một record.
- Foreign Key   : Tạo quan hệ giữa hai bảng.
- NOT NULL      : Không cho phép NULL.
- UNIQUE        : Không cho phép giá trị trùng.
- DEFAULT       : Giá trị mặc định.
- CHECK         : Kiểm tra điều kiện. (age INTEGER CHECK (age >= 18))
- IN            : Kiểm tra thuộc một tập giá trị.
- BETWEEN       : Khoảng giá trị.
- LIKE          : Tìm kiếm pattern.
- ILIKE         : PostgreSQL có ILIKE để tìm kiếm không phân biệt hoa thường.
- IS NULL       : Kiểm tra NULL.
```
**Các toán tử so sánh**
```bash
- =       : bằng
- <>      : khác
- !=      : khác
- >       : lớn hơn
- <       : nhỏ hơn
- >=      : lớn hơn hoặc bằng
- <=      : nhỏ hơn hoặc bằng
```
## INSERT INTO ... VALUES ... (Thêm dữ liệu)
**Ex: insert 1 record**
```sql
INSERT INTO users (name, email, age)
VALUES ('John', 'john@gmail.com', 25);
```
**Ex2: Thêm nhiều record**
```sql
INSERT INTO users (name, email, age)
VALUES
    ('John', 'john@gmail.com', 25),
    ('Alice', 'alice@gmail.com', 30),
    ('Bob', 'bob@gmail.com', 22);
```
## SELECT (đọc dữ liệu)
**Ex**
```sql
SELECT * FROM users;
```
**Ex2: Chọn một số column**
```sql
SELECT name, email
FROM users;
```
**Ex3: Đặt alias**
```sql
SELECT name AS username
FROM users;
```
## WHERE (Lọc dữ liệu)
**Ex**
```sql
SELECT * FROM users WHERE age > 18;
```
**Ex2: Nhiều điều kiện**
```sql
SELECT * FROM users WHERE age >= 18 AND is_active = TRUE;
```
## ORDER BY (Sắp xếp)
**Ex1: Tăng dần**
```sql
SELECT * FROM users ORDER BY age ASC;
```
**Ex2: Giảm dần**
```sql
SELECT * FROM users ORDER BY age DESC;
```
## LIMIT (Giới hạn số record)
**Ex**
```sql
SELECT *
FROM users
LIMIT 10;
```
## OFFSET (Bỏ qua một số record)
**Ex**
```sql
SELECT * FROM users LIMIT 10 OFFSET 20; -- Có thể hiểu: OFFSET 20 → bỏ 20 record đầu
```
##  DISTINCT (Loại bỏ giá trị trùng)
```sql
SELECT DISTINCT age FROM users;
```
## UPDATE (Cập nhật dữ liệu)
```sql
UPDATE users
SET age = 30
WHERE id = 1;
```
**Ex2: Nhiều column**
```sql
UPDATE users
SET
    name = 'John Doe',
    age = 30
WHERE id = 1;
```
## DELETE (Xóa record)
```sql
DELETE FROM users
WHERE id = 1;
```
## COUNT (Đếm record)
```sql
SELECT COUNT(*)
FROM users;
```
**Ex2: Đặt alias**
```sql
SELECT COUNT(*) AS total_users
FROM users;
```
## SUM (Tính tổng)
## AVG (Tính trung bình)
**Ex**
```sql
SELECT AVG(age)
FROM users;
```
## MIN / MAX
```sql
SELECT MIN(age)
FROM users;
```
```sql
SELECT MAX(age)
FROM users;
```
## GROUP BY (Nhóm dữ liệu)
**Ex**
```sql
SELECT age, COUNT(*)
FROM users
GROUP BY age;

-- age | count
-- ----+------
-- 20  | 5
-- 21  | 8
-- 22  | 3
```
## HAVING (Lọc sau GROUP BY)
**Ex**
```sql
SELECT age, COUNT(*)
FROM users
GROUP BY age
HAVING COUNT(*) > 5;
```
## JOIN (Đây là phần cực kỳ quan trọng khi làm backend)
**Ex**
```bash
Giả sử:
    users
    id | name

orders
    id | user_id | amount
    INNER JOIN

Chỉ lấy những record có quan hệ ở cả hai bảng.
```
```sql
SELECT
    users.name,
    orders.amount
FROM users
INNER JOIN orders
    ON users.id = orders.user_id;
```
## LEFT JOIN (Lấy tất cả users, kể cả user chưa có order)
```sql
SELECT
    users.name,
    orders.amount
FROM users
LEFT JOIN orders
    ON users.id = orders.user_id;

-- Đây là một trong những JOIN bạn sẽ dùng rất thường xuyên.
```
## RIGHT JOIN (Ngược lại LEFT JOIN)
```sql
SELECT
    users.name,
    orders.amount
FROM users
RIGHT JOIN orders
    ON users.id = orders.user_id;

-- Thực tế thường có thể viết lại thành LEFT JOIN để dễ đọc hơn.
```
## FULL OUTER JOIN (Lấy tất cả record của cả hai bảng)
```sql
SELECT *
FROM users
FULL OUTER JOIN orders
    ON users.id = orders.user_id;
```
## CROSS JOIN (Cartesian product)
```sql
SELECT *
FROM users
CROSS JOIN products;
```
## Subquery (Query bên trong query)
```sql
SELECT *
FROM users
WHERE age > (
    SELECT AVG(age)
    FROM users
);

-- Nghĩa là: lấy những user có tuổi lớn hơn tuổi trung bình.
```
## EXISTS (Kiểm tra có tồn tại record hay không)
```sql
SELECT *
FROM users u
WHERE EXISTS (
    SELECT 1
    FROM orders o
    WHERE o.user_id = u.id
);

-- Thường rất hữu ích với query phức tạp.
```
## ALTER TABLE ... add column ... (Thêm column)
```sql
ALTER TABLE users
ADD COLUMN phone VARCHAR(20);
```
## alter table ... drop column ... (Xóa column)
```sql
ALTER TABLE users
DROP COLUMN phone;
```
## alter table ... rename column ... (Đổi tên column)
```sql
ALTER TABLE users
RENAME COLUMN name TO full_name;
```
## alter table ... rename to ... (Đổi tên table)
```sql
ALTER TABLE users
RENAME TO customers;
```
## alter table ... alter column ... (Đổi kiểu dữ liệu)
```sql
ALTER TABLE users
ALTER COLUMN age TYPE BIGINT;
```
## alter table ... add constraint ... (Thêm constraint)
```sql
ALTER TABLE users
ADD CONSTRAINT unique_email UNIQUE (email);
```
## Index (Index giúp tăng tốc query)
## UNIQUE INDEX
## View
## Sequence
## SERIAL
## Transaction
## SAVEPOINT (Tạo điểm rollback trung gian)
## CASE (Điều kiện trong query)
```sql
SELECT
    name,
    age,
    CASE
        WHEN age >= 18 THEN 'adult'
        ELSE 'child'
    END AS category
FROM users;
```
## COALESCE (Lấy giá trị đầu tiên khác NULL)
## NULLIF (Nếu hai giá trị bằng nhau thì trả về NULL)
## concat
## lower
## upper
## length
## NOW()
## CURRENT_DATE;
## CURRENT_TIME;
## generated ... as identity (Column này để PostgreSQL tự sinh giá trị)
**Ex**
```sql
CREATE TABLE users (
    id INT GENERATED ALWAYS AS IDENTITY
);
```
# Function 
## CREATE FUNCTION (tạo một function)
**Ex**
```sql
CREATE FUNCTION test.update_update_date() -- có nghĩa: Tạo một function tên update_update_date trong schema test.
```
## REPLACE (thay thế)
**Ex**
```sql
CREATE OR REPLACE FUNCTION 
-- Có nghĩa: 
-- Nếu function chưa tồn tại → tạo mới.
-- Nếu đã tồn tại → thay nội dung function cũ bằng nội dung mới.
```
## LANGUAGE
**Ex**
```sql
LANGUAGE plpgsql 
-- nói cho PostgreSQL:
-- Code bên trong function được viết bằng ngôn ngữ PL/pgSQL.
-- PostgreSQL có nhiều cách viết function, nhưng plpgsql là cái bạn sẽ gặp rất thường xuyên.
```
## AS $$ ... $$
**Syn**
```bash
AS $$
BEGIN
    ...
END;
$$;

# có nghĩa: Phần code nằm giữa $$ và $$ chính là function body.
```
**Ex**
```sql
CREATE FUNCTION hello()
RETURNS text
LANGUAGE plpgsql
AS $$
BEGIN
    RETURN 'Hello';
END;
$$;

SELECT hello(); -- chạy hàm
```
## BEGIN ... END (là block code)
**Syn**
```bash
BEGIN
    code
END;
```
**Ex**
```sql
CREATE FUNCTION hello()
RETURNS text
LANGUAGE plpgsql
AS $$
BEGIN
    RETURN 'Hello';
END;
$$;
```
## Trigger (là một cơ chế để database tự động thực hiện một hành động khi một sự kiện xảy ra trên table)
```bash
Bạn có thể hiểu cực đơn giản:
    Trigger = "Nếu chuyện A xảy ra → tự động làm chuyện B."
```
**Ex1: Ví dụ đời thường**
```bash
Giả sử bạn có cửa tự động:
    Có người bước vào
          ↓
    Cảm biến phát hiện
          ↓
    Cửa tự động mở

Trong PostgreSQL:
    Có người UPDATE dữ liệu
          ↓
    Trigger phát hiện
          ↓
    Function tự động chạy
```
**Ex2**
```bash
Bạn có table:
    CREATE TABLE users (
        id SERIAL PRIMARY KEY,
        name TEXT,
        updated_at TIMESTAMP
    );

Bạn muốn: 
    - Mỗi lần users bị UPDATE thì updated_at tự động đổi thành thời gian hiện tại.
    - Nếu không có trigger, mỗi lần update bạn phải viết:
```
**Không có trigger**
```sql
UPDATE users
SET
    name = 'Thang',
    updated_at = CURRENT_TIMESTAMP
WHERE id = 1; 
-- Rất dễ quên updated_at.
```
**Có Trigger**
```bash
Bạn tạo trigger:
    UPDATE users
          ↓
    Trigger phát hiện
          ↓
    Tự động cập nhật updated_at

Sau đó application chỉ cần:
    UPDATE users
    SET name = 'Thang'
    WHERE id = 1;
-> Database tự động xử lý: name = 'Thang', updated_at = CURRENT_TIMESTAMP
```
**Trigger không phải Function**
```bash
Đây là chỗ người mới rất dễ nhầm. Hai cái có vai trò khác nhau:
    - Trigger -> Khi nào chạy?
    - Function -> Chạy cái gì?
```
**Trigger không cần application gọi**
```bash
Đây là điểm rất hay. Application Python:
    cursor.execute("""
        UPDATE users
        SET name = %s
        WHERE id = %s
    """, ("Nam", 1))

Python không cần biết có trigger.

Database tự:
    Python -> UPDATE -> PostgreSQL -> Trigger -> Function -> UPDATE_DATE = NOW() -> Đây là lý do trigger rất mạnh.
```
**Nhưng trigger cũng có mặt trái**
```bash
Không nên lạm dụng trigger. Vì application nhìn thấy:
    UPDATE users ...

    nhưng thực tế database có thể âm thầm làm:
        UPDATE users -> trigger 1 -> function -> INSERT audit -> trigger 2 -> ... -> Nếu có rất nhiều trigger, việc debug có thể trở nên khó.
```
### BEFORE và AFTER
### OLD và NEW
## Tại sao trigger function phải RETURN NEW?
```bash
NEW -> sửa NEW.updated_at -> RETURN NEW -> PostgreSQL sử dụng row mới này

Đặc biệt với: BEFORE UPDATE thì RETURN NEW cho PostgreSQL biết:
    "Đây là phiên bản row mà bạn nên tiếp tục xử lý."
```

11. Bây giờ đến phần quan trọng nhất: NEW

Function của bạn có:

NEW."UPDATE_DATE"

NEW là một record đặc biệt mà PostgreSQL cung cấp cho trigger function.

Đừng hiểu NEW là biến bạn tự tạo.

PostgreSQL tự đưa nó cho bạn.

Ví dụ table:

CREATE TABLE test.users (
    id integer,
    name text,
    "UPDATE_DATE" timestamp
);

Có row:

id | name  | UPDATE_DATE
---+-------+-------------------
1  | Thang | 2026-08-01

Khi chạy:

UPDATE test.users
SET name = 'Nam'
WHERE id = 1;

Trigger function có thể nhìn thấy row mới thông qua:

NEW

Nó đại diện cho:

row sau khi UPDATE
12. OLD là gì?

Ngoài NEW, trigger còn có:

OLD

Để hiểu:

OLD = row trước khi thay đổi


NEW = row sau khi thay đổi

Ví dụ:

Trước UPDATE:


OLD
id = 1
name = Thang


Sau UPDATE:


NEW
id = 1
name = Nam
13. NEW."UPDATE_DATE" nghĩa là gì?

Đây:

NEW."UPDATE_DATE"

có thể đọc:

Giá trị column UPDATE_DATE của row mới.

Giống Python:

new["UPDATE_DATE"]

hoặc object:

new.UPDATE_DATE
14. Dòng quan trọng nhất

Function của bạn:

NEW."UPDATE_DATE" = CURRENT_TIMESTAMP;

nghĩa là:

Gán thời gian hiện tại vào column UPDATE_DATE của row mới.

Ví dụ trước update:

id | name  | UPDATE_DATE
---+-------+-------------------
1  | Thang | 2026-08-01 10:00

Bạn chạy:

UPDATE test.users
SET name = 'Nam'
WHERE id = 1;

Trigger chạy:

NEW."UPDATE_DATE" = CURRENT_TIMESTAMP;

Kết quả:

id | name | UPDATE_DATE
---+------+-------------------
1  | Nam  | 2026-08-14 08:40

Bạn không cần tự:

UPDATE_DATE = ...

trong từng câu UPDATE nữa.

15. CURRENT_TIMESTAMP
CURRENT_TIMESTAMP

là thời điểm hiện tại của database/session.

Ví dụ:

SELECT CURRENT_TIMESTAMP;

Có thể ra:

2026-08-14 08:40:25.123+07
16. RETURN NEW

Đây là phần cực kỳ quan trọng với trigger BEFORE.

Function:

BEGIN
    NEW."UPDATE_DATE" = CURRENT_TIMESTAMP;
    RETURN NEW;
END;

Có nghĩa:

Nhận row mới
    ↓
Thay đổi UPDATE_DATE
    ↓
Trả row mới lại cho PostgreSQL

Tức:

NEW
 ↓
modify
 ↓
RETURN NEW
 ↓
PostgreSQL tiếp tục UPDATE
17. Tại sao phải RETURN NEW?

Vì đây là:

BEFORE UPDATE

Trigger chạy trước khi UPDATE thực sự được thực hiện.

PostgreSQL cho trigger function cơ hội:

"Hãy xem/chỉnh sửa row này trước khi tôi lưu nó."

Bạn chỉnh:

NEW."UPDATE_DATE"

xong phải:

RETURN NEW;

để nói:

"OK, dùng row này để UPDATE."

18. Bây giờ đến Trigger

Function mới chỉ là:

Một function

Nó chưa tự chạy.

Bạn cần Trigger:

CREATE TRIGGER ...

Trigger có nhiệm vụ:

Theo dõi một table và gọi function khi một event xảy ra.

Ví dụ:

UPDATE table
     ↓
Trigger phát hiện
     ↓
Gọi function
     ↓
Function sửa NEW.UPDATE_DATE
19. CREATE TRIGGER

Code:

CREATE TRIGGER trg_hoadon_type2_update_date

Tạo trigger có tên:

trg_hoadon_type2_update_date

Tên này do bạn tự đặt.

Ví dụ cũng có thể:

CREATE TRIGGER update_timestamp

Không có gì đặc biệt về tên trg_.

Người ta thường đặt prefix:

trg_

để nhìn vào biết đây là trigger.

20. BEFORE

Đoạn:

BEFORE UPDATE

nghĩa là:

Trigger chạy trước khi UPDATE được thực hiện.

Có:

BEFORE
AFTER
INSTEAD OF

Bạn sẽ gặp nhiều nhất:

BEFORE
AFTER

Ví dụ:

BEFORE UPDATE
UPDATE request
     ↓
TRIGGER
     ↓
UPDATE database

Còn:

AFTER UPDATE

là:

UPDATE database
     ↓
TRIGGER
21. UPDATE
BEFORE UPDATE

UPDATE là event kích hoạt trigger.

Các event phổ biến:

INSERT
UPDATE
DELETE
TRUNCATE

Ví dụ:

BEFORE INSERT

→ trước khi thêm row.

AFTER INSERT

→ sau khi thêm row.

BEFORE UPDATE

→ trước khi sửa row.

AFTER UPDATE

→ sau khi sửa row.

BEFORE DELETE

→ trước khi xóa row.

22. ON test."HOADON_TYPE2"
ON test."HOADON_TYPE2"

nghĩa là:

Trigger này được gắn vào table HOADON_TYPE2 trong schema test.

Cấu trúc:

test
 ↓
schema


"HOADON_TYPE2"
 ↓
table
23. Tại sao "HOADON_TYPE2" có dấu "?

Đây là một điểm SQL rất đáng học.

PostgreSQL phân biệt:

HOADON_TYPE2

và:

"HOADON_TYPE2"

PostgreSQL mặc định fold unquoted identifier thành lowercase.

Ví dụ:

CREATE TABLE Users (...);

thực tế PostgreSQL coi tên là:

users

Nhưng:

CREATE TABLE "Users" (...);

thì tên thực sự là:

Users

và phải viết đúng:

SELECT *
FROM "Users";

Tương tự:

"HOADON_TYPE2"

giữ nguyên chữ hoa.

Đây là lý do database schema cũ thường xuất hiện rất nhiều:

"HOADON_TYPE2"
"UPDATE_DATE"
24. FOR EACH ROW

Đây là phần rất quan trọng.

FOR EACH ROW

nghĩa là:

Trigger chạy một lần cho mỗi row bị ảnh hưởng.

Ví dụ:

UPDATE test.users
SET age = age + 1;

Có:

1,000 rows

thì:

FOR EACH ROW

→ function chạy 1,000 lần.

25. FOR EACH STATEMENT

Ngược lại:

FOR EACH STATEMENT

thì:

UPDATE users
SET age = age + 1;

dù update:

1 row

hay:

1,000,000 rows

trigger chỉ chạy:

1 lần

Đây là khác biệt cực kỳ quan trọng:

FOR EACH ROW
    1 row → 1 lần
    100 rows → 100 lần


FOR EACH STATEMENT
    1 row → 1 lần
    100 rows → 1 lần
26. EXECUTE FUNCTION

Cuối cùng:

EXECUTE FUNCTION test.update_update_date();

nghĩa là:

Khi trigger được kích hoạt, hãy gọi function test.update_update_date().

Đây là lúc hai phần kết nối với nhau:

FUNCTION
test.update_update_date()
        ↑
        │
EXECUTE FUNCTION
        │
        ↑
TRIGGER
trg_hoadon_type2_update_date
27. Đọc toàn bộ code bằng tiếng Việt

Code của bạn:

CREATE OR REPLACE FUNCTION test.update_update_date()
RETURNS TRIGGER
LANGUAGE plpgsql
AS $$
BEGIN
    NEW."UPDATE_DATE" = CURRENT_TIMESTAMP;
    RETURN NEW;
END;
$$;

Đọc thành:

Tạo hoặc thay thế một trigger function tên update_update_date trong schema test.

Function này trả về TRIGGER và được viết bằng PL/pgSQL.

Khi được gọi, lấy row mới (NEW), cập nhật column UPDATE_DATE thành thời gian hiện tại, rồi trả row mới lại.

Sau đó:

CREATE TRIGGER trg_hoadon_type2_update_date
BEFORE UPDATE ON test."HOADON_TYPE2"
FOR EACH ROW
EXECUTE FUNCTION test.update_update_date();

Đọc thành:

Tạo trigger trg_hoadon_type2_update_date.

Trigger chạy trước mỗi UPDATE trên table test."HOADON_TYPE2".

Với mỗi row bị update, gọi function test.update_update_date().

28. Toàn bộ flow

Đây là thứ bạn nên nhớ nhất:

User/Application
       │
       │
       ▼
UPDATE test."HOADON_TYPE2"
       │
       ▼
PostgreSQL phát hiện:
BEFORE UPDATE
       │
       ▼
Trigger
trg_hoadon_type2_update_date
       │
       ▼
EXECUTE FUNCTION
test.update_update_date()
       │
       ▼
NEW
       │
       ▼
NEW."UPDATE_DATE"
       │
       ▼
CURRENT_TIMESTAMP
       │
       ▼
RETURN NEW
       │
       ▼
PostgreSQL thực hiện UPDATE
29. Tự viết một Trigger từ đầu

Bây giờ thử một ví dụ đơn giản hơn.

Giả sử:

CREATE TABLE test.users (
    id SERIAL PRIMARY KEY,
    name TEXT,
    updated_at TIMESTAMP
);

Bạn muốn:

Mỗi khi user được update → tự động cập nhật updated_at.

Bước 1 — Function
CREATE OR REPLACE FUNCTION test.set_updated_at()
RETURNS TRIGGER
LANGUAGE plpgsql
AS $$
BEGIN
    NEW.updated_at = CURRENT_TIMESTAMP;


    RETURN NEW;
END;
$$;
Bước 2 — Trigger
CREATE TRIGGER trg_users_updated_at
BEFORE UPDATE ON test.users
FOR EACH ROW
EXECUTE FUNCTION test.set_updated_at();
Bước 3 — Test

Insert:

INSERT INTO test.users(name)
VALUES ('Thang');

Sau đó:

UPDATE test.users
SET name = 'Duc Thang'
WHERE id = 1;

Trigger tự động:

updated_at = CURRENT_TIMESTAMP
30. Trigger có thể làm nhiều thứ hơn

Ví dụ:

Tự động update timestamp
UPDATE
 ↓
updated_at = NOW()
Kiểm tra dữ liệu
INSERT
 ↓
kiểm tra
 ↓
nếu sai → RAISE EXCEPTION
Audit

Ví dụ:

users
   ↓
UPDATE
   ↓
trigger
   ↓
user_audit

Lưu:

ai sửa?
sửa lúc nào?
giá trị cũ?
giá trị mới?
Tự động tạo dữ liệu liên quan
INSERT order
      ↓
trigger
      ↓
insert order_log
31. OLD + NEW rất quan trọng

Ví dụ audit:

CREATE OR REPLACE FUNCTION test.audit_user()
RETURNS TRIGGER
LANGUAGE plpgsql
AS $$
BEGIN


    INSERT INTO test.user_audit(
        old_name,
        new_name
    )
    VALUES (
        OLD.name,
        NEW.name
    );


    RETURN NEW;


END;
$$;

Nếu:

OLD.name = 'Thang'
NEW.name = 'Duc'

thì audit lưu:

old_name | new_name
---------+---------
Thang    | Duc

Bạn sẽ gặp OLD và NEW rất nhiều khi làm Trigger.

32. OLD và NEW phụ thuộc event

Đây là bảng rất đáng nhớ:

Event	OLD	NEW
INSERT	❌	✅
UPDATE	✅	✅
DELETE	✅	❌

Tại sao?

INSERT

Chưa có row cũ:

OLD ❌
NEW ✅
UPDATE

Có cả trước và sau:

OLD ✅
NEW ✅
DELETE

Có row trước khi xóa nhưng không còn row mới:

OLD ✅
NEW ❌
33. Một lỗi người mới rất hay mắc

Đừng viết:

BEFORE DELETE
...
NEW.name

Vì DELETE không có NEW.

Phải:

OLD.name

Tương tự INSERT không có OLD.

34. IF trong Trigger Function

Sau khi hiểu function cơ bản, bạn có thể viết:

CREATE OR REPLACE FUNCTION test.check_age()
RETURNS TRIGGER
LANGUAGE plpgsql
AS $$
BEGIN


    IF NEW.age < 0 THEN
        RAISE EXCEPTION 'Age cannot be negative';
    END IF;


    RETURN NEW;


END;
$$;

Đây chính là lúc PL/pgSQL bắt đầu giống programming language:

IF
THEN
ELSE
LOOP
FOR
DECLARE
EXCEPTION
35. Lộ trình học mình khuyên bạn

Đừng nhảy ngay vào những trigger phức tạp.

Học theo thứ tự:

1. SQL cơ bản
   ↓
2. SELECT / INSERT / UPDATE / DELETE
   ↓
3. Schema / Table / Column
   ↓
4. information_schema
   ↓
5. PostgreSQL Function
   ↓
6. PL/pgSQL
   ↓
7. BEGIN / END
   ↓
8. Variables
   ↓
9. IF / ELSE
   ↓
10. LOOP / FOR
   ↓
11. RETURN
   ↓
12. Trigger
   ↓
13. OLD / NEW
   ↓
14. BEFORE / AFTER
   ↓
15. FOR EACH ROW
   ↓
16. Trigger Function
   ↓
17. Transaction / Exception
   ↓
18. Audit Trigger

Quan trọng nhất: Function và Trigger không phải hai thứ hoàn toàn độc lập. Trong đoạn code bạn đưa, Function chứa logic, còn Trigger quyết định khi nào logic đó được chạy.

FUNCTION = "Làm gì?"
TRIGGER  = "Khi nào làm?"

Đây là cách đơn giản nhất để bạn bắt đầu đọc những SQL script lớn của PostgreSQL.

Tiếp tục khám phá:

Thực hành trigger cập nhật updated_at
Viết trigger kiểm tra dữ liệu bằng IF
```
# Practices
## Xem cấu trúc bảng của một schema
```sql
SELECT table_name
FROM information_schema.tables
WHERE table_schema = 'test';
```
## Xem cấu trúc cột của 1 bảng
SELECT column_name
FROM information_schema.columns
WHERE table_schema = 'test'
  AND table_name = 'users';