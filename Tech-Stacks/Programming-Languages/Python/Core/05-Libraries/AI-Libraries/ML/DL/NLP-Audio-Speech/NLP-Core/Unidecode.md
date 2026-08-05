- [Unidecode Introduction (chuyển đổi unicode -\> ascii)](#unidecode-introduction-chuyển-đổi-unicode---ascii)
- [unidecode() (Xóa dấu tiếng việt)](#unidecode-xóa-dấu-tiếng-việt)
---
# Unidecode Introduction (chuyển đổi unicode -> ascii)
```bash
Nên dùng khi:
    - Xóa dấu tiếng việt
    - chuẩn hóa tên người
    - tìm kiếm không phân biệt dấu
    - tạo url (slug)
    - chuẩn hóa dữ liệu trước khi huấn luyện AI hoặc xử lý NLP
    - xuất dữ liệu chỉ hỗ trợ ascii
```
# unidecode() (Xóa dấu tiếng việt)
**Ex**
```python
from unidecode import unidecode

print(unidecode("tôi tên là lê đức thắng")) # toi ten la le duc thang
```