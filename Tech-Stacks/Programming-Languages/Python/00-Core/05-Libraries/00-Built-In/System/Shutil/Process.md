- [Shutil Introduction](#shutil-introduction)
- [copy() (Copy file)](#copy-copy-file)
- [copy2() (Copy file + metadata)](#copy2-copy-file--metadata)
- [copytree() (Copy cả thư mục)](#copytree-copy-cả-thư-mục)
- [move() (Di chuyển)](#move-di-chuyển)
- [rmtree() (Xóa thư mục)](#rmtree-xóa-thư-mục)
- [make\_archive() (Tạo file zip)](#make_archive-tạo-file-zip)
- [unpack\_archive() (Giải nén)](#unpack_archive-giải-nén)
- [copyfileobj() (Copy giữa 2 file object)](#copyfileobj-copy-giữa-2-file-object)
---
# Shutil Introduction
# copy() (Copy file)
**Ex**
```python
import shutil

shutil.copy("a.txt", "b.txt")
```
# copy2() (Copy file + metadata)
# copytree() (Copy cả thư mục)
# move() (Di chuyển)
# rmtree() (Xóa thư mục)
# make_archive() (Tạo file zip)
# unpack_archive() (Giải nén)
# copyfileobj() (Copy giữa 2 file object)

shutil.copy2("a.txt", "backup/a.txt")

Giữ lại:

thời gian tạo

quyền truy cập

✅ 3. Di chuyển file
shutil.move("a.txt", "folder/a.txt")

Giống lệnh mv trong Linux.

✅ 4. Xóa cả thư mục
shutil.rmtree("folder")

⚠ Xóa toàn bộ thư mục + file bên trong.

✅ 5. Copy cả thư mục
shutil.copytree("source", "backup")
3️⃣ Ví dụ quan trọng trong FastAPI (upload file)

Trong FastAPI bạn thường thấy:

import shutil
from fastapi import UploadFile

with open("uploads/avatar.png", "wb") as buffer:
    shutil.copyfileobj(file.file, buffer)
📌 Vì sao dùng copyfileobj?

file.file là file object

buffer là file object mới

copyfileobj() copy dữ liệu giữa 2 stream

Không load toàn bộ file vào RAM

Khi print thử:
print(type(file.file))

Output:

<class '_io.BufferedRandom'>
4️⃣ Tạo file zip
shutil.make_archive("backup", "zip", "my_folder")

Tạo file:

backup.zip
5️⃣ Giải nén
shutil.unpack_archive("backup.zip", "extract_folder")
6️⃣ So sánh shutil vs os
os	shutil
Thao tác thấp	Thao tác cao
os.remove	shutil.rmtree
os.rename	shutil.move

👉 shutil tiện hơn khi làm việc với file lớn và thư mục.

7️⃣ Khi nào nên dùng shutil?

Upload file (FastAPI, Django)

Backup dữ liệu

Copy thư mục

Tạo zip tự động

Tool CLI quản lý file

🎯 Kết luận

shutil là thư viện:

Built-in

Làm việc với file/folder

Mạnh khi xử lý file upload

Hay dùng trong backend web

Nếu bạn muốn mình giải thích sâu:

copy() vs copyfile() khác gì?

copyfileobj() hoạt động như nào?

Vì sao upload file lớn không nên dùng await file.read() mà nên dùng stream?

Mình phân tích sâu hệ thống file I/O cho bạn luôn 👌