- [Path (Tạo đối tượng)](#path-tạo-đối-tượng)
  - [/ (nối đường dẫn)](#-nối-đường-dẫn)
  - [.parent (dùng để lấy thư mục cha (parent directory) của một đường dẫn)](#parent-dùng-để-lấy-thư-mục-cha-parent-directory-của-một-đường-dẫn)
  - [.mkdir (Tạo thư mục)](#mkdir-tạo-thư-mục)
  - [.cwd() (thư mục làm việc hiện tại)](#cwd-thư-mục-làm-việc-hiện-tại)
  - [.iterdir() (Nó sẽ duyệt tất cả file và thư mục con)](#iterdir-nó-sẽ-duyệt-tất-cả-file-và-thư-mục-con)
  - [is\_dir() (Kiểm tra có phải thư mục không)](#is_dir-kiểm-tra-có-phải-thư-mục-không)
  - [.exists() (Kiểm tra file có tồn tại không)](#exists-kiểm-tra-file-có-tồn-tại-không)
  - [.name (Lấy tên cuối cùng)](#name-lấy-tên-cuối-cùng)
  - [.glob() (dùng để tìm các file hoặc thư mục theo một mẫu (pattern))](#glob-dùng-để-tìm-các-file-hoặc-thư-mục-theo-một-mẫu-pattern)
  - [.rglob()](#rglob)
---
# Path (Tạo đối tượng)
```bash
Dùng để biến một chuỗi thành một đối tượng đường dẫn.
  Nó là một đối tượng nên có rất nhiều hàm tiện ích.
```
**Ex**
```python
from pathlib import Path

path = Path("F:/jj/output/tables")

print(path) # F:\jj\output\tables
print(type(path)) # <class 'pathlib.WindowsPath'>
```
## / (nối đường dẫn)
**Ex**
```python
BASE_DIR = Path(r"D:\workspace\filter_signature")
YAML_PATH = BASE_DIR / "yolo_augmented_data" / "data.yaml"
```
## .parent (dùng để lấy thư mục cha (parent directory) của một đường dẫn)
**Ex1: Đường dẫn nhiều cấp**
```python
from pathlib import Path

path = Path("C:/Users/Thang/Documents/Python/demo.py")

print(path.parent) # C:\Users\Thang\Documents\Python
```
**Ex2: Lấy nhiều cấp cha**
```python
from pathlib import Path

path = Path("C:/Users/Thang/Documents/Python/demo.py")

print(path.parent)                # C:\Users\Thang\Documents\Python
print(path.parent.parent)         # C:\Users\Thang\Documents
print(path.parent.parent.parent)  # C:\Users\Thang
```
**Ex3: Lấy cấp cha thứ i**
```python
from pathlib import Path

path = Path("C:/Users/Thang/Documents/Python/demo.py")

print(path.parents[0]) # C:\Users\Thang\Documents\Python
print(path.parents[1]) # C:\Users\Thang\Documents
print(path.parents[2]) # C:\Users\Thang
```
## .mkdir (Tạo thư mục)
**Syn**
```bash
folder.mkdir()

- exist_ok=True:
    + Nếu thư mục chưa có → tạo mới.
    + Nếu đã có → bỏ qua, không báo lỗi
- parents=True: tự động tạo các thư mục cha nếu chưa có
```
## .cwd() (thư mục làm việc hiện tại)
**Syn**
```bash

- Output: <class 'pathlib.PosixPath'>
```
**Ex**
```python
from pathlib import Path

current_dir = Path.cwd()

print(current_dir)
/home/thang/project
```
## .iterdir() (Nó sẽ duyệt tất cả file và thư mục con)
**Ex**
```bash
tables
│
├── folder1
├── folder2
├── folder3
├── abc.txt
```
```python
from pathlib import Path

root = Path("tables")

for item in root.iterdir():
    print(item)
# tables\folder1
# tables\folder2
# tables\folder3
# tables\abc.txt
```
## is_dir() (Kiểm tra có phải thư mục không)
**Ex**
```bash
tables
│
├── folder1
├── folder2
├── a.txt
```
```python
for item in Path("tables").iterdir():
    print(item)
    print(item.is_dir())
# tables\folder1
# True

# tables\folder2
# True

# tables\a.txt
# False
```
## .exists() (Kiểm tra file có tồn tại không)
**Ex**
```python
from pathlib import Path

file = Path("abc.txt")

print(file.exists())
# Nếu có: True
# Không có: False
```
## .name (Lấy tên cuối cùng)
**Ex**
```python
folder = Path("F:/jj/output/tables/abc123")
print(folder.name) # abc123

file = Path("tables/test.json")
print(file.name) # test.json
```
## .glob() (dùng để tìm các file hoặc thư mục theo một mẫu (pattern))
**Syn**
```bash

- Output: Object - interable (đối tượng có thể )
```
**Ex1: Tìm tất cả file .txt trong cha**
```bash
# Giả sử thư mục của bạn là
# project/
# │
# ├── a.txt
# ├── b.txt
# ├── c.pdf
# ├── image.png
```
```python
from pathlib import Path

folder = Path("project")

for file in folder.glob("*.txt"):
    print(file)
# project\a.txt
# project\b.txt
```
**Ex2: Tìm tất cả file**
```python
from pathlib import Path

folder = Path("project")

for file in folder.glob("*"):
    print(file)
# a.txt
# b.txt
# c.pdf
# image.png
```
**Ex3: Tìm thư mục con**
```python
Giả sử
# project/
# │
# ├── data/
# ├── images/
# ├── test.py

from pathlib import Path

folder = Path("project")

for item in folder.glob("*"):
    if item.is_dir():
        print(item)
# project\data
# project\images
```
## .rglob()
**Ex: đếm file pdf**
```python
folder = Path(folder_path)

count = 0
for _ in folder.rglob("*.pdf"):
    count += 1
```