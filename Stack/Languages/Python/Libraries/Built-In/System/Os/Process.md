- [Create](#create)
  - [.mkdir()](#mkdir)
- [Check](#check)
  - [.path.isfile()](#pathisfile)
  - [.path.isdir()](#pathisdir)
  - [.path.exists()](#pathexists)
- [Search](#search)
- [Display](#display)
  - [.listdir()](#listdir)
  - [.getcwd()](#getcwd)
  - [__file__](#file)
  - [.path.dirname()](#pathdirname)
- [Process](#process)
  - [.join()](#join)
  - [.chdir()](#chdir)
  - [splitext()](#splitext)
  - [relpath()](#relpath)
  - [getenv](#getenv)
  - [system()](#system)
  - [name](#name)
  - [sep](#sep)
  - [pathsep](#pathsep)
---
# Create
## .mkdir()
**Ex: Tạo file/thư mục nếu chưa tồn tại**
```python
import os

if not os.path.exists("output"):
    os.mkdir("output")
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

# Display
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
## __file__
**Ex**
```python
print(__file__) # /home/thang/projects/tri_tue_nhan_tao/backend/visualizations/check_dataset.py (đường dẫn chạy file hiện tại)
```
## .path.dirname()
```bash
Lấy thư mục chứa file.
```
**Ex**
```python
print(os.path.dirname("/data/images/cat.jpg")) # /data/images
```
**Ex: Lấy đường dẫn thư mục gốc**
```python
BASE_DIR = os.path.dirname(os.path.dirname(__file__)) 

print(BASE_DIR) # /home/thang/projects/tri_tue_nhan_tao/backend
```
# Process
## .join()
```bash
- Ghép đường dẫn.
```
**Syn**
```bash
img_path = os.path.join(input_folder, img_name)
```
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
## getenv
## system()
## name
## sep
## pathsep
