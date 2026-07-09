- [Cách tạo database mariadb trong Linux](#cách-tạo-database-mariadb-trong-linux)
  - [Dùng terminal](#dùng-terminal)
- [Reset khóa kiểu int tự tăng về 1](#reset-khóa-kiểu-int-tự-tăng-về-1)
---
# Cách tạo database mariadb trong Linux
## Dùng terminal
**Step 1: truy cập vào maridb**
```bash
mariadb -u root -p | sudo mariadb # sau đó nhập mật khẩu root để truy cập

# thang@PhatToNhuLai:~$ sudo mariadb -u root -p
# Enter password: 
# Welcome to the MariaDB monitor.  Commands end with ; or \g.
# Your MariaDB connection id is 36
# Server version: 10.11.13-MariaDB-0ubuntu0.24.04.1 Ubuntu 24.04

# Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

# Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

# MariaDB [(none)]> 
```
**Step 2: tạo database - Ví dụ tạo database tên demo_db**
```bash
create database demo_db  # Tạo một database
    CHARACTER SET utf8mb4
    COLLATE utf8mb4_unicode_ci; # Như vậy mặc định schema demo_db sẽ dùng utf8mb4 + utf8mb4_unicode_ci

# kiểm tra
# SHOW DATABASES;
```
**Step 3: tạo user**
```bash
# Ví dụ
#     Username: demo_user
#     Password: 123456

CREATE USER 'demo_user'@'localhost' IDENTIFIED BY '123456';

# Nếu muốn user có thể đăng nhập từ máy khác
CREATE USER 'demo_user'@'%' IDENTIFIED BY '123456';
```
**Step 4: cấp quyền**
```bash
1. GRANT ALL PRIVILEGES ON demo_db.* TO 'demo_user'@'localhost'; # hoặc GRANT ALL PRIVILEGES ON demo_db.* TO 'demo_user'@'%';
2. FLUSH PRIVILEGES;
```
**Step 5: chọn database**
```bash
use demo_db;
```
**Step 6: tạo bảng test**
```bash
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```
**Step 7: insert dữ liệu**
```bash
INSERT INTO users(name,email)
VALUES
('Alice','alice@gmail.com'),
('Bob','bob@gmail.com');
```
**Step 8: kiểm tra**
```bash
SELECT * FROM users;
# +----+-------+-----------------+---------------------+
# | id | name  | email           | created_at          |
# +----+-------+-----------------+---------------------+
# | 1  | Alice | alice@gmail.com | ...                 |
# | 2  | Bob   | bob@gmail.com   | ...                 |
# +----+-------+-----------------+---------------------+
```
**Step 9: Thử đăng nhập bằng user vừa tạo**
```bash
1. exit;
2. mariadb -u demo_user -p demo_db # Đăng nhập lại
3. Nhập password: 123456
4. Kiểm tra: SELECT * FROM users;
# Nếu hiện dữ liệu là thành công.
```
Đúng rồi. Đây cũng là cách mà rất nhiều lập trình viên sử dụng:

Terminal → tạo database, user, phân quyền.
DBeaver → viết query dài, quản lý bảng, xem dữ liệu, ERD,...

Quy trình sẽ như sau.

Bước 1. Tạo database bằng Terminal

Ví dụ bạn đã tạo:

CREATE DATABASE demo_db;

CREATE USER 'demo_user'@'localhost' IDENTIFIED BY '123456';

GRANT ALL PRIVILEGES ON demo_db.* TO 'demo_user'@'localhost';

FLUSH PRIVILEGES;

Đến đây bạn thoát terminal cũng được, database đã được lưu trong MariaDB.

Bước 2. Mở DBeaver

Chọn

Database
    ↓
New Database Connection

hoặc bấm biểu tượng phích cắm có dấu +.

Bước 3. Chọn MariaDB

Chọn

MariaDB

Nếu chưa có Driver thì DBeaver sẽ hỏi tải, chỉ cần bấm Download.

Bước 4. Điền thông tin kết nối

Ví dụ:

Field	Giá trị
Host	localhost
Port	3306
Database	demo_db
User	demo_user
Password	123456

Sau đó bấm

Test Connection

Nếu hiện

Connected

hoặc

Success

thì bấm Finish.

Bước 5. Database sẽ xuất hiện bên trái

Lúc này Database Navigator sẽ giống như

MariaDB
└── localhost
    └── demo_db
        ├── Tables
        ├── Views
        ├── Procedures
        └── ...

Nếu chưa thấy

demo_db

thì

Chuột phải Connection

Refresh

hoặc nhấn F5.

Bước 6. Tạo file SQL

Chuột phải vào

demo_db

↓

SQL Editor

↓

New SQL Script

Hoặc dùng phím tắt:

Ctrl + Alt + Enter

DBeaver sẽ mở một tab như

Script-1.sql

Bạn có thể viết

CREATE TABLE users(
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(50)
);

INSERT INTO users(name)
VALUES ('Alice');

SELECT * FROM users;

Sau đó bấm nút ▶ Execute SQL Script hoặc nhấn Ctrl + Enter để chạy câu lệnh hiện tại (hoặc đoạn đã chọn).

Bước 7. Refresh để thấy bảng

Sau khi chạy:

demo_db
    Tables

chuột phải

Refresh

sẽ thấy

demo_db
    Tables
        users
Bước 8. Xem dữ liệu

Chuột phải vào

users

↓

View Data

↓

All Rows

Hoặc chạy

SELECT * FROM users;
Sơ đồ toàn bộ quy trình
Terminal

sudo mariadb
      │
      ▼
CREATE DATABASE demo_db;
CREATE USER ...
GRANT ...
      │
      ▼
Database đã tồn tại trong MariaDB
      │
      ▼
Mở DBeaver
      │
      ▼
New Connection
      │
      ▼
Host: localhost
Port: 3306
Database: demo_db
User: demo_user
Password: 123456
      │
      ▼
Finish
      │
      ▼
Database Navigator
      │
      ▼
demo_db
   ├── Tables
   ├── Views
   └── ...
      │
      ▼
SQL Editor
      │
      ▼
script.sql
      │
      ▼
Viết query
Nếu không thấy demo_db trong DBeaver

Hãy kiểm tra lần lượt:

Đã tạo database chưa? Trong terminal chạy:

mysql -u demo_user -p

rồi:

SHOW DATABASES;

Nếu có demo_db thì database đã tồn tại.

Thông tin kết nối đúng chưa? Đảm bảo Host = localhost, Port = 3306, User và Password đúng.

Đã cấp quyền cho user chưa? Với demo_user, chạy:

SHOW GRANTS FOR 'demo_user'@'localhost';

Bạn nên thấy quyền trên demo_db.*.

Nếu đây là lần đầu bạn dùng DBeaver, mình cũng có thể hướng dẫn bằng hình minh họa từng bước (New Connection → Test Connection → SQL Editor → Refresh Tables).
Cách 2: Dùng DBeaver Community Edition
Bước 1

Mở DBeaver

Chọn

New Database Connection
Bước 2

Chọn

MariaDB

(nếu chưa có driver thì DBeaver sẽ tự tải)

Bước 3

Điền thông tin

Ví dụ

Host:
localhost

Port:
3306

Database:

(có thể để trống)

Username:
root
Password:
(password của root)

Nhấn

Test Connection

Nếu hiện

Success

thì Next → Finish.

Bước 4

Mở SQL Editor

Chuột phải connection

SQL Editor

↓

New SQL Script
Bước 5

Paste toàn bộ

CREATE DATABASE demo_db;

CREATE USER 'demo_user'@'localhost'
IDENTIFIED BY '123456';

GRANT ALL PRIVILEGES
ON demo_db.*
TO 'demo_user'@'localhost';

FLUSH PRIVILEGES;

USE demo_db;

CREATE TABLE users(
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100),
    email VARCHAR(100)
);

INSERT INTO users(name,email)
VALUES
('Alice','alice@gmail.com'),
('Bob','bob@gmail.com');

SELECT * FROM users;

Bấm nút

▶ Execute SQL Script
Bước 6

Refresh

demo_db

Bạn sẽ thấy

demo_db
    Tables
        users
Bước 7

Test user mới

Tạo một connection mới

Host:
localhost

Port:
3306

Database:
demo_db

Username:
demo_user

Password:
123456

Bấm

Test Connection

Nếu thành công, mở SQL Editor và chạy:

SELECT * FROM users;
Kiểm tra bằng Terminal

Bạn có thể kiểm tra toàn bộ bằng các lệnh sau:

mysql -u demo_user -p demo_db
SHOW TABLES;

Kết quả mong đợi:

+------------------+
| Tables_in_demo_db|
+------------------+
| users            |
+------------------+

Tiếp theo:

DESCRIBE users;
SELECT * FROM users;

Nếu thấy dữ liệu Alice và Bob thì mọi thứ đã được cấu hình đúng.

Lưu ý bảo mật: Mật khẩu 123456 chỉ nên dùng để học hoặc thử nghiệm. Khi làm dự án thực tế, hãy đặt mật khẩu mạnh hơn (ít nhất 12 ký tự, kết hợp chữ hoa, chữ thường, số và ký tự đặc biệt).
# Reset khóa kiểu int tự tăng về 1
```sql
ALTER TABLE ten_bang AUTO_INCREMENT = 1;

- Bảng phải trống
- Nếu vẫn còn record có id = 10 → AUTO_INCREMENT sẽ không về 1
```