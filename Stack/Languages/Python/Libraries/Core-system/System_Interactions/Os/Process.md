- [Result](#result)
  - [os.path.exists()](#ospathexists)
  - [.listdir()](#listdir)
  - [.getcwd()](#getcwd)
- [Process](#process)
  - [.join()](#join)
  - [.chdir()](#chdir)
---
# Result
## os.path.exists()
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

Mkdir()

makefirs()

rmdir()

removedirs()


Remove()
Rename()
Stat()
path

Basename()
Dirname()
Lấy thư mục chứa file
Cú pháp:
print(os.path.dirname("/data/images/cat.jpg")) # /data/images
BASE_DIR = os.path.dirname(os.path.dirname(__file__)) 
print(__file__) # /home/thang/projects/tri_tue_nhan_tao/backend/visualizations/check_dataset.py (đường dẫn chạy file hiện tại)
print(BASE_DIR) # /home/thang/projects/tri_tue_nhan_tao/backend

isfile
isdir
splitext()
relpath()
getenv
system()
name
sep
pathsep
3️⃣ Phân biệt với các hàm liên quan (rất hay nhầm)
🔹 Chỉ kiểm tra file
os.path.isfile("data.txt")

🔹 Chỉ kiểm tra thư mục
os.path.isdir("logs")

🔹 Kiểm tra tồn tại + loại
path = "example"

if os.path.exists(path):
    if os.path.isfile(path):
        print("Là file")
    elif os.path.isdir(path):
        print("Là thư mục")

4️⃣ Tạo file/thư mục nếu chưa tồn tại (case thực tế)
Tạo thư mục
import os

if not os.path.exists("output"):
    os.mkdir("output")

Tạo nhiều cấp thư mục
os.makedirs("a/b/c", exist_ok=True)

5️⃣ Cách hiện đại hơn (Python ≥ 3.4) 🚀

Nên dùng pathlib thay vì os.path

from pathlib import Path

path = Path("data.txt")

if path.exists():
    print("Tồn tại")

Kiểm tra file / thư mục
path.is_file()
path.is_dir()

6️⃣ Lỗi thường gặp ❌

❌ Sai:

os.exists("file.txt")   # Không tồn tại hàm này


✅ Đúng:

os.path.exists("file.txt")


Nếu bạn đang dùng os.exists trong project cụ thể (ví dụ đọc file, upload, training model…), gửi mình đoạn code mình sẽ sửa giúp chi tiết nhé 👍