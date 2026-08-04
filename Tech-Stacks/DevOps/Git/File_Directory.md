- [cd (Thay đổi thư mục làm việc)](#cd-thay-đổi-thư-mục-làm-việc)
- [dir | ls (Hiển thị danh sách tập tin)](#dir--ls-hiển-thị-danh-sách-tập-tin)
- [clear (dọn dẹp câu lệnh)](#clear-dọn-dẹp-câu-lệnh)
- [mkdir (Tạo thư mục)](#mkdir-tạo-thư-mục)
- [rm](#rm)
  - [–d (xóa một thư mục rỗng)](#d-xóa-một-thư-mục-rỗng)
  - [–r](#r)
- [echo (ghi dữ liệu vào file)](#echo-ghi-dữ-liệu-vào-file)
- [touch (tạo file)](#touch-tạo-file)
- [cat (hiển thị nội dung file)](#cat-hiển-thị-nội-dung-file)
- [.git (file ghi lại lịch sử)](#git-file-ghi-lại-lịch-sử)
- [.gitignore (hạn chế thư mục commit)](#gitignore-hạn-chế-thư-mục-commit)
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
# echo (ghi dữ liệu vào file)
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
**Ex**
```bash
cat a.txt
```
# .git (file ghi lại lịch sử)
**Ex: Xóa .git và init lại từ đầu để xóa toàn bộ lịch sử repo**
```bash
1. Xóa thư mục git
  rm -rf .git # linux
  Remove-Item .git -Recurse -Force # Windows
2. Init lại
  git init
  git add .
  git commit -m "Initial commit"
  git remote add origin <repo-url>
  git push -f origin main
```
# .gitignore (hạn chế thư mục commit)
**Hạn chế thư mục push lên gitHub**
```bash
~/workspace/lightgbm
├── backend
│   └── dataset
├── docs
├── frontend
└── README.md
```
```bash
Muốn backend/dataset không push lên Git.

Bước 1: đứng ở root project
    - cd ~/workspace/lightgbm
Bước 2: tạo .gitignore
    - touch .gitignore
Bước 3: mở file .gitignore
    1. nano .gitignore
    2.  thêm dòng này: backend/dataset/
    3.  Lưu: Ctrl + O → Enter, Ctrl + X
Bước 4: kiểm tra
    - cat .gitignore
    - phải ra: backend/dataset/
Bước 5: add code
    - git add .
    - dataset sẽ bị bỏ qua.
    - Kiểm tra: git status (sẽ không thấy backend/dataset)
    - .gitignore cho project bạn có thể sau này mở rộng:
        backend/dataset/
        __pycache__/
        *.pyc
        .env
        venv/
```