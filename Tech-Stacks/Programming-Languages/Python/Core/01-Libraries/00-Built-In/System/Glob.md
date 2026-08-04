# Glob Introduction (dùng để tìm kiếm file hoặc thư mục theo mẫu (pattern))
```bash
Glob là thư viện chuẩn (standard library) của Python.
    Bạn không cần cài đặt. Chỉ cần: import glob -> là dùng được.
```
**glob dùng để làm gì?**
```bash
Nó giúp tìm file theo ký tự đại diện (*, ?, []) thay vì phải biết chính xác tên file.
```
**Syn**
```bash
glob.glob(pattern, recursive=True)
```
**Ex**
```bash
dataset/
    cat1.jpg
    cat2.jpg
    dog1.jpg
    dog2.jpg
```
```python
import glob

files = glob.glob("dataset/*.jpg") # Lấy tất cả file .jpg
print(files)
# [
#     'dataset/cat1.jpg',
#     'dataset/cat2.jpg',
#     'dataset/dog1.jpg',
#     'dataset/dog2.jpg'
# ]
```
# .glob()
**Ex1: Chỉ lấy file bắt đầu bằng cat**
```python
glob.glob("dataset/cat*.jpg") # ['dataset/cat1.jpg', 'dataset/cat2.jpg']
```
**Ex2: Lấy mọi file .png**
```python
glob.glob("images/*.png")
```
**Ex3: Tìm trong tất cả thư mục con**
```bash
dataset/
    train/
        a.jpg
    val/
        b.jpg
```
```python
glob.glob("dataset/**/*.jpg", recursive=True)
# [
#     'dataset/train/a.jpg',
#     'dataset/val/b.jpg'
# ]
```


Ví dụ 1: Không dùng recursive

Giả sử có cấu trúc:

dataset/
│
├── cat.jpg
├── dog.jpg
│
├── train/
│   ├── a.jpg
│   └── b.jpg
│
└── val/
    └── c.jpg

Code:

import glob

files = glob.glob("dataset/*.jpg")
print(files)

Kết quả:

[
    'dataset/cat.jpg',
    'dataset/dog.jpg'
]

👉 Chỉ lấy file trong dataset, không vào train/ và val/.

Ví dụ 2: Dùng recursive=True
import glob

files = glob.glob("dataset/**/*.jpg", recursive=True)
print(files)

Kết quả:

[
    'dataset/cat.jpg',
    'dataset/dog.jpg',
    'dataset/train/a.jpg',
    'dataset/train/b.jpg',
    'dataset/val/c.jpg'
]

👉 Lấy luôn các file trong mọi thư mục con.

Ý nghĩa của **
* → khớp với mọi tên file hoặc thư mục trong một cấp.
** → khớp với mọi cấp thư mục (chỉ có tác dụng khi recursive=True).

Ví dụ:

glob.glob("images/*")

Chỉ tìm trong images/.

Còn:

glob.glob("images/**/*.png", recursive=True)

Tìm tất cả file .png trong images và mọi thư mục con của nó.

Ví dụ thực tế trong AI

Đọc toàn bộ ảnh trong dataset:

dataset/
    train/
        cat/
        dog/
    val/
        cat/
        dog/
import glob

images = glob.glob("dataset/**/*.jpg", recursive=True)

for img in images:
    print(img)

Sẽ lấy được tất cả ảnh ở mọi thư mục con mà không cần biết trước cấu trúc thư mục.

Tóm tắt
Cú pháp	Kết quả
glob.glob("*.jpg")	Tìm .jpg trong thư mục hiện tại
glob.glob("images/*.jpg")	Tìm .jpg trong images
glob.glob("images/**/*.jpg", recursive=True)	Tìm .jpg trong images và tất cả thư mục con
recursive=False (mặc định)	Không tìm đệ quy
recursive=True	Cho phép ** tìm xuyên qua mọi cấp thư mục

Lưu ý: Chỉ đặt recursive=True thôi không đủ. Bạn cũng cần dùng ** trong mẫu tìm kiếm. Ví dụ:

glob.glob("dataset/*.jpg", recursive=True)

vẫn không tìm trong thư mục con. Muốn tìm đệ quy phải viết:

glob.glob("dataset/**/*.jpg", recursive=True)