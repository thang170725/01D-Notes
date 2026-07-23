- [os.path (Nhóm làm việc với đường dẫn)](#ospath-nhóm-làm-việc-với-đường-dẫn)
  - [.dirname() (Lấy thư mục cha của file hoặc thư mục)](#dirname-lấy-thư-mục-cha-của-file-hoặc-thư-mục)
  - [.abspath() (đổi đường dẫn thành đường dẫn tuyệt đối (absolute path))](#abspath-đổi-đường-dẫn-thành-đường-dẫn-tuyệt-đối-absolute-path)
  - [.join() (Ghép đường dẫn)](#join-ghép-đường-dẫn)
- [Create \& Config (Nhóm tạo \& cấu hình)](#create--config-nhóm-tạo--cấu-hình)
  - [.mkdir()](#mkdir)
  - [.path.exists()](#pathexists)
  - [os.makedirs() (Tạo thư mục, kể cả khi các thư mục cha chưa tồn tại)](#osmakedirs-tạo-thư-mục-kể-cả-khi-các-thư-mục-cha-chưa-tồn-tại)
  - [getenv](#getenv)
- [Check](#check)
  - [.path.isfile()](#pathisfile)
  - [.path.isdir()](#pathisdir)
- [Search](#search)
- [Display (Nhóm cung cấp thông tin)](#display-nhóm-cung-cấp-thông-tin)
  - [.listdir()](#listdir)
  - [.getcwd()](#getcwd)
  - [os.cpu\_count() (trả về Số lõi CPU mà Python nhìn thấy trên máy)](#oscpu_count-trả-về-số-lõi-cpu-mà-python-nhìn-thấy-trên-máy)
- [Process](#process)
  - [.chdir()](#chdir)
  - [splitext()](#splitext)
  - [relpath()](#relpath)
  - [system()](#system)
  - [name](#name)
  - [sep](#sep)
  - [pathsep](#pathsep)
- [Remove (Thao tác xóa)](#remove-thao-tác-xóa)
  - [os.remove() (xóa file)](#osremove-xóa-file)
---
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
# Create & Config (Nhóm tạo & cấu hình)
## .mkdir()
**Ex: Tạo file/thư mục nếu chưa tồn tại**
```python
import os

if not os.path.exists("output"):
    os.mkdir("output")
```
## .path.exists()
```bash
- Dùng để kiểm tra xem một đường dẫn (file hoặc thư mục) có tồn tại hay không.
```
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
## os.makedirs() (Tạo thư mục, kể cả khi các thư mục cha chưa tồn tại)
**Syn**
```bash
os.makedirs(name, mode=0o777, exist_ok=False)

- Input:
  + name	    : Đường dẫn thư mục cần tạo
  + mode	    : Quyền truy cập (Linux/macOS)
  + exist_ok	: Có báo lỗi nếu thư mục đã tồn tại không
    - Lỗi thường gặp
      os.makedirs("output")
      os.makedirs("output")
      Lần thứ hai sẽ lỗi: FileExistsError: [Errno 17] File exists: 'output'
    - Cách xử lý bằng exist_ok=True. os.makedirs("output", exist_ok=True)
      Lúc này:
        Chưa có → tạo.
        Đã có → bỏ qua.
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
# Check 
## .path.isfile()
```bash
Chỉ kiểm tra file
```
**Syn**
```bash
os.path.isfile("data.txt")
```
## .path.isdir()
```bash
Chỉ kiểm tra thư mục
```
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
# Search

# Display (Nhóm cung cấp thông tin)
```bash
dùng để  hiển thị nhằm cung cấp thêm thông tin.
``` 
## .listdir()
```bash
Liệt kê tên file/thư mục trong thư mục.
```
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
## .getcwd()
```bash
Trả về đường dẫn hiện tại
```
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
Basename()
## splitext()
## relpath()
## system()
## name
## sep
## pathsep
# Remove (Thao tác xóa)
## os.remove() (xóa file)
