- [__future__](#future)
  - [annotations (đây là tính năng của Python. Nó cho phép sử dụng tên class trước khi class được khai báo)](#annotations-đây-là-tính-năng-của-python-nó-cho-phép-sử-dụng-tên-class-trước-khi-class-được-khai-báo)
---
# __future__ 
## annotations (đây là tính năng của Python. Nó cho phép sử dụng tên class trước khi class được khai báo)
```bash
Annotation là thông tin chú thích về kiểu dữ liệu (type hint).
    Ví dụ:
        def add(a: int, b: int) -> int:
            return a + b
        # a: int

Annotation không bắt Python ép kiểu.
    Ví dụ
        def add(a: int, b: int) -> int:
            return a + b

        print(add("3", "5")) # 35
    
    vì annotation chỉ để:
        - IDE gợi ý
        - mypy kiểm tra kiểu
        - lập trình viên dễ đọc code
```
**Ex1: Không dùng __future__**
```python
def get_student() -> Student:
    return Student()

class Student:
    pass

# Python sẽ đọc file từ trên xuống.
# Đến đây Student Python hỏi: Student là ai? Nhưng class chưa được tạo.
# Kết quả NameError hoặc NameError: name 'Student' is not defined
```
**Ex: Có from __future__ import annotations**
```python
from __future__ import annotations

def get_student() -> Student:
    return Student()

class Student:
    pass

# Lần này Python không cố tìm Student ngay. Nó tự hiểu là "Student" -> nên không lỗi.
```
**Ex**
```python
# Nếu không có
from __future__ import annotations # Python cũ sẽ báo lỗi.

def test() -> FilterResult: # trong khi FilterResult nằm phía dưới.
```