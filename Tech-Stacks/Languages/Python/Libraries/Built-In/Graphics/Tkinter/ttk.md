- [ttk (là phiên bản widget đẹp hơn của Tkinter)](#ttk-là-phiên-bản-widget-đẹp-hơn-của-tkinter)
- [Button](#button)
- [.Entry()](#entry)
  - [.Label()](#label)
  - [.Style()](#style)
    - [.configure()](#configure)
  - [Combobox (Danh sách xổ xuống -dropdown)](#combobox-danh-sách-xổ-xuống--dropdown)
- [Treeview (Hiển thị dữ liệu dạng bảng hoặc cây)](#treeview-hiển-thị-dữ-liệu-dạng-bảng-hoặc-cây)
- [messagebox (dùng để hiện thị popup)](#messagebox-dùng-để-hiện-thị-popup)
  - [showinfo()](#showinfo)
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