- [Create \& Config (Tạo \& Cấu hình)](#create--config-tạo--cấu-hình)
  - [mkdir \& touch](#mkdir--touch)
- [Display (Cung cấp thông tin)](#display-cung-cấp-thông-tin)
  - [ls](#ls)
  - [pwd](#pwd)
  - [cat](#cat)
- [Remove (Xóa)](#remove-xóa)
  - [rmdir](#rmdir)
- [chmod (change mode, dùng để thay đổi quyền (permission) của file hoặc thư mục trên Linux/macOS)](#chmod-change-mode-dùng-để-thay-đổi-quyền-permission-của-file-hoặc-thư-mục-trên-linuxmacos)
---
# Create & Config (Tạo & Cấu hình)
## mkdir & touch
```bash
- mkdir   : Tạo ra thư mục
- touch : Tạo file
**Syn: mkdir**
```bash
1. mkdir git_test
2. `mkdir -p path/to/dir` # Tạo thư mục tầng (Nested)
```
**Syn: touch**
```bash
touch index.html (Tao một file tên là index.html)
```
# Display (Cung cấp thông tin)
## ls
```bash
- ls -r: Hiển thị tất cả các file trong các thư mục con.
- ls -a: Hiển thị các file ẩn.
- ls -al: sẽ liệt kê các file và thư mục với thông tin chi tiết như quyền, kích thước, chủ sở hữu, …
4. ls | wc -l       : Đếm TẤT CẢ (file + folder) trong thư mục cha (Ex: ls /home/user/test | wc -l)
5. ls -A | wc -l    : Đếm tất cả kể cả file ẩn
6. `ls -lah`        # Liệt kê file chi tiết (Size, Hidden):** 
```
## pwd
```bash
Xem đường dẫn thư mục làm việc hiện tại.
```
## cat 
**Ex**
```bash
cat file.text # Liệt kê nội dung của file.txt
```
# Remove (Xóa)
## rmdir
```bash
xóa thư mục thư mục a phải là thư mục trống.
```
# chmod (change mode, dùng để thay đổi quyền (permission) của file hoặc thư mục trên Linux/macOS)
**Ex**
```bash
Bạn có file: run.sh
  Nội dung:
    #!/bin/bash
    echo "Hello World"

Nếu chạy: ./run.sh # có thể gặp lỗi: Permission denied vì file chưa có quyền thực thi.

Thêm quyền:
  chmod +x run.sh

Bây giờ: ./run.sh # Hello World
```