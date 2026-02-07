- [.view() \& .copy()](#view--copy)
- [.Shape \& .shape() \& .size()](#shape--shape--size)
- [.reshape()](#reshape)
- [.flatten()](#flatten)
- [.ndim](#ndim)
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