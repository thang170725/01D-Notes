# Dataclasses Introduction (tự động tạo các hàm khởi tạo và các hàm tiện ích cho class chỉ chứa dữ liệu)
```bash
là thư viện builtin của Python (từ Python 3.7 trở lên), nên không cần cài bằng pip.
```
**Ex1: không dùng dataclass, bạn phải viết rất nhiều code**
```python
class Student:
    def __init__(self, name, age, score):
        self.name = name
        self.age = age
        self.score = score

# Muốn in đẹp hơn lại phải viết
def __repr__(self):
    ...

# Muốn so sánh
def __eq__(self):
    ...

# Muốn sort
def __lt__(self):
    ...

# => Rất nhiều code lặp.
```
**Ex2: Dùng dataclass**
```python
from dataclasses import dataclass

@dataclass
class Student:
    name: str
    age: int
    score: float

# Chỉ 4 dòng. Python tự sinh:
# __init__
# __repr__
# __eq__
```
# dataclass
**Ex1**
```python
from dataclasses import dataclass

@dataclass
class Student:
    name: str
    age: int
    score: float


s = Student("Nam", 20, 8.5)

print(s) # Student(name='Nam', age=20, score=8.5)
# Trong khi class bình thường sẽ là <__main__.Student object at 0x000001A4F...>
```
**Ex2: init được tạo sẵn**
```python
# Bạn không hề viết __init__ Nhưng vẫn gọi được
s = Student("Nam", 20, 8.5)

print(s.name) # Nam
print(s.age) # 20

# Python đã tự sinh
# def __init__(self, name, age, score):
#     self.name = name
#     self.age = age
#     self.score = score
```
**Ex3: So sánh object**
```python
from dataclasses import dataclass

@dataclass
class Student:
    name: str
    age: int

a = Student("Nam", 20)
b = Student("Nam", 20)
c = Student("Lan", 20)

print(a == b) # True
print(a == c) # False


# Nếu là class bình thường
class Student:
    def __init__(self, name, age):
        self.name = name
        self.age = age

a = Student("Nam",20)
b = Student("Nam",20)

print(a == b) # False. vì Python so địa chỉ bộ nhớ.
```
# asdict()
**Ex4: Chuyển sang dict**
```python
dataclasses còn có hàm asdict().

from dataclasses import dataclass, asdict

@dataclass
class Student:
    name: str
    age: int
    score: float

s = Student("Nam", 20, 8.5)

print(asdict(s))
# {
#     'name': 'Nam',
#     'age': 20,
#     'score': 8.5
# }
```