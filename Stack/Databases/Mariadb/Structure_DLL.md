- [create database](#create-database)
- [Use](#use)
- [Xóa bảng](#xóa-bảng)
- [Xóa một cột trong bảng](#xóa-một-cột-trong-bảng)
- [Xóa khóa ngoài](#xóa-khóa-ngoài)
- [Xóa khóa chính](#xóa-khóa-chính)
- [Xóa dữ liệu một hoặc nhiều hàng](#xóa-dữ-liệu-một-hoặc-nhiều-hàng)
- [Thêm khóa ngoài](#thêm-khóa-ngoài)
- [Đổi kiểu dữ liệu cho một cột](#đổi-kiểu-dữ-liệu-cho-một-cột)
- [Đổi kiểu dữ liệu và thêm khóa chính](#đổi-kiểu-dữ-liệu-và-thêm-khóa-chính)
---
# create database
```bash
- Dùng để tạo database.
```
**Syn**
```sql
create database MyDatabase  -- Tạo một database
    CHARACTER SET utf8mb4
    COLLATE utf8mb4_unicode_ci; -- Như vậy mặc định schema MyDatabase sẽ dùng utf8mb4 + utf8mb4_unicode_ci
```

# Use
```bash
Dùng để chọn database.
```
**Syn**
```sql
use MyDatabase;
```
# Xóa bảng
**Syn**
```bash
DROP TABLE Students;
```

# Xóa một cột trong bảng
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

# Xóa khóa ngoài
**Ex**
```sql
alter table listings 
drop foreign key fk_districts;
```

# Xóa khóa chính
```sql
ALTER TABLE districts
DROP PRIMARY KEY;
```

# Xóa dữ liệu một hoặc nhiều hàng
**Ex**
```sql
DELETE FROM Students
WHERE studentId = 's001';
DELETE FROM Students
WHERE className = 'IT01';
DELETE FROM Users
WHERE userId IN ('s001', 's002', 's003');
```
# Thêm khóa ngoài
```sql
ALTER TABLE listings
ADD CONSTRAINT fk_districts
FOREIGN KEY (id_districts)
REFERENCES districts(id)
ON UPDATE CASCADE
ON DELETE RESTRICT;
```
- [Đổi kiểu dữ liệu cho một cột](#đổi-kiểu-dữ-liệu-cho-một-cột)

---

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
# TRUNCATE TABLE
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
# alter table
**Syn**
```bash
ALTER TABLE ten_bang AUTO_INCREMENT = 1;

- Bảng phải trống
- Nếu vẫn còn record có id = 10 → AUTO_INCREMENT sẽ không về 1
```