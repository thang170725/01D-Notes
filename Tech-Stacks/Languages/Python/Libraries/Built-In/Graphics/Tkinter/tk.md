- [Tkinter Introduction (dùng để xây dựng giao diện đồ họa GUI - Graphical User Interface)](#tkinter-introduction-dùng-để-xây-dựng-giao-diện-đồ-họa-gui---graphical-user-interface)
- [.TkVersion (Kiểm tra xem tkinter có trong máy chưa?)](#tkversion-kiểm-tra-xem-tkinter-có-trong-máy-chưa)
- [Tk() (Tạo cửa sổ chính của ứng dụng)](#tk-tạo-cửa-sổ-chính-của-ứng-dụng)
  - [title() (Đật tiêu đề cho của sổ)](#title-đật-tiêu-đề-cho-của-sổ)
  - [geometry() (Đặt kích thước cửa sổ)](#geometry-đặt-kích-thước-cửa-sổ)
  - [.resizeable() (Không cho kéo dãn)](#resizeable-không-cho-kéo-dãn)
  - [.configure()](#configure)
  - [.config()](#config)
  - [mainloop()](#mainloop)
    - [.wifo\_children() (lấy danh sách tất cả widget con trực tiếp của một widge)](#wifo_children-lấy-danh-sách-tất-cả-widget-con-trực-tiếp-của-một-widge)
  - [pack() (Đưa widget lên cửa sổ)](#pack-đưa-widget-lên-cửa-sổ)
- [Component (thành phần)](#component-thành-phần)
  - [Label()](#label)
- [Button() (Tạo nút bấm)](#button-tạo-nút-bấm)
- [Entry() (Ô nhập một dòng)](#entry-ô-nhập-một-dòng)
- [Text (Ô nhập nhiều dòng)](#text-ô-nhập-nhiều-dòng)
- [Frame (Frame là khung chứa các widget)](#frame-frame-là-khung-chứa-các-widget)
- [Canvas (Dùng để vẽ hình)](#canvas-dùng-để-vẽ-hình)
- [Menu (Tạo thanh menu)](#menu-tạo-thanh-menu)
- [Checkbutton (Checkbox - chọn hoặc bỏ chọn)](#checkbutton-checkbox---chọn-hoặc-bỏ-chọn)
- [Radiobutton (Chọn một trong nhiều lựa chọn)](#radiobutton-chọn-một-trong-nhiều-lựa-chọn)
- [StringVar (Object quản lý chuỗi)](#stringvar-object-quản-lý-chuỗi)
- [render() (vẽ toàn bộ giao diện)](#render-vẽ-toàn-bộ-giao-diện)
  - [.grid() (dùng để sắp xếp các widget (Button, Label, Entry,...) theo dạng bảng (hàng và cột), giống như bảng trong Excel)](#grid-dùng-để-sắp-xếp-các-widget-button-label-entry-theo-dạng-bảng-hàng-và-cột-giống-như-bảng-trong-excel)
  - [column=0      column=1](#column0------column1)
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
## .resizeable() (Không cho kéo dãn)
```bash
self.resizable(False, False)
```
## .configure() 

**Syn**
```bash
widget.configure(option=value)
```
**Ex: Đổi màu nền cửa sổ**
```python
import tkinter as tk

root = tk.Tk()

root.configure(bg="yellow")

root.mainloop()
# +--------------------------+
# |                          |
# |                          |
# |     nền màu vàng         |
# |                          |
# +--------------------------+
```
## .config()
**Tại sao phải dùng config()?**
```bash
Khi tạo widget:
  label = tk.Label(
      root,
      text="Hello",
      bg="white"
  )
  => Sau này muốn đổi chữ thành "Python" thì sao?

Không thể sửa lại: label = tk.Label(...) -> vì widget đã được tạo.

Ta dùng:label.config(text="Python") -> để thay đổi thuộc tính.
```
**Ex: Đổi tiêu đề Label**
```python
import tkinter as tk

root = tk.Tk()

label = tk.Label(root, text="Hello")
label.pack()

label.config(text="Python")

root.mainloop()
# Ban đầu: Hello
# Sau khi gọi label.config(text="Python")
# ↓
# Kết quả: Python
```
**Ex4: Đổi nội dung Label sau khi bấm Button**
```python
import tkinter as tk

root = tk.Tk()

label = tk.Label(root, text="Waiting...")
label.pack()

def click():
    label.config(text="Clicked!")

button = tk.Button(root, text="Click", command=click)
button.pack()

root.mainloop()
# Ban đầu Waiting...
# [ Click ]
#     ↓
# Nhấn nút
#     ↓
# Clicked! -> [ Click ]
```
## mainloop()
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
### .wifo_children() (lấy danh sách tất cả widget con trực tiếp của một widge)
```bash
dùng để lấy danh sách tất cả các widget con trực tiếp của một widget.
```
**Ex**
```python
Ví dụ đơn giản:

import tkinter as tk

root = tk.Tk()

label = tk.Label(root, text="Tên")
label.pack()

entry = tk.Entry(root)
entry.pack()

button = tk.Button(root, text="Lưu")
button.pack()

children = root.winfo_children()

print(children)
Kết quả giả định
[
    <tkinter.Label object .!label>,
    <tkinter.Entry object .!entry>,
    <tkinter.Button object .!button>
]

Hoặc trên máy khác có thể hiện:

[.!label, .!entry, .!button]

Đây là một list các đối tượng widget, không phải chuỗi.

Ví dụ khác

Giả sử bạn có giao diện:

root
│
├── Label("Tên")
├── Entry
├── Button("Lưu")
└── Frame

thì:

children = root.winfo_children()

print(children)

Kết quả giả định:

[
    Label,
    Entry,
    Button,
    Frame
]

Bạn có thể duyệt:

for widget in root.winfo_children():
    print(widget)

Kết quả:

.!label
.!entry
.!button
.!frame
Nếu Frame cũng có widget con
root
│
├── Label
├── Button
└── Frame
      │
      ├── Entry
      └── Button

Thì:

root.winfo_children()

chỉ trả về:

[
    Label,
    Button,
    Frame
]

Muốn lấy widget bên trong Frame:

frame.winfo_children()

Kết quả:

[
    Entry,
    Button
]
Tóm tắt

Giả sử cây widget như sau:

root
├── Label
├── Entry
├── Button
└── Frame
      ├── Label
      └── Entry

Thì:

root.winfo_children()

➡️ Kết quả giả định:

[
    <Label>,
    <Entry>,
    <Button>,
    <Frame>
]

và:

frame.winfo_children()

➡️ Kết quả giả định:

[
    <Label>,
    <Entry>
]

winfo_children() chỉ lấy các widget con trực tiếp, không lấy các widget "cháu" (con của con).
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
widget.pack(pady=10)
```
**Ex**
```python
import tkinter as tk

root = tk.Tk()

button = tk.Button(root, text="Click")
button.pack()

root.mainloop()
```
# Component (thành phần)
## Label()
**Syn**
```python
title = tk.Label(
    root,
    text="Student Management",
    font=("Arial", 18, "bold"),
    bg="#F2F2F2",
    fg="blue"
)
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
frame = tk.Frame(
    parent,
    bg="#F2F2F2"
)
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
tk.Radiobutton(
  parent, 
  text="...", 
  variable=
)
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
# StringVar (Object quản lý chuỗi)
**Ex**
```python
import tkinter as tk

window = tk.Tk()

username = tk.StringVar()

entry = tk.Entry(window, textvariable=username)
entry.pack()

def show():
    print(username.get())

button = tk.Button(window, text="Print", command=show)
button.pack()

window.mainloop()
```
# render() (vẽ toàn bộ giao diện)
## .grid() (dùng để sắp xếp các widget (Button, Label, Entry,...) theo dạng bảng (hàng và cột), giống như bảng trong Excel)

1. Cú pháp
widget.grid(
    row=0,
    column=0,
    padx=0,
    pady=0,
    sticky="",
    rowspan=1,
    columnspan=1
)

Các tham số thường dùng:

Tham số	Ý nghĩa
row	Hàng
column	Cột
padx	Khoảng cách trái phải
pady	Khoảng cách trên dưới
sticky	Căn vị trí trong ô
rowspan	Chiếm nhiều hàng
columnspan	Chiếm nhiều cột
2. Ví dụ đơn giản nhất
import tkinter as tk

root = tk.Tk()

tk.Label(root, text="A").grid(row=0, column=0)
tk.Label(root, text="B").grid(row=0, column=1)
tk.Label(root, text="C").grid(row=1, column=0)
tk.Label(root, text="D").grid(row=1, column=1)

root.mainloop()

Kết quả giả định

+-------+-------+
|   A   |   B   |
+-------+-------+
|   C   |   D   |
+-------+-------+
3. Ví dụ với Button
import tkinter as tk

root = tk.Tk()

tk.Button(root, text="Nút 1").grid(row=0, column=0)
tk.Button(root, text="Nút 2").grid(row=0, column=1)
tk.Button(root, text="Nút 3").grid(row=1, column=0)
tk.Button(root, text="Nút 4").grid(row=1, column=1)

root.mainloop()

Kết quả

+-----------+-----------+
|  Nút 1    |  Nút 2    |
+-----------+-----------+
|  Nút 3    |  Nút 4    |
+-----------+-----------+
4. row và column

Ví dụ

tk.Label(root, text="Tên").grid(row=0, column=0)
tk.Entry(root).grid(row=0, column=1)

tk.Label(root, text="Tuổi").grid(row=1, column=0)
tk.Entry(root).grid(row=1, column=1)

Kết quả

Tên     [________]

Tuổi    [________]

Ở đây:

row=0

column=0      column=1
------------------------
Tên           Entry

row=1

Tuổi          Entry
5. padx và pady
tk.Button(root, text="OK").grid(
    row=0,
    column=0,
    padx=20,
    pady=10
)

Ý nghĩa

padx = khoảng cách ngang

      20px
|<---------->|

+---------+
| Button  |
+---------+

pady = khoảng cách dọc

     10px
      ↑
+---------+
| Button  |
+---------+
      ↓
     10px
6. columnspan

Một widget có thể chiếm nhiều cột.

tk.Button(root, text="Đăng nhập").grid(
    row=2,
    column=0,
    columnspan=2
)

Bố cục

+-----------+-----------+
| User      | Entry     |
+-----------+-----------+
| Pass      | Entry     |
+-----------+-----------+
|     Đăng nhập         |
+-----------------------+

Nút chiếm luôn hai cột.

7. rowspan
tk.Label(root, text="MENU").grid(
    row=0,
    column=0,
    rowspan=3
)

Kết quả

+------+-----------+
|      | Tên       |
|MENU  +-----------+
|      | Tuổi      |
|      +-----------+
|      | Địa chỉ   |
+------+-----------+

Label "MENU" kéo dài qua 3 hàng.

8. sticky

Mặc định widget nằm giữa ô.

+-------------+
|             |
|    Button   |
|             |
+-------------+

Có thể căn vị trí bằng sticky.

Căn trái
sticky="w"
+-------------+
|Button       |
|             |
+-------------+
Căn phải
sticky="e"
+-------------+
|       Button|
|             |
+-------------+
Căn trên
sticky="n"
+-------------+
|   Button    |
|             |
|             |
+-------------+
Căn dưới
sticky="s"
+-------------+
|             |
|             |
|   Button    |
+-------------+
Kéo giãn ngang
sticky="ew"
+-----------------------+
|#######################|
+-----------------------+

Widget kéo dài từ trái sang phải.

Kéo giãn toàn bộ
sticky="nsew"

Widget sẽ lấp đầy toàn bộ ô.

9. Ví dụ hoàn chỉnh
import tkinter as tk

root = tk.Tk()
root.title("Form đăng nhập")

tk.Label(root, text="Tên đăng nhập").grid(row=0, column=0)

tk.Entry(root).grid(row=0, column=1)

tk.Label(root, text="Mật khẩu").grid(row=1, column=0)

tk.Entry(root, show="*").grid(row=1, column=1)

tk.Button(
    root,
    text="Đăng nhập"
).grid(row=2, column=0, columnspan=2, pady=10)

root.mainloop()

Kết quả giao diện (minh họa)

+-------------------------------+
| Tên đăng nhập | [__________]  |
| Mật khẩu      | [**********]  |
|                               |
|      [ Đăng nhập ]            |
+-------------------------------+
10. Lưu ý quan trọng

Trong cùng một container (ví dụ cùng một root hoặc cùng một Frame), không được trộn pack() và grid().

❌ Sai:

tk.Label(root, text="A").pack()
tk.Button(root, text="B").grid(row=0, column=0)

Điều này sẽ gây lỗi vì root đang dùng hai cách bố trí khác nhau.

✔ Đúng:

frame1 = tk.Frame(root)
frame1.pack()

frame2 = tk.Frame(root)
frame2.pack()

tk.Label(frame1, text="A").pack()
tk.Button(frame2, text="B").grid(row=0, column=0)

Ở đây mỗi Frame chỉ sử dụng một geometry manager.

Mẹo để dễ nhớ

Hãy tưởng tượng cửa sổ là một bảng ô vuông:

        column

          0        1        2
      +--------+--------+--------+
row 0 |        |        |        |
      +--------+--------+--------+
row 1 |        |        |        |
      +--------+--------+--------+
row 2 |        |        |        |
      +--------+--------+--------+
row = số hàng.
column = số cột.
columnspan = chiếm nhiều cột.
rowspan = chiếm nhiều hàng.
sticky = căn hoặc kéo giãn widget trong ô.
padx, pady = thêm khoảng trống xung quanh widget.

Đây là cách bố trí được dùng nhiều nhất khi tạo form đăng nhập, form nhập dữ liệu, máy tính bỏ túi, giao diện quản lý, vì nó giúp các thành phần thẳng hàng và dễ sắp xếp.
Có. tk cũng có Frame, và ttk cũng có Frame.

Ví dụ:

tk.Frame
import tkinter as tk

root = tk.Tk()

frame = tk.Frame(
    root,
    bg="lightblue",
    width=200,
    height=100
)
frame.pack()

root.mainloop()

Kết quả giả định:

+----------------------+
|                      |
|      Frame           |  ← nền xanh nhạt
|                      |
+----------------------+

Bạn có thể đổi màu trực tiếp:

frame = tk.Frame(
    root,
    bg="yellow"
)
ttk.Frame
import tkinter as tk
from tkinter import ttk

root = tk.Tk()

frame = ttk.Frame(root)
frame.pack()

root.mainloop()

ttk.Frame sẽ dùng giao diện (theme) của hệ điều hành và không hỗ trợ:

bg="yellow"   # ❌ Lỗi

Muốn đổi màu thường phải dùng ttk.Style, và tùy theme mà việc đổi màu nền có thể không có tác dụng.

So sánh
