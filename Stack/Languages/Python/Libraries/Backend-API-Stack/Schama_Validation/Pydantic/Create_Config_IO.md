- [BaseModel](#basemodel)
- [Datatype](#datatype)
  - [Field()](#field)
  - [Literal](#literal)
- [EmailStr](#emailstr)
---
# BaseModel
```bash
- class nền của Pydantic, bạn kế thừa nó để tạo ra các “model dữ liệu”.
- Cần from pydantic import BaseModel
```
**Ex**
```python
from pydantic import BaseModel
from typing import List, Optional

class Product(BaseModel):
    id: int
    name: str
    price: float
    is_available: bool
    tags: List[str] = []
    discount: Optional[float] = None # có thể có hoặc không

data_ok = {
    "id": 1, # thay bằng 'a' -> báo lỗi
    "name": "iPhone 15",
    "price": 999.99,
    "is_available": True
}
p1 = Product(**data_ok)

print(f"Product 1: {p1.name} - {p1.price}$")
```
# Datatype
## Field() 
```bash
- dùng để
    + thêm validation
    + mô tả (description)
    + khai báo alias
    + cấu hình serialize / deserialize
```
**Syn**
```bash
from pydantic import BaseModel, Field

class User(BaseModel):
    name: str = Field(
    default,
    *,
    default_factory=None,
    alias=None,
    title=None,
    description=None,
    examples=None,
    gt=None, ge=None,
    lt=None, le=None,
    min_length=None,
    max_length=None,
    regex=None,
    multiple_of=None,
    max_digits=None,
    decimal_places=None,
    repr=True,
    exclude=False,
    include=None,
    const=False,
    extra={}
)
```
**Ex: alias**
```python
from pydantic import BaseModel, Field

class User(BaseModel):
    name: str = Field(alias='tên')
    age: int = Field(alias='tuổi')
    address: str = Field(alias='địa chỉ')

users = [{
    'tên': 'thắng',
    'tuổi': 18,
    'địa chỉ': 'hà nội'
}]

results = []
for u in users:
    results.append(User(**u))

print([r.model_dump() for r in results])

# [{'name': 'thắng', 'age': 18, 'address': 'hà nội'}]
```
## Literal
```bash
kiểu dữ liệu lựa chọn
```
**Ex**
```python
class AIAgent(BaseModel):
    intent: Literal['get_profile', "update_profile", "chat"]
```
# EmailStr
**Ex**
```python
from pydantic import BaseModel, Field, EmailStr
from typing import Optional

class User(BaseModel):
    id: int = Field(gt=0)
    username: str = Field(min_length=3, max_length=20)
    email: str = EmailStr
    age: Optional[int] = Field(ge=18)
    is_active: bool = True

user = User(
    id=1,
    username="thang123",
    email="thang@gmail.com",
    age=20
)

print(user)
```
