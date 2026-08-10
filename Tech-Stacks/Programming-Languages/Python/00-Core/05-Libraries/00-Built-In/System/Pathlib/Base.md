- [Pathlib Introduction (Dùng để thao tác với file và thư mục theo cách hiện đại hơn os.path. code sẽ dễ đọc hơn os)](#pathlib-introduction-dùng-để-thao-tác-với-file-và-thư-mục-theo-cách-hiện-đại-hơn-ospath-code-sẽ-dễ-đọc-hơn-os)
- [pathlib có nhanh bằng os không?](#pathlib-có-nhanh-bằng-os-không)
---
# Pathlib Introduction (Dùng để thao tác với file và thư mục theo cách hiện đại hơn os.path. code sẽ dễ đọc hơn os)
```bash
pathlib là thư viện chuẩn của Python (Standard Library) không cần tải. 
```
# pathlib có nhanh bằng os không?
```bash
Nếu bạn hỏi về tốc độ, thì câu trả lời ngắn là:

pathlib không nhanh hơn os đáng kể, và trong đa số chương trình bạn sẽ không cảm nhận được sự khác biệt.

Điểm khác nhau chủ yếu là API và cách viết, không phải hiệu năng.

Ví dụ

Dùng os:

import os

files = os.listdir("data")

for file in files:
    path = os.path.join("data", file)

    if os.path.isfile(path):
        print(path)

Dùng pathlib:

from pathlib import Path

files = Path("data").iterdir()

for file in files:
    if file.is_file():
        print(file)

Về bản chất, cả hai cuối cùng đều phải gọi xuống filesystem của hệ điều hành.

Nếu xét performance

Có thể hình dung:

Python code
    ↓
pathlib / os
    ↓
system call
    ↓
filesystem
    ↓
SSD / HDD

Chi phí lớn thường nằm ở:

filesystem
disk I/O
network filesystem

chứ không phải:

pathlib
vs
os

Ví dụ đọc 100.000 file:

pathlib
  ↓
filesystem I/O  ← thường là phần tốn thời gian lớn

os
  ↓
filesystem I/O

Chênh lệch API Python thường không phải bottleneck chính.

os có thể nhanh hơn một chút ở một số thao tác

Ví dụ:

os.path.exists(path)
os.path.isfile(path)
os.path.join(...)

so với:

Path(path).exists()
Path(path).is_file()
Path(...) / "file.txt"

os có thể có overhead Python thấp hơn trong một số trường hợp benchmark cực lớn.

Nhưng nếu code của bạn là:

for file in thousands_of_files:
    read_file(file)

thì thời gian đọc file thường lớn hơn nhiều.

pathlib có lợi thế rất lớn về code

Ví dụ:

from pathlib import Path

root = Path("data")

csv_files = list(root.glob("**/*.csv"))

Thay vì:

import os

csv_files = []

for root, dirs, files in os.walk("data"):
    for file in files:
        if file.endswith(".csv"):
            csv_files.append(os.path.join(root, file))

pathlib thường dễ đọc và ít lỗi hơn.

Đặc biệt khi bạn làm project Python lớn:

project_dir / "data" / "images" / "train"

rất dễ đọc.

Thay vì:

os.path.join(
    project_dir,
    "data",
    "images",
    "train"
)
Một điểm rất đáng chú ý với code AI/ML của bạn

Nếu bạn đang xử lý:

100.000 images
10.000 PDFs
CSV
YOLO dataset

thì đừng tối ưu:

pathlib vs os

trước.

Hãy quan tâm hơn tới:

I/O
SSD
parallel processing
multiprocessing
caching
batch processing
OpenCV
PIL
database
network storage

Ví dụ:

for path in Path("dataset").rglob("*.jpg"):
    image = cv2.imread(str(path))

thì bottleneck thường là:

SSD → đọc JPEG → decode JPEG

chứ không phải Path.rglob().

Kết luận
	os	pathlib
Tốc độ	Có thể nhỉnh hơn chút ở một số thao tác	Có thể có overhead nhỏ
Filesystem	✅	✅
Dễ đọc	⭐⭐⭐	⭐⭐⭐⭐⭐
Code hiện đại	⭐⭐⭐	⭐⭐⭐⭐⭐
Xử lý path phức tạp	Khá dài	Rất tiện
Project Python lớn	Tốt	Rất tốt

Nếu bạn đang viết project Python mới, mình khuyên dùng pathlib làm mặc định. os vẫn dùng khi bạn cần những API hệ điều hành cụ thể mà pathlib không cung cấp hoặc khi làm code thấp cấp hơn.

Đặc biệt với kiểu kiến trúc module/function mà bạn đang dùng, pathlib khá hợp: bạn có thể cho mỗi module nhận Path thay vì chuỗi đường dẫn, giúp code rõ ràng hơn.
```