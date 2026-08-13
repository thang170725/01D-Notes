+ [<<Back](../Base.md)

- [PostgreSQL Introduction](#postgresql-introduction)
- [Database](#database)
  - [CREATE DATABASE (tạo database)](#create-database-tạo-database)
  - [DROP DATABASE (xóa database)](#drop-database-xóa-database)
  - [ALTER DATABASE ... rename to ... (sửa tên database)](#alter-database--rename-to--sửa-tên-database)
- [Schema](#schema)
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
- [Practices](#practices)
  - [Xem cấu trúc bảng của một schema](#xem-cấu-trúc-bảng-của-một-schema)
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
Đúng, đây là chỗ PostgreSQL dễ làm người mới thấy hơi rối, vì MySQL/SQL Server dùng khái niệm này hơi khác nhau.

Hiểu đơn giản

Bạn có thể hình dung:

Database
   └── Schema
        └── Table

Trong trường hợp của bạn:

insmart_medical_ocr       ← Database
└── test                  ← Schema
    ├── test_permission_check
    └── HOADON_TYPE2

schema giống như một cái folder để phân loại table trong database.

So với MySQL

MySQL làm cho chuyện này hơi "ẩn" đi.

Bạn thường thấy:

MySQL
└── Database
    ├── users
    ├── orders
    └── products

Nhưng trong MySQL, database và schema gần như là synonym.

Ví dụ:

CREATE DATABASE shop;

USE shop;

CREATE TABLE users (...);

Bạn có cảm giác:

shop
└── users

Thực tế MySQL gọi DATABASE và SCHEMA gần như cùng một khái niệm.

SQL Server thì có schema

SQL Server thực ra cũng có schema, chỉ là có thể bạn chưa để ý.

Ví dụ mặc định:

Database
└── dbo
    ├── Users
    ├── Orders
    └── Products

dbo chính là schema.

Khi bạn viết:

SELECT *
FROM dbo.Users;

thì:

dbo     = schema
Users   = table

SQL Server có thể có:

Database
├── dbo
│   ├── Users
│   └── Orders
│
└── accounting
    ├── Invoices
    └── Payments
PostgreSQL cũng tương tự SQL Server

Database của bạn:

insmart_medical_ocr

bên trong:

Schemas
├── public
├── test
└── ...

Ví dụ:

insmart_medical_ocr
│
├── public
│   ├── users
│   └── orders
│
└── test
    ├── test_permission_check
    └── HOADON_TYPE2

Vì vậy khi bạn viết:

SELECT *
FROM test.HOADON_TYPE2;

thì PostgreSQL hiểu:

test       → schema
HOADON_TYPE2 → table
Vậy public là gì?

Đây cũng là thứ bạn sẽ gặp rất nhiều trong PostgreSQL.

Một database PostgreSQL mới thường có schema mặc định tên:

public

Nếu bạn tạo:

CREATE TABLE users (
    id INT
);

thì mặc định nó thường nằm ở:

public.users

Bạn có thể viết rõ:

CREATE TABLE public.users (
    id INT
);

Còn bảng của bạn nằm trong schema test, nên:

CREATE TABLE test.HOADON_TYPE2 (...);
Tại sao lại cần Schema?

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

Cùng tên HOADON_TYPE2 nhưng nằm ở 3 schema khác nhau, hoàn toàn được.

Bạn truy cập:

SELECT * FROM production.HOADON_TYPE2;

hoặc:

SELECT * FROM test.HOADON_TYPE2;

hoặc:

SELECT * FROM dev.HOADON_TYPE2;

Đây chính là lý do schema rất tiện để tách dev / test / production mà không nhất thiết phải tạo 3 database riêng.

Một cách nhớ rất dễ
Hệ quản trị	Cấu trúc thường thấy
MySQL	database → table
SQL Server	database → schema → table
PostgreSQL	database → schema → table

Nhưng MySQL cũng có khái niệm schema, chỉ là MySQL coi schema gần như đồng nghĩa với database, nên bạn ít thấy tầng riêng biệt đó.

Còn PostgreSQL:

Database
    ↓
Schema
    ↓
Table
    ↓
Column

Trong trường hợp của bạn:

insmart_medical_ocr
        ↓
       test
        ↓
HOADON_TYPE2

nên câu SQL CREATE TABLE test.HOADON_TYPE2 là hoàn toàn chuẩn.

Tiếp tục tìm hiểu PostgreSQL:

Phân biệt database, schema và table
Kiểm tra schema test và bảng HOADON_TYPE2
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
# Practices
## Xem cấu trúc bảng của một schema
```sql
SELECT table_name
FROM information_schema.tables
WHERE table_schema = 'test';
```