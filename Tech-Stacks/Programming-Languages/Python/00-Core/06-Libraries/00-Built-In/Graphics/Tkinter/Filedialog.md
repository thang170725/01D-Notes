- [Filedialog Introdution (dùng để mở hộp thoại chọn file hoặc thư mục, giúp người dùng chọn file bằng giao diện thay vì phải nhập đường dẫn bằng tay)](#filedialog-introdution-dùng-để-mở-hộp-thoại-chọn-file-hoặc-thư-mục-giúp-người-dùng-chọn-file-bằng-giao-diện-thay-vì-phải-nhập-đường-dẫn-bằng-tay)
- [askopenfilename()	(Chọn 1 file)](#askopenfilenamechọn-1-file)
- [askopenfilenames() (Chọn nhiều file)](#askopenfilenames-chọn-nhiều-file)
- [asksaveasfilename() (Chọn nơi lưu file)](#asksaveasfilename-chọn-nơi-lưu-file)
- [askdirectory() (Chọn thư mục)](#askdirectory-chọn-thư-mục)
---
[Back](Base.md)
# Filedialog Introdution (dùng để mở hộp thoại chọn file hoặc thư mục, giúp người dùng chọn file bằng giao diện thay vì phải nhập đường dẫn bằng tay)
```bash
Ví dụ như khi bạn bấm nút "Open File..." trong Word hay Photoshop, đó chính là một dạng file dialog.
```
# askopenfilename()	(Chọn 1 file)
**Syn**
```bash
file_path = filedialog.askopenfilename(
    title="Tiêu đề cửa sổ",
    initialdir="Đường dẫn mặc định",
    filetypes=[("Tên", "*.đuôi")]
)

- Input:
    + title=str                         : tiêu đề cửa sổ
    + initialdir=str                    : Chỉ định thư mục mở đầu tiên. # Ví dụ initialdir="D:/Pictures" -> Khi mở dialog sẽ vào D:\Pictures thay vì Documents.
    + filetypes=List[Tuple[str, str], ] : Người dùng chỉ nhìn thấy các file đúng định dạng.
- Output: str
```
**Ex**
```python
import tkinter as tk
from tkinter import filedialog

root = tk.Tk()
root.withdraw()      # Ẩn cửa sổ chính

file_path = filedialog.askopenfilename()

print(file_path) # Nếu chọn image1.png thì ra C:/Users/Thang/Desktop/image1.png
```
**Ex: chọn ảnh**
```bash
from tkinter import filedialog

path = filedialog.askopenfilename(
    title="Chọn ảnh",
    filetypes=[
        ("Image", "*.png *.jpg *.jpeg")
    ]
)

print(path) # dog.png thì path = C:/Images/dog.png
```
# askopenfilenames() (Chọn nhiều file)
# asksaveasfilename() (Chọn nơi lưu file)
# askdirectory() (Chọn thư mục)