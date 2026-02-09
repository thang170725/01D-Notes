- [.argmin() \& .argmax()](#argmin--argmax)
---
# .argmin() & .argmax()
```bash
- argmin    : Vị trí phần tử nhỏ nhất.
- argmax    : Vị trí phần tử lớn nhất.
```
**Syn: argmin**
```bash
numpy.argmin(a, axis=None)
```
**Syn: argmax**
```bash
numpy.argmax(a, axis=None)
```
**Ex1: agrmin**
```python
import numpy as np

a = np.array([10, 5, 7, 4, 8])
print(np.argmin(a)) # 3

# Giá trị nhỏ nhất là 3, nằm ở index 3
```
**Ex2: argmin**
```python
a = np.array([[4, 2, 9],
              [1, 6, 3]])

print(np.argmin(a, axis=0)) # Theo cột
print(np.argmin(a, axis=1)) # Theo hàng

# Kết quả
# [1 0 1]
# [1 2]
```