- [IO Introduction (dùng để làm việc với luồng dữ liệu (stream))](#io-introduction-dùng-để-làm-việc-với-luồng-dữ-liệu-stream)
- [Create (Nhóm khởi tạo)](#create-nhóm-khởi-tạo)
  - [StringIO](#stringio)
- [Process (Nhóm xử lý)](#process-nhóm-xử-lý)
  - [Write (ghi dữ liệu)](#write-ghi-dữ-liệu)
  - [Read (Đọc dữ liệu)](#read-đọc-dữ-liệu)
  - [Seek (Con trỏ file)](#seek-con-trỏ-file)
---
# IO Introduction (dùng để làm việc với luồng dữ liệu (stream))
```bash
Dùng để:
    + đọc/ghi file
    + xử lý dữ liệu dạng text hoặc bytes trong bộ nhớ
    + giả lập file mà không cần tạo file thật
- Thư viện này rất hữu ích khi:
    + test code
    + xử lý CSV/JSON tạm thời
    + redirect output
    + làm việc với API/upload file
```
# Create (Nhóm khởi tạo)
## StringIO
```bash
- StringIO là một class trong module io.
- Nó tạo ra một file giả trong RAM để làm việc với chuỗi (str).
- Thay vì:
    with open("data.txt", "w") as f:
        f.write("hello")
    + ta có thể:
        from io import StringIO

        f = StringIO()
        f.write("hello")
    + Không tạo file thật trên ổ cứng.
**Syn**
```bash
from io import StringIO

buffer = StringIO()
```
# Process (Nhóm xử lý)
## Write (ghi dữ liệu)
```bash
Ghi dữ liệu
```
**Ex**
```python
buffer.write("Hello\n")
buffer.write("World")

print(buffer.getvalue()) # Lấy toàn bộ nội dung
# Hello
# 
```
## Read (Đọc dữ liệu)
```bash
- Giống file thật.
```
**Ex**
```bash
from io import StringIO

buffer = StringIO("Dong 1\nDong 2")

print(buffer.read())
# Dong 1
# Dong 2
```
## Seek (Con trỏ file)
```bash
Sau khi đọc hoặc ghi, vị trí con trỏ sẽ thay đổi.
```
**Ex**
```python
from io import StringIO

buffer = StringIO()

buffer.write("abc")

print(buffer.read()) # Không đọc được gì vì con trỏ đang ở cuối.

buffer.seek(0) # Cần đưa con trỏ về đầu

print(buffer.read()) # abc
```