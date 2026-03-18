- [Kiểu dữ liệu](#kiểu-dữ-liệu)
  - [JSON](#json)
- [insert into](#insert-into)
- [delete](#delete)
  - [Xóa dữ liệu một hoặc nhiều hàng](#xóa-dữ-liệu-một-hoặc-nhiều-hàng)
  - [on delete cascade](#on-delete-cascade)
- [Update](#update)
  - [update](#update-1)
- [Select](#select)
  - [Hiển thị nhiều field của nhiều bảng](#hiển-thị-nhiều-field-của-nhiều-bảng)
  - [Hiển thị nhiều field của nhiều bảng có điều kiện](#hiển-thị-nhiều-field-của-nhiều-bảng-có-điều-kiện)
- [like](#like)
- [group\_by](#group_by)
- [count](#count)
- [DISTINCT](#distinct)
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
## JSON
**Ex**
```bash
'{"title":"Buổi tập chân + mông","muscle_group":["Đùi trước","Đùi sau","Mông","Bắp chân"],"suggested_exercises":["Barbell Squat","Leg Press","Lunges","Standing Calf Raise"]}'
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
# Update
## update
```bash
cập nhật dữ liệu
```
**Ex: update - set - where**
```sql
UPDATE workout_plans
SET note = 'Chest and Triceps workout'
WHERE id = 5;
```
- [Kiểu dữ liệu](#kiểu-dữ-liệu)
  - [JSON](#json)
- [insert into](#insert-into)
- [delete](#delete)
  - [Xóa dữ liệu một hoặc nhiều hàng](#xóa-dữ-liệu-một-hoặc-nhiều-hàng)
  - [on delete cascade](#on-delete-cascade)
- [Update](#update)
  - [update](#update-1)
- [Select](#select)
  - [Hiển thị nhiều field của nhiều bảng](#hiển-thị-nhiều-field-của-nhiều-bảng)
  - [Hiển thị nhiều field của nhiều bảng có điều kiện](#hiển-thị-nhiều-field-của-nhiều-bảng-có-điều-kiện)
- [like](#like)
- [group\_by](#group_by)
- [count](#count)
- [DISTINCT](#distinct)
---
# Select
```bash
Dùng để xem dữ liệu trong bảng.
```
```bash
SELECT * FROM Students limit 50;

- limit: số dòng cần xem.
```
## Hiển thị nhiều field của nhiều bảng
**Ex1**
```sql
SELECT
    s.studentId,
    s.fullNameStudent,
    s.major,
    s.className,
    u.email,
    u.role
FROM Students s
JOIN Users u ON s.userId = u.userId;
```
## Hiển thị nhiều field của nhiều bảng có điều kiện
```sql
SELECT
    c.courseName,
    s.fullNameStudent,
    t.fullNameTeacher,
    t.department
FROM Courses c
JOIN Students s ON c.studentId = s.studentId
JOIN Teachers t ON c.teacherId = t.teacherId;
Xem danh sách gắn với một điều kiện nào đó:
SELECT * FROM Courses WHERE courseId = '2';
```
# like
**Ex: truy vấn dữ liệu theo điều kiện**
```sql
SELECT * FROM exercises WHERE name LIKE '%Mountain%'
```
# group_by
```bash
Dùng để gom các dòng có cùng giá trị lại thành một nhóm
```
# count
```bash
Dùng để đếm số dòng trong mỗi nhóm
```
**Ex: đếm số user trong mỗi phòng ban**
```bash
| id | name | department |
| -- | ---- | ---------- |
| 1  | A    | IT         |
| 2  | B    | HR         |
| 3  | C    | IT         |
| 4  | D    | HR         |
| 5  | E    | IT         |
```
```sql
SELECT department, COUNT(*) AS total
FROM employees
GROUP BY department;

| department | total |
| ---------- | ----- |
| IT         | 3     |
| HR         | 2     |
```
# DISTINCT 
```bash
dùng để loại bỏ các giá trị trùng lặp trong kết quả query.
```
**Ex1: Dùng DISTINCT cơ bản**
```bash
Bài toán: Lấy danh sách các môn học không trùng

Table Teacher
teacher_id	subject_id
1	          Math
1	          Math
2	          Physics
3	          Math
```
```sql
SELECT subject_id FROM Teacher;

-- 👉 Kết quả:
-- Math
-- Math
-- Physics
-- Math

-- ✅ Dùng DISTINCT
SELECT DISTINCT subject_id FROM Teacher;

-- 👉 Kết quả:
-- Math
-- Physics
```