- [directory structure](#directory-structure)
- [Introduction](#introduction)
- [Installation](#installation)
---
# directory structure
```bash
Pydantic/                   # mình dùng thư mục này để xem kiến thức về pydantic
├── Create_Config_IO.md     # mình dùng file để cấu hình, khởi tạo và định nghĩa kiểu dữ liệu và IO
├── Validators.md           # mình dùng file để kiểm tra dữ liệu, tạo ràng buộc: @field_validator, @model_validator
├── Process.md              # mình dùng file để thao tác với dữ liệu
└── Base.md                 # mình dùng file để xem kiến thức và tiện ích
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