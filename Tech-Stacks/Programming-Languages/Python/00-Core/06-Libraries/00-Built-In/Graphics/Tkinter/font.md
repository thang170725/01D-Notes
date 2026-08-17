- [nametofont()](#nametofont)
  - [.actual()](#actual)
---
# nametofont()
```bash
nametofont là hàm trong module tkinter.font dùng để lấy đối tượng Font từ tên của một font đã tồn tại. 
    Điều này rất hữu ích khi bạn muốn sửa font mặc định của Tkinter hoặc dùng lại một font đã được tạo trước đó.
```
**Syn**
```bash
from tkinter import font

f = font.nametofont(name)
Tham số
Tham số	Kiểu dữ liệu	Ý nghĩa
name	str	Tên của font cần lấy.
Giá trị trả về
Kiểu dữ liệu: tkinter.font.Font
Trả về đối tượng Font để bạn có thể đọc hoặc thay đổi các thuộc tính của font.
```
Ví dụ 2: Thay đổi font mặc định của toàn bộ ứng dụng
import tkinter as tk
from tkinter import font

root = tk.Tk()

default_font = font.nametofont("TkDefaultFont")

default_font.configure(
    family="Segoe UI",
    size=12,
    weight="bold"
)

tk.Label(root, text="Xin chào").pack()
tk.Button(root, text="Button").pack()

root.mainloop()

Vì bạn sửa TkDefaultFont, các widget sử dụng font mặc định sẽ tự động cập nhật.

Ví dụ 3: Lấy lại font đã tạo
import tkinter as tk
from tkinter import font

root = tk.Tk()

my_font = font.Font(
    name="MyFont",
    family="Arial",
    size=14
)

same_font = font.nametofont("MyFont")

print(my_font is same_font)

Kết quả:

True

Hai biến cùng tham chiếu đến một đối tượng Font.

Một số font mặc định của Tkinter
Tên	Dùng cho
"TkDefaultFont"	Font mặc định của hầu hết widget.
"TkTextFont"	Widget Text.
"TkFixedFont"	Font đơn cách (monospace).
"TkMenuFont"	Menu.
"TkHeadingFont"	Tiêu đề.
"TkCaptionFont"	Chú thích.
"TkIconFont"	Biểu tượng.
"TkTooltipFont"	Tooltip (nếu có).
"TkSmallCaptionFont"	Chú thích nhỏ.
Khi nào nên dùng nametofont()?
Muốn chỉnh font mặc định của toàn bộ ứng dụng.
Muốn lấy lại một font đã đặt tên (name="...") để tái sử dụng.
Muốn đọc hoặc sửa các thuộc tính của một font hiện có mà không cần tạo đối tượng Font mới.

Nói ngắn gọn:

font.Font(...) → tạo một font mới.
font.nametofont("...") → lấy một font đã tồn tại theo tên.
## .actual()
**Ex1: Lấy font mặc định của Tkinter**
```python
import tkinter as tk
from tkinter import font

root = tk.Tk()

default_font = font.nametofont("TkDefaultFont")

print(default_font.actual())
# {
#     'family': 'Segoe UI',
#     'size': 9,
#     'weight': 'normal',
#     'slant': 'roman',
#     'underline': 0,
#     'overstrike': 0
# }
```