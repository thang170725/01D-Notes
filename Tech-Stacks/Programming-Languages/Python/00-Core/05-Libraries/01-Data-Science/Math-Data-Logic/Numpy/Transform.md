- [.tolist()](#tolist)
- [.Shape \& .shape() \& .size()](#shape--shape--size)
- [.reshape()](#reshape)
- [.flatten()](#flatten)
- [.ndim](#ndim)
- [.ndmin](#ndmin)
- [\[\] (Scling)](#-scling)
- [Clip()](#clip)
- [.argmin() \& .argmax()](#argmin--argmax)
- [Hstack](#hstack)
- [.pad() (Thêm phần đệm)](#pad-thêm-phần-đệm)
---
# .tolist()
```bash
Để chuyển từ mảng numpy sang mảng thường.
```
**Syn**
```bash
arr.tolist()
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
# Hstack
```bash
- Dùng để nối mảng theo chiều ngang. 
    + 1D array -> nối thành 1 mảng dài hơn
    + 2D array -> nối theo cột
- Các mảng phải:
    + Có cùng số hàng (rows) nếu là 2D
    + Hoặc cùng shape phù hợp
```
**Syn**
```bash
np.hstack(tup)

- Input:
    + tup: list/tuple các mảng numpy
```
**Ex1**
```python
import numpy as np

a = np.array([1, 2])
b = np.array([3, 4])

np.hstack((a, b)) # [1 2 3 4]
```
**Ex2: Ví dụ 2: 2D**
```python
a = np.array([[1, 2],
              [3, 4]])

b = np.array([[5, 6],
              [7, 8]])

np.hstack((a, b))
# [[1 2 5 6]
#  [3 4 7 8]]
```
# .pad() (Thêm phần đệm)
```bash
- Trong NumPy, hàm numpy.pad() dùng để thêm phần đệm (padding) vào mảng.
    + ví dụ thêm số 0 quanh ma trận, thêm giá trị ở đầu/cuối vector, hoặc mở rộng ảnh.
```
**Syn**
```bash
numpy.pad(array, pad_width, mode='constant', **kwargs)

- Input:
    + array     : mảng cần pad
    + pad_width : số lượng phần tử thêm
    + mode	    : cách thêm
```
**Ex1: Ví dụ cơ bản**
```python
import numpy as np

a = np.array([1, 2, 3])
b = np.pad(a, pad_width=2) # thêm 2 số ở đầu, thêm 2 số ở cuối, mặc định thêm số 0

print(b) # [0 0 1 2 3 0 0]
```
**Ex2: Padding khác nhau cho từng chiều**
```python
b = np.pad(a,
           ((1, 2),
            (3, 4)))
print(b)
# trên: 1 hàng
# dưới: 2 hàng
# trái: 3 cột
# phải: 4 cột
```