- [directory structure](#directory-structure)
- [Introduction](#introduction)
- [Installation](#installation)
---
# directory structure
```bash
Pydantic/
├── 01_models_fields.md       # Định nghĩa Model & kiểu dữ liệu: BaseModel, Field, Alias, Type Hinting
├── 02_validators.md         # Kiểm tra dữ liệu: @field_validator, @model_validator
├── 03_serialization.md      # Xuất, chuyển đổi dữ liệu: model_dump, model_dump_json, ConfigDict
├── 04_data_types.md         # Các kiểu dữ liệu đặc biệt: EmailStr, HttpUrl, SecretStr
└── 05_settings_management.md # Quản lý cấu hình: BaseSettings, .env loading
```
# Introduction
```bash
- Trong Python thông thường, bạn có thể truyền bất cứ thứ gì vào một đối tượng. Với Pydantic, bạn tạo ra một "khung bảo vệ". Dữ liệu đi vào phải đi qua cái khung này:
  + Nếu đúng kiểu: Nó được chấp nhận.
  + Nếu sai kiểu nhưng có thể sửa: Nó sẽ tự động được ép kiểu (ví dụ chuỗi "10" thành số 10).
  + Nếu sai hoàn toàn: Nó sẽ chặn lại và báo lỗi chi tiết.
- Pydantic là 'vị vua' trong thế giới API, nhưng ít khi được sử dụng trong lõi tính toán trong AI/Data Science
```
# Installation
```bash
pip install pydantic
```