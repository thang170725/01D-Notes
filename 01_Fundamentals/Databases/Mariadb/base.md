- [Cấu trúc thư mục](#cấu-trúc-thư-mục)
- [Giới thiệu](#giới-thiệu)
- [Cách tạo db](#cách-tạo-db)
---
# Cấu trúc thư mục
```bash
Mariadb/
├── 01_Datatypes.md       # Gom từ Data-Type/base.md (Số, chữ, thời gian)
├── 02_Structure_DDL.md   # [Data Definition] Tạo/Sửa/Xóa Database, Table (Create, Drop, Alter)
├── 03_Data_DML.md        # [Data Manipulation] Thao tác dữ liệu (Insert, Update, Delete)
├── 04_Query_DQL.md       # [Data Query] Truy vấn dữ liệu (Select, Join, Group by)
└── 05_Advanced.md        # Backup, Restore, User/Permission, Index
```
# Giới thiệu
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
