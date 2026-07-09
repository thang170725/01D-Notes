- [Kiểu dữ liệu](#kiểu-dữ-liệu)
  - [JSON](#json)
  - [unique key](#unique-key)
  - [index](#index)
- [insert into](#insert-into)
- [delete](#delete)
  - [Xóa dữ liệu một hoặc nhiều hàng](#xóa-dữ-liệu-một-hoặc-nhiều-hàng)
  - [on delete cascade](#on-delete-cascade)
- [Update](#update)
  - [update](#update-1)
- [Search (tìm kiếm, lọc, xem dữ liệu)](#search-tìm-kiếm-lọc-xem-dữ-liệu)
  - [Select (xem dữ liệu trong bảng)](#select-xem-dữ-liệu-trong-bảng)
  - [select ... limit](#select--limit)
  - [select ... order by](#select--order-by)
  - [union all](#union-all)
- [like (truy vấn dữ liệu theo điều kiện)](#like-truy-vấn-dữ-liệu-theo-điều-kiện)
  - [REGEXP (công cụ khớp mẫu cực mạnh)](#regexp-công-cụ-khớp-mẫu-cực-mạnh)
- [Math (Nhóm xử lý tính toán)](#math-nhóm-xử-lý-tính-toán)
  - [count](#count)
  - [sum (Để cộng tổng các giá trị trong 1 cột hoặc khác cột)](#sum-để-cộng-tổng-các-giá-trị-trong-1-cột-hoặc-khác-cột)
  - [DISTINCT](#distinct)
  - [ROUND() (dùng để làm tròn số)](#round-dùng-để-làm-tròn-số)
  - [TRUNCATE()](#truncate)
- [Time (Nhóm thời gian)](#time-nhóm-thời-gian)
  - [WEEK()](#week)
  - [YEARWEEK()](#yearweek)
  - [YEAR()](#year)
  - [MONTH()](#month)
- [COALESCE() (xử lý NULL)](#coalesce-xử-lý-null)
- [char\_length()](#char_length)
- [Process](#process)
  - [Case ... When ... then ... else ... end (biểu thức điều kiện)](#case--when--then--else--end-biểu-thức-điều-kiện)
  - [if()](#if)
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
## unique key
**Ex**
```sql
CREATE TABLE likes (
    user_id INT,
    post_id INT,

    UNIQUE KEY uk_user_post (user_id, post_id)
);

INSERT INTO likes VALUES (1, 100); -- OK
INSERT INTO likes VALUES (1, 101); -- OK
INSERT INTO likes VALUES (2, 100); -- OK
INSERT INTO likes VALUES (1, 100); -- ❌
```
## index
**Ex**
```sql
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    email VARCHAR(100),
    name VARCHAR(50),

    UNIQUE KEY uk_email (email), -- chống trùng + nhanh
    INDEX idx_name (name)        -- chỉ để search nhanh
);
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
# Search (tìm kiếm, lọc, xem dữ liệu)
## Select (xem dữ liệu trong bảng)
## select ... limit
```bash
SELECT * FROM Students limit 50;

- limit: số dòng cần xem.
```
## select ... order by
```bash
Xem dữ liệu được sắp xếp có thứ tự
```
**Syn**
```bash
SELECT * FROM your_table ORDER BY name ASC;
```
**Hiển thị nhiều field của nhiều bảng**
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
**Hiển thị nhiều field của nhiều bảng có điều kiện**
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
## union all
```bash
UNION ALL = nối kết quả của nhiều câu SELECT lại với nhau (giữ nguyên tất cả dữ liệu)
```
**Ex**
```bash
bảng A:
| name |
| ---- |
| An   |
| Bình |

bảng B:
| name  |
| ----- |
| Bình  |
| Cường |
```
```sql
SELECT name FROM A
UNION ALL
SELECT name FROM B;
-- | name  |
-- | ----- |
-- | An    |
-- | Bình  |
-- | Bình  |
-- | Cường |
```
# like (truy vấn dữ liệu theo điều kiện)
**Ex**
```sql
SELECT * FROM exercises WHERE name LIKE '%Mountain%'
```
## REGEXP (công cụ khớp mẫu cực mạnh)
**Syn**
```bash
... REGEXP "^An"

- "^An": bắt đầu bằng An
- 'abc$': Cuối chuỗi
- 'cat|dog': Hoặc
- 'A+': Ít nhất 1 lần
- 'A*': 0 hoặc nhiều lần
- "?": 0 hoặc 1 lần
- 'G{3}': Chính xác n lần
- "G{3,}": Ít nhất n lần
- '[ABC]': Một ký tự trong tập
```
# Math (Nhóm xử lý tính toán)
## count
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
## sum (Để cộng tổng các giá trị trong 1 cột hoặc khác cột)
**Ex1: Tính tổng các giá trị trong 1 cột**
```sql
Employees table:
| emp_id | event_day  | in_time | out_time |
| ------ | ---------- | ------- | -------- |
| 1      | 2020-11-28 | 4       | 32       |
| 1      | 2020-11-28 | 55      | 200      |
| 1      | 2020-12-3  | 1       | 42       |
| 2      | 2020-11-28 | 3       | 33       |
| 2      | 2020-12-9  | 47      | 74       |

select sum(in_time) from Employees
-- | sum(in_time) |
-- | ------------ |
-- | 110          |
```
**Ex2: Tính tổng các giá trị khác cột**
```sql
Employees table:
| emp_id | event_day  | in_time | out_time |
| ------ | ---------- | ------- | -------- |
| 1      | 2020-11-28 | 4       | 32       |
| 1      | 2020-11-28 | 55      | 200      |
| 1      | 2020-12-3  | 1       | 42       |
| 2      | 2020-11-28 | 3       | 33       |
| 2      | 2020-12-9  | 47      | 74       |

select sum(out_time - in_time) from Employees
-- | sum(out_time - in_time) |
-- | ----------------------- |
-- | 271                     |
```
## DISTINCT 
```bash
ùng để loại bỏ các giá trị trùng lặp trong kết quả query.
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
## ROUND() (dùng để làm tròn số)
**Syn**
```bash
ROUND(number, decimal_places)

- number: Số cần làm tròn.
- decimal_places (tùy chọn):
  > 0: Giữ lại số chữ số thập phân.
  = 0: Làm tròn đến số nguyên (mặc định nếu không truyền).
  < 0: Làm tròn sang bên trái dấu thập phân (hàng chục, hàng trăm,...).
```
**Ex1: Làm tròn đến số nguyên**
```sql
SELECT ROUND(3.14159); -- 3

SELECT ROUND(3.8); -- 4
```
**Ex2: Giữ lại 2 chữ số thập phân**
```sql
SELECT ROUND(3.14159, 2); -- 3.14
```
**Ex3: Làm tròn sang hàng chục, trăm**
```bash
SELECT ROUND(127, -1); -- 130

SELECT ROUND(1567, -2); -- 1600
``` 
## TRUNCATE()
# Time (Nhóm thời gian)
## WEEK()
```bash
- Để lấy số tuần trong năm từ một ngày.
```
**Syn**
```bash
WEEK(date, mode])

- Input:
  + date: ngày cần tính
  + mode (tuỳ chọn): cách tính tuần
    - 0	Chủ nhật	tuần có ngày 1/1
    - 1	Thứ 2	tuần có ≥ 4 ngày (ISO gần chuẩn)
    - 2	Chủ nhật	tuần có ≥ 4 ngày
    - 3	Thứ 2	tuần có ngày 1/1
    - 4–7	các biến thể khác
```
**Ex**
```bash
SELECT 
  WEEK('2026-01-01', 0) AS mode0,
  WEEK('2026-01-01', 1) AS mode1;
```
## YEARWEEK() 
```bash
Dùng để lấy năm + tuần (year + week number) từ một giá trị ngày (DATE, DATETIME).
```
**Syn**
```bash
YEARWEEK(date, mode)

- Input:
  + date: ngày cần xử lý
  + mode (tùy chọn): quy định cách tính tuần (quan trọng)
    - 0 (default)	Tuần bắt đầu CN
    - 1	Tuần bắt đầu Thứ 2
    - 2	ISO (tuần đầu tiên có ít nhất 4 ngày)
    - 3	ISO + bắt đầu Thứ 2 (hay dùng nhất)
```
**Ex**
```sql
SELECT YEARWEEK('2026-04-15', 1); -- 202615
-- → nghĩa là: tuần 15 của năm 2026
```
## YEAR()
```bash
Lấy năm từ kiểu Lấy năm từ kiểu DATE, DATETIME, TIMESTAMP
```
**Ex**
```sql
SELECT YEAR('2026-04-11'); -- 2026
```
## MONTH() 
```bash
- lấy tháng từ ngày
- Công dụng lấy tháng (1 → 12)
```
**Ex**
```sql
SELECT MONTH('2026-04-11'); -- 4
```
# COALESCE() (xử lý NULL)
```bash
Công dụng trả về giá trị KHÔNG NULL đầu tiên
```
**Syn**
```bash
COALESCE(value1, value2, value3, ...)
```
**Ex**
```sql
SELECT COALESCE(NULL, NULL, 10, 20); -- 10
```
# char_length()
```bash
Trả về số ký tự trong chuỗi
```
**Ex**
```sql
SELECT tweet_id
FROM Tweets
WHERE CHAR_LENGTH(content) > 15;
```
# Process
## Case ... When ... then ... else ... end (biểu thức điều kiện)
```bash
CASE
    ↓
    bắt đầu biểu thức điều kiện

WHEN
    ↓
    điều kiện 1

THEN
    ↓
    giá trị trả về nếu đúng

ELSE
    ↓
    giá trị mặc định

END
    ↓
    kết thúc biểu thức
```
**Ex**
```sql
CASE
    WHEN score >= 8 THEN 'Giỏi'
    WHEN score >= 5 THEN 'Đạt'
    ELSE 'Trượt'
END
```
## if()