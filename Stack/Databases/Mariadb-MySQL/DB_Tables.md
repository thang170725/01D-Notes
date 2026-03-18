- [Create \& Use](#create--use)
  - [create database](#create-database)
  - [Use](#use)
  - [create table](#create-table)
- [Add](#add)
  - [Thêm cột vào db](#thêm-cột-vào-db)
  - [Thêm khóa ngoài](#thêm-khóa-ngoài)
- [Đổi kiểu dữ liệu cho một cột](#đổi-kiểu-dữ-liệu-cho-một-cột)
- [Đổi kiểu dữ liệu và thêm khóa chính](#đổi-kiểu-dữ-liệu-và-thêm-khóa-chính)
- [Delete](#delete)
  - [TRUNCATE TABLE](#truncate-table)
  - [Xóa bảng](#xóa-bảng)
  - [drop column](#drop-column)
  - [Xóa khóa ngoài](#xóa-khóa-ngoài)
  - [Xóa khóa chính](#xóa-khóa-chính)
- [Update](#update)
- [alter table](#alter-table)
- [JOIN (nối bảng)](#join-nối-bảng)
  - [join (inner join)](#join-inner-join)
  - [left join](#left-join)
---
# Create & Use
## create database
```bash
- Dùng để tạo database.
```
**Syn**
```sql
create database MyDatabase  -- Tạo một database
    CHARACTER SET utf8mb4
    COLLATE utf8mb4_unicode_ci; -- Như vậy mặc định schema MyDatabase sẽ dùng utf8mb4 + utf8mb4_unicode_ci
```
## Use
```bash
Dùng để chọn database.
```
**Syn**
```sql
use MyDatabase;
```
## create table
**Syn**
```bash
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    ...
) ENGINE=InnoDB;

- ENGINE=InnoDB: chỉ định storage engine cho bảng trong MySQL.Nó quyết định:
  + Dữ liệu được lưu thế nào?
  + Có hỗ trợ transaction không?
  + Có khóa ngoại không?
  + Cơ chế lock ra sao?
  + InnoDB: là engine mặc định và phổ biến nhất của MySQL hiện nay. Nó cung cấp:
    1. Transaction (ACID). Cho phép dùng:
      START TRANSACTION;
      COMMIT;
      ROLLBACK;
    Rất quan trọng khi:
      + Thanh toán
      + Trừ tiền
      + Tạo đơn hàng
      + Ghi nhiều bảng cùng lúc
    2. Foreign Key (ràng buộc khóa ngoại)
      + FOREIGN KEY (user_id) REFERENCES users(id)
      + Chỉ InnoDB mới hỗ trợ foreign key chuẩn.
    3. Row-level locking (khóa từng dòng)
      + InnoDB khóa 1 dòng, không khóa cả bảng. => Hiệu năng cao khi nhiều user cùng truy cập.
      + Ví dụ:
        - 1000 người cùng login
        - 100 người cập nhật chỉ số BMI
        -> Không bị khóa toàn bảng.
    4. Crash recovery
      + Nếu server bị sập:
      + InnoDB có cơ chế phục hồi dữ liệu
      + Không mất dữ liệu giữa chừng
```
# Add
## Thêm cột vào db
**Ex**
```bash
ALTER TABLE platform
ADD COLUMN created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP;

# nếu thêm nhiều cột thì dùng ',' sau mỗi lệnh add
```
## Thêm khóa ngoài
```sql
ALTER TABLE listings
ADD CONSTRAINT fk_districts
FOREIGN KEY (id_districts)
REFERENCES districts(id)
ON UPDATE CASCADE
ON DELETE RESTRICT;
```
# Đổi kiểu dữ liệu cho một cột
```bash
ALTER TABLE ten_bang
MODIFY COLUMN ten_cot KIEU_DU_LIEU_MOI;
```

# Đổi kiểu dữ liệu và thêm khóa chính
```sql
ALTER TABLE districts
MODIFY COLUMN id INT UNSIGNED NOT NULL AUTO_INCREMENT,
ADD PRIMARY KEY (id);
```
# Delete
## TRUNCATE TABLE
```bash
- Khuyên dùng nếu bạn muốn xóa sạch dữ liệu và reset ID về 1
```
**Syn**
```bash
TRUNCATE TABLE ten_bang;

- Xóa toàn bộ dữ liệu
- Reset AUTO_INCREMENT về 1
- Nhanh hơn DELETE
- Lưu ý:
    + Không dùng được nếu bảng đang bị FOREIGN KEY reference
    + Không rollback được (auto commit)
```
## Xóa bảng
**Syn**
```bash
DROP TABLE Students;
```
## drop column
```bash
Xóa một cột trong bảng
```
**Syn**
```bash
ALTER TABLE ten_bang
DROP COLUMN ten_cot;
```
**Ex**
```sql
ALTER TABLE Students
DROP COLUMN className,
DROP COLUMN major;
```

## Xóa khóa ngoài
**Ex**
```sql
alter table listings 
drop foreign key fk_districts;
```

## Xóa khóa chính
```sql
ALTER TABLE districts
DROP PRIMARY KEY;
```
# Update
# alter table
**Syn**
```bash
ALTER TABLE ten_bang AUTO_INCREMENT = 1;

- Bảng phải trống
- Nếu vẫn còn record có id = 10 → AUTO_INCREMENT sẽ không về 1
```
# JOIN (nối bảng)
## join (inner join)
```bash
- JOIN mặc định trong SQL thực ra là INNER JOIN.
```
**Ex**
```bash
Bảng students
id	name
1	  An
2	  Bình
3	  Cường

Bảng scores
student_id	score
1	          8
2	          9
```
```sql
SELECT students.name, scores.score
FROM students
JOIN scores
ON students.id = scores.student_id;

-- name	score
-- An	8
-- Bình	9
-- Cường bị mất vì không có điểm.
```
## left join
```bash
- Giữ tất cả dữ liệu bảng bên trái.
- Nếu bảng phải không có → NULL.
```
**Ex**
```sql
SELECT students.name, scores.score
FROM students
LEFT JOIN scores
ON students.id = scores.student_id;

-- name	score
-- An	8
-- Bình	9
-- Cường	NULL
-- Cường vẫn còn dù không có điểm.
```