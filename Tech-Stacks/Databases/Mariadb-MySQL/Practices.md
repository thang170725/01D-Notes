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
# Reset khóa kiểu int tự tăng về 1
```sql
ALTER TABLE ten_bang AUTO_INCREMENT = 1;

- Bảng phải trống
- Nếu vẫn còn record có id = 10 → AUTO_INCREMENT sẽ không về 1
```