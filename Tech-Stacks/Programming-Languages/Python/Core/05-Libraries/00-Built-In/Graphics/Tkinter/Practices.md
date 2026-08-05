- [Quản lý công việc (ôn tập kiểm tra thường xuyên 1)](#quản-lý-công-việc-ôn-tập-kiểm-tra-thường-xuyên-1)
- [Quản lý sinh viên](#quản-lý-sinh-viên)
- [Quản lý nhân viên](#quản-lý-nhân-viên)
- [Quản lý sản phẩm](#quản-lý-sản-phẩm)
---
# Quản lý công việc (ôn tập kiểm tra thường xuyên 1)
```bash
Viết chương trình bằng ngôn ngữ Python thực hiện các công việc sau:
    - Giao diện ứng dụng: Tạo một cửa sổ với tkinter, bao gồm các phần nhập thông tin công việc mới, danh sách công việc hiện tại, và các nút chức năng.
    - Các widget cần dùng: Sử dụng Label, Entry, Text, Button:
        + Entry để nhập tên công việc.
        + Text hoặc Label để hiển thị danh sách công việc.
        + Button để thêm, lưu hoặc xóa công việc.
    - Sử dụng grid() với các thuộc tính row, column, padx, pady để sắp xếp widget trên giao diện.
    - Gán sự kiện cho các widget bằng bind:
    - Nhấn nút "Thêm công việc" để thêm công việc vào danh sách.
    - Nhấn đúp vào công việc trong danh sách để hiện chi tiết.
    - Nhấn nút "Xóa công việc" để xóa công việc khỏi danh sách.
    - Sử dụng messagebox thông báo khi thêm thành công và xác nhận khi xóa công việc.
    - Lưu thông tin công việc vào file JSON (tasks.json) với các thông tin như: tên công việc, mô tả, và ngày tạo.
    - Đọc và hiển thị dữ liệu JSON khi khởi động ứng dụng.
    - Thay đổi và cập nhật dữ liệu: Cho phép thay đổi thông tin và lưu lại vào file JSON khi cập nhật.
```
```python
from __future__ import annotations

import tkinter as tk
import json
import xml.sax

from xml.dom import minidom
from tkinter import ttk, messagebox
from dataclasses import dataclass
from datetime import datetime

@dataclass
class Job:
    name: str
    des: str
    date: datetime

class JobManager(tk.Tk):
    def __init__(self):
        super().__init__()

        self.geometry("800x600")
        self.resizable(False, False)

        # biến lưu dữ liệu
        self.job = {}

        self._render()

        # self._load_json()
        # self._load_xml_sax()
        self._load_xml_dom()
        self.after(100, lambda: messagebox.showinfo("Thông báo", "Load data thành công"))

    def _render(self):
        fields = [("name", "Tên công việc"), ("des", "Mô tả công việc")]

        for i, (key, label) in enumerate(fields):
            tk.Label(self, text=label).grid(column=0, row=i)
            entry = tk.Entry(self, width=30)
            entry.grid(column=1, row=i)

            self.job[key] = entry
        
        buttons = [
            ("add", self.add_job),
            ("update", self.update_job),
            ("remove", self.remove_job),
            ("save_json", self.save_json),
            ("save_xml_sax", self.save_xml_sax),
            ("save_xml_dom", self.save_xml_dom)
        ]
        for i, (key, command) in enumerate(buttons):
            tk.Button(self, text=key.upper(), command=command).grid(column=i, row=2)
        
        # tree view
        columns = ['name', 'des', 'date']
        self.table = ttk.Treeview(self, columns=columns, show="headings", height=10)
        for col in columns:
            self.table.heading(col, text=col.upper())
            self.table.column(column=col, width=200, anchor='center')
        self.table.grid(column=0, row=3, columnspan=6)

        self.table.bind("<<TreeviewSelect>>", self._tree_selected)
    
    def _get_job(self):
        return Job(name=self.job['name'].get(), des=self.job['des'].get(), date=datetime.now())
    
    def _clear_form(self):
        for entry in self.job.values():
            entry.delete(0, tk.END)
    
    def _load_json(self):
        with open('jobs.json', 'r', encoding="utf-8") as f: 
            data = json.load(f)

        for row in data:
            self.table.insert("", tk.END, values=(row['name'], row['des'], row['date']))

    def _load_xml_sax(self):
        handler = MyHandler()
        parser = xml.sax.make_parser()
        parser.setContentHandler(handler)
        parser.parse('jobs.xml')
        
        jobs = handler.jobs
        for raw in jobs:
            self.table.insert("", tk.END, values=(raw['name'], raw['des'], raw['date']))

    def _load_xml_dom(self):
        dom = minidom.parse("jobs.xml")
    
        jobs = dom.getElementsByTagName("job")
    
        for job in jobs:
            name = job.getElementsByTagName("name")[0].firstChild.data
            des = job.getElementsByTagName("des")[0].firstChild.data
            date = job.getElementsByTagName("date")[0].firstChild.data
    
            self.table.insert("", tk.END, values=(name, des, date))

    def _tree_selected(self, events):
        self._clear_form()

        selection = self.table.selection()
        if not selection:
            return
        
        item = selection[0]
        self.selected_item = item

        values = self.table.item(item)["values"]
        key = ["name", "des"]
        for (k, v) in zip(key, values):
            self.job[k].insert(0, v)
    
    def add_job(self):
        job = self._get_job()

        self.table.insert("", tk.END, values=(job.name, job.des, job.date))
        self._clear_form()

    def update_job(self):
        job = self._get_job()

        self.table.item(self.selected_item, values=(job.name, job.des, job.date))
        self._clear_form()

    def remove_job(self):
        self.table.delete(self.selected_item)
        self._clear_form()

    def save_json(self):
        jobs = []

        for item in self.table.get_children():
            values = self.table.item(item, "values")

            jobs.append({
                "name": values[0],
                "des": values[1],
                "date": values[2]
            })
        
        with open("jobs.json", "w") as f:
            json.dump(jobs, f)
        
        messagebox.showinfo("Thong bao", "luu json thanh cong")
            
    def save_xml_sax(self):
        with open('jobs.xml', 'w') as f:
            f.write('<jobs>\n')
            for item in self.table.get_children():
                value = self.table.item(item)['values']
                f.write(f'''
                <job>
                    <name>{value[0]}</name>
                    <des>{value[1]}</des>
                    <date>{value[2]}</date>
                </job>\n''')
            f.write('</jobs>') 
        
        messagebox.showinfo("Thong bao", "luu xml thanh cong")

    def save_xml_dom(self):
        pass

class MyHandler(xml.sax.ContentHandler):
    def __init__(self):
        self.content = ""
        self.current_job = {}
        self.jobs = []

    def startElement(self, name, attrs):
        self.content = ""

        if name == "job":
            self.current_job = {}

    def characters(self, content):
        self.content += content

    def endElement(self, name):
        if name in ("name", "des", "date"):
            self.current_job[name] = self.content.strip()

        elif name == "job":
            self.jobs.append(self.current_job)

if __name__ == "__main__":
    app = JobManager()
    app.mainloop()
```
# Quản lý sinh viên
```python
from __future__ import annotations
from tkinter import font
from dataclasses import dataclass
import tkinter as tk
from tkinter import ttk, messagebox
import xml.sax
from xml.sax.handler import ContentHandler

# =====================================================
# Student
# =====================================================
@dataclass
class Student:
    id: str
    fullname: str
    classroom: str
    age: int
    python: float
    java: float

# =====================================================
# Form
# =====================================================
class Form(tk.Tk):
    def __init__(self):
        super().__init__()

        # setup window
        self.title("Quản lý sinh viên")
        self.geometry("850x550")
        self.resizable(False, False)
        default_font = font.nametofont("TkDefaultFont")
        default_font.configure(
            family="Segoe UI",
            size=10
        )

        self.students = []
        self.selected_index = None
        self.entries = {}

        self.render()


    # =====================================================
    # Giao diện
    # =====================================================
    def render(self):
        # ---------------- Form ----------------
        fields = [
            ("Mã SV", "id"),
            ("Họ tên", "fullname"),
            ("Lớp", "classroom"),
            ("Tuổi", "age"),
            ("Python", "python"),
            ("Java", "java")
        ]
        for row, (label, key) in enumerate(fields):
            tk.Label(self, text=label).grid(row=row, column=0, sticky="w", pady=2)
            entry = tk.Entry(self, width=30)
            entry.grid(row=row, column=1, padx=5, pady=2)

            self.entries[key] = entry


        # ---------------- Button ----------------
        buttons = [
            ("Thêm", self.add_student),
            ("Sửa", self.update_student),
            ("Xóa", self.remove_student),
            ("Lưu XML", self.save_xml),
            ("Đọc XML", self.load_xml),
            ("Thống kê", self.statistic)
        ]
        for col, (text, command) in enumerate(buttons):
            tk.Button(
                self,
                text=text,
                width=10,
                command=command
            ).grid(
                row=6,
                column=col,
                padx=3,
                pady=8
            )


        # ---------------- Search ----------------
        tk.Label(self, text="Tìm tên").grid(
            row=7,
            column=0,
            sticky="w"
        )

        self.search_entry = tk.Entry(self)

        self.search_entry.grid(
            row=7,
            column=1,
            sticky="we"
        )

        tk.Button(
            self,
            text="Tìm",
            command=self.search
        ).grid(row=7, column=2)

        tk.Button(
            self,
            text="Sắp xếp tên",
            command=self.sort_name
        ).grid(row=7, column=3)

        tk.Button(
            self,
            text="Sắp xếp ĐTB",
            command=self.sort_average
        ).grid(row=7, column=4)


        # ---------------- TreeView ----------------

        columns = (
            "id",
            "fullname",
            "classroom",
            "age",
            "python",
            "java"
        )

        self.tree = ttk.Treeview(
            self,
            columns=columns,
            show="headings",
            height=12
        )

        for col in columns:
            self.tree.heading(col, text=col.upper())

            self.tree.column(
                col,
                width=100,
                anchor="center"
            )

        self.tree.grid(
            row=8,
            column=0,
            columnspan=6,
            sticky="nsew"
        )

        self.tree.bind(
            "<<TreeviewSelect>>",
            self.tree_selected
        )

        self.grid_rowconfigure(8, weight=1)
        self.grid_columnconfigure(1, weight=1)


    # =====================================================
    # Lấy dữ liệu từ Form
    # =====================================================
    def get_student(self):
        try:
            student = Student(
                id=self.entries["id"].get().strip(),
                fullname=self.entries["fullname"].get().strip(),
                classroom=self.entries["classroom"].get().strip(),
                age=int(self.entries["age"].get()),
                python=float(self.entries["python"].get()),
                java=float(self.entries["java"].get())
            )
        except ValueError:
            messagebox.showerror(
                "Lỗi",
                "Tuổi hoặc điểm không hợp lệ!"
            )

            return None

        # Không được để trống
        if not all([
            student.id,
            student.fullname,
            student.classroom
        ]):

            messagebox.showerror(
                "Lỗi",
                "Không được để trống!"
            )

            return None

        # Điểm phải từ 0 -> 10
        if not (
            0 <= student.python <= 10 and
            0 <= student.java <= 10
        ):

            messagebox.showerror(
                "Lỗi",
                "Điểm phải từ 0 đến 10!"
            )

            return None

        return student


    # =====================================================
    # Xóa Form
    # =====================================================

    def clear_form(self):
        for entry in self.entries.values():
            entry.delete(0, tk.END)



    # =====================================================
    # Thêm 1 dòng vào TreeView
    # =====================================================
    def insert_tree(self, student):
        self.tree.insert(
            "",
            tk.END,
            values=(
                student.id,
                student.fullname,
                student.classroom,
                student.age,
                student.python,
                student.java
            )
        )


    # =====================================================
    # Cập nhật TreeView
    # =====================================================

    def refresh_tree(self):

        self.tree.delete(*self.tree.get_children())

        for student in self.students:
            self.insert_tree(student)


    # =====================================================
    # Chọn dòng trên TreeView
    # =====================================================

    def tree_selected(self, event):

        selected = self.tree.selection()

        if not selected:
            return

        self.selected_index = self.tree.index(selected[0])

        values = self.tree.item(selected[0])["values"]

        self.clear_form()

        keys = [
            "id",
            "fullname",
            "classroom",
            "age",
            "python",
            "java"
        ]

        for key, value in zip(keys, values):
            self.entries[key].insert(0, value)

    # =====================================================
    # Thêm sinh viên
    # =====================================================

    def add_student(self):

        student = self.get_student()

        if student is None:
            return

        # Kiểm tra trùng mã
        if any(s.id == student.id for s in self.students):

            messagebox.showerror(
                "Lỗi",
                "Mã sinh viên đã tồn tại!"
            )

            return

        self.students.append(student)
        self.insert_tree(student)
        self.clear_form()
        self.selected_index = None


    # =====================================================
    # Sửa sinh viên
    # =====================================================
    def update_student(self):
        if self.selected_index is None:
            messagebox.showwarning("Thông báo", "Hãy chọn sinh viên!")

            return

        student = self.get_student()

        if student is None:
            return

        # Kiểm tra trùng mã (bỏ qua chính nó)
        for i, s in enumerate(self.students):
            if i != self.selected_index and s.id == student.id:
                messagebox.showerror("Lỗi", "Mã sinh viên đã tồn tại!")

                return

        self.students[self.selected_index] = student
        self.refresh_tree()
        self.clear_form()
        self.selected_index = None


    # =====================================================
    # Xóa sinh viên
    # =====================================================

    def remove_student(self):

        if self.selected_index is None:

            messagebox.showwarning(
                "Thông báo",
                "Hãy chọn sinh viên!"
            )

            return

        if not messagebox.askyesno(
            "Xác nhận",
            "Bạn có chắc muốn xóa?"
        ):
            return

        self.students.pop(self.selected_index)
        self.refresh_tree()
        self.clear_form()
        self.selected_index = None

    # =====================================================
    # Lưu XML
    # =====================================================

    def save_xml(self):
        with open("students.xml", "w", encoding="utf-8") as f:
            f.write("<students>\n")

            for s in self.students:
                f.write(f"""
                    <student>
                        <id>{s.id}</id>
                        <fullname>{s.fullname}</fullname>
                        <classroom>{s.classroom}</classroom>
                        <age>{s.age}</age>
                        <python>{s.python}</python>
                        <java>{s.java}</java>
                    </student>
                """)

            f.write("</students>")

        messagebox.showinfo(
            "Thông báo",
            "Lưu XML thành công!"
        )


    # =====================================================
    # Đọc XML bằng SAX
    # =====================================================

    def load_xml(self):

        try:

            handler = StudentHandler()

            xml.sax.parse(
                "students.xml",
                handler
            )

            self.students = handler.students

            self.refresh_tree()

            self.clear_form()

            messagebox.showinfo(
                "Thông báo",
                "Đọc XML thành công!"
            )

        except:

            messagebox.showerror(
                "Lỗi",
                "Không đọc được file XML!"
            )

    # =====================================================
    # Tìm kiếm theo tên
    # =====================================================

    def search(self):

        keyword = self.search_entry.get().strip().lower()

        self.tree.delete(*self.tree.get_children())

        for student in self.students:

            if keyword in student.fullname.lower():

                self.insert_tree(student)


    # =====================================================
    # Sắp xếp theo tên
    # =====================================================

    def sort_name(self):

        self.students.sort(
            key=lambda s: s.fullname.lower()
        )

        self.refresh_tree()


    # =====================================================
    # Sắp xếp theo điểm trung bình
    # =====================================================

    def sort_average(self):

        self.students.sort(
            key=lambda s: (s.python + s.java) / 2,
            reverse=True
        )

        self.refresh_tree()


    # =====================================================
    # Thống kê
    # =====================================================

    def statistic(self):

        if not self.students:

            messagebox.showinfo(
                "Thông báo",
                "Chưa có dữ liệu!"
            )

            return

        scores = [
            (s.python + s.java) / 2
            for s in self.students
        ]

        messagebox.showinfo(
            "Thống kê",

            f"""Tổng sinh viên: {len(self.students)}

    Điểm TB lớp: {sum(scores)/len(scores):.2f}

    Điểm cao nhất: {max(scores):.2f}

    Điểm thấp nhất: {min(scores):.2f}
    """
        )

# =====================================================
# SAX Handler
# =====================================================

class StudentHandler(ContentHandler):

    def __init__(self):

        self.students = []
        self.student = None
        self.tag = ""

    def startElement(self, name, attrs):

        self.tag = name

        if name == "student":

            self.student = Student(
                "", "", "", 0, 0, 0
            )

    def characters(self, content):

        content = content.strip()

        if not content:
            return

        match self.tag:

            case "id":
                self.student.id = content

            case "fullname":
                self.student.fullname = content

            case "classroom":
                self.student.classroom = content

            case "age":
                self.student.age = int(content)

            case "python":
                self.student.python = float(content)

            case "java":
                self.student.java = float(content)

    def endElement(self, name):

        if name == "student":
            self.students.append(self.student)

        self.tag = ""

# =====================================================
# Main
# =====================================================
if __name__ == "__main__":
    app = Form()
    app.mainloop()
```
# Quản lý nhân viên
```bash
Quản lý nhân viên gồm (Mã nhân viên)
    - Họ tên
    - Phòng ban
    - Tuổi
    - Lương
    - Thưởng

Chức năng:
    - Thêm
    - Sửa
    - Xóa
    - Tìm kiếm
    - Sắp xếp
    - Thống kê
    - Lưu XML bằng DOM (minidom)
    - Đọc XML bằng DOM (minidom)
```
```python
from __future__ import annotations

from dataclasses import dataclass
import tkinter as tk
from tkinter import ttk, messagebox
from xml.dom import minidom


# =====================================================
# Employee
# =====================================================

@dataclass
class Employee:
    id: str
    fullname: str
    department: str
    age: int
    salary: float
    bonus: float


# =====================================================
# Form
# =====================================================

class Form(tk.Frame):

    def __init__(self, master):

        super().__init__(master)

        self.pack(fill="both", expand=True, padx=10, pady=10)

        self.employees = []
        self.selected_index = None
        self.entries = {}

        self.render()


    # =====================================================
    # Giao diện
    # =====================================================

    def render(self):

        # ---------------- Form ----------------

        fields = [
            ("Mã NV", "id"),
            ("Họ tên", "fullname"),
            ("Phòng ban", "department"),
            ("Tuổi", "age"),
            ("Lương", "salary"),
            ("Thưởng", "bonus")
        ]

        for row, (label, key) in enumerate(fields):

            tk.Label(self, text=label).grid(
                row=row,
                column=0,
                sticky="w",
                pady=3
            )

            entry = tk.Entry(self, width=30)

            entry.grid(
                row=row,
                column=1,
                padx=5,
                pady=3
            )

            self.entries[key] = entry


        # ---------------- Button ----------------

        buttons = [

            ("Thêm", self.add_employee),

            ("Sửa", self.update_employee),

            ("Xóa", self.remove_employee),

            ("Lưu XML", self.save_xml),

            ("Đọc XML", self.load_xml),

            ("Thống kê", self.statistic)

        ]

        for col, (text, command) in enumerate(buttons):

            tk.Button(
                self,
                text=text,
                width=10,
                command=command
            ).grid(
                row=6,
                column=col,
                padx=3,
                pady=8
            )


        # ---------------- Search ----------------

        tk.Label(self, text="Tìm tên").grid(
            row=7,
            column=0,
            sticky="w"
        )

        self.search_entry = tk.Entry(self)

        self.search_entry.grid(
            row=7,
            column=1,
            sticky="we"
        )

        tk.Button(
            self,
            text="Tìm",
            command=self.search
        ).grid(row=7, column=2)

        tk.Button(
            self,
            text="Sắp xếp tên",
            command=self.sort_name
        ).grid(row=7, column=3)

        tk.Button(
            self,
            text="Sắp xếp tổng",
            command=self.sort_income
        ).grid(row=7, column=4)


        # ---------------- TreeView ----------------

        columns = (
            "id",
            "fullname",
            "department",
            "age",
            "salary",
            "bonus"
        )

        self.tree = ttk.Treeview(
            self,
            columns=columns,
            show="headings",
            height=12
        )

        for col in columns:

            self.tree.heading(col, text=col.upper())

            self.tree.column(
                col,
                width=100,
                anchor="center"
            )

        self.tree.grid(
            row=8,
            column=0,
            columnspan=6,
            sticky="nsew"
        )

        self.tree.bind(
            "<<TreeviewSelect>>",
            self.tree_selected
        )

        self.grid_rowconfigure(8, weight=1)
        self.grid_columnconfigure(1, weight=1)


    # =====================================================
    # Các hàm sẽ viết ở phần sau
    # =====================================================

    # =====================================================
    # Lấy dữ liệu từ Form
    # =====================================================

    def get_employee(self):

        try:

            employee = Employee(
                id=self.entries["id"].get().strip(),
                fullname=self.entries["fullname"].get().strip(),
                department=self.entries["department"].get().strip(),
                age=int(self.entries["age"].get()),
                salary=float(self.entries["salary"].get()),
                bonus=float(self.entries["bonus"].get())
            )

        except ValueError:

            messagebox.showerror(
                "Lỗi",
                "Tuổi, lương hoặc thưởng không hợp lệ!"
            )

            return None

        # Kiểm tra dữ liệu rỗng
        if not all([
            employee.id,
            employee.fullname,
            employee.department
        ]):

            messagebox.showerror(
                "Lỗi",
                "Không được để trống!"
            )

            return None

        # Kiểm tra dữ liệu hợp lệ
        if (
            employee.age <= 0 or
            employee.salary < 0 or
            employee.bonus < 0
        ):

            messagebox.showerror(
                "Lỗi",
                "Dữ liệu không hợp lệ!"
            )

            return None

        return employee


    # =====================================================
    # Xóa dữ liệu trên Form
    # =====================================================

    def clear_form(self):

        for entry in self.entries.values():
            entry.delete(0, tk.END)

        self.selected_index = None


    # =====================================================
    # Thêm một dòng vào TreeView
    # =====================================================

    def insert_tree(self, employee):

        self.tree.insert(
            "",
            tk.END,
            values=(
                employee.id,
                employee.fullname,
                employee.department,
                employee.age,
                employee.salary,
                employee.bonus
            )
        )


    # =====================================================
    # Hiển thị lại TreeView
    # =====================================================

    def refresh_tree(self):

        self.tree.delete(*self.tree.get_children())

        for employee in self.employees:

            self.insert_tree(employee)


    # =====================================================
    # Chọn một dòng trên TreeView
    # =====================================================

    def tree_selected(self, event):

        selected = self.tree.selection()

        if not selected:
            return

        # Lưu vị trí đang chọn
        self.selected_index = self.tree.index(selected[0])

        values = self.tree.item(selected[0])["values"]

        self.clear_form()

        keys = [
            "id",
            "fullname",
            "department",
            "age",
            "salary",
            "bonus"
        ]

        for key, value in zip(keys, values):

            self.entries[key].insert(0, value)

    # =====================================================
    # Thêm nhân viên
    # =====================================================

    def add_employee(self):

        employee = self.get_employee()

        if employee is None:
            return

        # Kiểm tra trùng mã
        if any(e.id == employee.id for e in self.employees):

            messagebox.showerror(
                "Lỗi",
                "Mã nhân viên đã tồn tại!"
            )

            return

        self.employees.append(employee)

        self.insert_tree(employee)

        self.clear_form()

        messagebox.showinfo(
            "Thông báo",
            "Thêm thành công!"
        )


    # =====================================================
    # Sửa nhân viên
    # =====================================================

    def update_employee(self):

        if self.selected_index is None:

            messagebox.showwarning(
                "Thông báo",
                "Hãy chọn nhân viên!"
            )

            return

        employee = self.get_employee()

        if employee is None:
            return

        # Kiểm tra trùng mã (bỏ qua chính dòng đang sửa)
        for i, e in enumerate(self.employees):

            if (
                i != self.selected_index and
                e.id == employee.id
            ):

                messagebox.showerror(
                    "Lỗi",
                    "Mã nhân viên đã tồn tại!"
                )

                return

        self.employees[self.selected_index] = employee

        self.refresh_tree()

        self.clear_form()

        messagebox.showinfo(
            "Thông báo",
            "Sửa thành công!"
        )


    # =====================================================
    # Xóa nhân viên
    # =====================================================

    def remove_employee(self):

        if self.selected_index is None:

            messagebox.showwarning(
                "Thông báo",
                "Hãy chọn nhân viên!"
            )

            return

        if not messagebox.askyesno(
            "Xác nhận",
            "Bạn có chắc muốn xóa?"
        ):
            return

        self.employees.pop(self.selected_index)

        self.refresh_tree()

        self.clear_form()

        messagebox.showinfo(
            "Thông báo",
            "Xóa thành công!"
        )

    # =====================================================
    # Lưu XML bằng DOM
    # =====================================================

    def save_xml(self):

        # Tạo document
        doc = minidom.Document()

        # Root
        root = doc.createElement("employees")
        doc.appendChild(root)

        # Thêm từng nhân viên
        for employee in self.employees:

            employee_node = doc.createElement("employee")

            data = {
                "id": employee.id,
                "fullname": employee.fullname,
                "department": employee.department,
                "age": employee.age,
                "salary": employee.salary,
                "bonus": employee.bonus
            }

            for tag, value in data.items():

                node = doc.createElement(tag)

                text = doc.createTextNode(str(value))

                node.appendChild(text)

                employee_node.appendChild(node)

            root.appendChild(employee_node)

        # Ghi file
        with open("employees.xml", "w", encoding="utf-8") as file:

            file.write(
                doc.toprettyxml(indent="    ")
            )

        messagebox.showinfo(
            "Thông báo",
            "Lưu XML thành công!"
        )

    # =====================================================
    # Đọc XML bằng DOM
    # =====================================================

    def load_xml(self):

        try:

            doc = minidom.parse("employees.xml")

            self.employees.clear()

            employee_nodes = doc.getElementsByTagName(
                "employee"
            )

            for node in employee_nodes:

                employee = Employee(

                    id=node.getElementsByTagName("id")[0].firstChild.data,

                    fullname=node.getElementsByTagName("fullname")[0].firstChild.data,

                    department=node.getElementsByTagName("department")[0].firstChild.data,

                    age=int(
                        node.getElementsByTagName("age")[0].firstChild.data
                    ),

                    salary=float(
                        node.getElementsByTagName("salary")[0].firstChild.data
                    ),

                    bonus=float(
                        node.getElementsByTagName("bonus")[0].firstChild.data
                    )

                )

                self.employees.append(employee)

            self.refresh_tree()

            self.clear_form()

            messagebox.showinfo(
                "Thông báo",
                "Đọc XML thành công!"
            )

        except Exception:

            messagebox.showerror(
                "Lỗi",
                "Không đọc được file XML!"
            )

    # =====================================================
    # Tìm kiếm theo tên
    # =====================================================

    def search(self):

        keyword = self.search_entry.get().strip().lower()

        self.tree.delete(*self.tree.get_children())

        for employee in self.employees:

            if keyword in employee.fullname.lower():

                self.insert_tree(employee)


    # =====================================================
    # Sắp xếp theo tên
    # =====================================================

    def sort_name(self):

        self.employees.sort(
            key=lambda e: e.fullname.lower()
        )

        self.refresh_tree()


    # =====================================================
    # Sắp xếp theo tổng thu nhập
    # =====================================================

    def sort_income(self):

        self.employees.sort(
            key=lambda e: e.salary + e.bonus,
            reverse=True
        )

        self.refresh_tree()


    # =====================================================
    # Thống kê
    # =====================================================

    def statistic(self):

        if not self.employees:

            messagebox.showinfo(
                "Thông báo",
                "Chưa có dữ liệu!"
            )
            return

        incomes = [
            employee.salary + employee.bonus
            for employee in self.employees
        ]

        messagebox.showinfo(

            "Thống kê",

            f"""Tổng nhân viên: {len(self.employees)}

    Tổng thu nhập TB: {sum(incomes)/len(incomes):.2f}

    Thu nhập cao nhất: {max(incomes):.2f}

    Thu nhập thấp nhất: {min(incomes):.2f}
    """
        )

# =====================================================
# Main
# =====================================================

if __name__ == "__main__":

    root = tk.Tk()

    root.title("Quản lý nhân viên")

    root.geometry("850x550")

    Form(root)

    root.mainloop()
```
# Quản lý sản phẩm
```bash
Thông tin sản phẩm
    - Mã sản phẩm
    - Tên sản phẩm
    - Loại
    - Số lượng
    - Đơn giá
    - Nhà sản xuất

Chức năng
    - Thêm
    - Sửa
    - Xóa
    - Lưu JSON
    - Đọc JSON
    - Tìm kiếm
    - Sắp xếp
    - Thống kê
```
```python
from __future__ import annotations
from dataclasses import dataclass, asdict
import tkinter as tk
from tkinter import ttk, messagebox
import json


# =====================================================
# Product
# =====================================================

@dataclass
class Product:
    id: str
    name: str
    category: str
    quantity: int
    price: float
    manufacturer: str


# =====================================================
# Form
# =====================================================

class Form(tk.Frame):

    def __init__(self, master):

        super().__init__(master)

        self.pack(fill="both", expand=True, padx=10, pady=10)

        self.products = []
        self.selected_index = None
        self.entries = {}

        self.render()


    # =====================================================
    # Giao diện
    # =====================================================

    def render(self):

        fields = [

            ("Mã SP", "id"),

            ("Tên SP", "name"),

            ("Loại", "category"),

            ("Số lượng", "quantity"),

            ("Đơn giá", "price"),

            ("Nhà SX", "manufacturer")

        ]

        for row, (label, key) in enumerate(fields):

            tk.Label(
                self,
                text=label
            ).grid(row=row, column=0, sticky="w")

            entry = tk.Entry(self, width=30)

            entry.grid(row=row, column=1, pady=3)

            self.entries[key] = entry


        buttons = [

            ("Thêm", self.add_product),

            ("Sửa", self.update_product),

            ("Xóa", self.remove_product),

            ("Lưu JSON", self.save_json),

            ("Đọc JSON", self.load_json),

            ("Thống kê", self.statistic)

        ]

        for col, (text, command) in enumerate(buttons):

            tk.Button(
                self,
                text=text,
                width=10,
                command=command
            ).grid(row=6, column=col)


        tk.Label(
            self,
            text="Tìm tên"
        ).grid(row=7, column=0)

        self.search_entry = tk.Entry(self)

        self.search_entry.grid(row=7, column=1)

        tk.Button(
            self,
            text="Tìm",
            command=self.search
        ).grid(row=7, column=2)

        tk.Button(
            self,
            text="Sắp xếp tên",
            command=self.sort_name
        ).grid(row=7, column=3)

        tk.Button(
            self,
            text="Sắp xếp giá",
            command=self.sort_price
        ).grid(row=7, column=4)


        columns = (
            "id",
            "name",
            "category",
            "quantity",
            "price",
            "manufacturer"
        )

        self.tree = ttk.Treeview(
            self,
            columns=columns,
            show="headings",
            height=12
        )

        for col in columns:

            self.tree.heading(col, text=col.upper())

            self.tree.column(
                col,
                width=100,
                anchor="center"
            )

        self.tree.grid(
            row=8,
            column=0,
            columnspan=6,
            sticky="nsew"
        )

        self.tree.bind(
            "<<TreeviewSelect>>",
            self.tree_selected
        )


    # ==========================
    # Viết ở các phần sau
    # ==========================

    # =====================================================
    # Lấy dữ liệu từ Form
    # =====================================================
    
    def get_product(self):
    
        try:
        
            product = Product(
                id=self.entries["id"].get().strip(),
                name=self.entries["name"].get().strip(),
                category=self.entries["category"].get().strip(),
                quantity=int(self.entries["quantity"].get()),
                price=float(self.entries["price"].get()),
                manufacturer=self.entries["manufacturer"].get().strip()
            )
    
        except ValueError:
        
            messagebox.showerror(
                "Lỗi",
                "Số lượng hoặc đơn giá không hợp lệ!"
            )
    
            return None
    
        # Kiểm tra dữ liệu rỗng
        if not all([
            product.id,
            product.name,
            product.category,
            product.manufacturer
        ]):
    
            messagebox.showerror(
                "Lỗi",
                "Không được để trống!"
            )
    
            return None
    
        # Kiểm tra dữ liệu hợp lệ
        if (
            product.quantity < 0 or
            product.price < 0
        ):
    
            messagebox.showerror(
                "Lỗi",
                "Số lượng và đơn giá phải >= 0!"
            )
    
            return None
    
        return product
    
    
    # =====================================================
    # Xóa dữ liệu trên Form
    # =====================================================
    
    def clear_form(self):
    
        for entry in self.entries.values():
            entry.delete(0, tk.END)
    
        self.selected_index = None
    
    
    # =====================================================
    # Thêm một dòng vào TreeView
    # =====================================================
    
    def insert_tree(self, product):
    
        self.tree.insert(
            "",
            tk.END,
            values=(
                product.id,
                product.name,
                product.category,
                product.quantity,
                product.price,
                product.manufacturer
            )
        )
    
    
    # =====================================================
    # Hiển thị lại TreeView
    # =====================================================
    
    def refresh_tree(self):
    
        self.tree.delete(*self.tree.get_children())
    
        for product in self.products:
        
            self.insert_tree(product)
    
    
    # =====================================================
    # Chọn một dòng trên TreeView
    # =====================================================
    
    def tree_selected(self, event):
    
        selected = self.tree.selection()
    
        if not selected:
            return
    
        # Lưu vị trí đang chọn
        self.selected_index = self.tree.index(selected[0])
    
        values = self.tree.item(selected[0])["values"]
    
        self.clear_form()
    
        keys = [
            "id",
            "name",
            "category",
            "quantity",
            "price",
            "manufacturer"
        ]
    
        for key, value in zip(keys, values):
        
            self.entries[key].insert(0, value)

    # =====================================================
    # Thêm sản phẩm
    # =====================================================

    def add_product(self):

        product = self.get_product()

        if product is None:
            return

        # Kiểm tra trùng mã
        if any(p.id == product.id for p in self.products):

            messagebox.showerror(
                "Lỗi",
                "Mã sản phẩm đã tồn tại!"
            )

            return

        self.products.append(product)

        self.insert_tree(product)

        self.clear_form()

        messagebox.showinfo(
            "Thông báo",
            "Thêm thành công!"
        )


    # =====================================================
    # Sửa sản phẩm
    # =====================================================

    def update_product(self):

        if self.selected_index is None:

            messagebox.showwarning(
                "Thông báo",
                "Hãy chọn sản phẩm!"
            )

            return

        product = self.get_product()

        if product is None:
            return

        # Kiểm tra trùng mã (bỏ qua chính dòng đang sửa)
        for i, p in enumerate(self.products):

            if (
                i != self.selected_index and
                p.id == product.id
            ):

                messagebox.showerror(
                    "Lỗi",
                    "Mã sản phẩm đã tồn tại!"
                )

                return

        self.products[self.selected_index] = product

        self.refresh_tree()

        self.clear_form()

        messagebox.showinfo(
            "Thông báo",
            "Sửa thành công!"
        )


    # =====================================================
    # Xóa sản phẩm
    # =====================================================

    def remove_product(self):

        if self.selected_index is None:

            messagebox.showwarning(
                "Thông báo",
                "Hãy chọn sản phẩm!"
            )

            return

        if not messagebox.askyesno(
            "Xác nhận",
            "Bạn có chắc muốn xóa?"
        ):
            return

        self.products.pop(self.selected_index)

        self.refresh_tree()

        self.clear_form()

        messagebox.showinfo(
            "Thông báo",
            "Xóa thành công!"
        )

    # =====================================================
    # Lưu JSON
    # =====================================================

    def save_json(self):

        data = [
            asdict(product)
            for product in self.products
        ]

        with open(
            "products.json",
            "w",
            encoding="utf-8"
        ) as file:

            json.dump(
                data,
                file,
                indent=4,
                ensure_ascii=False
            )

        messagebox.showinfo(
            "Thông báo",
            "Lưu JSON thành công!"
        )

    # =====================================================
    # Đọc JSON
    # =====================================================

    def load_json(self):

        try:

            with open(
                "products.json",
                "r",
                encoding="utf-8"
            ) as file:

                data = json.load(file)

            self.products = [
                Product(**item)
                for item in data
            ]

            self.refresh_tree()

            self.clear_form()

            messagebox.showinfo(
                "Thông báo",
                "Đọc JSON thành công!"
            )

        except Exception:

            messagebox.showerror(
                "Lỗi",
                "Không đọc được file JSON!"
            )

    # =====================================================
    # Tìm kiếm theo tên
    # =====================================================
    
    def search(self):
    
        keyword = self.search_entry.get().strip().lower()
    
        self.tree.delete(*self.tree.get_children())
    
        for product in self.products:
        
            if keyword in product.name.lower():
            
                self.insert_tree(product)
    
    
    # =====================================================
    # Sắp xếp theo tên
    # =====================================================
    
    def sort_name(self):
    
        self.products.sort(
            key=lambda p: p.name.lower()
        )
    
        self.refresh_tree()
    
    
    # =====================================================
    # Sắp xếp theo đơn giá
    # =====================================================
    
    def sort_price(self):
    
        self.products.sort(
            key=lambda p: p.price,
            reverse=True
        )
    
        self.refresh_tree()
    
    
    # =====================================================
    # Thống kê
    # =====================================================
    
    def statistic(self):
    
        if not self.products:
        
            messagebox.showinfo(
                "Thông báo",
                "Chưa có dữ liệu!"
            )
            return
    
        total_quantity = sum(
            p.quantity for p in self.products
        )
    
        total_value = sum(
            p.quantity * p.price
            for p in self.products
        )
    
        average_price = (
            sum(p.price for p in self.products)
            / len(self.products)
        )
    
        max_price = max(
            p.price for p in self.products
        )
    
        min_price = min(
            p.price for p in self.products
        )
    
        messagebox.showinfo(
        
            "Thống kê",
    
            f"""Tổng sản phẩm: {len(self.products)}
    
    Tổng số lượng: {total_quantity}
    
    Tổng giá trị kho: {total_value:.2f}
    
    Đơn giá trung bình: {average_price:.2f}
    
    Đơn giá cao nhất: {max_price:.2f}
    
    Đơn giá thấp nhất: {min_price:.2f}
    """
        )


# =====================================================
# Main
# =====================================================

if __name__ == "__main__":

    root = tk.Tk()

    root.title("Quản lý sản phẩm")

    root.geometry("850x550")

    Form(root)

    root.mainloop()
```