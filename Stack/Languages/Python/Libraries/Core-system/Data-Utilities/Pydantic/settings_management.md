Xuất dữ liệu với alias (by_alias=True)

Mặc định khi .dict() hoặc .json() → dùng tên field trong code.

u.dict()
# {'user_id': 1}


Muốn dùng alias:

u.dict(by_alias=True)
# {'userId': 1}


👉 Rất hay dùng khi:

API backend dùng snake_case

Frontend dùng camelCase

5️⃣ Cho phép dùng cả alias và tên field gốc
class User(BaseModel):
    user_id: int = Field(alias="userId")

    class Config:
        allow_population_by_field_name = True


Giờ cả 2 đều hợp lệ:

User(userId=1)
User(user_id=1)

6️⃣ Validation + alias cùng lúc
class Product(BaseModel):
    price: float = Field(
        alias="unitPrice",
        gt=0,
        description="Giá sản phẩm"
    )

7️⃣ alias_generator (tự động đổi snake_case → camelCase)

Siêu tiện khi model lớn 👇

def to_camel(s: str) -> str:
    parts = s.split("_")
    return parts[0] + "".join(word.capitalize() for word in parts[1:])

class User(BaseModel):
    user_id: int
    full_name: str

    class Config:
        alias_generator = to_camel
        allow_population_by_field_name = True


Input:

{
  "userId": 1,
  "fullName": "Thắng"
}

8️⃣ Pydantic v2 (nếu bạn dùng)

Pydantic v2 vẫn dùng Field, nhưng config đổi sang model_config:

from pydantic import BaseModel, Field
from pydantic import ConfigDict

class User(BaseModel):
    user_id: int = Field(alias="userId")

    model_config = ConfigDict(
        populate_by_name=True
    )

9️⃣ Tóm tắt nhanh
Mục đích	Cú pháp
Alias	Field(alias="userId")
Xuất alias	.dict(by_alias=True)
Nhận cả 2 tên	allow_population_by_field_name=True
Bắt buộc field	Field(...)
Auto camelCase	alias_generator

Nếu bạn muốn:

ví dụ FastAPI

so sánh Pydantic v1 vs v2

hoặc convert snake_case ↔ camelCase chuẩn frontend

👉 nói mình biết nhé 😄