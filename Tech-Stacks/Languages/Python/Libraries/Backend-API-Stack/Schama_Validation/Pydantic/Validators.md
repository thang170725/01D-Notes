
- [@validator()](#validator)
- [@field\_validator()](#field_validator)
- [@model\_validator()](#model_validator)
---
# @validator()
```bash
- Là hàm kiểm tra / chỉnh sửa dữ liệu trước khi model được tạo.
```
**Ex**
```python
from pydantic import BaseModel, validator

class User(BaseModel):
    username: str

    @validator("username")
    def check_username(cls, v):
        if len(v) < 3:
            raise ValueError("username quá ngắn")
        return v
```
# @field_validator()
Là hàm kiểm tra hoặc biến đổi dữ liệu của MỘT FIELD trước hoặc sau khi Pydantic gán vào model
**Syn**
```bash
@field_validator("username", mode="before")
- mode: quyết định validator chạy trước hay sau khi pydantic xử lý dữ liệu
```
**Ex**
```python
from pydantic import BaseModel, Field, field_validator
from typing import Optional

class User(BaseModel):
    username: str
    email: str = Field(pattern=r'^[\w\.]+@\w+\.\w+$')
    age: Optional[int] = Field(default=None, ge=18)
    is_active: bool = True

    @field_validator("username", mode="before")
    def check_username(cls, v):
        v = str(v).strip().lower()

        if " " in v:
            raise ValueError("username không được chứa khoảng trắng")

        if v == "admin":
            raise ValueError('username không được là "admin"')

        return v

    @field_validator("email")
    def check_email(cls, v):
        domain = v.split("@")[1]
        if domain not in {"gmail.com", "company.com"}:
            raise ValueError("Domain không được phép")
        return v

User( username=" ThangNguyen ", email="thang@gmail.com", age=20 )
```
# @model_validator()
Là validator chạy sau khi TẤT CẢ field đã hợp lệ → dùng để kiểm tra mối quan hệ giữa các field
**syn**
```bash
from pydantic import BaseModel, model_validator

class User(BaseModel):
    age: int

    @model_validator(mode="after")
    def check_model(self):
        return self
```
**Ex**
```python
from pydantic import BaseModel, Field, field_validator, model_validator
from typing import Optional

class User(BaseModel):
    username: str
    email: str = Field(pattern=r'^[\w\.]+@\w+\.\w+$')
    age: Optional[int] = Field(default=None, ge=18)
    is_active: bool = True
    is_young: bool = Field(default=False, exclude=True)

    @field_validator("username", mode="before")
    def check_username(cls, v):
        v = str(v).strip().lower()

        if " " in v:
            raise ValueError("username không được chứa khoảng trắng")

        if v == "admin":
            raise ValueError('username không được là "admin"')

        return v

    @field_validator("email")
    def check_email(cls, v):
        domain = v.split("@")[1]
        if domain not in {"gmail.com", "company.com"}:
            raise ValueError("Domain không được phép")
        return v

    @model_validator(mode="after")
    def check_model(self):
        # logic 1
        self.is_young = self.age is not None and self.age < 25

        # logic 2
        if self.is_active is False and self.age is None:
            raise ValueError("age must exist when user is inactive")

        # logic 3
        if self.username.startswith("test"):
            domain = self.email.split("@")[1]
            if domain != "company.com":
                raise ValueError("test users must use company.com email")

        return self
```