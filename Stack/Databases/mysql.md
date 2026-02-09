- [Kiểu dữ liệu](#kiểu-dữ-liệu)
- [Tạo | Thêm](#tạo--thêm)
  - [create database](#create-database)
  - [Use](#use)
  - [create table \& primary key \& foreign key](#create-table--primary-key--foreign-key)
  - [auto\_increment](#auto_increment)
- [Xem](#xem)
  - [Select](#select)
  - [show table](#show-table)
  - [Describe](#describe)

---





## create table & primary key & foreign key
Tạo bảng, khóa chính và khóa ngoài.
**Syn**
```sql
CREATE TABLE Orders (
    OrderID int NOT NULL,
    OrderNumber int NOT NULL,
    PersonID int,
    PRIMARY KEY (OrderID),
    FOREIGN KEY (PersonID) REFERENCES Persons(PersonID)
);
CREATE TABLE Orders (
    OrderID int NOT NULL,
    OrderNumber int NOT NULL,
    PersonID int,
    PRIMARY KEY (OrderID),
    CONSTRAINT FK_PersonOrder FOREIGN KEY (PersonID)
    REFERENCES Persons(PersonID)
);
```



## auto_increment
Để tạo cột tự tăng. bắt buộc kiểu int
**Syn**
```sql
CREATE TABLE Test (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(50)
); -- id sẽ tự động tăng 1 mỗi lần bạn INSERT.

-- Bạn chỉ cần thêm dữ liệu như:
-- INSERT INTO Test (name) VALUES ('Thắng');
-- INSERT INTO Test (name) VALUES ('Nam');
```




## show table
Dùng để xem tên các bảng trong db.
**Syb**
```bash
show tables;
```

## Describe
Xem kiểu dữ liệu và toàn bộ dữ liệu của bảng.
Cú pháp:
DESCRIBE Schedules;
-- hoặc
DESC Schedules;

Chỉnh sửa
Đổi charset/collation của database
Cú pháp:
ALTER DATABASE MyDatabase
    CHARACTER SET = utf8mb4
    COLLATE = utf8mb4_unicode_ci;
Đổi charset/collation của một bảng
Cú pháp:
ALTER TABLE Students
    CONVERT TO CHARACTER SET utf8mb4
    COLLATE utf8mb4_unicode_ci;
ALTER TABLE Students
    MODIFY fullNameStudent VARCHAR(50)
    CHARACTER SET utf8mb4
    COLLATE utf8mb4_unicode_ci;

Đổi tên cột trong bảng
ALTER TABLE ten_bang CHANGE ten_cot_cu ten_cot_moi kieu_du_lieu;
order by 
Dùng để sắp xếp kết quả của câu query theo một (hoặc nhiều) cột.
Cập nhật giá trị cho một cột trong một hàng hoặc nhiều hàng
UPDATE Students
SET major = 'Trí tuệ nhân tạo'
WHERE studentId = 1;
UPDATE Students
SET
    major = 'Khoa học máy tính',
    className = 'CS02'
WHERE studentId = 1;


