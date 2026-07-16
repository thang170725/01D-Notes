- [Create \& Config (Tạo \& Cấu hình)](#create--config-tạo--cấu-hình)
  - [mkdir \& touch](#mkdir--touch)
- [Display (Cung cấp thông tin)](#display-cung-cấp-thông-tin)
  - [ls](#ls)
  - [pwd](#pwd)
  - [cat](#cat)
- [Remove (Xóa)](#remove-xóa)
  - [rmdir](#rmdir)
- [chmod (change mode, dùng để thay đổi quyền (permission) của file hoặc thư mục trên Linux/macOS.](#chmod-change-mode-dùng-để-thay-đổi-quyền-permission-của-file-hoặc-thư-mục-trên-linuxmacos)
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
# chmod (change mode, dùng để thay đổi quyền (permission) của file hoặc thư mục trên Linux/macOS.

Ví dụ:

chmod +x run.sh

Nghĩa là:

Thêm quyền execute (x) để file run.sh có thể được chạy như một chương trình.

Ví dụ dễ hiểu

Bạn có file:

run.sh

Nội dung:

#!/bin/bash

echo "Hello World"

Nếu chạy:

./run.sh

có thể gặp lỗi:

Permission denied

vì file chưa có quyền thực thi.

Thêm quyền:

chmod +x run.sh

Bây giờ:

./run.sh

Kết quả:

Hello World
Xem quyền của file

Dùng:

ls -l

Ví dụ:

-rw-r--r-- 1 user user 120 Jul 9 run.sh

Phần đầu:

-rw-r--r--

chính là quyền của file.

Sau khi:

chmod +x run.sh

sẽ thành:

-rwxr-xr-x

Có thêm chữ x (execute).

Ý nghĩa của r, w, x
r = read     (đọc)
w = write    (ghi)
x = execute  (thực thi)

Ví dụ:

-rwxr-xr--

Tách thành 3 nhóm:

- rwx r-x r--
  │   │   │
  │   │   └── Người khác (others)
  │   └────── Nhóm (group)
  └────────── Chủ sở hữu (owner)
Dùng số để cấp quyền

Ngoài +x, còn có cách dùng số.

Giá trị:

r = 4
w = 2
x = 1

Ví dụ:

chmod 755 run.sh

Tương đương:

Owner : rwx = 7 = 4+2+1
Group : r-x = 5 = 4+1
Other : r-x = 5 = 4+1

Kết quả:

-rwxr-xr-x

Ví dụ:

chmod 644 test.txt

thì:

-rw-r--r--

Owner được đọc và ghi, còn group và others chỉ được đọc.

Một số lệnh thường gặp
chmod +x file.sh      # Thêm quyền chạy

chmod -x file.sh      # Bỏ quyền chạy

chmod 755 file.sh     # rwxr-xr-x

chmod 644 file.txt    # rw-r--r--

chmod 777 file.sh     # rwxrwxrwx (không nên dùng trong thực tế vì quá rộng quyền)
Tóm tắt
chmod = thay đổi quyền truy cập file/thư mục.
+x = thêm quyền thực thi.
ls -l = xem quyền hiện tại.
755, 644 là cách biểu diễn quyền bằng số, rất phổ biến trong Linux.