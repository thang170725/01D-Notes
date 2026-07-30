- [Directory Structure](#directory-structure)
- [Introduction](#introduction)
---
# Directory Structure
```bash
Tempfile/       # mình dùng thư mục này để xem kiến thức về tempfile
├── Base.md     # mình dùng thư mục này để xem kiến thức và tiện ích
└── Process.md  # mình dùng thư mục này thể thao tác trong tempfile
```
# Introduction
```bash
- tempfile là một module có sẵn trong Python Standard Library, dùng để tạo và quản lý các file/thư mục tạm thời.
- Bạn không cần cài đặt gì cả, chỉ cần: import tempfile
- Tại sao cần file tạm?
    + Ví dụ:
        - Tải file từ internet rồi xử lý
        - Chuyển đổi SVG → PDF
        - Giải nén file
        - Xử lý ảnh trước khi lưu chính thức
    + Thay vì tạo:
        - file = open("temp.pdf", "w") rồi phải tự xóa, thì dùng tempfile: with tempfile.NamedTemporaryFile() as f: # dùng file
        - Khi kết thúc, file được xóa tự động.
```