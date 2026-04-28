- [os.path (Nhóm làm việc với đường dẫn)](#ospath-nhóm-làm-việc-với-đường-dẫn)
  - [.dirname()](#dirname)
  - [.abspath()](#abspath)
  - [.join()](#join)
- [Create \& Config (Nhóm tạo \& cấu hình)](#create--config-nhóm-tạo--cấu-hình)
  - [.mkdir()](#mkdir)
  - [getenv](#getenv)
- [Check](#check)
  - [.path.isfile()](#pathisfile)
  - [.path.isdir()](#pathisdir)
  - [.path.exists()](#pathexists)
- [Search](#search)
- [Display (Nhóm cung cấp thông tin)](#display-nhóm-cung-cấp-thông-tin)
  - [.listdir()](#listdir)
  - [.getcwd()](#getcwd)
- [Process](#process)
  - [.chdir()](#chdir)
  - [splitext()](#splitext)
  - [relpath()](#relpath)
  - [system()](#system)
  - [name](#name)
  - [sep](#sep)
  - [pathsep](#pathsep)
---
# os.path (Nhóm làm việc với đường dẫn)
## .dirname()
```bash
Lấy thư mục chứa file.
```
**Ex1**
```python
print(os.path.dirname("/data/images/cat.jpg")) # /data/images
```
**Ex: Lấy đường dẫn thư mục gốc**
```python
BASE_DIR = os.path.dirname(os.path.dirname(__file__)) 

print(BASE_DIR) # /home/thang/projects/tri_tue_nhan_tao/backend

# Ví dụ path = "/home/thang/projects/tri_tue_nhan_tao/backend/app.py"
# Lần 1: os.path.dirname(path) -> /home/thang/projects/tri_tue_nhan_tao/backend
# Lần 2: -> /home/thang/projects/tri_tue_nhan_tao
```
## .abspath()
```bash
Dùng để đổi đường dẫn đó thành đường dẫn tuyệt đối (absolute path).
```
**Syn**
```bash
os.path.abspath(path)

- Input:
  + path  : đường dẫn tương đối hoặc file
```
**Ex1: chuyển 1 đường dẫn tương đối thành đường dẫn tuyệt đối**
```python
import os

print(os.path.abspath("backend/utils.py")) # /home/thang/workspace/lightgbm/backend/utils.py
```
**Ex2: Lưu ý abspath gặp / thì giữ nguyên**
```python
import os

print(os.path.abspath("/backend/utils.py")) # /backend/utils.py
```
## .join()
```bash
- Dùng để ghép đường dẫn.
```
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
Remove()
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
