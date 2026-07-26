- [Tkinter Introduction (dùng để xây dựng giao diện đồ họa GUI - Graphical User Interface)](#tkinter-introduction-dùng-để-xây-dựng-giao-diện-đồ-họa-gui---graphical-user-interface)
- [.TkVersion (Kiểm tra xem tkinter có trong máy chưa?)](#tkversion-kiểm-tra-xem-tkinter-có-trong-máy-chưa)
- [Tk() (Tạo cửa sổ chính của ứng dụng)](#tk-tạo-cửa-sổ-chính-của-ứng-dụng)
  - [title() (Đật tiêu đề cho của sổ)](#title-đật-tiêu-đề-cho-của-sổ)
  - [geometry() (Đặt kích thước cửa sổ)](#geometry-đặt-kích-thước-cửa-sổ)
  - [.resizeable() (Không cho kéo dãn)](#resizeable-không-cho-kéo-dãn)
  - [.configure() (thiết lập hoặc thay đổi thuộc tính của một widget)](#configure-thiết-lập-hoặc-thay-đổi-thuộc-tính-của-một-widget)
  - [.config() (thiết lập hoặc thay đổi thuộc tính của một widget)](#config-thiết-lập-hoặc-thay-đổi-thuộc-tính-của-một-widget)
  - [mainloop()](#mainloop)
    - [.wifo\_children() (lấy danh sách tất cả widget con trực tiếp của một widge)](#wifo_children-lấy-danh-sách-tất-cả-widget-con-trực-tiếp-của-một-widge)
- [Component (thành phần)](#component-thành-phần)
  - [Label() (Hiển thị văn bản)](#label-hiển-thị-văn-bản)
- [Button() (Tạo nút bấm)](#button-tạo-nút-bấm)
  - [Entry() (Ô nhập một dòng)](#entry-ô-nhập-một-dòng)
    - [.get()](#get)
    - [.delete()](#delete)
- [Text (Ô nhập nhiều dòng)](#text-ô-nhập-nhiều-dòng)
- [Frame (Frame là khung chứa các widget)](#frame-frame-là-khung-chứa-các-widget)
- [Canvas (Dùng để vẽ hình)](#canvas-dùng-để-vẽ-hình)
- [Menu (Tạo thanh menu)](#menu-tạo-thanh-menu)
- [Checkbutton (Checkbox - chọn hoặc bỏ chọn)](#checkbutton-checkbox---chọn-hoặc-bỏ-chọn)
- [Radiobutton (Chọn một trong nhiều lựa chọn)](#radiobutton-chọn-một-trong-nhiều-lựa-chọn)
- [StringVar (Object quản lý chuỗi)](#stringvar-object-quản-lý-chuỗi)
- [render() (vẽ toàn bộ giao diện)](#render-vẽ-toàn-bộ-giao-diện)
  - [.grid() (dùng để sắp xếp các widget (Button, Label, Entry,...) theo dạng bảng (hàng và cột), giống như bảng trong Excel)](#grid-dùng-để-sắp-xếp-các-widget-button-label-entry-theo-dạng-bảng-hàng-và-cột-giống-như-bảng-trong-excel)
- [Listbox()](#listbox)
- [Display (hiển thị)](#display-hiển-thị)
  - [.pack() (Đưa widget lên cửa sổ)](#pack-đưa-widget-lên-cửa-sổ)
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
## .configure() (thiết lập hoặc thay đổi thuộc tính của một widget)
**Syn**
```bash
widget.configure(
    bg="yellow",
    family="Segoe UI",
    size=10
)

- Input:
    + family:
        - Segoe UI      : font hỗ trợ tiếng việt tốt nhất trên Windows
        - DejaVu Sans   : font hỗ trợ tiếng việt tốt nhất trên Linux
    + size=10: cỡ chữ 
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
## .config() (thiết lập hoặc thay đổi thuộc tính của một widget)
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
# [
#     <tkinter.Label object .!label>,
#     <tkinter.Entry object .!entry>,
#     <tkinter.Button object .!button>
# ]
# Hoặc trên máy khác có thể hiện:
# [.!label, .!entry, .!button]
```
# Component (thành phần)
## Label() (Hiển thị văn bản)
**Syn**
```python
title = tk.Label(
    root,
    text="Student Management",
    font=("Arial", 18, "bold"),
    bg="#F2F2F2",
    fg="blue"
)

- input:
    + fg: màu chữ
    + bg: màu nền sau chữ
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
# Button() (Tạo nút bấm)
**Syn**
```bash
tk.Button(parent, text="Tên nút")
```
**Ex**
```python
import tkinter as tk

root = tk.Tk()

button = tk.Button(root, text="Đăng nhập")
button.pack()

root.mainloop()
```
## Entry() (Ô nhập một dòng)
**Syn**
```bash
entry = tk.Entry(
    parent,
    width=25,
    font=("Arial", 11)
)
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
### .get()
**Ex**
```python
root = tk.Tk()
    entry = tk.Entry(root)
    entry.pack()
    tk.Button(root, text="Gửi", command=lambda: print(entry.get())).pack()
    root.mainloop()
```
### .delete()
Entry.delete(first, last) có cú pháp:

entry.delete(first, last)

Trong đó:

first: vị trí bắt đầu xóa.
last: vị trí kết thúc xóa.
Tại sao là 0?

Chuỗi trong Entry được đánh số từ 0.

Ví dụ:

Hello
01234
H ở vị trí 0
e ở vị trí 1
l ở vị trí 2
...

Nên:

entry.delete(0)

chỉ xóa ký tự đầu tiên (H).

Tại sao là tk.END?

tk.END là hằng số của Tkinter, có nghĩa là đến cuối chuỗi.

Ví dụ:

entry.insert(0, "Hello")

Nếu gọi:

entry.delete(0, tk.END)

thì:

Hello
^^^^^

Tất cả ký tự từ vị trí 0 đến cuối đều bị xóa.

Kết quả:

(Entry rỗng)

Ví dụ khác
entry.insert(0, "Hello")
Xóa ký tự đầu
entry.delete(0)
ello
Xóa từ vị trí 1 đến 3
entry.delete(1, 3)
Ho

vì đã xóa:

e l l
Xóa từ vị trí 2 đến cuối
entry.delete(2, tk.END)
He
Tại sao không dùng delete()?

Vì Entry không biết bạn muốn xóa phần nào.

Khác với Text hay list, phương thức delete() của Entry bắt buộc phải chỉ rõ phạm vi cần xóa.

Do đó:

entry.delete()

sẽ báo lỗi:

TypeError: delete() missing required positional argument
Vì sao hầu hết mọi người đều dùng
entry.delete(0, tk.END)

Sau khi người dùng nhấn Gửi, thường muốn làm trống ô nhập để nhập dữ liệu mới.

Ví dụ:

def submit():
    print(entry.get())
    entry.delete(0, tk.END)

Quy trình:

Nhập: Nguyễn Văn A
        ↓
Nhấn Gửi
        ↓
In: Nguyễn Văn A
        ↓
Entry trở thành rỗng

Đây là cách chuẩn và được dùng rất phổ biến trong Tkinter.
**Ex**
```python
root = tk.Tk()
entry = tk.Entry(root)
entry.pack()
def submit():
    print(entry.get())
    entry.delete(0, tk.END)
tk.Button(root, text="Gửi", command=submit).pack()
root.mainloop()
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
**Syn**
```bash
widget.grid(
    row=0,
    column=0,
    padx=0,
    pady=0,
    sticky="",
    rowspan=1,
    columnspan=1
)

- Input:
    + row       : Hàng
    + column	: Cột
    + padx	    : Khoảng cách trái phải
    + pady	    : Khoảng cách trên dưới
    + sticky	: Căn vị trí trong ô
    + rowspan	: Chiếm nhiều hàng
    + columnspan: Chiếm nhiều cột
```
**Ex**
```python
import tkinter as tk

root = tk.Tk()

tk.Label(root, text="A").grid(row=0, column=0)
tk.Label(root, text="B").grid(row=0, column=1)
tk.Label(root, text="C").grid(row=1, column=0)
tk.Label(root, text="D").grid(row=1, column=1)

root.mainloop()
# +-------+-------+
# |   A   |   B   |
# +-------+-------+
# |   C   |   D   |
# +-------+-------+
```
**Ex2: Button**
```python
import tkinter as tk

root = tk.Tk()

tk.Button(root, text="Nút 1").grid(row=0, column=0)
tk.Button(root, text="Nút 2").grid(row=0, column=1)
tk.Button(root, text="Nút 3").grid(row=1, column=0)
tk.Button(root, text="Nút 4").grid(row=1, column=1)

root.mainloop()
# +-----------+-----------+
# |  Nút 1    |  Nút 2    |
# +-----------+-----------+
# |  Nút 3    |  Nút 4    |
# +-----------+-----------+
```
# Listbox()
**Syn**
```bash
student_listbox = tk.Listbox(
    root,
    width=55,
    height=10,
    font=("Arial", 11)
)
```
# Display (hiển thị)
## .pack() (Đưa widget lên cửa sổ)
```bash
Nếu không gọi pack(), widget sẽ không xuất hiện
```
**Syn**
```bash
widget.pack(

- Input:
    + fill= (str)   : Widget sẽ giãn theo chiều nào nếu còn không gian trống.
        - "x" 
        - "y"
        - "both"
        - "none"
    + expand=True (bool)    : Widget có được phép nhận phần không gian dư của widget cha hay không
    + padx=10 (int) : Khoảng cách bên ngoài widget theo chiều ngang (trái/phải).
    + pady=10 (int) : Khoảng cách bên ngoài widget theo chiều dọc (trên/dưới).
)
```
**Ex**
```python
import tkinter as tk

root = tk.Tk()

button = tk.Button(root, text="Click")
button.pack()

root.mainloop()
```