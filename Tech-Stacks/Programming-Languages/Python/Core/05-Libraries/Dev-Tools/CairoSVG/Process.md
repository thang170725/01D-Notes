- [.svg2pdf() (chuyển svg sang pdf)](#svg2pdf-chuyển-svg-sang-pdf)
---
# .svg2pdf() (chuyển svg sang pdf)
**Syn**
```bash
cairosvg.svg2pdf(
    bytestring=None,
    file_obj=None,
    url=None,
    write_to=None
)

- Input:
    + bytestring    : SVG dưới dạng bytes
    + file_obj	    : File object đã mở
    + url	        : Đường dẫn file SVG
    + write_to	    : Nơi ghi PDF
```
**Ex1: SVG từ file**
```python
import cairosvg

cairosvg.svg2pdf(
    url="input.svg",
    write_to="output.pdf"
)

# input.svg
# ↓
# output.pdf
```
**Ex2: SVG từ chuỗi**
```python
import cairosvg

svg = """
<svg xmlns="http://www.w3.org/2000/svg"
     width="100"
     height="100">
  <circle
      cx="50"
      cy="50"
      r="40"
      fill="red"/>
</svg>
"""

cairosvg.svg2pdf(
    bytestring=svg.encode("utf-8"),
    write_to="circle.pdf"
)
```
**Ex3: Trả về bytes PDF**
```python
import cairosvg

pdf_bytes = cairosvg.svg2pdf(
    url="input.svg"
) # pdf_bytes là: bytes

# Sau đó tự lưu:
with open("output.pdf", "wb") as f:
    f.write(pdf_bytes)
```
**Ex4: Dùng file object**
```python
import cairosvg

with open("output.pdf", "wb") as pdf:
    cairosvg.svg2pdf(
        url="input.svg",
        write_to=pdf
    )
```