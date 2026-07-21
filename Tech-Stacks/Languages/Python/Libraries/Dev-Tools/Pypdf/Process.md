- [PdfReader (mở PDF để đọc)](#pdfreader-mở-pdf-để-đọc)
  - [.pages](#pages)
- [PdfWriter (đối tượng dùng để tạo hoặc ghi ra một file PDF mới)](#pdfwriter-đối-tượng-dùng-để-tạo-hoặc-ghi-ra-một-file-pdf-mới)
  - [.add\_page()](#add_page)
  - [.append() (Thêm trang)](#append-thêm-trang)
---
# PdfReader (mở PDF để đọc)
## .pages 
# PdfWriter (đối tượng dùng để tạo hoặc ghi ra một file PDF mới)
```bash
- Hãy hình dung:
    + PdfWriter = tạo PDF kết quả.
```
**Ex: copy toàn bộ trang từ input.pdf sang output.pdf**
```python
from pypdf import PdfReader, PdfWriter

reader = PdfReader("input.pdf")
writer = PdfWriter()

for page in reader.pages:
    writer.add_page(page)

with open("output.pdf", "wb") as f:
    writer.write(f)
```
**Ex2: Ghép nhiều PDF**
```bash
Ví dụ có:
    - a.pdf
    - b.pdf
```
```python
from pypdf import PdfReader, PdfWriter

writer = PdfWriter()

for file in ["a.pdf", "b.pdf"]:
    reader = PdfReader(file)

    for page in reader.pages:
        writer.add_page(page)

with open("merged.pdf", "wb") as f:
    writer.write(f)

# a.pdf
# +
# b.pdf
# ↓
# merged.pdf
```
**Ex3: Lấy một vài trang**
```python
from pypdf import PdfReader, PdfWriter

reader = PdfReader("book.pdf")
writer = PdfWriter()

writer.add_page(reader.pages[0])

with open("page1.pdf", "wb") as f:
    writer.write(f)
```
## .add_page() 
## .append() (Thêm trang)
**Syn**
```bash
writer.append("a.pdf")

with open("merged.pdf", "wb") as f:
    writer.write(f)
```