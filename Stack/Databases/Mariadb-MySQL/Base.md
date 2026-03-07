- [Directory Structure](#directory-structure)
- [Introduction](#introduction)
- [Cách tạo db](#cách-tạo-db)
---
# Directory Structure
```bash
Mariadb/              # mình dùng thư mục này để xem kiến thức về Mariadb
├── DB_Tables.md      # mình dùng file này để thao tác với DB, Table
├── Data.md           # mình dùng file này đểthao tác với dữ liệu 
├── Query_DQL.md      # mình dùng file này để truy vấn dữ liệu
└── Base.md           # mình dùng file này để xem kiến thức, tiện ích
```
# Introduction
```bash
- MariaDB là một hệ quản trị CSDL RIÊNG BIỆT. Không phải “chế độ” của MySQL
- MySQL ban đầu do Monty Widenius tạo. Oracle mua MySQL. Monty fork MySQL → tạo MariaDB. MariaDB = con ruột của MySQL gốc
```
**Vì sao query giống MySQL gần như 100%?**
```bash
- MariaDB giữ tương thích ngược MySQL
- Cùng SQL dialect
- Cùng protocol
- Cùng port 3306
```
# Cách tạo db
```bash
1. mariadb -u root -p | sudo mariadb
2. create database tên_db | CREATE DATABASE IF NOT EXISTS mydb; | CREATE DATABASE HousePriceProject CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci
3. SHOW DATABASES;
4. USE mydb;
2.  CREATE USER 'ai_user'@'localhost' IDENTIFIED BY 'ai123'; (Tạo user mới)
3.
    GRANT ALL PRIVILEGES ON house_price_project.* TO 'ai_user'@'localhost';
    FLUSH PRIVILEGES;
4. SHOW GRANTS FOR 'myuser'@'localhost'; (GRANT ALL PRIVILEGES ON `mydb`.* TO 'myuser'@'localhost';)

4.  SELECT user, host FROM mysql.user;
5.  EXIT;
6.  mariadb -u ai_user -p
```
