- [Title() \& set\_title()](#title--set_title)
- [Xlabel() \& ylabel() \&  set\_ylabel() \& set\_xlabel()](#xlabel--ylabel---set_ylabel--set_xlabel)
- [Axis()](#axis)
- [subplots() \& subplot()](#subplots--subplot)
- [figure()](#figure)
- [khung hình với kích thước 10x4 inches sẽ được hiển thị lên màn hình](#khung-hình-với-kích-thước-10x4-inches-sẽ-được-hiển-thị-lên-màn-hình)
- [tight\_layout()](#tight_layout)
- [imshow()](#imshow)
- [.colorbar()](#colorbar)
---
# Title() & set_title() 
```bash
Thiết lập tiêu đề của khung hình, khi cửa sổ đó chỉ có một hình ảnh.
```
# Xlabel() & ylabel() &  set_ylabel() & set_xlabel()
```bash
Thiết lập tiêu đề cho trục x, y của đồ thị, khi trong cửa sổ đó chỉ có một đồ thị.
```
**Syn: xlabel**
```bash
plt.xlabel("Intent")
```
**Syn: ylabel**
```bash
plt.ylabel("Số lượng")
```
# Axis()
```bash
Tắt hoặc hiển thị trục X,Y trên hình ảnh (ẩn các số và vạch trục).
```
**Syn**
```bash
plt.axis(‘on | off’)
```
# subplots() & subplot()
```bash
Dùng khi vẽ phức tạp, nhiều axes, muốn quản lý dễ dàng.
```
**Syn: subplots**
```bash
self.fig, self.ax = plt.subplots(2, 2, figsize=(12, 5))

- fig: <class 'matplotlib.figure.Figure'>
- ax: là mảng numy 2d gồm các axes
```
**Syn: subplot**
```bash
plt.subplot(nrows, ncols, index)

- nrows: Số hàng trong lưới.
- ncols: Số cột trong lưới.
- index: Vị trí con trỏ hiện tại
```
**Ex1: subplots**
```python
import matplotlib.pyplot as plt
 
label = ['Model A', 'Model B'] # Dữ liệu về máy
counts = [3, 5]

edu_label = ['BS', 'MS', 'PhD'] # Dữ liệu về học vị
edu_counts = [10, 5, 2]


fig, ax = plt.subplots(1, 2, figsize=(12, 5)) # Tạo figure với 1 hàng, 2 cột

# Biểu đồ cột cho mô hình máy
ax[0].bar(label, counts)
ax[0].set_title("Biểu đồ máy")
ax[0].set_ylabel("Số lượng")
ax[0].set_xlabel("Loại máy")

# Biểu đồ cột cho trình độ học vấn
ax[1].bar(edu_label, edu_counts)
ax[1].set_title("Biểu đồ học vị")
ax[1].set_ylabel("Số lượng")
ax[1].set_xlabel("Loại học vị")

# Hiển thị biểu đồ
plt.show()
```
# figure()
Cài đặt kích thước của một khung hình.
import matplotlib.pyplot as plt
from sklearn.datasets import load_digits
digits = load_digits()
plt.figure(figsize=(10,4))
plt.imshow(digits.images[0], cmap='gray')
plt.show()
# khung hình với kích thước 10x4 inches sẽ được hiển thị lên màn hình
# tight_layout()
Nếu một giao diện có nhiều biểu đồ thì hãy sử dụng phương thức này để các biểu đồ không bị chồng lên nhau.
Cú pháp: 
plt.tight_layout()
Xticks()
Cú pháp:
plt.xticks(rotation=45)
# imshow()
```bash
- Dùng để hiển thị ma trận như một ảnh.
- Ma trận 2D (100×100) → được hiểu là ảnh grayscale
```
# .colorbar()
```bash
- Để hiển thị thanh màu bên cạnh
- Thanh này cho biết:
    + màu đen ↔ giá trị nhỏ (0)
    + màu trắng ↔ giá trị lớn (200)
- Rất hữu ích khi:
    + debug ảnh
    + xem khoảng giá trị pixel
    + xử lý ảnh / heatmap / ma trận
```