- [Cách tạo db mariadb bằng terminal linux](#cách-tạo-db-mariadb-bằng-terminal-linux)
- [Reset khóa kiểu int tự tăng về 1](#reset-khóa-kiểu-int-tự-tăng-về-1)
---
# Cách tạo db mariadb bằng terminal linux
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
# Reset khóa kiểu int tự tăng về 1
```sql
ALTER TABLE ten_bang AUTO_INCREMENT = 1;

- Bảng phải trống
- Nếu vẫn còn record có id = 10 → AUTO_INCREMENT sẽ không về 1
```