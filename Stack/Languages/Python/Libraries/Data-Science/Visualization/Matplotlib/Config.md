- [Title() \& set\_title()](#title--set_title)
- [.xlabel() \& .ylabel() \&  .set\_ylabel() \& .set\_xlabel()](#xlabel--ylabel---set_ylabel--set_xlabel)
- [xlim \& ylim](#xlim--ylim)
- [Axis()](#axis)
- [subplots() \& subplot()](#subplots--subplot)
- [figure()](#figure)
- [tight\_layout()](#tight_layout)
- [.colorbar()](#colorbar)
---
# Title() & set_title() 
```bash
Thiết lập tiêu đề của khung hình, khi cửa sổ đó chỉ có một hình ảnh.
```
# .xlabel() & .ylabel() &  .set_ylabel() & .set_xlabel()
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
# xlim & ylim
```bash
- Dùng để thiết lập phạm vi (giới hạn) trục x và trục y của biểu đồ.
```
**Syn: xlim**
```bash
plt.xlim(xmin, xmax)
```
**Syn: ylim**
```bash
plt.ylim(ymin, ymax)
```
**Ex**
```python
import matplotlib.pyplot as plt

x = [1, 2, 3, 4, 5]
y = [10, 20, 30, 40, 50]

plt.plot(x, y)

plt.xlim(0, 6)   # giới hạn trục x từ 0 → 6
plt.ylim(0, 60)  # giới hạn trục y từ 0 → 60

plt.show()
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
```bash
Cài đặt kích thước của một khung hình.
```
**Ex**
```python
import matplotlib.pyplot as plt
from sklearn.datasets import load_digits

digits = load_digits()

plt.figure(figsize=(10,4)) # cài đặt khung hình với kích thước 10x4 inches

plt.imshow(digits.images[0], cmap='gray')
plt.show()
```
# tight_layout()
```bash
Nếu một giao diện có nhiều biểu đồ thì hãy sử dụng phương thức này để các biểu đồ không bị chồng lên nhau.
```
**Syn**
```bash
plt.tight_layout()
```
Xticks()
Cú pháp:
plt.xticks(rotation=45)
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