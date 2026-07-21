messagebox là một module của Tkinter dùng để hiển thị các hộp thoại (dialog) như:

Thông báo thành công.
Báo lỗi.
Cảnh báo.
Hỏi người dùng Yes/No.
Hỏi OK/Cancel.
Hỏi Retry/Cancel,...
1. Import
import tkinter as tk
from tkinter import messagebox

Hoặc

from tkinter import *
from tkinter import messagebox
2. showinfo() - Thông báo

Dùng để hiển thị thông tin.

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

Kết quả:

+----------------------+
| Thông báo            |
|                      |
| Đăng nhập thành công!|
|                      |
|        [ OK ]        |
+----------------------+
3. showwarning() - Cảnh báo
messagebox.showwarning(
    "Cảnh báo",
    "Bạn chưa nhập tuổi!"
)

Hiển thị biểu tượng ⚠️.

4. showerror() - Báo lỗi
messagebox.showerror(
    "Lỗi",
    "Sai mật khẩu!"
)

Hiển thị biểu tượng ❌.

5. askyesno()

Hỏi người dùng.

answer = messagebox.askyesno(
    "Xác nhận",
    "Bạn có muốn xóa?"
)

print(answer)

Nếu chọn

Yes

thì

answer == True

Nếu chọn

No

thì

answer == False

Ví dụ

if messagebox.askyesno("Thoát", "Bạn muốn thoát?"):
    root.destroy()
6. askokcancel()
result = messagebox.askokcancel(
    "Đóng",
    "Bạn muốn đóng chương trình?"
)

Trả về

True

hoặc

False
7. askretrycancel()
result = messagebox.askretrycancel(
    "Lỗi",
    "Không kết nối được!"
)

Nếu chọn Retry

True

Nếu Cancel

False
8. askquestion()
answer = messagebox.askquestion(
    "Thoát",
    "Bạn chắc chắn?"
)

print(answer)

Kết quả là

'yes'

hoặc

'no'

Lưu ý: askquestion() trả về chuỗi, còn askyesno() trả về giá trị Boolean (True/False).

Ví dụ hoàn chỉnh
import tkinter as tk
from tkinter import messagebox

root = tk.Tk()
root.geometry("300x200")

def login():
    username = entry.get()

    if username == "":
        messagebox.showwarning(
            "Thiếu dữ liệu",
            "Vui lòng nhập tên."
        )
    else:
        messagebox.showinfo(
            "Thành công",
            f"Xin chào {username}"
        )

entry = tk.Entry(root)
entry.pack(pady=10)

btn = tk.Button(root, text="Đăng nhập", command=login)
btn.pack()

root.mainloop()

Hoạt động:

Nếu ô nhập rỗng → hiện hộp thoại cảnh báo.
Nếu có tên → hiện hộp thoại thông báo.
Trong project của bạn

Trong file DashboardTab bạn đang học, messagebox được dùng theo đúng các tình huống phổ biến:

Báo lỗi
messagebox.showerror(
    "Không lưu được",
    str(exc)
)

Nếu xảy ra lỗi khi lưu dữ liệu, sẽ hiện cửa sổ lỗi với nội dung của ngoại lệ.

Thông báo thành công
messagebox.showinfo(
    "Đã lưu",
    "Mục tiêu cá nhân đã được cập nhật."
)

Khi lưu mục tiêu thành công, chương trình thông báo cho người dùng.

Cảnh báo
messagebox.showwarning(
    "Cảnh báo vượt ngưỡng",
    "..."
)

Nếu các chỉ số sức khỏe vượt ngưỡng, chương trình sẽ hiển thị hộp thoại cảnh báo.

Tóm tắt các hàm thường dùng
Hàm	Mục đích	Giá trị trả về
showinfo()	Hiển thị thông báo	Không có
showwarning()	Hiển thị cảnh báo	Không có
showerror()	Hiển thị lỗi	Không có
askyesno()	Hỏi Yes/No	True hoặc False
askokcancel()	Hỏi OK/Cancel	True hoặc False
askretrycancel()	Hỏi Retry/Cancel	True hoặc False
askquestion()	Hỏi Yes/No	"yes" hoặc "no"

Trong các ứng dụng Tkinter thực tế, ba hàm được dùng nhiều nhất là showinfo(), showwarning() và showerror(), vì chúng phù hợp với hầu hết các tình huống thông báo kết quả, cảnh báo và xử lý lỗi.