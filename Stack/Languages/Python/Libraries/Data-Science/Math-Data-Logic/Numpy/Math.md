- [max() \& .max() \& min() \& .min()](#max--max--min--min)
- [.sum()](#sum)
- [std() \& var()](#std--var)
- [Exp()](#exp)
- [np.power() \& \*\*](#nppower--)
- [Sqrt()](#sqrt)
  - [Pi](#pi)
- [.mean() \& .median()](#mean--median)
- [+ \& - \& \* \& /](#-------)
- [dot() \& @ \& matmul()](#dot----matmul)
- [exp()](#exp-1)
- [argsort()](#argsort)
- [bincount()](#bincount)
- [Log2()](#log2)
- [Concatenate](#concatenate)
- [Stack](#stack)
- [Hstack](#hstack)
- [Vstack](#vstack)
- [Split](#split)
- [Array\_split](#array_split)
- [percentile()](#percentile)
- [maximum()](#maximum)
- [polyfit()](#polyfit)
- [linalg](#linalg)
  - [eig()](#eig)
- [norm()](#norm)
- [Tính khoảng cách 2 điểm trong không gian 2d](#tính-khoảng-cách-2-điểm-trong-không-gian-2d)
---
# max() & .max() & min() & .min()
```bash
Dùng để tìm số lớn nhất và số bé nhất trong mảng numpy.
```
**Ex**
```python
import numpy as np

a = np.array([1,2,3,4])
print(a.max()) # 4
print(np.max(a)) # 4
# cách sử dụng tương tự cho min và .min()
```
# .sum()
```bash
Để tính tổng. Trả về một số thực hoặc nguyên
```
**Syn**
```bash
numpy.sum(a, axis=None, dtype=None, out=None, keepdims=False, initial=0, where=True)

- a         : Mảng đầu vào (array-like)
- axis:	    : Trục cần tính tổng (None, 0, 1, tuple…)
- dtype:	: Kiểu dữ liệu của kết quả
- out	    : Mảng để lưu kết quả
- keepdims	: Giữ nguyên số chiều sau khi sum
- initial	: Giá trị khởi tạo cho phép cộng
-where	    : Điều kiện để chọn phần tử khi tính tổng
```
**Ex1: Sum toàn bộ mảng**
```python
import numpy as np

a = np.array([1, 2, 3, 4])
print(np.sum(a)) # 10
```
**Ex2: Sum theo trục (axis)**
```python
a = np.array([[1, 2, 3],
              [4, 5, 6]])

print(np.sum(a, axis=0)) # Sum theo cột
print(np.sum(a, axis=1)) # Sum theo hàng

# Kết quả
# [5 7 9]
# [ 6 15]
```
**Ex3: Giữ nguyên số chiều (keepdims=True)**
```python
print(np.sum(a, axis=1, keepdims=True))

# Kết quả
# [[ 6]
#  [15]]
# Hữu ích khi muốn broadcast với mảng ban đầu.
```
**Ex4: Chỉ định kiểu dữ liệu (dtype)**
```python
a = np.array([1, 2, 3], dtype=np.int8)
print(np.sum(a, dtype=np.int64))

# Tránh tràn số khi làm việc với số nguyên nhỏ.
```
**Ex4: Sử dụng where (tính tổng có điều kiện)**
```python
a = np.array([1, 2, 3, 4, 5])

print(np.sum(a, where=(a % 2 == 0))) # Chỉ sum các số chẵn

# Kết quả
# 6
```
**Ex5: Tham số initial**
```python
print(np.sum(a, initial=10))

# Kết quả
# 25
# Tổng = 10 + (1+2+3+4+5)
```
**Ex6: Dùng out để lưu kết quả**
```python
result = np.zeros(1)
np.sum(a, out=result)
print(result)
```
# std() & var()
```bash
- std   : tính độ lệnh chuẩn tổng thể
- var   : tìm phương sai. 
```
**Ex1: độ lệch chuẩn tổng thế**
```python
value = [12,34,45,70,86]  
  
print(np.std(value)) # 26.150334605889842
```
**Ex2: phương sai tổng thể**
```bash
import numpy as np

value = [12,34,45,70,86]
print(np.var(value)) # 683.8399999999999
```
# Exp()
# np.power() & **
```python
a = np.array([1,2,3])
    
print(a**2, np.power(a, 2)) # [1 4 9] [1 4 9]
```
# Sqrt()
```bash
- sqrt  : Để tính căn thức bậc 2.
```
**Ex**
```python
img = np.array(4)

print(np.sqrt(img)) # 2.0
```
## Pi
**Ex**
```bash
a = np.pi

print(a) # 3.141592653589793
```
# .mean() & .median()
```bash
- mean      : Để tìm ra giá trị trung bình của một dãy số. 
- median   : Là giá trị trung vị (giá trị ở giữa)
```
**Ex: mean**
```python
Speed = [90, 105, 55, 60, 75]
print(np.mean(speed)) # 77.0
```
**Ex: median**
```python
speed = [90, 105, 55, 60, 75]
print(np.median(speed)) # 75.0
```
# + & - & * & /
```bash
- '+' : cộng từng phần tử.
- '-' : trừ từng phần tử.
- '*' : nhân từng phần tử.
- '/' : chia từng phần từ.
```
**Ex1: '+'**
```python
import numpy as np

arr1 = np.array([[2,1,3], [5,6,7]])
arr2 = np.array([[1,2,3], [0,4,5]])

print(arr1+arr2)

# [[ 3  3  6]
#  [ 5 10 12]]
```
**Ex2: '*'**
```python
arr = np.array([[5, 10], [1,2]], dtype=float)
arr1 = np.array([[2, 3], [1,2]], dtype=float)
print(arr*arr1)

# [[10. 30.]
#  [ 1.  4.]]
```
# dot() & @ & matmul()
```bash
- Để nhân ma trận. 1 chiều hoặc n chiều.
- mảng >2D (tensor) thì dot không hỗ trợ tốt, còn @, matmul hỗ trợ broadcasting – Tốt.
```
**Ex**
```python
a = np.array([
    [1,2,3],
    [1,1,1],
    [2,3,4]
])
b = np.array([
    [2,2,2],
    [1,2,3],
    [4,3,1]
])

res = np.dot(a,b)

print(res)

# [[16 15 11]
#  [ 7  7  6]
#  [23 22 17]]
```
# exp()
```bash
Để tính e mũ n
```
**Syn**
```bash
np.exp(2) # e**2
```
# argsort()
```bash
Trả về chỉ số các phần tử được sắp xếp theo cách tăng dần.
```
# bincount()
# Log2()
# Concatenate
# Stack
# Vstack
# Split
# Array_split
# percentile()
```bash
- Để tìm phần trăm thứ n.
- Ý tưởng: 
    1. Sắp xếp mảng tăng dần
    2. index = (q/100) * (n-1)
    3. Nội suy: <value> = <value0> + (<value1> – <value0>) * (index – floor(index))
```
**Ex1: [60,40,50,30,20,10] – Tìm phần trăm thứ 12**
```bash
1. Sắp mảng tăng dần: [10,20,30,40,50,60]
2. index = (12/100) * (6-1) = 0.6
3. Nội suy: value = 10 + (20-10) * (0.6 – 0) = 16
```
**Ex2**
```python
import numpy as np
import math

ages = [60,40,50,30,20,10]
x = np.percentile(ages, 12)

print(x) # 16.0
```
# maximum()
**Ex**
```bash
import numpy as np

a = np.maximum(0,2)

print(a) # 2
```
# polyfit()
```bash
Được dùng để khớp một đa thức với một tập dữ liệu. Hàm này rất hữu ích trong việc tim ra mối quan hệ giữa các biến và dự đoán các giá trị trong tương lai.
```
**Syn** 
```bash
numpy.polyfit(x, y, deg, rcond = None, full = False, w = None, cov = False)

- x: Mảng các tọa độ x của các điểm dữ liệu.
- y: Mảng các tọa độ y của các điểm dữ liệu.
- deg: Bậc của đa thức cần khớp
- full: Nếu là True, hàm này sẽ trả về thêm thông tin về phép khớp.
- w: Mảng trọng số áp dụng cho các điểm dữ liệu.
- cov: Nếu là True, hàm này sẽ trả về ma trận hiệp phương sai của các hệ số.
```
- [linalg](#linalg)
  - [eig()](#eig)
- [norm()](#norm)
- [Tính khoảng cách 2 điểm trong không gian 2d](#tính-khoảng-cách-2-điểm-trong-không-gian-2d)
---
# linalg
## eig()
# norm()
```bash
- Thường được dùng để tính khoảng cách hai điểm trong không gian.
```
**Ex**
```python
import numpy as np

# Tạo một mảng chứa tọa độ của 3 điểm: (3,4), (1,1), và (0,5)
points = np.array([
    [3, 4],
    [1, 1],
    [0, 5]
])

# Tính L2 norm (khoảng cách Euclidean) theo từng hàng (axis=1)
distances = np.linalg.norm(points, axis=1)

print("Các điểm:")
print(points)
print("\nKhoảng cách từ gốc tọa độ đến mỗi điểm:")
print(distances)
Các điểm:
[[3 4]
 [1 1]
 [0 5]]

Khoảng cách từ gốc tọa độ đến mỗi điểm:
[5.         1.41421356 5.        ]
```
# Tính khoảng cách 2 điểm trong không gian 2d
```python
import numpy as np

coordinates = np.array([
    [1,2],
    [3,4]
])

distance = np.linalg.norm(coordinates[0]-coordinates[1])
print(distance) # 2.8284271247461903
```