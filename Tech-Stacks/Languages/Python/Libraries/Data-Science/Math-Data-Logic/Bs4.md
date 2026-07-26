# Bs4 Introduction (dùng để phân tích (parse) HTML hoặc XML)
```bash
Nó biến chuỗi HTML thành một cây (tree) các object để bạn dễ dàng:
    - tìm thẻ (<div>, <p>, <a>, ...)
    - lấy nội dung
    - lấy thuộc tính (href, class, id, ...)
    - sửa HTML
    - xóa thẻ
    - trích xuất text
```
# BeautifulSoup (biến nó thành các object để truy cập như tree)
**Syn**
```bash
soup = BeautifulSoup(html, 'html.parser')

- Input:
    + html: chuỗi HTML cần phân tích
    + 'html.parser': parser dùng để đọc HTML
```
**Ex**
```python
from bs4 import BeautifulSoup

html = """
<html>
    <body>
        <h1>Hello</h1>
        <p>Python</p>
    </body>
</html>
"""

soup = BeautifulSoup(html, "html.parser")

print(soup.h1) # <h1>Hello</h1>
```
## .text (Muốn lấy nội dung)
## .get_text() (dùng để lấy toàn bộ nội dung text bên trong một thẻ, bỏ hết các tag HTML)
**Syn**
```bash
get_text(
    separator=..., 
    strip=True
)

- Input:
    + separator=: nối các dòng bằng ký tự bất kỳ # separator=" | " Kết quả: ChatGPT | Python | Machine Learning
    + strip=True: sẽ loại bỏ khoảng trắng và ký tự xuống dòng ở đầu/cuối
```
**Ex**
```python
from bs4 import BeautifulSoup

html = """
<div>
    <h1>ChatGPT</h1>
    <p>Python</p>
    <p>Machine Learning</p>
</div>
"""

soup = BeautifulSoup(html, "html.parser")

print(soup.div.get_text())
# ChatGPT
# Python
# Machine Learning
```