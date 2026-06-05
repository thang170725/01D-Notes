- [.text()](#text)
- [.select()](#select)
  - [.ask()](#ask)
---
# .text()
# .select()
**Ex**
```python
choice = questionary.select(
    "Chọn ngôn ngữ",
    choices=["Python", "Java", "Go"]
).ask()
# ? Chọn ngôn ngữ

# ❯ Python
#   Java
#   Go
```
## .ask()
```python
import questionary

name = questionary.text(
    "Tên của bạn là gì?"
).ask()

print(name)
? Tên của bạn là gì?
> Thắng
```
