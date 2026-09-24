- [Messagebox Introduction (dùng để hiển thị các hộp thoại (dialog))](#messagebox-introduction-dùng-để-hiển-thị-các-hộp-thoại-dialog)
- [showinfo() (Thông báo)](#showinfo-thông-báo)
- [showwarning() (Cảnh báo)](#showwarning-cảnh-báo)
- [showerror() (Báo lỗi)](#showerror-báo-lỗi)
- [askyesno() (Hỏi người dùng)](#askyesno-hỏi-người-dùng)
- [askokcancel()](#askokcancel)
- [askretrycancel()](#askretrycancel)
- [askquestion()](#askquestion)
---
# Messagebox Introduction (dùng để hiển thị các hộp thoại (dialog))
# showinfo() (Thông báo)
```bash
Dùng để hiển thị thông tin.
```
**Ex**
```python
import tkinter as tk
from tkinter import messagebox

root = tk.Tk()

def hello():
    messagebox.showinfo(
        "Thông báo",
        "Đăng nhập thành công!"
    )

tk.Button(root, text="Nhấn", command=hello).pack()

root.mainloop()
# +----------------------+
# | Thông báo            |
# |                      |
# | Đăng nhập thành công!|
# |                      |
# |        [ OK ]        |
# +----------------------+
```
# showwarning() (Cảnh báo)
**Syn**
```bash
messagebox.showwarning(
    "Cảnh báo",
    "Bạn chưa nhập tuổi!"
) 
# Hiển thị biểu tượng ⚠️.
```
# showerror() (Báo lỗi)
**Syn**
```bash
messagebox.showerror(
    "Lỗi",
    "Sai mật khẩu!"
)
# Hiển thị biểu tượng ❌
```
# askyesno() (Hỏi người dùng)
**Ex**
```python
answer = messagebox.askyesno(
    "Xác nhận",
    "Bạn có muốn xóa?"
)
print(answer)
# Nếu chọn Yes -> thì answer == True
# Nếu chọn No -> thì answer == False
```
# askokcancel()
**Syn**
```bash
result = messagebox.askokcancel(
    "Đóng",
    "Bạn muốn đóng chương trình?"
)
```
# askretrycancel()
**Syn**
```bash
result = messagebox.askretrycancel(
    "Lỗi",
    "Không kết nối được!"
)
```
# askquestion()
```bash
answer = messagebox.askquestion(
    "Thoát",
    "Bạn chắc chắn?"
)

print(answer)

