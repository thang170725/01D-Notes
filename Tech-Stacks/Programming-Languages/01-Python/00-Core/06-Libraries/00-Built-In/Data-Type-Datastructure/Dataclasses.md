- [Dataclasses Introduction (tự động tạo các hàm khởi tạo và các hàm tiện ích cho class chỉ chứa dữ liệu)](#dataclasses-introduction-tự-động-tạo-các-hàm-khởi-tạo-và-các-hàm-tiện-ích-cho-class-chỉ-chứa-dữ-liệu)
- [dataclass](#dataclass)
  - [__dict__](#dict)
- [field() (cho phép cấu hình từng thuộc tính)](#field-cho-phép-cấu-hình-từng-thuộc-tính)
- [asdict() (Chuyển sang dict)](#asdict-chuyển-sang-dict)
---
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
**Syn**
```bash
@dataclass(slots=True)
class ...:

- Input:
    + slots=True: giúp giảm bộ nhớ sử dụng và tăng tốc truy cập thuộc tính
```
**Ex1**
```python
from dataclasses import dataclass

@dataclass
class Student:
    name: str
    age: int
    score: float


s = Student("Nam", 20, 8.5) # bạn không hề viết __init__ Nhưng vẫn gọi được, python đã tự sinh __init__(self, name, age, score):

print(s) # Student(name='Nam', age=20, score=8.5)
# Trong khi class bình thường sẽ là <__main__.Student object at 0x000001A4F...>
```
**Ex2: So sánh object**
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
**Ex3: dùng với slot**
```python
# không dùng slots
from dataclasses import dataclass

@dataclass
class Page:
    page: int
    text: str

page = Page(1, 'des')
page.date = "17-07-2005"
print(page.__dict__) # {'page': 1, 'text': 'des', 'date': '17-07-2005'}
```
```python
# dùng slot
from dataclasses import dataclass

@dataclass(slots=True)
class Page:
    page: int
    text: str

page = Page(1, 'des')
page.date = "17-07-2005"
print(page.__dict__) # lỗi
```
## __dict__
# field() (cho phép cấu hình từng thuộc tính)
**Syn**
```bash
a = field(
    default_factory=list,
    default=18
)

- Input:
    + default: khởi tạo giá trị mặc định
```
**Ex: default_factory**
**không dùng default factory**
```python
from dataclasses import dataclass

@dataclass
class A:
    data: list = []

a = A()
a.data.append(1)

b = A()
b.data.append(2)

print(a, b) # lỗi
```
**sử dụng default factory**
```python
from dataclasses import dataclass, field

@dataclass
class A:
    data: list = field(default_factory=list)

a = A()
a.data.append(1)

b = A()
b.data.append(2)

print(a, b) # A(data=[1]) A(data=[2])
```
repr=False

Không hiện khi in object.

@dataclass
class User:
    name: str
    password: str = field(repr=False)
print(User("Tom", "123"))

Kết quả

User(name='Tom')
compare=False

Không dùng field này để so sánh.

@dataclass
class Page:
    page: int
    minhash: object = field(compare=False)

Khi

Page(1, a) == Page(1, b)

vẫn là

True

vì chỉ so sánh page.

init=False

Không xuất hiện trong constructor.

@dataclass
class Page:
    text: str
    clean_text: str = field(init=False)

Lúc tạo

Page("Hello")

không cần truyền clean_text.

Bạn sẽ tự tính sau.
# asdict() (Chuyển sang dict)
**Ex**
```python
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
__post_init__

Đây là hàm đặc biệt của dataclass.

Sau khi __init__ chạy xong, Python sẽ gọi __post_init__.

Ví dụ

from dataclasses import dataclass, field

@dataclass
class Page:
    raw_text: str
    clean_text: str = field(init=False)

    def __post_init__(self):
        self.clean_text = self.raw_text.lower()
p = Page("HELLO")
print(p.clean_text)

Kết quả

hello

Bạn không cần tự viết __init__.

5. Có thể viết staticmethod và classmethod không?

Có.

@dataclass
class Page:
    page: int
    text: str

    @staticmethod
    def normalize(text):
        return text.lower()

    @classmethod
    def empty(cls):
        return cls(0, "")

Sử dụng

Page.normalize("HELLO")

Page.empty()
6. Ví dụ phù hợp với project OCR của bạn
from dataclasses import dataclass, field
from datasketch import MinHash

@dataclass(slots=True)
class Page:
    page: int
    raw_text: str

    clean_text: str = ""
    ngrams: set[str] = field(default_factory=set)
    minhash: MinHash | None = field(default=None, compare=False)

    def normalize(self):
        self.clean_text = self.raw_text.lower().strip()

    def build_ngrams(self, n: int = 5):
        text = self.clean_text
        self.ngrams = {
            text[i:i+n]
            for i in range(len(text) - n + 1)
        }

Sử dụng:

page = Page(1, "Hello World")

page.normalize()
page.build_ngrams()

print(page.clean_text)
print(len(page.ngrams))