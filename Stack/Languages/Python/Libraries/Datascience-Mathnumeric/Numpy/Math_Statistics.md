- [max() \& .max() \& min() \& .min()](#max--max--min--min)
- [.sum()](#sum)
- [.mean() \& .median()](#mean--median)
- [+ \& - \& \* \& /](#-------)
- [Dot() \& @ \& matmul()](#dot----matmul)
- [exp()](#exp)
- [trả về phương sai tổng thể](#trả-về-phương-sai-tổng-thể)
- [Tổng số điểm](#tổng-số-điểm)
- [Sinh ngẫu nhiên (x, y) trong \[-1, 1\]](#sinh-ngẫu-nhiên-x-y-trong--1-1)
- [Đếm số điểm nằm trong đường tròn](#đếm-số-điểm-nằm-trong-đường-tròn)
- [Tính tỉ lệ và xấp xỉ pi](#tính-tỉ-lệ-và-xấp-xỉ-pi)
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
Std()
Là độ lệnh chuẩn tổng thể
Ví dụ:
Tính độ lệch chuẩn tổng thể và độ lệch chuẩn mẫu của 5 số 12,34,45,70,86
    1) Tính trung bình cộng: (12 + 34 + 45 + 70 + 86) / 5 = 49.4 
    2) Tính phương sai mẫu: ((12-49.4)**2 + (34-49.4)**2 + (45-49.4)**2 + …) / (5-1) = 854.8 
Tính phương sai tổng thể: ((12-49.4)**2 + (34-49.4)**2 + (45-49.4)**2 + …) / 5 = 683.84  
    1) Tính độ lệch chuẩn của phương sai mẫu: np.sqrt(854.8)= 29.23696291
       Tính độ lệch chuẩn của phương sai tổng thể: np.sqrt(683.84) = 26.15 
Cú pháp:
value = [12,34,45,70,86]    
print(np.std(value)) # trả về độ lệch chuẩn tổng thế
26.150334605889842
Exp()
Power() & Sqrt()
Để tính căn thức bậc 2.
Cú pháp:
a = np.sqrt(arr) hoặc a = np.power(arr, n)
img = np.array(4)
print(np.sqrt(img)) # 2.0
Pi
a = np.pi
print(a)
3.141592653589793
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
# Dot() & @ & matmul()
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
Để tính e mũ n
Cú pháp:
np.exp(2) # e**2
argsort()
Trả về chỉ số các phần tử được sắp xếp theo cách tăng dần.
bincount()
Log2()

Concatenate
Stack
Hstack
Vstack
Split
Array_split
var()
Để tìm phương sai.
Phương sai là một số đo cho biết mức độ phân tán của các giá trị trong tập dữ liệu so với giá trị trung bình của tập dữ liệu đó. Phương sai cho biết các giá trị trong tập dữ liệu “lan rộng” ra sao xung quanh giá trị trung bình.
Phương sai càng lớn thì giá trị trong tập dữ liệu càng phân tán xa so với giá trị trung bình và ngược lại.
import numpy as np
def main():
    value = [12,34,45,70,86]
    print(np.var(value))
main()
683.8399999999999
# trả về phương sai tổng thể
percentile()
Để tìm phần trăm thứ n.
Ý tưởng: 
    1. Sắp xếp mảng tăng dần
    2. index = (q/100) * (n-1)
    3. Nội suy: <value> = <value0> + (<value1> – <value0>) * (index – floor(index))
value0 = 10, value1 = 20
Ví dụ: [60,40,50,30,20,10] – Tìm phần trăm thứ 12
    1. Sắp mảng tăng dần: [10,20,30,40,50,60]
    2. index = (12/100) * (6-1) = 0.6
    3. Nội suy: value = 10 + (20-10) * (0.6 – 0) = 16
Code:
import numpy as np
import math
def main():
    ages = [60,40,50,30,20,10]
    x = np.percentile(ages, 12)
    print(x)
main()
16.0
maximum()
import numpy as np
a = np.maximum(0,2)
print(a)
2
polyfit()
Được dùng để khớp một đa thức với một tập dữ liệu. Hàm này rất hữu ích trong việc tim ra mối quan hệ giữa các biến và dự đoán các giá trị trong tương lai.
Cú pháp: numpy.polyfit(x, y, deg, rcond = None, full = False, w = None, cov = False)
    • x: Mảng các tọa độ x của các điểm dữ liệu.
    • y: Mảng các tọa độ y của các điểm dữ liệu.
    • deg: Bậc của đa thức cần khớp
    • full: Nếu là True, hàm này sẽ trả về thêm thông tin về phép khớp.
    • w: Mảng trọng số áp dụng cho các điểm dữ liệu.
    • cov: Nếu là True, hàm này sẽ trả về ma trận hiệp phương sai của các hệ số.
Tham số đầu ra:
Trả về một mảng các hệ số của đa thức đã khớp. Nếu full = True, hàm này sẽ trả về một tuple chứa các hệ số, phần dư bình phương, hạng của ma trận Vandermonde và các giá trị riêng của ma trận hiệp phương sai.
import numpy as np
def main():
    x = [1, 3, 5, 6, 7, 8, 9, 10, 12, 13, 14, 15, 16, 18, 19, 21, 22, 23]
    y = [100, 90, 80, 60, 60, 55, 60, 65, 70, 70, 75, 76, 78, 79, 90, 99, 99, 100]

    print(np.polyfit(x, y, 2))
main()
[ 0.29363675 -6.34185897 99.32921645]
Tìm hệ số của phương trình bậc 2 khi biết 10 điểm
import numpy as np
def main():
    x = [1,2,3,4,5,6,7,8,9,10]
    y = [0,6,14,24,36,50,66,84,104,126]
    print(np.polyfit(x, y, 2))
main()
[ 1.  3. -4.]
poly1d()
Để biểu diễn 1 đa thức một chiều, lớp này cung cấp các phương thức để thực hiện các phép toán trên đa thức, chẳng hạn như tính giá trị đa thức tại một điểm, tính đạo hàm và tính tích phân của đa thức.
Cú pháp: numpy.poly1d(c_or_r, r = False, variable = None)
    • c_or_r: Mảng các hệ số của đa thức, theo thứ tự giảm dần của bậc, Hoặc, nếu r = True, thì đây mảng các nghiệm của đa thức.
    • r: Nếu là True, c_or_r được hiểu là mảng các nghiệm của đa thức.
    • variable: Chuỗi ký tự tự biểu diễn biến của đa thức. Mặc định là “x”.
import numpy as np
def main():
    x = [1,2,3,4,5,6,7,8,9,10]
    y = [0,6,14,24,36,50,66,84,104,126]
    # đa thức bậc 2
    res = np.poly1d(np.polyfit(x, y, 2))
    # res trả về kế quả là một đa thức bậc 2
    # res = x^2 + 3x - 4
    print(res)
    # 2^2 + 3*2 - 4 = 6
    print(res(2))
main()
   2
1 x + 3 x – 4
5.99999999999999

deriv()
integ()
Log()
L


column_stack()
Bài tập
Đếm số điểm nằm trong một hình tròn và giá trị pi
Giả sử bạn muốn tính xấp xỉ giá trị π bằng phương pháp Monte Carlo:
– Sinh ngẫu nhiên N điểm trong hình vuông [-1, 1] × [-1, 1]
– Đếm bao nhiêu điểm nằm trong đường tròn bán kính 1
– π ≈ 4 * (số điểm trong hình tròn / tổng số điểm)
import numpy as np

# Tổng số điểm
N = 1_000_000  # 1 triệu điểm

# Sinh ngẫu nhiên (x, y) trong [-1, 1]
x = np.random.uniform(-1, 1, N)
y = np.random.uniform(-1, 1, N)

# Đếm số điểm nằm trong đường tròn
inside = (x**2 + y**2) <= 1
count_inside = np.sum(inside)

# Tính tỉ lệ và xấp xỉ pi
pi_estimate = 4 * count_inside / N

print(f"Số điểm trong đường tròn: {count_inside}")
print(f"Xấp xỉ π = {pi_estimate}")
Clip()
Để giới hạn giá trị của các phần tử trong mảng trong một khoảng nhất định.
Cú pháp:
np.clip(array, min_value, max_value)
    • array: Mảng cần xử lý
    • min_value: Giá trị nhỏ nhất cho phép
    • max_value: Giá trị lớn nhất cho phép
a = np.array([-5, 0, 5, 10, 15, 20])
clipped = np.clip(a, 0, 10)
print(clipped) # [0 0 5 10 10 10]