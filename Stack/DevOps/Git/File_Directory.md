- [cd (Thay đổi thư mục làm việc)](#cd-thay-đổi-thư-mục-làm-việc)
- [dir | ls (Hiển thị danh sách tập tin)](#dir--ls-hiển-thị-danh-sách-tập-tin)
- [clear (dọn dẹp câu lệnh)](#clear-dọn-dẹp-câu-lệnh)
- [mkdir (Tạo thư mục)](#mkdir-tạo-thư-mục)
- [rm](#rm)
  - [–d (xóa một thư mục rỗng)](#d-xóa-một-thư-mục-rỗng)
  - [–r](#r)
- [echo (tạo file)](#echo-tạo-file)
- [touch (tạo file)](#touch-tạo-file)
- [cat (hiển thị nội dung file)](#cat-hiển-thị-nội-dung-file)
---
# cd (Thay đổi thư mục làm việc)
**Ex: Quay về  một cấp**
```bash
cd ..
```
# dir | ls (Hiển thị danh sách tập tin)
```bash
1. dir – in ra chữ màu trắng
2. ls- in ra chữ màu xanh (dễ nhìn hơn)
```
# clear (dọn dẹp câu lệnh)
# mkdir (Tạo thư mục)
```bash
mkdir text # Tạo ra một folder tên là text
```
# rm 
**Ex: xóa file**
```bash
rm name.txt # File name.txt sẽ bị xóa
```
## –d (xóa một thư mục rỗng)
```bash
rm –d EX1 # Thư mục rỗng EX1 bị xóa
```
## –r
```bash
Để xóa thư mục có dữ liệu.
```
**Ex**
```bash 
rm –r EX1 # Thư mục EX1 sẽ bị xóa
```
# echo (tạo file)
**Ex1: không ghi đề**
```bash
echo “text” >> name.txt # Tạo file name.txt có nội dung là text, không ghi đè.
```
**Ex2: ghi đè**
```bash
echo “text” > name.txt # Tạo file name.txt có nội dung là text,ghi đè nếu đã có nội dung từ trước.
```
# touch (tạo file)
```bash
touch listName.txt # Tạo ra một file tên là listName.txt
```
# cat (hiển thị nội dung file)