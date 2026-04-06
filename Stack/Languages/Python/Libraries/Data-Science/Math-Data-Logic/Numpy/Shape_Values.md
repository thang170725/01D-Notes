- [.view() \& .copy()](#view--copy)
- [.Shape \& .shape() \& .size()](#shape--shape--size)
- [.reshape()](#reshape)
- [.flatten()](#flatten)
- [.ndim](#ndim)
- [.ndmin](#ndmin)
- [\[\] (Scling)](#-scling)
- [Clip()](#clip)
- [.argmin() \& .argmax()](#argmin--argmax)
---
# .view() & .copy()
```bash
- view  : Tạo một chế độ xem focus vào mảng gốc.
- copy  : Để sao chép một mảng.
```
**Ex1: view**
```python
arr = np.array([1, 2, 3, 4, 5])
x = arr.view()

arr[0] = 42

print(arr) # [42 2 3 4 5]
print(x) # [42 2 3 4 5]
```
**Ex2: copy**
```python
arr = np.array([1, 2, 3, 4, 5])
x = arr.copy()
arr[0] = 42
print(arr) # [42 2 3 4 5]
print(x) # [1 2 3 4 5]
```
# .Shape & .shape() & .size()
```bash
Trả về kích thước mảng.
```
**Ex1**
```python
arr = np.array([5,10,15,20,25])
print(np.size(arr)) # 5
```
**Ex2**
```python
import numpy as np

coordinates = np.array([
    [1,2],
    [3,4]
])
print(np.size(coordinates))
```
# .reshape()
Kiểm tra kích thước và thay đổi kích thước.
# .flatten()
```bash
Để “làm phẳng” (chuyển từ mảng nhiều chiều → mảng 1 chiều).
```
**Syn**
```bash
array.flatten(order='C')

- order
    + 'C': duyệt theo hàng (row-major order — mặc định).
    + 'F': duyệt theo cột (column-major order — kiểu Fortran).
```
**Ex**
```python
arr = np.array([[1, 2, 3],
                [4, 5, 6]])

flat2 = arr.flatten(order='C')
flat3 = arr.flatten(order='F')
print(flat1, flat2, flat3, flat4) # [1 2 3 4 5 6] [1 4 2 5 3 6]
```
# .ndim
```bash
Trả về số chiều của numpy.
```
**Ex**
```python
arr = np.array((1,2,3))
print(arr.ndim) # 1
```
# .ndmin
```bash
Ép mảng về số chiều mong muốn.
```
**Ex**
```python
import numpy as np

arr = np.array([1, 2, 3, 4], ndmin=2)

print(arr) # [[1 2 3 4]]
print('number of dimensions :', arr.ndim) # number of dimensions : 2
```
# [] (Scling)
```bash
Có thể dùng để cắt mảng
```
**Syn**
```bash
arr[rows, cols]

- Input:
    + dấu ',': để tách chiều
    + dấu ':': để cắt theo range
```
# Clip()
```bash
Để giới hạn giá trị của các phần tử trong mảng trong một khoảng nhất định.
```
**Syn**
```bash
np.clip(array, min_value, max_value)

- array: Mảng cần xử lý
- min_value: Giá trị nhỏ nhất cho phép
- max_value: Giá trị lớn nhất cho phép
```
**Ex**
```python
a = np.array([-5, 0, 5, 10, 15, 20])
clipped = np.clip(a, 0, 10)
print(clipped) # [0 0 5 10 10 10]
```
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