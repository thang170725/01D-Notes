- [ttk (là phiên bản widget đẹp hơn của Tkinter)](#ttk-là-phiên-bản-widget-đẹp-hơn-của-tkinter)
- [Button](#button)
- [.Entry()](#entry)
  - [.Label()](#label)
  - [.get() (lấy nội dung người dùng nhập)](#get-lấy-nội-dung-người-dùng-nhập)
  - [.Style()](#style)
    - [.configure()](#configure)
  - [Combobox (Danh sách xổ xuống -dropdown)](#combobox-danh-sách-xổ-xuống--dropdown)
- [Treeview (Hiển thị dữ liệu dạng bảng hoặc cây)](#treeview-hiển-thị-dữ-liệu-dạng-bảng-hoặc-cây)
  - [heading()](#heading)
  - [.column() (chỉnh độ rộng cột)](#column-chỉnh-độ-rộng-cột)
  - [.insert() (thêm dữ liệu)](#insert-thêm-dữ-liệu)
  - [.selection() (lấy dòng đang chọn)](#selection-lấy-dòng-đang-chọn)
  - [.delete() (xóa dòng)](#delete-xóa-dòng)
  - [.item (Nó dùng để lấy thông tin hoặc cập nhật thông tin của một dòng (item))](#item-nó-dùng-để-lấy-thông-tin-hoặc-cập-nhật-thông-tin-của-một-dòng-item)
    - [.values (lấy giá trị của selection)](#values-lấy-giá-trị-của-selection)
  - [.get\_children() (dùng để lấy danh sách các item con của một node)](#get_children-dùng-để-lấy-danh-sách-các-item-con-của-một-node)
  - [.index()](#index)
- [Lấy item đang chọn](#lấy-item-đang-chọn)
- [Lấy vị trí](#lấy-vị-trí)
- [Lấy dữ liệu](#lấy-dữ-liệu)
- [Cập nhật dữ liệu của item](#cập-nhật-dữ-liệu-của-item)
- [Xóa item](#xóa-item)
- [Lấy toàn bộ item](#lấy-toàn-bộ-item)
- [.Frame (giống như 1 cái hộp)](#frame-giống-như-1-cái-hộp)
  - [.winfow\_children()](#winfow_children)
    - [.destroy() (xóa từng widget)](#destroy-xóa-từng-widget)
    - [.pack() (Đặt frame vào window)](#pack-đặt-frame-vào-window)
    - [grid()](#grid)
- [Notebook (widget dùng để tạo giao diện có nhiều tab)](#notebook-widget-dùng-để-tạo-giao-diện-có-nhiều-tab)
  - [.add() (Thêm một tab)](#add-thêm-một-tab)
  - [select() (Chuyển sang tab khác)](#select-chuyển-sang-tab-khác)
  - [forget() (Xóa một tab)](#forget-xóa-một-tab)
  - [tabs() (Lấy danh sách tất cả tab)](#tabs-lấy-danh-sách-tất-cả-tab)
  - [index() (Lấy chỉ số của tab)](#index-lấy-chỉ-số-của-tab)
- [columnconfigure() (dùng để cấu hình các cột của grid())](#columnconfigure-dùng-để-cấu-hình-các-cột-của-grid)
- [Frame](#frame)
- [Events (xử lý sự kiện)](#events-xử-lý-sự-kiện)
  - [bind() (dùng để bắt sự kiện)](#bind-dùng-để-bắt-sự-kiện)
---
# ttk (là phiên bản widget đẹp hơn của Tkinter)
```bash
tk và ttk đều là thư viện tạo giao diện trong Tkinter, nhưng chúng có sự khác biệt quan trọng:
    tk	                        ttk
    Widget giao diện cổ điển	Widget giao diện hiện đại
    Dễ đổi màu (bg, fg)	        Chủ yếu dùng theme (Style) để đổi giao diện
    Nhìn khá cũ             	Nhìn giống ứng dụng Windows/macOS/Linux
    Có nhiều thuộc tính màu	    Ít thuộc tính màu trực tiếp hơn
```
# Button
**Ex**
```python
import tkinter as tk
from tkinter import ttk

root = tk.Tk()

btn = ttk.Button(
    root,
    text="Đăng nhập"
)
btn.pack()

root.mainloop()
# ┌──────────────────┐
# │   Đăng nhập      │   ← Theo giao diện hệ điều hành
# └──────────────────┘
```
# .Entry()
## .Label()
## .get() (lấy nội dung người dùng nhập)
## .Style()
### .configure()
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
tree = ttk.Treeview(
  master,
  columns,
  show="headings",
  height=,
  selectmode
)

- Input:
  + master (widget): widget cha
  + columns (tuple, list): danh sách tên các cột 
  + show (str): hiển thị phần nào (tree, headings)
  + height (int): số dòng hiển thị
  + selectmode (str): Chế độ chọn (browse, extended, none)
```
## heading()
**Ex**
```python
import tkinter as tk
from tkinter import ttk

root = tk.Tk()

tree = ttk.Treeview(
    root,
    columns=("id", "name", "class"),
    show="headings"
)

tree.heading("id", text="Mã SV")
tree.heading("name", text="Tên")
tree.heading("class", text="Lớp")

tree.pack(fill="both", expand=True)

root.mainloop()
```
## .column() (chỉnh độ rộng cột)
**Syn**
```bash
tree.column(
  "id",
  width=,
  anchor="center"
)

- Input:
  + anchor= (str): căn lề
    - 'center': căn giữa
```
## .insert() (thêm dữ liệu)
**Syn**
```bash
tree.insert(
    "",
    tk.END,
    values=("SV01", "Nguyễn Văn A", "CNTT1")
)
```
## .selection() (lấy dòng đang chọn)
**Syn**
```bash
selected = tree.selection()
```
## .delete() (xóa dòng)
**syn**
```bash
item = tree.selection()[0]

tree.delete(item)
```
## .item (Nó dùng để lấy thông tin hoặc cập nhật thông tin của một dòng (item))
**Ex: Lấy dữ liệu của item**
```python
values = self.table.item(item, "values") # values = self.table.item(item)["values"]
```
**Ex2: Cập nhật item**
```python
self.table.item(
    item,
    values=("New Name", "New Des", "2026-07-27")
) # Sau đó dòng được cập nhật ngay.
```
### .values (lấy giá trị của selection)
## .get_children() (dùng để lấy danh sách các item con của một node)
**Syn**
```bash
tree.get_children(item=None)

- item=None (hoặc ""): lấy các item ở cấp gốc (root).
- Output: Hàm trả về một tuple chứa các item id.
```
**Ex1: Lấy tất cả các dòng**
```python
import tkinter as tk
from tkinter import ttk

root = tk.Tk()

tree = ttk.Treeview(root)
tree.pack()

tree.insert("", "end", text="A")
tree.insert("", "end", text="B")
tree.insert("", "end", text="C")

print(tree.get_children()) # ('I001', 'I002', 'I003')
```
## .index()
Trong ttk.Treeview, index() dùng để lấy vị trí (0-based) của một item trong danh sách các item cùng cấp.

Cú pháp
tree.index(item)
item: ID của item (ví dụ "I001").
Trả về: số nguyên 0, 1, 2, ...
Ví dụ 1
import tkinter as tk
from tkinter import ttk

root = tk.Tk()

tree = ttk.Treeview(root)
tree.pack()

id1 = tree.insert("", "end", text="A")
id2 = tree.insert("", "end", text="B")
id3 = tree.insert("", "end", text="C")

print(tree.index(id1))
print(tree.index(id2))
print(tree.index(id3))

Kết quả

0
1
2
Ví dụ 2: Lấy index của dòng đang chọn
def select(event):
    item = tree.selection()[0]
    print(item)              # I002
    print(tree.index(item))  # 1

Nếu người dùng chọn dòng thứ hai thì:

I002
1
Ví dụ 3: Dùng để update

Nếu bạn có một list dữ liệu:

jobs = [
    Job("A", "aaa"),
    Job("B", "bbb"),
    Job("C", "ccc")
]

Người dùng chọn một dòng:

item = tree.selection()[0]
idx = tree.index(item)

jobs[idx].name = "New name"

index() giúp biết dòng đang chọn tương ứng với phần tử nào trong list.

Ví dụ 4: Kết hợp get_children()
for item in tree.get_children():
    print(tree.index(item), tree.item(item)["values"])

Kết quả

0 ['A', 'aaa']
1 ['B', 'bbb']
2 ['C', 'ccc']
index() khác gì iid?

Giả sử:

id1 = tree.insert("", "end", values=("A",))
id2 = tree.insert("", "end", values=("B",))

Ta có:

print(id1)
I001
print(tree.index(id1))
0
I001 là ID của item (không đổi trừ khi bạn xóa item đó).
0 là vị trí hiện tại của item trong Treeview.

Nếu bạn xóa dòng đầu:

tree.delete(id1)

thì:

print(tree.index(id2))

sẽ là

0

vì id2 đã trở thành dòng đầu tiên.

Các hàm thường đi cùng index()
# Lấy item đang chọn
item = tree.selection()[0]

# Lấy vị trí
idx = tree.index(item)

# Lấy dữ liệu
values = tree.item(item, "values")

# Cập nhật dữ liệu của item
tree.item(item, values=("New", "Data"))

# Xóa item
tree.delete(item)

# Lấy toàn bộ item
items = tree.get_children()

Trong các ứng dụng CRUD như chương trình quản lý công việc của bạn, index() thường được dùng để ánh xạ giữa dòng đang chọn trong Treeview và phần tử tương ứng trong danh sách (list) mà bạn đang quản lý trong bộ nhớ.
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
**Ex**
```python
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
```
### .pack() (Đặt frame vào window)
**Syn**
```bash

- fill:
  + both: chiếm cả ngang và dọc
- expand:
  + True
```
### grid()
# Notebook (widget dùng để tạo giao diện có nhiều tab)
```bash
(giống như tab trên trình duyệt Chrome hoặc tab trong Visual Studio Code). Mỗi tab sẽ chứa một Frame, và bên trong Frame đó bạn có thể đặt các widget khác như Label, Button, Entry,...


Khi nào dùng Notebook?
    Notebook rất hữu ích khi muốn chia chương trình thành nhiều màn hình trong cùng một cửa sổ. Ví dụ:
        - Tab "Đăng nhập" và "Đăng ký".
        - Tab "Thông tin sinh viên", "Điểm", "Học phí".
        - Tab "Khách hàng", "Sản phẩm", "Hóa đơn" trong phần mềm quản lý.

    Một cấu trúc thường gặp là:
        Tk()
        │
        └── Notebook
            │
            ├── Frame (Tab 1)
            │     ├── Label
            │     ├── Entry
            │     └── Button
            │
            ├── Frame (Tab 2)
            │     ├── Treeview
            │     └── Button
            │
            └── Frame (Tab 3)
                  ├── Canvas
                  └── Label

Có thể hiểu đơn giản rằng Notebook là "quản lý các Frame theo dạng tab": mỗi tab chính là một Frame, và bạn xây dựng giao diện của từng tab giống như làm việc với một cửa sổ nhỏ độc lập.
```
**Syn**
```python
from tkinter import ttk

notebook = ttk.Notebook(parent)

- parent: cửa sổ hoặc Frame chứa Notebook.
```
## .add() (Thêm một tab)
**Syn**
```bash
notebook.add(frame, text="Tab 1")
```
**Ex**
```python
import tkinter as tk
from tkinter import ttk

root = tk.Tk()
root.title("Ví dụ Notebook")
root.geometry("400x300")

# Tạo Notebook
notebook = ttk.Notebook(root)

# Tab 1
tab1 = ttk.Frame(notebook)
notebook.add(tab1, text="Trang chủ")

label1 = ttk.Label(tab1, text="Đây là nội dung tab Trang chủ")
label1.pack(pady=20)

# Tab 2
tab2 = ttk.Frame(notebook)
notebook.add(tab2, text="Cài đặt")

button = ttk.Button(tab2, text="Lưu")
button.pack(pady=20)

# Hiển thị Notebook
notebook.pack(fill="both", expand=True)

root.mainloop()
# +--------------------------------------+
# | Trang chủ | Cài đặt                  |
# +--------------------------------------+
# |                                      |
# | Đây là nội dung tab Trang chủ        |
# |                                      |
# +--------------------------------------+

# Khi nhấn Cài đặt:
# +--------------------------------------+
# | Trang chủ | Cài đặt                  |
# +--------------------------------------+
# |                                      |
# |             [ Lưu ]                  |
# |                                      |
# +--------------------------------------+
```
## select() (Chuyển sang tab khác)
## forget() (Xóa một tab)
## tabs() (Lấy danh sách tất cả tab)
## index() (Lấy chỉ số của tab)
# columnconfigure() (dùng để cấu hình các cột của grid())
**Syn**
```bash
container.columnconfigure(index, weight=...)

- Input:
    + container: Tk, Frame, ttk.Frame,...
    + index: chỉ số cột (0, 1, 2, ...)
    + weight: độ ưu tiên giãn của cột.
        - 0: không giãn.
        - 1: giãn.
        - 2: giãn gấp đôi cột có weight=1.
```
**Ex1: Không dùng columnconfigure()**
```python
import tkinter as tk
from tkinter import ttk

root = tk.Tk()
root.geometry("400x150")

ttk.Button(root, text="Button 1").grid(row=0, column=0)
ttk.Button(root, text="Button 2").grid(row=0, column=1)

root.mainloop()
# Khi kéo rộng cửa sổ, hai nút vẫn nằm sát nhau, khoảng trống chỉ xuất hiện bên phải.
# +----------------------------------+
# |[Button1][Button2]                |
# |                                  |
# +----------------------------------+
```
**Ex2: Dùng columnconfigure()**
```python
import tkinter as tk
from tkinter import ttk

root = tk.Tk()
root.geometry("400x150")

# Cho cả hai cột được giãn đều
root.columnconfigure(0, weight=1)
root.columnconfigure(1, weight=1)

ttk.Button(root, text="Button 1").grid(
    row=0, column=0, sticky="ew"
)

ttk.Button(root, text="Button 2").grid(
    row=0, column=1, sticky="ew"
)

root.mainloop()

# Kết quả khi kéo rộng cửa sổ:
# +-------------------------------------------+
# |[------Button1------][------Button2------] |
# |                                           |
# +-------------------------------------------+
```
# Frame
```bash
Frame giống như một chiếc hộp để chứa các widget khác.
```
**Ex**
```python
import tkinter as tk

root = tk.Tk()

frame = tk.Frame(root, bg="lightgray")
frame.pack(padx=20, pady=20)

tk.Label(frame, text="Tên").pack()

tk.Entry(frame).pack()

tk.Button(frame, text="Lưu").pack()

root.mainloop()
```
# Events (xử lý sự kiện)
## bind() (dùng để bắt sự kiện)
**Syn**
```bash
widget.bind(sequence, callback)

- Input:
  + sequence (str)  : Tên sự kiện cần bắt.
    - "<Button-1>": bấm chuột trái.
    - "<Return>": bắt enter
    - "<<TreeviewSelect>>": chọn trong treeview.
  + callback (callable) : Hàm được gọi khi sự kiện xảy ra. Hàm phải nhận một tham số event.
```
**Ex1: Bắt sự kiện click Button**
```python
import tkinter as tk
from tkinter import ttk

def on_click(event):
    print("Đã click")

root = tk.Tk()

button = ttk.Button(root, text="Click")
button.pack()

button.bind("<Button-1>", on_click)

root.mainloop()
```
**Ex2: Bắt Enter trong Entry**
```python
import tkinter as tk
from tkinter import ttk

def on_enter(event):
    print(event.widget.get())

root = tk.Tk()

entry = ttk.Entry(root)
entry.pack()

entry.bind("<Return>", on_enter)

root.mainloop()
```
event là gì?

Khi bind() gọi callback, Tkinter truyền vào một đối tượng Event.

Ví dụ

def on_click(event):
    print(event.x)
    print(event.y)

Các thuộc tính thường dùng:

Thuộc tính	Ý nghĩa
event.widget	Widget phát sinh sự kiện.
event.x	Tọa độ chuột trong widget.
event.y	Tọa độ Y.
event.x_root	Tọa độ trên màn hình.
event.y_root	Tọa độ trên màn hình.
event.keysym	Phím được nhấn.
event.char	Ký tự nhập.
Với Treeview

Đây là widget dùng bind() nhiều nhất.

1. Chọn một dòng
tree.bind("<<TreeviewSelect>>", on_select)
def on_select(event):
    item = tree.selection()[0]
    values = tree.item(item)["values"]
    print(values)

Ví dụ kết quả

['SV01', 'Nguyễn Văn A', 'CNTT1']
2. Double Click
tree.bind("<Double-1>", on_double_click)
def on_double_click(event):
    item = tree.selection()[0]
    print(tree.item(item)["values"])

<Double-1> = double click chuột trái.

3. Click chuột phải
tree.bind("<Button-3>", on_right_click)
Các sự kiện thường dùng
Sequence	Ý nghĩa
<Button-1>	Click chuột trái
<Button-2>	Chuột giữa
<Button-3>	Chuột phải
<Double-1>	Double click
<Triple-1>	Triple click
<Motion>	Di chuyển chuột
<Enter>	Chuột đi vào widget
<Leave>	Chuột rời widget
<Return>	Enter
<Escape>	Esc
<Key>	Nhấn phím bất kỳ
<KeyPress-a>	Nhấn phím a
<KeyRelease>	Thả phím
<FocusIn>	Widget nhận focus
<FocusOut>	Widget mất focus
<<TreeviewSelect>>	Chọn dòng trong Treeview
<<ComboboxSelected>>	Chọn giá trị trong Combobox
command và bind khác nhau thế nào?

Đối với Button:

button = ttk.Button(
    root,
    text="Lưu",
    command=save
)
command chỉ xử lý một hành động mặc định (nhấn nút).

Nếu muốn bắt thêm sự kiện chuột:

button.bind("<Button-3>", show_menu)

hoặc:

button.bind("<Enter>", highlight)

thì phải dùng bind().

Quy tắc chung:

Dùng command khi widget hỗ trợ hành động mặc định (Button, Menu...).
Dùng bind() khi cần bắt các sự kiện cụ thể như chuột, bàn phím, focus hoặc các sự kiện đặc biệt của ttk như <<TreeviewSelect>> và <<ComboboxSelected>>.