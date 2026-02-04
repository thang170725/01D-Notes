```bash
- Dùng để tương tác với hệ điều hành gồm: Làm việc với file và thư mục, Xử lý đường dẫn, Lấy thông tin môi trường (environment), chạy lệnh hệ thống
- Không cần tải, cần import os
```

.chdir()
Chuyển đến thư mục khác
Cú pháp:
os.chdir("C:/Users/Thang/Documents")


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