- [Kiểu dữ liệu](#kiểu-dữ-liệu)
- [insert into](#insert-into)
- [delete](#delete)
  - [Xóa dữ liệu một hoặc nhiều hàng](#xóa-dữ-liệu-một-hoặc-nhiều-hàng)
---
# Kiểu dữ liệu
```bash
CHAR(n)         : Kiểu chuỗi với độ dài cố địnhv
VARCHAR(n)      : Kiểu chuỗi với độ dài chính xác
TEXT            : Dữ liệu kiếu chuỗi với độ dài lớn (tối đa 2,147,483,647 ký tự)
NTEXT           : Dữ liệu kiếu chuỗi với độ dài lớn và hỗ trợ UNICODE (tối đa 1,073,741,823 ký tự
INT             : kiểu số nguyên
TINYTINT        : Số nguyên có giá trị từ -231 đến 231 - 1
FLOAT           : Số thực có giá trị từ -1.79E+308 đến 1.79E+308
double          : Kiểu số thực.
DECIMAL(p,s)    : Tương tự kiểu Numeric
enum            : kiểu giữ liệu bắt buộc phải có giá trị
MONEY           : Kiểu tiền tệ
DATETIME        : Kiểu ngày giờ (chính xác đến phần trăm của giây)
SMALLDATETIME   : Kiểu ngày giờ (chính xác đến phút)
unique          : Không cho trùng giá trị
SMALLINT        :
BIGINT          :
IMAGE           : 
```
# insert into
```bash
- Dùng để thêm dữ liệu vào bảng.
```
**Ex**
```sql
-- Thêm 1 dòng --
INSERT INTO Students (studentId, userId, fullNameStudent, major, className)
VALUES (1, 101, 'Nguyễn Văn A', 'Công nghệ thông tin', 'CNTT01');

-- Thêm nhiều dòng --
INSERT INTO Students (studentId, userId, fullNameStudent, major, className)
VALUES
(2, 102, 'Trần Thị B', 'Khoa học máy tính', 'KHMT01'),
(3, 103, 'Lê Văn C', 'Hệ thống thông tin', 'HTTT01');
```
# delete
## Xóa dữ liệu một hoặc nhiều hàng
**Ex**
```sql
DELETE FROM Students
WHERE studentId = 's001';
DELETE FROM Students
WHERE className = 'IT01';
DELETE FROM Users
WHERE userId IN ('s001', 's002', 's003');
```
```bash
dùng để xóa dữ liệu (record/row) trong bảng.
```
**Syn**
```bash
DELETE FROM ten_bang
WHERE dieu_kien;
```
## on delete cascade
```bash
dùng để tự động xóa dữ liệu con khi dữ liệu cha bị xóa trong quan hệ khóa ngoại (FOREIGN KEY).
```
**Ex**
```sql
FOREIGN KEY (program_id)
REFERENCES workout_programs(id)
ON DELETE CASCADE
```