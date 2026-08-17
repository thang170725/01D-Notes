- [.text()](#text)
- [.select()](#select)
  - [.ask()](#ask)
- [.path (dùng để yêu cầu người dùng nhập hoặc chọn một đường dẫn (file hoặc thư mục) trong terminal)](#path-dùng-để-yêu-cầu-người-dùng-nhập-hoặc-chọn-một-đường-dẫn-file-hoặc-thư-mục-trong-terminal)
---
# .text()
# .select()
**Ex: sử dụng select**
```python
import questionary

choice = questionary.select(
    "Chọn ngôn ngữ",
    choices=["Python", "Java", "Go"]
).ask()

print(choice)
# ? Chọn ngôn ngữ

# ❯ Python
#   Java
#   Go

# (.venv) thang@PhatToNhuLai:~/workspace/Download-YT$ python tool.py
# ? Chọn ngôn ngữ Java
# Java
```
## .ask()
```python
import questionary

name = questionary.text(
    "Tên của bạn là gì?"
).ask()

print(name)
# (.venv) thang@PhatToNhuLai:~/workspace/Download-YT$ python tool.py
# ? Tên của bạn là gì? thắng
# thắng
```
# .path (dùng để yêu cầu người dùng nhập hoặc chọn một đường dẫn (file hoặc thư mục) trong terminal)
**Syn**
```bash

- Output: str
```
**Ex**
```python
import questionary

file_path = questionary.path(
    "Chọn file dữ liệu:"
).ask()

print(file_path)
# ? Chọn file dữ liệu: ./data/sales.csv
# ./data/sales.csv
```