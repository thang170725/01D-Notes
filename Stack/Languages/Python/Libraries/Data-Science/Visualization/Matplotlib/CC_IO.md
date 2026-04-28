- [Title() \& set\_title()](#title--set_title)
- [X \& Y Axis (Nhóm cấu hình trên trục X,Y)](#x--y-axis-nhóm-cấu-hình-trên-trục-xy)
  - [.xlabel() \& .ylabel() \&  .set\_ylabel() \& .set\_xlabel()](#xlabel--ylabel---set_ylabel--set_xlabel)
  - [set\_xticks() \& set\_yticks()](#set_xticks--set_yticks)
- [xlim \& ylim](#xlim--ylim)
- [Config (Nhóm cấu hình)](#config-nhóm-cấu-hình)
- [Axis()](#axis)
  - [subplots() \& subplot()](#subplots--subplot)
    - [flatten()](#flatten)
- [figure()](#figure)
  - [tight\_layout()](#tight_layout)
- [.colorbar()](#colorbar)
- [Save (Nhóm lưu)](#save-nhóm-lưu)
  - [plt.savefig()](#pltsavefig)
---
# Title() & set_title() 
```bash
Thiết lập tiêu đề của khung hình, khi cửa sổ đó chỉ có một hình ảnh.
```
# X & Y Axis (Nhóm cấu hình trên trục X,Y)
## .xlabel() & .ylabel() &  .set_ylabel() & .set_xlabel()
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
## set_xticks() & set_yticks()
```bash
Dùng để đặt vị trí các vạch chia (ticks) trên trục X và Y.
```
**Syn**
```bash
ax.set_xticks(vị_trí_ticks)
ax.set_yticks(vị_trí_ticks)
# truyền vào list/array các vị trí muốn hiện.
```
**Ex1**
```bash
import matplotlib.pyplot as plt

x=[1,2,3,4,5]
y=[10,20,15,30,25]

fig, ax = plt.subplots()

ax.plot(x,y)

ax.set_xticks([1,3,5])
ax.set_yticks([10,20,30])

plt.show()

# Chỉ hiện:
# X: 1,3,5
# Y: 10,20,30
```
**Ex2: Time series ví dụ**
```python
ax.set_xticks([
    dates.iloc[0],
    dates.iloc[-1]
])

# Chỉ hiện đầu và cuối timeline.
```
**Ex3: Tự chọn bước nhảy**
```bash
ax.set_yticks(
    range(0,301,50)
)

# ra: 0 50 100 150 200 250 300
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
# Config (Nhóm cấu hình)
# Axis()
```bash
Tắt hoặc hiển thị trục X,Y trên hình ảnh (ẩn các số và vạch trục).
```
**Syn**
```bash
plt.axis(‘on | off’)
```
## subplots() & subplot()
```bash
- Để cấu hình vùng hiển thị khi cần vẽ nhiều biểu đồ trong cùng 1 page
- Dùng khi vẽ phức tạp, nhiều axes, muốn quản lý dễ dàng.
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
### flatten() 
```bash
- Dùng khi bạn tạo nhiều subplot bằng plt.subplots() và muốn biến mảng các Axes từ 2 chiều thành 1 chiều để dễ lặp.
- Vì sao cần flatten()
```
**Ex1: không dùng flatten()**
```python
import matplotlib.pyplot as plt

fig, axes = plt.subplots(2, 3)

print(axes)

# axes lúc này là mảng 2 chiều:
# [
#  [ax1 ax2 ax3]
#  [ax4 ax5 ax6]
# ]

# Muốn truy cập từng subplot: axes[0,1].plot(...) -> Khá bất tiện nếu lặp.
```
**Ex2: Dùng flatten()**
```python
import matplotlib.pyplot as plt
import numpy as np

fig, axes = plt.subplots(2,3)

axes = axes.flatten()

for i, ax in enumerate(axes):
    x = np.linspace(0,10,100)
    y = np.sin(x+i)
    ax.plot(x,y)
    ax.set_title(f'Plot {i}')

plt.tight_layout()
plt.show()

# Sau: axes = axes.flatten()
# thì: [ax1, ax2, ax3, ax4, ax5, ax6]
# -> thành mảng 1 chiều. Giờ dùng: axes[4].plot(...) dễ hơn nhiều.
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
## tight_layout()
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
# Save (Nhóm lưu)
## plt.savefig()
**Syn**
```bash
plt.savefig(
    "ten_file.png",
    dpi=300
)

- Input:
    + dpi   : Chỉ định độ phân giải (tốt cho báo cáo/paper)
```