- [MyMuPDFfitz (thư viện rất mạnh để đọc, chỉnh sửa, trích xuất nội dung và chuyển đổi PDF)](#mymupdffitz-thư-viện-rất-mạnh-để-đọc-chỉnh-sửa-trích-xuất-nội-dung-và-chuyển-đổi-pdf)
- [Installation](#installation)
- [.open() (đọc file pdf)](#open-đọc-file-pdf)
  - [get\_text()](#get_text)
  - [.number](#number)
  - [.get\_pixmap()](#get_pixmap)
  - [.rect](#rect)
  - [.get\_images()](#get_images)
  - [.insert\_text()](#insert_text)
  - [insert\_image()](#insert_image)
  - [.save()](#save)
  - [.insert\_pdf()](#insert_pdf)
- [.Matrix()](#matrix)
- [Practices](#practices)
  - [Đọc PDF và lưu từng trang thành ảnh](#đọc-pdf-và-lưu-từng-trang-thành-ảnh)
---
# MyMuPDFfitz (thư viện rất mạnh để đọc, chỉnh sửa, trích xuất nội dung và chuyển đổi PDF)
```bash
fitz dùng để làm gì?
    1. Đọc PDF
    2. Lấy văn bản
    3. Đọc từng trang
    4. Chuyển PDF thành ảnh
    5. Lấy kích thước trang
    6. Lấy ảnh trong PDF
    7. Chèn chữ vào PDF
    8. Chèn ảnh
    9. Ghép nhiều PDF
    10. OCR
```
# Installation
```bash
1. pip install pymupdf # Import: import fitz
2. python -c "import fitz; print(fitz.__doc__)" # Kiểm tra
```
# .open() (đọc file pdf)
```bash
import fitz

doc = fitz.open("sample.pdf")

print(len(doc)) # 15 (Nghĩa là PDF có 15 trang)
```
## get_text()
```python 
import fitz

doc = fitz.open("sample.pdf")

page = doc[0]

text = page.get_text()

print(text) # Hello World
```
## .number
## .get_pixmap()
**Ex**
```python
import fitz

doc = fitz.open("sample.pdf")

page = doc[0]

pix = page.get_pixmap()

pix.save("page1.png")
# sample.pdf
# ↓
# page1.png
```
## .rect
**Ex**
```python
import fitz

doc = fitz.open("data/317978.pdf")

print(doc[0].rect) # Rect(0.0, 0.0, 595.0, 842.0) tọa độ x0, y0, x1, y1
```
## .get_images()
## .insert_text()
## insert_image()
## .save()
## .insert_pdf()
# .Matrix() 
Nếu muốn ảnh nét hơn

mat = fitz.Matrix(2,2)

pix = page.get_pixmap(matrix=mat)

pix.save("page_hd.png")

Trong đó

Matrix(2,2)

↓

phóng to 2 lần

↓

ảnh sắc nét hơn
# Practices
## Đọc PDF và lưu từng trang thành ảnh
import fitz

doc = fitz.open("sample.pdf")

for i, page in enumerate(doc):
    pix = page.get_pixmap(matrix=fitz.Matrix(2, 2))
    pix.save(f"page_{i+1}.png")

doc.close()

Sau khi chạy, nếu sample.pdf có 3 trang, bạn sẽ thu được:

sample.pdf
│
├── page_1.png
├── page_2.png
└── page_3.png
13. Ví dụ: Trích xuất toàn bộ văn bản
import fitz

doc = fitz.open("sample.pdf")

all_text = ""

for page in doc:
    all_text += page.get_text()

doc.close()

print(all_text)

Nếu PDF có lớp văn bản (text layer), bạn sẽ lấy được toàn bộ nội dung mà không cần OCR. Nếu PDF chỉ là ảnh quét (scan), page.get_text() thường trả về chuỗi rỗng hoặc rất ít nội dung; khi đó cần kết hợp get_pixmap() với một công cụ OCR như Tesseract hoặc PaddleOCR để nhận dạng chữ từ ảnh.

Tóm tắt các hàm quan trọng
Hàm	Công dụng
fitz.open()	Mở PDF
doc[i] hoặc doc.load_page(i)	Lấy trang thứ i
page.get_text()	Trích xuất văn bản từ trang
page.get_pixmap()	Render trang thành ảnh
pix.save()	Lưu ảnh ra file
page.insert_text()	Thêm văn bản vào PDF
page.insert_image()	Chèn ảnh vào PDF
doc.insert_pdf()	Ghép PDF
page.get_images()	Liệt kê ảnh trong trang
page.rect	Lấy kích thước trang
doc.save()	Lưu PDF sau khi chỉnh sửa

Trong các dự án xử lý tài liệu và OCR, fitz thường đóng vai trò là cầu nối giữa PDF và xử lý ảnh: mở PDF, render từng trang thành ảnh chất lượng cao, sau đó chuyển ảnh sang OpenCV (cv2) hoặc NumPy để tiền xử lý và đưa vào mô hình OCR. Đây cũng là lý do bạn thường thấy fitz, numpy và cv2 được import cùng nhau trong các pipeline OCR.