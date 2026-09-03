+ [<<Back](../Base.md)
- [Check Database (Kiểm tra database)](#check-database-kiểm-tra-database)
  - [Linux (Kiểm tra db trên linux)](#linux-kiểm-tra-db-trên-linux)
    - [sudo mysql/mariadb -u root -p (Đăng nhập quyền root)](#sudo-mysqlmariadb--u-root--p-đăng-nhập-quyền-root)
    - [mysql --version | mysql -V](#mysql---version--mysql--v)
    - [mariadb --version](#mariadb---version)
    - [systemctl status ...](#systemctl-status-)
    - [ps -ef | grep -E "mysqld|mariadbd" (Kiểm tra tiến trình)](#ps--ef--grep--e-mysqldmariadbd-kiểm-tra-tiến-trình)
    - [ss -tlnp | grep 3306 hoặc netstat -tlnp | grep 3306 (Kiểm tra cổng mặc định 3306)](#ss--tlnp--grep-3306-hoặc-netstat--tlnp--grep-3306-kiểm-tra-cổng-mặc-định-3306)
    - [where mysql](#where-mysql)
    - [SELECT VERSION();](#select-version)
- [Create \& Use (Tạo và dùng)](#create--use-tạo-và-dùng)
  - [create database ... (Tạo database)](#create-database--tạo-database)
  - [Use ... (Dùng để chọn database)](#use--dùng-để-chọn-database)
  - [create table ... (Tạo bảng)](#create-table--tạo-bảng)
- [Add (Thêm)](#add-thêm)
  - [alter table ... add column ... (Thêm cột vào bảng)](#alter-table--add-column--thêm-cột-vào-bảng)
  - [add constraint ... foreign key ... references (Thêm khóa ngoài)](#add-constraint--foreign-key--references-thêm-khóa-ngoài)
- [Delete (Xóa)](#delete-xóa)
  - [DROP DATABASE ... (xóa database)](#drop-database--xóa-database)
  - [TRUNCATE TABLE ... (Khuyên dùng nếu bạn muốn xóa sạch dữ liệu và reset ID về 1)](#truncate-table--khuyên-dùng-nếu-bạn-muốn-xóa-sạch-dữ-liệu-và-reset-id-về-1)
  - [drop table ... (Xóa bảng)](#drop-table--xóa-bảng)
  - [alter table ... drop column (xóa cột trong bảng)](#alter-table--drop-column-xóa-cột-trong-bảng)
  - [alter table ... drop foreign key ... (xóa khóa ngoài)](#alter-table--drop-foreign-key--xóa-khóa-ngoài)
  - [alter table ... drop primary key ... (xóa khóa chính)](#alter-table--drop-primary-key--xóa-khóa-chính)
- [Update (cập nhật \& thay đổi)](#update-cập-nhật--thay-đổi)
  - [alter ... modify column ... (Dùng để thay đổi định nghĩ một cột trong bảng)](#alter--modify-column--dùng-để-thay-đổi-định-nghĩ-một-cột-trong-bảng)
  - [alter ... change ... (Thường dùng để đổi tên cột)](#alter--change--thường-dùng-để-đổi-tên-cột)
  - [alter ... rename to (Thường dùng để thay đổi tên bảng)](#alter--rename-to-thường-dùng-để-thay-đổi-tên-bảng)
- [JOIN (nối bảng)](#join-nối-bảng)
  - [inner join (JOIN mặc định trong SQL thực ra là INNER JOIN)](#inner-join-join-mặc-định-trong-sql-thực-ra-là-inner-join)
  - [left join (Giữ tất cả dữ liệu bảng bên trái. Nếu bảng phải không có → NULL.)](#left-join-giữ-tất-cả-dữ-liệu-bảng-bên-trái-nếu-bảng-phải-không-có--null)
  - [right join (Ngược lại với LEFT JOIN: lấy tất cả bên phải)](#right-join-ngược-lại-với-left-join-lấy-tất-cả-bên-phải)
  - [full join | full outer join (Lấy tất cả của cả hai bên Khớp thì ghép Không khớp thì bên còn lại là NULL)](#full-join--full-outer-join-lấy-tất-cả-của-cả-hai-bên-khớp-thì-ghép-không-khớp-thì-bên-còn-lại-là-null)
- [Transform (Nhóm làm thay đổi hình dạng bảng)](#transform-nhóm-làm-thay-đổi-hình-dạng-bảng)
  - [group by](#group-by)
---
# Check Database (Kiểm tra database)
## Linux (Kiểm tra db trên linux)
### sudo mysql/mariadb -u root -p (Đăng nhập quyền root)
### mysql --version | mysql -V
**Ex**
```bash
thang@PhatToNhuLai:~$ mysql --version
mysql  Ver 15.1 Distrib 10.11.13-MariaDB, for debian-linux-gnu (x86_64) using  EditLine wrapper
thang@PhatToNhuLai:~$ mysql -V
mysql  Ver 15.1 Distrib 10.11.13-MariaDB, for debian-linux-gnu (x86_64) using  EditLine wrapper
```
### mariadb --version
```bash
dpkg -l | grep -Ei "mysql|mariadb" (Kiểm tra package đã cài)
```
### systemctl status ...
**Ex**
```bash
systemctl status mysql hoặc systemctl status mariadb
# Nếu service tồn tại sẽ hiển thị trạng thái active (running) hoặc inactive.
```
### ps -ef | grep -E "mysqld|mariadbd" (Kiểm tra tiến trình)
### ss -tlnp | grep 3306 hoặc netstat -tlnp | grep 3306 (Kiểm tra cổng mặc định 3306)
### where mysql
### SELECT VERSION();
```bash
# Nếu là MariaDB sẽ hiện kiểu
# 10.11.13-MariaDB-0ubuntu0.24.04.1
```
# Create & Use (Tạo và dùng)
## create database ... (Tạo database)
**Syn**
```sql
create database MyDatabase  -- Tạo một database
    CHARACTER SET utf8mb4
    COLLATE utf8mb4_unicode_ci; -- Như vậy mặc định schema MyDatabase sẽ dùng utf8mb4 + utf8mb4_unicode_ci

- character set: dữ liệu chữ sẽ được mã hóa như thế nào
  | Character Set | Hỗ trợ                          | Khi nào dùng         |
  | ------------- | ------------------------------- | -------------------- |
  | `latin1`      | Tây Âu                          | Hệ thống cũ          |
  | `ascii`       | Chỉ 128 ký tự ASCII             | Dữ liệu rất đơn giản |
  | `utf8`        | Unicode nhưng chỉ tối đa 3 byte | Không nên dùng       |
  | `utf8mb4`     | Unicode đầy đủ (4 byte)         | Nên dùng mặc định    |
  | `ucs2`        | Unicode 2 byte cố định          | Ít dùng              |
  | `utf16`       | Unicode UTF-16                  | Hiếm dùng            |
  | `utf32`       | Unicode UTF-32                  | Rất hiếm             |
- collation: quy tắc so sánh và sắp xếp dữ liệu chữ đó
  + utfmb4_uicode_ci: không phân biết hoa thường
    | Hậu tố | Ý nghĩa                                       |
    | ------ | --------------------------------------------- |
    | `ci`   | Case Insensitive (không phân biệt hoa thường) |
    | `cs`   | Case Sensitive (phân biệt hoa thường)         |
    | `bin`  | So sánh theo byte                             |
    | `ai`   | Accent Insensitive (không phân biệt dấu)      |
    | `as`   | Accent Sensitive (phân biệt dấu)              |
```
## Use ... (Dùng để chọn database)
**Syn**
```sql
use MyDatabase;
```
## create table ... (Tạo bảng)
**Syn**
```bash
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    ...
) ENGINE=InnoDB;

- ENGINE=InnoDB: chỉ định storage engine cho bảng trong MySQL. Nó quyết định:
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
# Add (Thêm)
## alter table ... add column ... (Thêm cột vào bảng)
**Ex**
```bash
ALTER TABLE platform
ADD COLUMN created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP; # nếu thêm nhiều cột thì dùng ',' sau mỗi lệnh add
```
**Ex2: thêm một cột sau một cột khác**
```sql
ALTER TABLE table_name
ADD COLUMN new_column datatype
AFTER existing_column;
```
## add constraint ... foreign key ... references (Thêm khóa ngoài)
**Ex**
```sql
ALTER TABLE listings -- Sửa cấu trúc của bảng listings.
ADD CONSTRAINT fk_districts -- Thêm một ràng buộc (constraint) mới
FOREIGN KEY (id_districts) -- Cột id_districts của bảng listings là khóa ngoại
REFERENCES districts(id) -- Giá trị trong listings.id_districts phải tồn tại trong districts.id
ON UPDATE CASCADE -- Nếu khóa chính ở bảng cha thay đổi, bảng con tự cập nhật theo
ON DELETE RESTRICT; -- Không cho phép xóa dữ liệu ở bảng cha nếu bảng con vẫn đang tham chiếu tới nó
```
# Delete (Xóa)
## DROP DATABASE ... (xóa database)
**Syn**
```bash
DROP DATABASE ten_database;
```
## TRUNCATE TABLE ... (Khuyên dùng nếu bạn muốn xóa sạch dữ liệu và reset ID về 1)
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
## drop table ... (Xóa bảng)
**Syn**
```bash
DROP TABLE Students;
```
## alter table ... drop column (xóa cột trong bảng)
**Syn**
```bash
ALTER TABLE ten_bang
DROP COLUMN ten_cot;
```
**Ex1: Xóa cột**
```sql
ALTER TABLE Students
DROP COLUMN className,
DROP COLUMN major;
```
## alter table ... drop foreign key ... (xóa khóa ngoài)
**Ex1: Xóa khóa ngoài**
```sql
alter table listings 
drop foreign key fk_districts;
```
## alter table ... drop primary key ... (xóa khóa chính)
**Ex1: Xóa khóa chính**
```sql
ALTER TABLE districts
DROP PRIMARY KEY;
```
# Update (cập nhật & thay đổi)
## alter ... modify column ... (Dùng để thay đổi định nghĩ một cột trong bảng)
**Ex: Đổi kiểu dữ liệu cho một cột**
```bash
ALTER TABLE ten_bang
MODIFY COLUMN ten_cot KIEU_DU_LIEU_MOI;
```
## alter ... change ... (Thường dùng để đổi tên cột)
**Syn**
```bash
ALTER TABLE table_name
CHANGE old_column_name new_column_name column_definition;
```
**Ex**
```sql
ALTER TABLE users
CHANGE username user_name VARCHAR(100);
```
## alter ... rename to (Thường dùng để thay đổi tên bảng)
**Ex**
```sql
alter table meals rename to food_library; -- đổi tên bảng từ meals thành food_library
```
# JOIN (nối bảng)
## inner join (JOIN mặc định trong SQL thực ra là INNER JOIN)
**Ex: join bằng inner join**
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
JOIN scores ON students.id = scores.student_id;

-- name	score
-- An	  8
-- Bình	9

-- Cường bị mất vì không có điểm.
```
## left join (Giữ tất cả dữ liệu bảng bên trái. Nếu bảng phải không có → NULL.)
**Ex: join bảng bằng left join**
```bash
Bảng students:
  id	name
  1	  An
  2	  Bình
  3	  Cường

Bảng scores:
  student_id	score
  1	          8
  2	          9
```
```sql
SELECT students.name, scores.score FROM students
LEFT JOIN scores ON students.id = scores.student_id;

-- name	score
-- An	8
-- Bình	9
-- Cường	NULL

-- Cường vẫn còn dù không có điểm.
```
## right join (Ngược lại với LEFT JOIN: lấy tất cả bên phải)
## full join | full outer join (Lấy tất cả của cả hai bên Khớp thì ghép Không khớp thì bên còn lại là NULL)
```bash
Mariadb không hỗ trợ trực tiếp outer join mà phải kết hợp left join và right join
```
# Transform (Nhóm làm thay đổi hình dạng bảng)
## group by
```bash
Dùng để gom các dòng có cùng giá trị lại thành một nhóm
```