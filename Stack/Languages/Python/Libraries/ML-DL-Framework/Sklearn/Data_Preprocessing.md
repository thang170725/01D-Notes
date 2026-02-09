- [.fit() \& .transfrom() \& .fit\_transform()](#fit--transfrom--fit_transform)
- [StandardScaler()](#standardscaler)
- [LabelEncoder()](#labelencoder)
- [.fit\_transform()](#fit_transform)
- [dữ liệu gốc dạng chuỗi](#dữ-liệu-gốc-dạng-chuỗi)
- [tạo LabelEncoder](#tạo-labelencoder)
- [mã hóa từ chuỗi sang số](#mã-hóa-từ-chuỗi-sang-số)
- [dữ liệu gốc dạng chuỗi](#dữ-liệu-gốc-dạng-chuỗi-1)
- [tạo LabelEncoder](#tạo-labelencoder-1)
- [mã hóa từ chuỗi sang số](#mã-hóa-từ-chuỗi-sang-số-1)
---
# .fit() & .transfrom() & .fit_transform()
```bash
- fit               : học dữ liệu.
- fit_transform     : kết hợp 2 bước fit và transform
```
**Syn** 
```bash
model.fit(X, y)
```
# StandardScaler()
```bash
- Dùng để chuẩn hóa dữ liệu. Trả về một đối tượng Scaler với các phương thức để chuyển đổi tập dữ liệu.
- Tập dữ liệu có nhiều đơn vị khác nhau lên cần chuẩn hóa dữ liệu tránh độ lệch quá lớn.
```
**Ex1**
```bash
- Có thể khó để so sánh thể tích 1,0 với trọng lượng 790, nhưng nếu chúng ta chia tỷ lệ cả hai thành các giá trị tương đương, chúng ta có thể dễ dàng thấy giá trị này được so sánh với giá trị kia như thế nào.
- Có nhiều phương pháp khác nhau để chia tỷ lệ dữ liệu, trong hướng dẫn này, chúng ta sẽ sử dụng một phương pháp gọi là chuẩn hóa.
- Phương pháp chuẩn hóa sử dụng công thức này: z = (x - u) / s
    + z : là giá trị mới
    + x : là giá trị ban đầu
    + u : là giá trị trung bình
    + s : là độ lệch chuẩn.
```
**Ex**
```python
import pandas
from sklearn import linear_model
from sklearn.preprocessing import StandardScaler
scale = StandardScaler()

df = pandas.read_csv("data.csv")
X = df[['Weight', 'Volume']]

scaledX = scale.fit_transform(X)

print(scaledX)

# [[-2.10389253 -1.59336644]
#  [-0.55407235 -1.07190106]
#  [-1.52166278 -1.59336644]
#  [-1.78973979 -1.85409913]
#  [-0.63784641 -0.28970299]
#  [-1.52166278 -1.59336644]
#  [-0.76769621 -0.55043568]
#  [ 0.3046118  -0.28970299]
#  [-0.7551301  -0.28970299]
#  [-0.59595938 -0.0289703 ]
#  [-1.30803892 -1.33263375]
#  [-1.26615189 -0.81116837]
#  [-0.7551301  -1.59336644]
#  [-0.16871166 -0.0289703 ]
#  [ 0.14125238 -0.0289703 ]
#  [ 0.15800719 -0.0289703 ]
#  [ 0.3046118  -0.0289703 ]
#  [-0.05142797  1.53542584]
#  [-0.72580918 -0.0289703 ]
#  [ 0.14962979  1.01396046]
#  [ 1.2219378  -0.0289703 ]
#  [ 0.5685001   1.01396046]
#  [ 0.3046118   1.27469315]
#  [ 0.51404696 -0.0289703 ]
#  [ 0.51404696  1.01396046]
#  [ 0.72348212 -0.28970299]
#  [ 0.8281997   1.01396046]
#  [ 1.81254495  1.01396046]
#  [ 0.96642691 -0.0289703 ]
#  [ 1.72877089  1.01396046]
#  [ 1.30990057  1.27469315]
#  [ 1.90050772  1.01396046]
#  [-0.23991961 -0.0289703 ]
#  [ 0.40932938 -0.0289703 ]
#  [ 0.47215993 -0.0289703 ]
#  [ 0.4302729   2.31762392]]
```
# LabelEncoder()
```bash
Dùng để chuyển đổi các giá trị thành các số nguyên.
```
**Ex1**
```python
from sklearn.preprocessing import LabelEncoder

arr = ['reb', 'blue', 'blue', 'orange', 'red', 'yellow', 'blue'] # dữ liệu gốc dạng chuỗi

le = LabelEncoder()# tạo LabelEncoder

encoded = le.fit_transform(arr) # mã hóa từ chuỗi sang số

print(arr, encoded) # ['reb', 'blue', 'blue', 'orange', 'red', 'yellow', 'blue'] [2 0 0 1 3 4 0]
```
**Ex2**
```python
from sklearn.preprocessing import LabelEncoder
import pandas as pd
# dữ liệu gốc dạng chuỗi
arr = pd.DataFrame(
    {
        'city': ['hanoi', 'hcm', 'da nang', 'da nang', 'hue']
    }
)

le = LabelEncoder() # tạo LabelEncoder

arr['encode city'] = le.fit_transform(arr['city']) # mã hóa từ chuỗi sang số

print(arr)

#       city  encode city
# 0    hanoi            1
# 1      hcm            2
# 2  da nang            0
# 3  da nang            0
# 4      hue            3
```