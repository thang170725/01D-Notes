- [Convert Datatype (chuyển đổi dữ liệu)](#convert-datatype-chuyển-đổi-dữ-liệu)
  - [model\_dump() (Chuyển object Pydantic → dict Python)](#model_dump-chuyển-object-pydantic--dict-python)
---
# Convert Datatype (chuyển đổi dữ liệu)
## model_dump() (Chuyển object Pydantic → dict Python)
```bash
Dùng khi bạn muốn:
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
- exclude_unset : True / Fasle
    + Client chỉ gửi fullname
        {
          "fullname": "Thang"
        }
    + Nếu dùng: payload.model_dump()
        Kết quả: Nó tự thêm cả field default.
            {
              "fullname": "Thang",
              "age": 18,
              "address": None
            }
    + Nếu dùng: payload.model_dump(exclude_unset=True)
        Kết quả: Chỉ lấy field thực sự được gửi lên.
            {
              "fullname": "Thang"
            }
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