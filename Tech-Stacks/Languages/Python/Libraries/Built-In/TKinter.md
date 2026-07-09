- [Tkinter Introduction (dùng để xây dựng giao diện đồ họa GUI - Graphical User Interface)](#tkinter-introduction-dùng-để-xây-dựng-giao-diện-đồ-họa-gui---graphical-user-interface)
- [.TkVersion (Kiểm tra xem tkinter có trong máy chưa?)](#tkversion-kiểm-tra-xem-tkinter-có-trong-máy-chưa)
- [Tk() (Tạo cửa sổ chính của ứng dụng)](#tk-tạo-cửa-sổ-chính-của-ứng-dụng)
  - [title() (Đật tiêu đề cho của sổ)](#title-đật-tiêu-đề-cho-của-sổ)
  - [geometry() (Đặt kích thước cửa sổ)](#geometry-đặt-kích-thước-cửa-sổ)
  - [mainloop() (tạo vòng lặp giữ của sổ xuất hiện)](#mainloop-tạo-vòng-lặp-giữ-của-sổ-xuất-hiện)
- [Label() (Hiển thị văn bản)](#label-hiển-thị-văn-bản)
  - [pack() (Đưa widget lên cửa sổ)](#pack-đưa-widget-lên-cửa-sổ)
- [Button() (Tạo nút bấm)](#button-tạo-nút-bấm)
- [Entry() (Ô nhập một dòng)](#entry-ô-nhập-một-dòng)
- [Text (Ô nhập nhiều dòng)](#text-ô-nhập-nhiều-dòng)
- [Frame (Frame là khung chứa các widget)](#frame-frame-là-khung-chứa-các-widget)
- [Canvas (Dùng để vẽ hình)](#canvas-dùng-để-vẽ-hình)
- [Menu (Tạo thanh menu)](#menu-tạo-thanh-menu)
- [Checkbutton (Checkbox - chọn hoặc bỏ chọn)](#checkbutton-checkbox---chọn-hoặc-bỏ-chọn)
- [Radiobutton (Chọn một trong nhiều lựa chọn)](#radiobutton-chọn-một-trong-nhiều-lựa-chọn)
- [ttk](#ttk)
  - [Combobox (Danh sách xổ xuống -dropdown)](#combobox-danh-sách-xổ-xuống--dropdown)
- [Treeview (Hiển thị dữ liệu dạng bảng hoặc cây)](#treeview-hiển-thị-dữ-liệu-dạng-bảng-hoặc-cây)
---
# Tkinter Introduction (dùng để xây dựng giao diện đồ họa GUI - Graphical User Interface)
```bash
tkinter là thư viện chuẩn của Python. 
    Với tkinter, bạn có thể tạo các ứng dụng có cửa sổ, nút bấm, ô nhập liệu, bảng, menu,... thay vì chỉ chạy trên terminal.

Tkinter dùng để làm gì?
    Một số ứng dụng phổ biến:
        - Ứng dụng quản lý (quản lý sinh viên, nhân viên,...)
        - Máy tính bỏ túi
        - Notepad
        - Trình xem ảnh
        - Form nhập dữ liệu
        - Dashboard đơn giản
        - Tool nội bộ
```
# .TkVersion (Kiểm tra xem tkinter có trong máy chưa?)
```python
import tkinter

print(tkinter.TkVersion) # 8.6
```
# Tk() (Tạo cửa sổ chính của ứng dụng)
**Syn**
```bash
root = tk.Tk()
```
## title() (Đật tiêu đề cho của sổ)
**Syn**
```bash
root.title("Tên cửa sổ")
```
**Ex**
```python
import tkinter as tk

root = tk.Tk()
root.title("Ứng dụng đầu tiên")
root.mainloop()
# +-----------------------+
# | Ứng dụng đầu tiên     |
# +-----------------------+
```
## geometry() (Đặt kích thước cửa sổ)
**Syn**
```bash
root.geometry("widthxheight")
```
**Ex**
```python
import tkinter as tk

root = tk.Tk()
root.geometry("400x300")
root.mainloop()
# Kết quả: cửa sổ rộng 400px, cao 300px
```
## mainloop() (tạo vòng lặp giữ của sổ xuất hiện)
```bash
Nếu không gọi hàm này, cửa sổ sẽ đóng ngay
```
**Syn**
```bash
import tkinter as tk

root = tk.Tk()
root.mainloop()
# Kết quả: xuất hiện một cửa sổ trống
```
# Label() (Hiển thị văn bản)
**Syn**
```bash
label = tk.Label(parent, text="Nội dung")
```
**Ex**
```bash
import tkinter as tk

root = tk.Tk()

label = tk.Label(root, text="Xin chào")
label.pack()

root.mainloop()
# Kết quả: Xin chào
```
## pack() (Đưa widget lên cửa sổ)
```bash
Nếu không gọi pack(), widget sẽ không xuất hiện
```
**Syn**
```bash
widget.pack()
```
**Ex**
```python
import tkinter as tk

root = tk.Tk()

button = tk.Button(root, text="Click")
button.pack()

root.mainloop()
```
# Button() (Tạo nút bấm)
**Syn**
```bash
tk.Button(parent, text="Tên nút")
```
**Ex**
import tkinter as tk

root = tk.Tk()

button = tk.Button(root, text="Đăng nhập")
button.pack()

root.mainloop()
# Entry() (Ô nhập một dòng)
**Syn**
```bash
entry = tk.Entry(parent)
```
**Ex**
```python
import tkinter as tk

root = tk.Tk()

entry = tk.Entry(root)
entry.pack()

root.mainloop()
# Người dùng có thể nhập: Nguyễn Văn A
```
# Text (Ô nhập nhiều dòng)
**Syn**
```bash
text = tk.Text(parent)
```
**Ex**
```bash
import tkinter as tk

root = tk.Tk()

text = tk.Text(root, height=5, width=30)
text.pack()

root.mainloop()
# Có thể nhập:
# Xin chào
# Đây là dòng thứ hai
```
# Frame (Frame là khung chứa các widget)
```bash
Giúp chia giao diện thành nhiều phần.
```
**Syn**
```bash
frame = tk.Frame(parent)
```
**Ex**
```python
import tkinter as tk

root = tk.Tk()

frame = tk.Frame(root)
frame.pack()

tk.Button(frame, text="OK").pack()

root.mainloop())
```
# Canvas (Dùng để vẽ hình)
**Syn**
```bash
canvas = tk.Canvas(parent)
```
**Ex**
```python
import tkinter as tk

root = tk.Tk()

canvas = tk.Canvas(root, width=200, height=200)
canvas.pack()

canvas.create_oval(50, 50, 150, 150)

root.mainloop()
# Kết quả: vẽ một hình tròn.
```
# Menu (Tạo thanh menu)
**Syn**
```bash
menu = tk.Menu(root)
root.config(menu=menu)
```
**Ex**
```python
import tkinter as tk

root = tk.Tk()

menu = tk.Menu(root)
root.config(menu=menu)

menu.add_command(label="File")

root.mainloop()
# Kết quả:
# File
# xuất hiện trên thanh menu.
```
# Checkbutton (Checkbox - chọn hoặc bỏ chọn)
**Syn**
```bash
tk.Checkbutton(parent, text="...")
```
**Ex**
```python
import tkinter as tk

root = tk.Tk()

check = tk.Checkbutton(root, text="Tôi đồng ý")
check.pack()

root.mainloop()
# ☐ Tôi đồng ý
```
# Radiobutton (Chọn một trong nhiều lựa chọn)
**Syn**
```bash
tk.Radiobutton(parent, text="...")
```
**Ex**
```python
import tkinter as tk

root = tk.Tk()

choice = tk.IntVar()

tk.Radiobutton(root, text="Nam", variable=choice, value=1).pack()
tk.Radiobutton(root, text="Nữ", variable=choice, value=2).pack()

root.mainloop()
# Kết quả:
# ○ Nam
# ○ Nữ
# Chỉ chọn được một
```
# ttk
## Combobox (Danh sách xổ xuống -dropdown)
**Syn**
```bash
from tkinter import ttk

ttk.Combobox(parent, values=[...])
```
**Ex**
```python
import tkinter as tk
from tkinter import ttk

root = tk.Tk()

combo = ttk.Combobox(root, values=["Python", "Java", "C++"])
combo.pack()

root.mainloop()
# Người dùng chọn:
# ▼ Python
# ▼ Java
# ▼ C++
```
# Treeview (Hiển thị dữ liệu dạng bảng hoặc cây)
**Syn**
```bash
tree = ttk.Treeview(parent)
```
**Ex**
```python
import tkinter as tk
from tkinter import ttk

root = tk.Tk()

tree = ttk.Treeview(root, columns=("Tên",), show="headings")
tree.heading("Tên", text="Tên")
tree.insert("", "end", values=("An",))
tree.insert("", "end", values=("Bình",))

tree.pack()

root.mainloop()
# Kết quả:
# +-----------+
# |   Tên     |
# +-----------+
# |   An      |
# |   Bình    |
# +-----------+
```