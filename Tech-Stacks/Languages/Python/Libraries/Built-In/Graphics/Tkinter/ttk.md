- [ttk](#ttk)
- [ttk (là phiên bản widget đẹp hơn của Tkinter)](#ttk-là-phiên-bản-widget-đẹp-hơn-của-tkinter)
  - [Combobox (Danh sách xổ xuống -dropdown)](#combobox-danh-sách-xổ-xuống--dropdown)
- [Treeview (Hiển thị dữ liệu dạng bảng hoặc cây)](#treeview-hiển-thị-dữ-liệu-dạng-bảng-hoặc-cây)
- [messagebox (dùng để hiện thị popup)](#messagebox-dùng-để-hiện-thị-popup)
  - [showinfo()](#showinfo)
- [.Frame (giống như 1 cái hộp)](#frame-giống-như-1-cái-hộp)
  - [.winfow\_children()](#winfow_children)
    - [.destroy() (xóa từng widget)](#destroy-xóa-từng-widget)
    - [.pack() (Đặt frame vào window)](#pack-đặt-frame-vào-window)
    - [grid()](#grid)
---
# ttk
# ttk (là phiên bản widget đẹp hơn của Tkinter)
tk và ttk đều là thư viện tạo giao diện trong Tkinter, nhưng chúng có sự khác biệt quan trọng:

tk	ttk
Widget giao diện cổ điển	Widget giao diện hiện đại
Dễ đổi màu (bg, fg)	Chủ yếu dùng theme (Style) để đổi giao diện
Nhìn khá cũ	Nhìn giống ứng dụng Windows/macOS/Linux
Có nhiều thuộc tính màu	Ít thuộc tính màu trực tiếp hơn
Ví dụ 1: Button
Dùng tk.Button
import tkinter as tk

root = tk.Tk()

btn = tk.Button(
    root,
    text="Đăng nhập",
    bg="blue",
    fg="white"
)
btn.pack()

root.mainloop()

Kết quả giả định:

+------------------+
| Đăng nhập        |   ← Nền xanh, chữ trắng
+------------------+

Bạn có thể đổi màu rất dễ:

bg="red"
fg="yellow"
Dùng ttk.Button
import tkinter as tk
from tkinter import ttk

root = tk.Tk()

btn = ttk.Button(
    root,
    text="Đăng nhập"
)
btn.pack()

root.mainloop()

Kết quả giả định:

┌──────────────────┐
│   Đăng nhập      │   ← Theo giao diện hệ điều hành
└──────────────────┘

Nếu viết:

ttk.Button(root, text="Đăng nhập", bg="blue")

sẽ báo lỗi:

TypeError:
unknown option "-bg"

vì ttk không dùng bg, fg, mà dùng Style.

Ví dụ 2: Entry
tk.Entry
entry = tk.Entry(
    root,
    bg="yellow",
    fg="red"
)

Có thể đổi màu trực tiếp.

ttk.Entry
entry = ttk.Entry(root)

Không có:

bg="yellow"

Muốn đổi phải tạo Style.

Ví dụ 3: Label
tk
label = tk.Label(
    root,
    text="Hello",
    bg="green",
    fg="white"
)
ttk
label = ttk.Label(
    root,
    text="Hello"
)

Muốn đổi màu:

style = ttk.Style()

style.configure(
    "My.TLabel",
    foreground="red"
)

label = ttk.Label(
    root,
    text="Hello",
    style="My.TLabel"
)
Khi nào dùng cái nào?

Nếu chỉ học Tkinter hoặc làm giao diện đơn giản:

tk.Label
tk.Button
tk.Entry

là đủ.

Nếu làm ứng dụng thực tế:

ttk.Label
ttk.Button
ttk.Entry
ttk.Combobox
ttk.Treeview

sẽ đẹp hơn và giao diện đồng nhất với hệ điều hành.

Ví dụ kết hợp
import tkinter as tk
from tkinter import ttk

root = tk.Tk()

tk.Label(root, text="tk Label", bg="yellow").pack(pady=5)

ttk.Label(root, text="ttk Label").pack(pady=5)

tk.Button(root, text="tk Button", bg="lightblue").pack(pady=5)

ttk.Button(root, text="ttk Button").pack(pady=5)

root.mainloop()

Trong ví dụ này:

tk.Label có nền vàng vì hỗ trợ bg.
ttk.Label dùng giao diện mặc định của hệ điều hành.
tk.Button có nền xanh nhạt theo bg.
ttk.Button có giao diện hiện đại theo theme và bỏ qua các thuộc tính như bg, fg.
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
# .Frame (giống như 1 cái hộp)
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
## .winfow_children() 
**Ex**
```python
import tkinter as tk
from tkinter import ttk

root = tk.Tk()

frame = ttk.Frame(root)
frame.pack()

label = ttk.Label(frame, text="Tên")
label.pack()

entry = ttk.Entry(frame)
entry.pack()

button = ttk.Button(frame, text="Lưu")
button.pack()

print(root.winfo_children()) # [<tkinter.ttk.Frame object .!frame>] hoặc [.!frame]
print(frame.winfo_children())
# [
#     <tkinter.ttk.Label object .!frame.!label>,
#     <tkinter.ttk.Entry object .!frame.!entry>,
#     <tkinter.ttk.Button object .!frame.!button>
# ]

# hoặc:

# [
#     .!frame.!label,
#     .!frame.!entry,
#     .!frame.!button
# ]
```
### .destroy() (xóa từng widget)
Đây là ví dụ đơn giản nhất để hiểu destroy() khi dùng ttk.

import tkinter as tk
from tkinter import ttk

root = tk.Tk()

frame = ttk.Frame(root)
frame.pack(padx=10, pady=10)

ttk.Label(frame, text="Tên").pack()
ttk.Entry(frame).pack()
ttk.Button(frame, text="Lưu").pack()

print("Trước khi destroy:")
print(frame.winfo_children())

frame.destroy()

print("Sau khi destroy:")
print(root.winfo_children())

root.mainloop()
Giao diện trước khi destroy()
root
│
└── Frame
      │
      ├── Label
      ├── Entry
      └── Button
Kết quả giả định
Trước khi destroy:
[
    .!frame.!label,
    .!frame.!entry,
    .!frame.!button
]

Sau khi chạy

frame.destroy()

thì Frame và toàn bộ widget bên trong đều bị xóa.

Nếu kiểm tra:

print(root.winfo_children())

kết quả giả định:

Sau khi destroy:
[]

vì root không còn widget con nào nữa.

Ví dụ chỉ xóa một Button
import tkinter as tk
from tkinter import ttk

root = tk.Tk()

label = ttk.Label(root, text="Tên")
label.pack()

entry = ttk.Entry(root)
entry.pack()

button = ttk.Button(root, text="Lưu")
button.pack()

print("Trước:")
print(root.winfo_children())

button.destroy()

print("Sau:")
print(root.winfo_children())

root.mainloop()
Trước khi xóa
root
├── Label
├── Entry
└── Button

Kết quả giả định:

Trước:
[
    .!label,
    .!entry,
    .!button
]
Sau khi
button.destroy()

giao diện còn:

root
├── Label
└── Entry

Kết quả giả định:

Sau:
[
    .!label,
    .!entry
]
Ý nghĩa của destroy()

destroy() sẽ xóa hoàn toàn widget khỏi giao diện và giải phóng tài nguyên. Sau khi gọi:

button.destroy()

thì button không còn tồn tại trên cửa sổ nữa và bạn không thể dùng lại chính widget đó (ví dụ gọi button.pack() sẽ gây lỗi). Nếu muốn có nút mới, bạn phải tạo lại:

button = ttk.Button(root, text="Lưu")
button.pack()

Đây là điểm khác với pack_forget() hoặc grid_forget(): các phương thức đó chỉ ẩn widget, còn destroy() thì xóa hẳn widget.
### .pack() (Đặt frame vào window)
**Syn**
```bash

- fill:
  + both: chiếm cả ngang và dọc
- expand:
  + True
```
### grid()