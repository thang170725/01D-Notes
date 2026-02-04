- [insert into](#insert-into)
- [delete](#delete)
---
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
```bash
dùng để xóa dữ liệu (record/row) trong bảng.
```
**Syn**
```bash
DELETE FROM ten_bang
WHERE dieu_kien;
```