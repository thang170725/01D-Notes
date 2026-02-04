- [ls](#ls)
- [mkdir \& touch](#mkdir--touch)
---
# ls
```bash
- ls -r: Hiển thị tất cả các file trong các thư mục con.
- ls -a: Hiển thị các file ẩn.
- ls -al: sẽ liệt kê các file và thư mục với thông tin chi tiết như quyền, kích thước, chủ sở hữu, …
4. ls | wc -l       : Đếm TẤT CẢ (file + folder) trong thư mục cha (Ex: ls /home/user/test | wc -l)
5. ls -A | wc -l    : Đếm tất cả kể cả file ẩn
```
File + folder
find . | wc -l

Chỉ file
find . -type f | wc -l

Chỉ folder
find . -type d | wc -l
# mkdir & touch
```bash
- mkdir   : Tạo ra thư mục
- touch : Tạo file
**Syn: mkdir**
```bash
mkdir git_test
```
**Syn: touch**
```bash
touch index.html (Tao một file tên là index.html)
```
# pwd
```bash
Xem đường dẫn thư mục làm việc hiện tại.
```
# cat 
**Ex**
```bash
cat file.text # Liệt kê nội dung của file.txt
```
# rmdir a
```bash
xóa thư mục a, thư mục a phải là thư mục trống.
```