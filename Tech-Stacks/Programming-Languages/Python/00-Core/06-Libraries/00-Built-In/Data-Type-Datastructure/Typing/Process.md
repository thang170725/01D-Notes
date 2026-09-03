- [Dict](#dict)
- [List](#list)
- [Protocol](#protocol)
- [Tuple](#tuple)
- [TypeDict (mô tả kiểu dictionary trong đó mỗi key có kiểu dữ liệu xác định)](#typedict-mô-tả-kiểu-dictionary-trong-đó-mỗi-key-có-kiểu-dữ-liệu-xác-định)
- [Annotated (gắn thêm metadata cho một kiểu dữ liệu)](#annotated-gắn-thêm-metadata-cho-một-kiểu-dữ-liệu)
---
# Dict 
```python
from typing import Dict

def count_words(words: List[str]) -> Dict[str, int]:
    counts = {}
    for w in words:
        counts[w] = counts.get(w, 0) + 1
    return counts

print(count_words(["a", "b", "a"]))

# IDE sẽ gợi ý rằng key là str, value là int.
```
# List
```python
from typing import List

def sum_list(numbers: List[int]) -> List[int]:
    return numbers

print(sum_list([1, 2, 3]))          # truyền đúng -> không lỗi
print(sum_list(["a", "b", "c"]))    # truyền sai -> không lỗi

# Chỉ dùng để gợi ý cho IDE không gây lỗi runtime dù có truyền sai
```
```bash
- Trong Python typing, Union dùng để khai báo rằng một biến / tham số / giá trị trả về có thể thuộc nhiều kiểu khác nhau.
- Dùng khi:
    + Hàm nhận nhiều kiểu đầu vào
    + Giá trị trả về không cố định 1 kiểu
    + Viết API / thư viện rõ ràng hơn
- Không cần dùng khi:
    + Kiểu dữ liệu luôn cố định
    + Code nhỏ, dùng nhanh, không cần type check
- Lưu ý: Union không ép kiểu, nó chỉ để:
    + IDE gợi ý
    + Tool kiểm tra type (mypy, pyright…)
    + Code rõ ràng hơn
    + Union rất hay dùng khi bạn cần xử lý khác nhau theo kiểu dữ liệu.
```
**Syn**
```bash
Union[Kiểu1, Kiểu2, Kiểu3, ...]
- Nghĩa là: giá trị có thể là Kiểu1 hoặc Kiểu2 hoặc Kiểu3…
```
**Ex**
```python
from typing import Union

def double(x: Union[int, float]) -> Union[int, float]:
    return x * 2

print(double(5))
print(double(2.5))

# 10
# 5.0
# Hàm trả về int hoặc float
```
**Ex**
```python
def show(value: Union[int, str, bool]):
    print(value)
show(10)
show("hello")
show(True)

# 10
# hello
# True
```
from typing import Union

def process(x: Union[int, str]):
    if isinstance(x, int):
        return x + 1
    else:
        return x.upper()

Chạy thử
print(process(5))
print(process("python"))

Kết quả
6
PYTHON

1. Cú pháp mới (Python 3.10+)

Từ Python 3.10, bạn có thể viết ngắn gọn hơn:

def double(x: int | float) -> int | float:
    return x * 2


👉 Hai cách này hoàn toàn tương đương:

Union[int, float]
int | float
# Protocol
**Ex**
```python
# 1. Định nghĩa "interface" bằng Protocol
class Speaker(Protocol):
    def speak(self) -> str:
        ...

# 2. Các class KHÔNG cần kế thừa Speaker
class Dog:
    def speak(self) -> str:
        return "Gâu gâu"

class Human:
    def speak(self) -> str:
        return "Hello"

class Robot:
    def speak(self) -> str:
        return "Beep beep"

# 3. Class KHÔNG đúng interface
class Cat:
    def meow(self) -> str:
        return "Meo meo"

# 4. Hàm dùng duck typing
def make_sound(x: Speaker) -> None:
    print(x.speak())

if __name__ == "__main__":
    make_sound(Dog())
    make_sound(Human())
    make_sound(Robot())
    make_sound(Cat())
```
**Ex2**
```python
from typing import Protocol

class Information(Protocol):
    def information():
        pass

class Student:
    def __init__(self, gpa):
        self.gpa = gpa
        
    def information(self):
        if self.gpa > 3.2:
            return "Được khen thưởng"
        else:
            return "Không được khen"

class Teacher:
    def __init__(self, research):
        self.research = research
        
    def information(self):
        if self.research >= 2 :
            return "Được khen thưởng"
        else:
            return "Không được khen"

class Manager:
    def __init__(self):
        ...
    def information(self):
        return "được khen thưởng"

def main_information(obj : Information):
    print(obj.information())  

s = Student(3.2)
t = Teacher(3)
m = Manager()

main_information(s)
main_information(t)
main_information(m)
```
# Tuple
```python
from typing import Tuple

def get_user() -> Tuple[int, str]:
    return (1, "Thắng")

user = get_user()
print(user)

# IDE sẽ hiểu tuple luôn có đúng 2 phần tử: int và str.
```
# TypeDict (mô tả kiểu dictionary trong đó mỗi key có kiểu dữ liệu xác định)
```bash
Nó rất hữu ích khi làm việc với type hint và các công cụ như mypy, pyright, hoặc IDE
```
**Ex**
```bash
from typing import TypedDict

class User(TypedDict):
    name: str
    age: int
    email: str

user: User = {
    "name": "Alice",
    "age": 25,
    "email": "alice@example.com"
}

print(user["name"])

# Nếu khai báo sai kiểu:

# user: User = {
#     "name": "Alice",
#     "age": "25",      # Sai, phải là int
#     "email": "alice@example.com"
# }

# Type checker sẽ báo lỗi
```
# Annotated (gắn thêm metadata cho một kiểu dữ liệu) 
```bash
Bản thân type checker vẫn xem nó là kiểu gốc, nhưng các framework (ví dụ: FastAPI, Pydantic, Typer, LangGraph, ...) có thể đọc metadata này để thực hiện các hành vi đặc biệt.

Annotated không thay đổi kiểu dữ liệu, mà chỉ cung cấp thông tin cho LangGraph.
```