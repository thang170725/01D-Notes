- [Display (Nhóm cung cấp thông tin)](#display-nhóm-cung-cấp-thông-tin)
  - [.listdir() (Liệt kê tên file/thư mục trong thư mục)](#listdir-liệt-kê-tên-filethư-mục-trong-thư-mục)
  - [.getcwd() (Trả về đường dẫn hiện tại)](#getcwd-trả-về-đường-dẫn-hiện-tại)
  - [os.cpu\_count() (trả về Số lõi CPU mà Python nhìn thấy trên máy)](#oscpu_count-trả-về-số-lõi-cpu-mà-python-nhìn-thấy-trên-máy)
- [os.path (Nhóm làm việc với đường dẫn)](#ospath-nhóm-làm-việc-với-đường-dẫn)
  - [.dirname() (Lấy thư mục cha của file hoặc thư mục)](#dirname-lấy-thư-mục-cha-của-file-hoặc-thư-mục)
  - [.abspath() (đổi đường dẫn thành đường dẫn tuyệt đối (absolute path))](#abspath-đổi-đường-dẫn-thành-đường-dẫn-tuyệt-đối-absolute-path)
  - [.join() (Ghép đường dẫn)](#join-ghép-đường-dẫn)
  - [.basename() (Dùng để lấy tên file hoặc tên thư mục cuối cùng từ một đường dẫn)](#basename-dùng-để-lấy-tên-file-hoặc-tên-thư-mục-cuối-cùng-từ-một-đường-dẫn)
  - [os.path.splitext() (Dùng để tách tên file và phần mở rộng)](#ospathsplitext-dùng-để-tách-tên-file-và-phần-mở-rộng)
  - [check (kiểm tra)](#check-kiểm-tra)
    - [.path.exists() (Dùng để kiểm tra xem một đường dẫn (file hoặc thư mục) có tồn tại hay không)](#pathexists-dùng-để-kiểm-tra-xem-một-đường-dẫn-file-hoặc-thư-mục-có-tồn-tại-hay-không)
    - [.path.isfile() (Chỉ kiểm tra file)](#pathisfile-chỉ-kiểm-tra-file)
  - [.path.isdir() (Chỉ kiểm tra thư mục)](#pathisdir-chỉ-kiểm-tra-thư-mục)
- [Create \& Config (Nhóm tạo \& cấu hình)](#create--config-nhóm-tạo--cấu-hình)
  - [.mkdir()](#mkdir)
  - [os.makedirs() (Tạo thư mục, kể cả khi các thư mục cha chưa tồn tại)](#osmakedirs-tạo-thư-mục-kể-cả-khi-các-thư-mục-cha-chưa-tồn-tại)
  - [getenv](#getenv)
- [Process](#process)
  - [.chdir()](#chdir)
  - [relpath()](#relpath)
  - [system()](#system)
  - [name](#name)
  - [sep](#sep)
  - [pathsep](#pathsep)
- [Remove (Thao tác xóa)](#remove-thao-tác-xóa)
  - [os.remove() (xóa file)](#osremove-xóa-file)
---
# Display (Nhóm cung cấp thông tin)
## .listdir() (Liệt kê tên file/thư mục trong thư mục)
**Ex1**
```python
import os
print(os.listdir('.')) # ['test.py', 'output.txt', 'images', '.venv', 'input.txt']
```
**Ex2: liệt kê tất cả các file .txt trong thư mục**
```python
import os
for filename in os.listdir("."):
    if filename.endswith(".txt"):
        print(filename)
```
## .getcwd() (Trả về đường dẫn hiện tại)
**Syn**
```bash
os.getcwd()
```
## os.cpu_count() (trả về Số lõi CPU mà Python nhìn thấy trên máy)
**Ex**
```python
import os

print(os.cpu_count()) # 
```
# os.path (Nhóm làm việc với đường dẫn)
## .dirname() (Lấy thư mục cha của file hoặc thư mục)
**Ex1: Lấy thư mục cha**
```python
print(os.path.dirname("/data/images/cat.jpg")) # /data/images
```
**Ex2: lùi 2 cấp thư mục**
```python
import os

BASE_DIR_1 = os.path.dirname(__file__) 
BASE_DIR_2 = os.path.dirname(BASE_DIR_1) 

print(__file__)
print(BASE_DIR_1) 
print(BASE_DIR_2)
# (.venv) thang@PhatToNhuLai:~/workspace/lightgbm/backend$ python test.py
# /home/thang/workspace/lightgbm/backend/test.py
# /home/thang/workspace/lightgbm/backend
# /home/thang/workspace/lightgbm
```
## .abspath() (đổi đường dẫn thành đường dẫn tuyệt đối (absolute path))
**Syn**
```bash
os.path.abspath(path)

- Input:
  + path  : đường dẫn tương đối hoặc file
```
**Ex1: chuyển 1 đường dẫn tương đối thành đường dẫn tuyệt đối**
```python
import os

cur_path = os.path.abspath("utils/test.py")
print(cur_path)
# (.venv) thang@PhatToNhuLai:~/workspace/lightgbm/backend$ python test.py
# /home/thang/workspace/lightgbm/backend/utils/test.py
```
**Ex2: Lưu ý abspath gặp / thì giữ nguyên**
```python
import os

print(os.path.abspath("/backend/utils.py")) # /backend/utils.py
```
## .join() (Ghép đường dẫn)
**Syn**
```bash
img_path = os.path.join(input_folder, img_name)
```
**Ex**
```python
import os

base_url = os.path.dirname(__file__)
print(os.path.join(base_url, "docs/dataset.txt")) # /home/thang/workspace/lightgbm/backend/docs/dataset.txt
```
## .basename() (Dùng để lấy tên file hoặc tên thư mục cuối cùng từ một đường dẫn)
**Syn**
```bash
import os

os.path.basename(path)
```
**Ex1: lấy file**
```python
import os

path = "dataset/train/cat.jpg"

print(os.path.basename(path)) # cat.jpg
```
**Ex2: lấy tên thư mục**
```python
path = "dataset/train"

print(os.path.basename(path)) # train
```
## os.path.splitext() (Dùng để tách tên file và phần mở rộng)
**Syn**
```bash

- Output: Nó trả về tuple gồm: (filename, extension)
```
**Ex**
```python
import os

path = "cat.jpg"

print(os.path.splitext(path)) # ('cat', '.jpg')
```
os.path.relpath() dùng để lấy đường dẫn tương đối (relative path) từ một thư mục gốc đến một file hoặc thư mục khác.

Cú pháp
os.path.relpath(path, start)
path: đường dẫn cần chuyển.
start: thư mục làm mốc (mặc định là thư mục hiện tại .).

Giá trị trả về là đường dẫn tương đối.

Ví dụ 1: Cơ bản
import os

path = r"D:\workspace\project\data\images\img1.jpg"
start = r"D:\workspace\project"

result = os.path.relpath(path, start)

print(result)

Kết quả

data\images\img1.jpg

Nó đã bỏ phần chung D:\workspace\project.

Ví dụ 2: Trong dự án YOLO

Giả sử cấu trúc:

project/
│
├── data/
│   ├── images/
│   │   ├── a.jpg
│   │   └── train/
│   │       └── b.jpg
│   │
│   └── labels/

Bạn duyệt bằng os.walk():

import os

image_root = "data/images"

for root, dirs, files in os.walk(image_root):
    for file in files:
        full_path = os.path.join(root, file)

        rel_path = os.path.relpath(full_path, image_root)

        print(rel_path)

Kết quả

a.jpg
train\b.jpg

Đây là cách rất hay để giữ nguyên cấu trúc thư mục.

Ví dụ 3: Tạo thư mục labels tương ứng

Giả sử

images/
│
├── train/
│     img1.jpg
│
└── test/
      img2.jpg

Muốn tạo

labels/
│
├── train/
│
└── test/

Code

import os

image_root = "images"
label_root = "labels"

for root, dirs, files in os.walk(image_root):

    rel_dir = os.path.relpath(root, image_root)

    label_dir = os.path.join(label_root, rel_dir)

    print(label_dir)

Kết quả

labels\.
labels\train
labels\test

Thường sẽ dùng tiếp

os.makedirs(label_dir, exist_ok=True)
Ví dụ 4: Đổi từ ảnh sang label
import os

image_path = r"data/images/train/img001.jpg"

relative = os.path.relpath(image_path, "data/images")

print(relative)

Kết quả

train\img001.jpg

Sau đó

label_path = os.path.join(
    "data/labels",
    os.path.splitext(relative)[0] + ".txt"
)

print(label_path)

Kết quả

data/labels/train/img001.txt

Đây là cách rất phổ biến trong các dự án YOLO.

Ví dụ 5: start mặc định

Nếu không truyền start

import os

print(os.path.relpath(r"D:\test\a.txt"))

thì Python sẽ lấy thư mục làm việc hiện tại (os.getcwd()) làm mốc.

Ví dụ nếu:

Current folder:
D:\workspace

thì kết quả

..\test\a.txt
Kết hợp os.walk() và relpath()

Đây là mẫu code rất thường gặp:

import os

source = "images"

for root, dirs, files in os.walk(source):
    for file in files:

        full_path = os.path.join(root, file)

        relative_path = os.path.relpath(full_path, source)

        print(relative_path)

Nếu có cấu trúc:

images/
├── a.jpg
├── train/
│   ├── b.jpg
│   └── c.jpg
└── test/
    └── d.jpg

Thì kết quả là:

a.jpg
train\b.jpg
train\c.jpg
test\d.jpg

Đây là lý do relpath() thường được dùng cùng os.walk(): os.walk() giúp lấy đường dẫn đầy đủ của từng file, còn relpath() chuyển chúng thành đường dẫn tương đối, giúp bạn dễ dàng tái tạo cấu trúc thư mục ở nơi khác hoặc ánh xạ giữa images/ và labels/ trong các dự án như YOLO.
## check (kiểm tra)
### .path.exists() (Dùng để kiểm tra xem một đường dẫn (file hoặc thư mục) có tồn tại hay không)
**Syn**
```bash
import os

os.path.exists(path)
```
**Ex1: Kiểm tra file**
```python
import os

if os.path.exists("data.txt"):
    print("File tồn tại")
else:
    print("File không tồn tại")
```
**Ex2: Kiểm tra thư mục**
```python
import os

if os.path.exists("logs"):
    print("Thư mục tồn tại")
```
### .path.isfile() (Chỉ kiểm tra file)
**Syn**
```bash
os.path.isfile("data.txt")
```
## .path.isdir() (Chỉ kiểm tra thư mục)
**Syn**
```bash
os.path.isdir("logs")
```
**Ex**
```python
path = "example"

if os.path.exists(path):
    if os.path.isfile(path):
        print("Là file")
    elif os.path.isdir(path):
        print("Là thư mục")
```
# Create & Config (Nhóm tạo & cấu hình)
## .mkdir()
**Ex: Tạo file/thư mục nếu chưa tồn tại**
```python
import os

if not os.path.exists("output"):
    os.mkdir("output")
```
## os.makedirs() (Tạo thư mục, kể cả khi các thư mục cha chưa tồn tại)
**Syn**
```bash
os.makedirs(name, mode=0o777, exist_ok=False)

- Input:
  + name	    : Đường dẫn thư mục cần tạo
  + mode	    : Quyền truy cập (Linux/macOS)
  + exist_ok	: Có báo lỗi nếu thư mục đã tồn tại không
    - True: Chưa có → tạo. Đã có → bỏ qua.
```
**Ex1: Tạo một thư mục**
```python
import os

os.makedirs("output")
# project/
# └── output/
```
**Ex2: Tạo nhiều cấp thư mục**
```python
import os

os.makedirs("build/pdf/output")
# build/
# └── pdf/
#     └── output/
# Nếu build và pdf chưa tồn tại thì Python sẽ tự tạo.
```
## getenv
```bash
- Biến môi trường thường dùng để:
  + Lưu cấu hình (API key, DB URL, port…)
  + Tránh hard-code giá trị nhạy cảm trong code
  + Dễ thay đổi theo môi trường (dev / test / production)
=> getenv giúp bạn đọc các giá trị này trong runtime
```
**Syn**
```bash
import os

os.getenv(key, default=None)

- key: tên biến môi trường
- default: giá trị mặc định nếu biến không tồn tại (optional)
``` 
**Ex**
```python
import os

port = os.getenv("PORT", "3000")

print(port)
```
# Process
## .chdir()
```bash
Chuyển đến thư mục khác
```
**Syn**
```bash
os.chdir("C:/Users/Thang/Documents")
```
makefirs()
rmdir()
removedirs()
Rename()
Stat()
path
## relpath()
## system()
## name
## sep
## pathsep
os.walk() dùng để duyệt toàn bộ cây thư mục (folder và các thư mục con). Đây là hàm rất hay dùng khi xử lý dataset, ví dụ như YOLO.

Cú pháp
import os

for root, dirs, files in os.walk(path):
    ...

Trong đó:

root: đường dẫn của thư mục hiện tại.
dirs: danh sách các thư mục con trong root.
files: danh sách các file trong root.
Ví dụ 1: In toàn bộ file

Giả sử cấu trúc thư mục:

dataset/
│
├── images/
│   ├── a.jpg
│   ├── b.jpg
│   └── train/
│       ├── c.jpg
│       └── d.jpg
│
└── labels/
    ├── a.txt
    └── b.txt

Code:

import os

for root, dirs, files in os.walk("dataset"):
    print("Thư mục:", root)

    print("Folder con:", dirs)

    print("File:", files)

    print("-" * 40)

Kết quả:

Thư mục: dataset
Folder con: ['images', 'labels']
File: []

----------------------------------------

Thư mục: dataset/images
Folder con: ['train']
File: ['a.jpg', 'b.jpg']

----------------------------------------

Thư mục: dataset/images/train
Folder con: []
File: ['c.jpg', 'd.jpg']

----------------------------------------

Thư mục: dataset/labels
Folder con: []
File: ['a.txt', 'b.txt']
Ví dụ 2: Lấy toàn bộ ảnh jpg
import os

for root, dirs, files in os.walk("dataset"):
    for file in files:
        if file.endswith(".jpg"):
            print(os.path.join(root, file))

Kết quả

dataset/images/a.jpg
dataset/images/b.jpg
dataset/images/train/c.jpg
dataset/images/train/d.jpg

os.path.join() sẽ ghép đường dẫn đúng theo hệ điều hành.

Ví dụ 3: Đếm số lượng ảnh
import os

count = 0

for root, dirs, files in os.walk("dataset"):
    for file in files:
        if file.lower().endswith((".jpg", ".png", ".jpeg")):
            count += 1

print("Số ảnh:", count)
Ví dụ 4: Lấy tên file và đường dẫn
import os

for root, dirs, files in os.walk("dataset"):
    for file in files:

        full_path = os.path.join(root, file)

        print("Tên file :", file)
        print("Đường dẫn:", full_path)

Ví dụ:

Tên file : c.jpg
Đường dẫn: dataset/images/train/c.jpg
Ví dụ 5: Chỉ duyệt các file .txt
import os

for root, dirs, files in os.walk("dataset"):
    for file in files:
        if file.endswith(".txt"):
            print(file)

Kết quả

a.txt
b.txt
Ví dụ 6: Rất hay dùng trong YOLO

Giả sử bạn muốn lấy tất cả ảnh trong dataset:

import os

image_paths = []

for root, dirs, files in os.walk("dataset"):
    for file in files:
        if file.lower().endswith((".jpg", ".jpeg", ".png")):
            image_paths.append(os.path.join(root, file))

print(len(image_paths))

Sau đó có thể dùng:

for image_path in image_paths:
    print(image_path)
os.walk() hoạt động như thế nào?

Mỗi vòng lặp, nó trả về một bộ ba (root, dirs, files).

Ví dụ với cấu trúc:

dataset/
│
├── train/
│   ├── img1.jpg
│   └── img2.jpg
│
└── valid/
    └── img3.jpg

Các lần lặp sẽ là:

root = "dataset"
dirs = ["train", "valid"]
files = []

↓

root = "dataset/train"
dirs = []
files = ["img1.jpg", "img2.jpg"]

↓

root = "dataset/valid"
dirs = []
files = ["img3.jpg"]
So sánh với glob

Nếu chỉ muốn lấy ảnh trong một thư mục, glob thường ngắn gọn hơn:

from glob import glob

images = glob("dataset/*.jpg")

Nếu muốn lấy cả các thư mục con:

from glob import glob

images = glob("dataset/**/*.jpg", recursive=True)

Còn os.walk() linh hoạt hơn vì ngoài file, bạn còn có thể xử lý thư mục (dirs), lọc theo nhiều điều kiện hoặc thay đổi cách duyệt trong quá trình lặp. Vì vậy trong các dự án xử lý dữ liệu lớn hoặc xây dựng pipeline, os.walk() thường được dùng nhiều hơn.
# Remove (Thao tác xóa)
## os.remove() (xóa file)
