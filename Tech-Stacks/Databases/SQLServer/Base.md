# SQL Sever Introduction 
# Datatype (Kiểu dữ liệu)
```bash
- Char(n)     : Cố định n ký tự # Char(10) nếu điền ‘An’ database vẫn dùng 10
- Varchar(n)  : Chỉ dùng đúng số ký tự cần # Varchar(10) nếu điều ‘An’ database chỉ dùng 2
```
# Insert into ... values ...
**Ex1: insert 1 dòng**
```sql
INSERT INTO Users (Username, Password, Email)
VALUES (N'admin', N'123456', N'admin@example.com');
```
**Ex2: insert nhiều dòng**
```sql
INSERT INTO Users (Username, Password, Email)
VALUES
    (N'user1', N'pass1', N'user1@example.com'),
    (N'user2', N'pass2', N'user2@example.com'),
    (N'user3', N'pass3', N'user3@example.com');
```
# alter table ...
**Syn**
```bash
ALTER TABLE TenBang
```
# alter column ... (Đổi kiểu dữ liệu của cột)
**Syn**
```bash
ALTER COLUMN TenCot KieuDuLieuMoi [NULL | NOT NULL];
```
ALTER TABLE Users
# update ... set ... where
**Ex**
```sql
UPDATE Users
  SET Username = N'thắng'
  WHERE Username = N'lê đức thắng'; -- WHERE rất quan trọng để chỉ định hàng nào sẽ được cập nhật. Nếu bỏ WHERE, tất cả các dòng trong bảng sẽ bị đổi
```