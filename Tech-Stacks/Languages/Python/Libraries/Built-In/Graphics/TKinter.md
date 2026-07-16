- [Tkinter Introduction (dùng để xây dựng giao diện đồ họa GUI - Graphical User Interface)](#tkinter-introduction-dùng-để-xây-dựng-giao-diện-đồ-họa-gui---graphical-user-interface)
- [.TkVersion (Kiểm tra xem tkinter có trong máy chưa?)](#tkversion-kiểm-tra-xem-tkinter-có-trong-máy-chưa)
- [Tk() (Tạo cửa sổ chính của ứng dụng)](#tk-tạo-cửa-sổ-chính-của-ứng-dụng)
  - [title() (Đật tiêu đề cho của sổ)](#title-đật-tiêu-đề-cho-của-sổ)
  - [geometry() (Đặt kích thước cửa sổ)](#geometry-đặt-kích-thước-cửa-sổ)
  - [.resizeable() (Không cho kéo dãn)](#resizeable-không-cho-kéo-dãn)
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
- [StringVar (Object quản lý chuỗi)](#stringvar-object-quản-lý-chuỗi)
- [render() (vẽ toàn bộ giao diện)](#render-vẽ-toàn-bộ-giao-diện)
  - [.grid() (dùng để sắp xếp các widget (Button, Label, Entry,...) theo dạng bảng (hàng và cột), giống như bảng trong Excel)](#grid-dùng-để-sắp-xếp-các-widget-button-label-entry-theo-dạng-bảng-hàng-và-cột-giống-như-bảng-trong-excel)
  - [column=0      column=1](#column0------column1)
- [ttk](#ttk)
  - [Combobox (Danh sách xổ xuống -dropdown)](#combobox-danh-sách-xổ-xuống--dropdown)
- [Treeview (Hiển thị dữ liệu dạng bảng hoặc cây)](#treeview-hiển-thị-dữ-liệu-dạng-bảng-hoặc-cây)
- [messagebox (dùng để hiện thị popup)](#messagebox-dùng-để-hiện-thị-popup)
  - [showinfo()](#showinfo)
- [ttk (là phiên bản widget đẹp hơn của Tkinter)](#ttk-là-phiên-bản-widget-đẹp-hơn-của-tkinter)
  - [.Frame (giống như 1 cái hộp)](#frame-giống-như-1-cái-hộp)
    - [.wifo\_children() (lấy tất cả widget bên trong Frame)](#wifo_children-lấy-tất-cả-widget-bên-trong-frame)
    - [.destroy() (xóa từng widget)](#destroy-xóa-từng-widget)
    - [.pack() (Đặt frame vào window)](#pack-đặt-frame-vào-window)
    - [grid()](#grid)
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
# messagebox (dùng để hiện thị popup)
## showinfo()
# ttk (là phiên bản widget đẹp hơn của Tkinter)
## .Frame (giống như 1 cái hộp)
```bash
Frame trong Tkinter/ttk có thể hiểu đơn giản là một cái khung (container) để chứa các widget khác như Label, Button, Entry,...

Nếu không có Frame, mọi widget sẽ nằm trực tiếp trên cửa sổ (Tk).
```
**Ex1: Không dùng Frame**
```python
import tkinter as tk
from tkinter import ttk

root = tk.Tk()
root.geometry("300x180")

ttk.Label(root, text="Username").pack()
ttk.Entry(root).pack()

ttk.Label(root, text="Password").pack()
ttk.Entry(root).pack()

ttk.Button(root, text="Login").pack()

root.mainloop()

# +---------------------------+
# |                           |
# | Username                  |
# | [______________]          |
# |                           |
# | Password                  |
# | [______________]          |
# |                           |
# |    [ Login ]              |
# |                           |
# +---------------------------+
# Mọi widget đều nằm trực tiếp trên root.
```
**Ex2: Dùng một Frame**
```python
import tkinter as tk
from tkinter import ttk

root = tk.Tk()
root.geometry("300x180")

frame = ttk.Frame(root, padding=20)
frame.pack(fill="both", expand=True)

ttk.Label(frame, text="Username").pack()
ttk.Entry(frame).pack()

ttk.Label(frame, text="Password").pack()
ttk.Entry(frame).pack()

ttk.Button(frame, text="Login").pack(pady=10)

root.mainloop()

# +--------------------------------+
# |                                |
# |   +------------------------+   |
# |   | Username               |   |
# |   | [______________]       |   |
# |   |                        |   |
# |   | Password               |   |
# |   | [______________]       |   |
# |   |                        |   |
# |   |     [ Login ]          |   |
# |   +------------------------+   |
# |                                |
# +--------------------------------+
# Khung bên trong chính là Frame.
```
**Ex3: Hai Frame**
```python
import tkinter as tk
from tkinter import ttk

root = tk.Tk()
root.geometry("400x250")

top = ttk.Frame(root, padding=10)
top.pack(fill="x")

bottom = ttk.Frame(root, padding=10)
bottom.pack(fill="both", expand=True)

ttk.Label(top, text="Personal Health Tracker").pack()

ttk.Button(bottom, text="Login").pack(pady=5)
ttk.Button(bottom, text="Register").pack()

root.mainloop()

# +---------------------------------------+
# | Personal Health Tracker               |  ← top Frame
# +---------------------------------------+
# |                                       |
# |           [ Login ]                   |
# |                                       |
# |         [ Register ]                  |
# |                                       |
# |                                       |
# +---------------------------------------+
```
### .wifo_children() (lấy tất cả widget bên trong Frame)
### .destroy() (xóa từng widget)
Trong Tkinter, destroy() dùng để xóa một widget hoặc đóng toàn bộ cửa sổ.

Có hai cách dùng phổ biến:

widget.destroy() → Xóa một widget.
root.destroy() → Đóng chương trình.
Ví dụ 1: Xóa một Button
import tkinter as tk

root = tk.Tk()

button = tk.Button(root, text="Tôi sẽ biến mất")
button.pack()

def xoa_button():
    button.destroy()

btn = tk.Button(root, text="Xóa Button", command=xoa_button)
btn.pack()

root.mainloop()
Ban đầu
+-----------------------+
| [Tôi sẽ biến mất]     |
| [Xóa Button]          |
+-----------------------+
Sau khi bấm "Xóa Button"
+-----------------------+
| [Xóa Button]          |
+-----------------------+

Nút đầu tiên đã bị xóa khỏi giao diện.

Ví dụ 2: Đóng cửa sổ
import tkinter as tk

root = tk.Tk()

tk.Button(
    root,
    text="Thoát",
    command=root.destroy
).pack()

root.mainloop()

Khi nhấn Thoát, toàn bộ cửa sổ sẽ đóng.

Ví dụ 3: Xóa Label
import tkinter as tk

root = tk.Tk()

label = tk.Label(root, text="Xin chào")
label.pack()

def xoa():
    label.destroy()

tk.Button(root, text="Xóa Label", command=xoa).pack()

root.mainloop()
Ban đầu
Xin chào

[Xóa Label]
Sau khi nhấn
[Xóa Label]
Ví dụ 4: Xóa Entry sau khi nhập
import tkinter as tk

root = tk.Tk()

entry = tk.Entry(root)
entry.pack()

def gui():
    print(entry.get())
    entry.destroy()

tk.Button(root, text="Gửi", command=gui).pack()

root.mainloop()

Ví dụ:

Người dùng nhập

Hello

Nhấn Gửi

Console

Hello

Giao diện

[Gửi]

Ô nhập liệu đã biến mất.

Ví dụ 5: Xóa toàn bộ Frame
import tkinter as tk

root = tk.Tk()

frame = tk.Frame(root, bg="lightblue")
frame.pack()

tk.Label(frame, text="Tên").pack()
tk.Entry(frame).pack()

def xoa_form():
    frame.destroy()

tk.Button(root, text="Ẩn Form", command=xoa_form).pack()

root.mainloop()
Ban đầu
Tên
[________]

[Ẩn Form]
Sau khi bấm
[Ẩn Form]

Cả Frame cùng các widget bên trong đều bị xóa.

Khi nào dùng destroy()?

Đóng chương trình:

root.destroy()

Xóa một widget:

label.destroy()

Xóa một cửa sổ con (Toplevel):

window.destroy()

Xóa cả một nhóm widget bằng cách đặt chúng trong một Frame, rồi gọi:

frame.destroy()
Lưu ý

Sau khi một widget đã bị destroy(), bạn không thể hiển thị lại chính widget đó bằng pack() hay grid().

Ví dụ:

label.destroy()

label.pack()   # ❌ Lỗi

Nếu muốn hiển thị lại, bạn phải tạo một widget mới:

label = tk.Label(root, text="Xin chào")
label.pack()

Đó là điểm khác biệt với pack_forget() hoặc grid_forget(), vốn chỉ ẩn widget chứ không xóa hẳn nó.
### .pack() (Đặt frame vào window)
**Syn**
```bash

- fill:
  + both: chiếm cả ngang và dọc
- expand:
  + True
```
### grid()