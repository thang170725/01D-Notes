- [Select](#select)
  - [Hiển thị nhiều field của nhiều bảng](#hiển-thị-nhiều-field-của-nhiều-bảng)
  - [Hiển thị nhiều field của nhiều bảng có điều kiện](#hiển-thị-nhiều-field-của-nhiều-bảng-có-điều-kiện)
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