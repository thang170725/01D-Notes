- [Pillow Introduction (là thư viện xử lý ảnh phổ biến nhất trong Python)](#pillow-introduction-là-thư-viện-xử-lý-ảnh-phổ-biến-nhất-trong-python)
- [Installation](#installation)
- [__version__](#version)
- [Image](#image)
  - [.show() (Hiển thị ảnh)](#show-hiển-thị-ảnh)
  - [.save() (Lưu ảnh)](#save-lưu-ảnh)
  - [.resize()](#resize)
  - [crop()](#crop)
  - [rotate()](#rotate)
- [ImageTk](#imagetk)
---
# Pillow Introduction (là thư viện xử lý ảnh phổ biến nhất trong Python)
```bash
Nó là phiên bản được phát triển tiếp từ thư viện PIL (Python Imaging Library). Nếu bạn làm về Computer Vision, YOLO, OCR, hay xử lý PDF thành ảnh thì gần như chắc chắn sẽ dùng đến Pillow.
```
**Pillow dùng để làm gì?**
```bash
Nó hỗ trợ gần như mọi thao tác cơ bản trên ảnh.
    - Đọc ảnh
    - Lưu ảnh
    - Resize
    - Crop
    - Rotate
    - Flip
    - Chuyển màu RGB ↔ Grayscale
    - Thay đổi độ sáng
    - Blur
    - Sharpen
    - Thêm chữ
    - Vẽ hình
    - Chuyển định dạng PNG ↔ JPG
```
# Installation
```bash
1. pip install pillow
```
# __version__
**Ex**
```python
import PIL

print(PIL.__version__)
```
# Image
**Ex**
```python
from PIL import Image

img = Image.open("cat.jpg")

print(img.size) # (1920, 1080)
print(img.mode) # RGB
```
## .show() (Hiển thị ảnh)
## .save() (Lưu ảnh)
## .resize()
## crop()
crop = img.crop((100, 50, 500, 300))

Ý nghĩa

(left, top, right, bottom)
## rotate()
img2 = img.rotate(90)

Hoặc

img2 = img.rotate(
    30,
    expand=True
)

expand=True

→ tự mở rộng canvas để ảnh không bị cắt.

1. Flip

Lật trái phải

from PIL import Image

img2 = img.transpose(Image.FLIP_LEFT_RIGHT)

Lật trên dưới

img2 = img.transpose(Image.FLIP_TOP_BOTTOM)
10. Chuyển sang grayscale
gray = img.convert("L")

L

0~255
11. Chuyển RGB
rgb = img.convert("RGB")
12. Chuyển RGBA

Có alpha

rgba = img.convert("RGBA")
13. Đọc kích thước
width, height = img.size

print(width)
print(height)
14. Lấy pixel
pixel = img.getpixel((100, 50))

print(pixel)

Ví dụ

(120, 55, 90)
15. Gán pixel
img.putpixel((100, 50), (255, 0, 0))
16. Blur
from PIL import ImageFilter

blur = img.filter(ImageFilter.BLUR)

Gaussian

blur = img.filter(
    ImageFilter.GaussianBlur(radius=2)
)
17. Sharpen
sharp = img.filter(
    ImageFilter.SHARPEN
)
18. Edge Detection
edge = img.filter(
    ImageFilter.FIND_EDGES
)
19. Vẽ lên ảnh
from PIL import ImageDraw

draw = ImageDraw.Draw(img)

draw.rectangle(
    (100,100,300,300),
    outline="red",
    width=5
)
20. Viết chữ
from PIL import ImageDraw

draw = ImageDraw.Draw(img)

draw.text(
    (20,20),
    "Hello",
    fill="red"
)
21. Resize chất lượng cao
img.resize(
    (640,640),
    Image.Resampling.LANCZOS
)

Ngoài ra còn:

NEAREST
BILINEAR
BICUBIC
LANCZOS

LANCZOS thường cho chất lượng tốt nhất khi thu nhỏ ảnh.

22. Chuyển sang NumPy

Đây là thao tác rất hay dùng trong AI.

import numpy as np

array = np.array(img)

Kết quả

(H, W, C)

Ví dụ

(640,640,3)
23. Từ NumPy sang Pillow
img = Image.fromarray(array)
24. Đọc nhiều ảnh
from pathlib import Path
from PIL import Image

folder = Path("images")

images = []

for file in folder.glob("*.png"):
    images.append(Image.open(file))
25. Dùng trong YOLO

Trong dự án YOLO của bạn, Pillow rất hữu ích khi muốn đọc ảnh trước rồi mới đưa vào mô hình, thay vì để mô hình tự đọc từ đường dẫn:

from PIL import Image
from ultralytics import YOLO

model = YOLO("best.pt")

img = Image.open("test.png")

results = model.predict(img)

Hoặc chuyển sang NumPy:

import numpy as np
from PIL import Image

img = Image.open("test.png")

img_np = np.array(img)

results = model.predict(img_np)

Điều này phù hợp với hướng bạn đang tối ưu pipeline: đọc ảnh một lần (có thể song song), sau đó truyền trực tiếp dữ liệu ảnh vào predict để giảm chi phí đọc file lặp lại.

26. Khi nào nên dùng Pillow và khi nào dùng OpenCV?
Tiêu chí	Pillow	OpenCV
Đọc/ghi ảnh	✅	✅
Resize, crop, rotate	✅	✅
Xử lý ảnh cơ bản	✅	✅
Vẽ chữ, khung	✅	✅
Thuật toán Computer Vision	❌	✅
Tốc độ xử lý	Tốt	Thường nhanh hơn cho nhiều tác vụ
Màu mặc định	RGB	BGR
Dễ sử dụng	⭐⭐⭐⭐⭐	⭐⭐⭐⭐

Khuyến nghị cho dự án YOLO của bạn: nếu mục tiêu là xây dựng pipeline dự đoán nhanh và chỉ cần đọc ảnh, resize hoặc chuyển đổi định dạng trước khi đưa vào mô hình thì Pillow là lựa chọn đơn giản và phù hợp. Nếu sau này bạn cần nhiều phép xử lý ảnh nâng cao (lọc, phát hiện biên, hình thái học, camera/video...), hãy kết hợp thêm OpenCV.
# ImageTk