- [model\_dump()](#model_dump)
- [ConfigDict](#configdict)
  - [Sự khác biệt giữa dùng và không dùng ConfigDict](#sự-khác-biệt-giữa-dùng-và-không-dùng-configdict)
---
# model_dump()
```bash
- Chuyển object Pydantic → dict Python
- Dùng khi bạn muốn:
    + Trả JSON cho API
    + Ghi DB
    + Log dữ liệu
    + Gửi dữ liệu sang service khác
```
**Syn**
```bash
data = user.model_dump(
    exclude_none=True,
    include={"id", "name"},
    exclude={"age"},
    mode="json"
)

- exclude_none  : Loại bỏ phần tử có giá trị là None
- include       : chỉ lấy một vài field
- exclude       : bỏ một vài field
- mode          : trả về một định dạng
```
**Ex**
```python
from pydantic import BaseModel

class User(BaseModel):
    id: int
    name: str
    age: int | None = None

user = User(id=1, name="Thắng", age=25)

data = user.model_dump()
print(data)


# {
#     'id': 1,
#     'name': 'Thắng',
#     'age': 25
# }
```
# ConfigDict
```bash
- dùng để cấu hình cho BaseModel trong Pydantic v2. Nó thay thế hoàn toàn class Config ở Pydantic v1.
- ConfigDict = “cài đặt hành vi cho model”
```
**Syn**
```bash
from pydantic import BaseModel, ConfigDict

model_config = ConfigDict(
    extra='forbid',
    validate_assignment=True,
    from_attributes=
)

- Bắt buộc: tên biến phải là model_config
- extra            
    + ignore    : bỏ qua filed dư (mặc định)
    + allow     : cho phép field dư
    + forbid    : ném looiz nếu có field dư
- from_attributes   : 
    + True là đọc dữ liệu từ Object.attribute
    + False chỉ nhận dict
```
## Sự khác biệt giữa dùng và không dùng ConfigDict
**Không dùng**
```python
class User(BaseModel):
    id: int
    name: str

u = User(id=1, name="An", age=20)
print(u)

# Không lỗi, age bị bỏ qua (mặc định)
```
**Dùng**
```python
class User(BaseModel):
    model_config = ConfigDict(extra='forbid')

    id: int
    name: str

User(id=1, name="An", age=20)
```