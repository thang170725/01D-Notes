- [Path (Tạo đối tượng)](#path-tạo-đối-tượng)
  - [.mkdir (Tạo thư mục)](#mkdir-tạo-thư-mục)
  - [.cwd() (thư mục làm việc hiện tại)](#cwd-thư-mục-làm-việc-hiện-tại)
  - [.iterdir() (Nó sẽ duyệt tất cả file và thư mục con)](#iterdir-nó-sẽ-duyệt-tất-cả-file-và-thư-mục-con)
  - [is\_dir() (Kiểm tra có phải thư mục không)](#is_dir-kiểm-tra-có-phải-thư-mục-không)
  - [exists() (Kiểm tra file có tồn tại không)](#exists-kiểm-tra-file-có-tồn-tại-không)
  - [name (Lấy tên cuối cùng)](#name-lấy-tên-cuối-cùng)
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
print(type(path)) # Lúc này path không còn là chuỗi nữa. <class 'pathlib.WindowsPath'>
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
## exists() (Kiểm tra file có tồn tại không)
**Ex**
```python
from pathlib import Path

file = Path("abc.txt")

print(file.exists())
# Nếu có: True
# Không có: False
```
## name (Lấy tên cuối cùng)
**Ex**
```python
folder = Path("F:/jj/output/tables/abc123")
print(folder.name) # abc123

file = Path("tables/test.json")
print(file.name) # test.json
```