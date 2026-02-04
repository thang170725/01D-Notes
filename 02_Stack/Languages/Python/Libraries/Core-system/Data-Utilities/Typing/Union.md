```bash
- Trong Python typing, Union dùng để khai báo rằng một biến / tham số / giá trị trả về có thể thuộc nhiều kiểu khác nhau.
- Dùng khi:
    + Hàm nhận nhiều kiểu đầu vào
    + Giá trị trả về không cố định 1 kiểu
    + Viết API / thư viện rõ ràng hơn
- Không cần dùng khi:
    + Kiểu dữ liệu luôn cố định
    + Code nhỏ, dùng nhanh, không cần type check
- Lưu ý: Union không ép kiểu, nó chỉ để:
    + IDE gợi ý
    + Tool kiểm tra type (mypy, pyright…)
    + Code rõ ràng hơn
    + Union rất hay dùng khi bạn cần xử lý khác nhau theo kiểu dữ liệu.
```
**Syn**
```bash
Union[Kiểu1, Kiểu2, Kiểu3, ...]
- Nghĩa là: giá trị có thể là Kiểu1 hoặc Kiểu2 hoặc Kiểu3…
```
**Ex**
```python
from typing import Union

def double(x: Union[int, float]) -> Union[int, float]:
    return x * 2

print(double(5))
print(double(2.5))

# 10
# 5.0
# Hàm trả về int hoặc float
```
**Ex**
```python
def show(value: Union[int, str, bool]):
    print(value)
show(10)
show("hello")
show(True)

# 10
# hello
# True
```
from typing import Union

def process(x: Union[int, str]):
    if isinstance(x, int):
        return x + 1
    else:
        return x.upper()

Chạy thử
print(process(5))
print(process("python"))

Kết quả
6
PYTHON

1. Cú pháp mới (Python 3.10+)

Từ Python 3.10, bạn có thể viết ngắn gọn hơn:

def double(x: int | float) -> int | float:
    return x * 2


👉 Hai cách này hoàn toàn tương đương:

Union[int, float]
int | float

