- [thuật toán chuyển từ hệ 10 sang hệ 2](#thuật-toán-chuyển-từ-hệ-10-sang-hệ-2)
---
# thuật toán chuyển từ hệ 10 sang hệ 2
**Ex1**
```python
num = 0
res = ""

if num == 0:
    res = "0"
else:
    while num != 0:
        res = str(num % 2) + res
        num //= 2

print(res)
```
**Ex2**
```python
num = 13
res = ""

while num:
    res = str(num & 1) + res
    num >>= 1

print(res)
```