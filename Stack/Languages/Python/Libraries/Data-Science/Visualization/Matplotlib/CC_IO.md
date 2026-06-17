- [Introduction (Dùng để cấu hình (tức là bước trước khi vẽ biểu đồ))](#introduction-dùng-để-cấu-hình-tức-là-bước-trước-khi-vẽ-biểu-đồ)
- [Title() \& set\_title()](#title--set_title)
- [.suptitle()](#suptitle)
- [X \& Y Axis (Nhóm cấu hình trên trục X,Y)](#x--y-axis-nhóm-cấu-hình-trên-trục-xy)
  - [.xlabel() \& .ylabel() \&  .set\_ylabel() \& .set\_xlabel()](#xlabel--ylabel---set_ylabel--set_xlabel)
  - [set\_xticks() \& set\_yticks() (Dùng để đặt vị trí các vạch chia (ticks) trên trục X và Y)](#set_xticks--set_yticks-dùng-để-đặt-vị-trí-các-vạch-chia-ticks-trên-trục-x-và-y)
  - [.tick\_params() (dùng để chỉnh sửa các "tick" trên trục)](#tick_params-dùng-để-chỉnh-sửa-các-tick-trên-trục)
  - [xlim \& ylim (Dùng để thiết lập phạm vi (giới hạn) trục x và trục y của biểu đồ.)](#xlim--ylim-dùng-để-thiết-lập-phạm-vi-giới-hạn-trục-x-và-trục-y-của-biểu-đồ)
- [Config (Nhóm cấu hình)](#config-nhóm-cấu-hình)
- [Axis()](#axis)
  - [subplots() (Để cấu hình vùng hiển thị khi cần vẽ nhiều biểu đồ trong cùng 1 page)](#subplots-để-cấu-hình-vùng-hiển-thị-khi-cần-vẽ-nhiều-biểu-đồ-trong-cùng-1-page)
  - [subplot()](#subplot)
    - [flatten()](#flatten)
  - [.subplots\_adjust() (dùng để điều chỉnh khoảng cách giữa các subplot (các biểu đồ con) trong cùng một figure)](#subplots_adjust-dùng-để-điều-chỉnh-khoảng-cách-giữa-các-subplot-các-biểu-đồ-con-trong-cùng-một-figure)
- [figure() (Cài đặt kích thước của một khung hình)](#figure-cài-đặt-kích-thước-của-một-khung-hình)
  - [tight\_layout() (Để các biểu đồ không bị chồng lên nhau nếu một giao diện có nhiều biểu đồ)](#tight_layout-để-các-biểu-đồ-không-bị-chồng-lên-nhau-nếu-một-giao-diện-có-nhiều-biểu-đồ)
- [.colorbar()](#colorbar)
- [.legend() (Hiển thị chú thích)](#legend-hiển-thị-chú-thích)
- [.grid() (Hiện lưới)](#grid-hiện-lưới)
- [Save (Nhóm lưu)](#save-nhóm-lưu)
  - [plt.savefig() (lưu lại biểu đồ)](#pltsavefig-lưu-lại-biểu-đồ)
---
# Introduction (Dùng để cấu hình (tức là bước trước khi vẽ biểu đồ))
# Title() & set_title() 
```bash
Thiết lập tiêu đề của khung hình, khi cửa sổ đó chỉ có một hình ảnh.
```
# .suptitle()
**Syn**
```bash
plt.suptitle(
    "Aggregate Load Profiles of Random Days",
    fontsize=14    
)
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
## set_xticks() & set_yticks() (Dùng để đặt vị trí các vạch chia (ticks) trên trục X và Y)
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
## .tick_params() (dùng để chỉnh sửa các "tick" trên trục)
```bash
Tick gồm 2 thứ:
    - vạch chia trên trục.
    - nhãn (label) đi kèm vạch chia.
```
**Ex**
```bash
  ^
10|           ●
  |
  |
  |
  |
  +----------------->
    0   2   4   6   8

- 0 2 4 6 8 là tick labels.
- Các vạch nhỏ dưới chúng là ticks
```
**Syn**
```bash
ax[i].tick_params(...) hoặc plt.tick_params(...)

plt.tick_params(
    axis='x', 
    rotation=45, 
    labelsize=10, 
    colors='blue',
    labelbottom=False,
    length=10,
    width=2
)

- Input:
    + axis=: chỉnh trục
        - 'x': chỉ chỉnh trục x
        - 'y': chỉ chỉnh trục y
        - 'both': chỉnh cả 2 trục
    + labelsize=10: Chỉnh kích thước chữ
    + rotation=45: Xoay chữ 
    + labelbottom=: Ẩn nhãn
        - False: cho phép ẩn nhãn
    + length=10: Chỉnh độ dài vạch
    + width=2: Chỉnh độ dày vạch
```
## xlim & ylim (Dùng để thiết lập phạm vi (giới hạn) trục x và trục y của biểu đồ.)
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
## subplots() (Để cấu hình vùng hiển thị khi cần vẽ nhiều biểu đồ trong cùng 1 page)
```bash
Dùng khi vẽ phức tạp, nhiều axes, muốn quản lý dễ dàng.
```
**Syn: subplots**
```bash
self.fig, self.ax = plt.subplots(2, 2, figsize=(12, 5))

- Output:
    + fig: <class 'matplotlib.figure.Figure'>
    + ax: là mảng numy 2d gồm các axes
```
## subplot()
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
## .subplots_adjust() (dùng để điều chỉnh khoảng cách giữa các subplot (các biểu đồ con) trong cùng một figure)
**Ex: không dùng subplots_adjust**
```bash
Ví dụ bạn tạo:
fig, axes = plt.subplots(3, 3)
thì sẽ có 9 biểu đồ:
┌─────┬─────┬─────┐
│     │     │     │
├─────┼─────┼─────┤
│     │     │     │
├─────┼─────┼─────┤
│     │     │     │
└─────┴─────┴─────┘
Mặc định, matplotlib tự quyết định khoảng cách giữa chúng.
```
**Syn**
```bash
plt.subplots_adjust(
    wspace=0.2,
    hspace=0.2
)

- wspace: Là khoảng cách theo chiều ngang giữa các cột.
- hspace: Là khoảng cách theo chiều dọc giữa các hàng.
```
**Ex1**
```python
plt.subplots_adjust(wspace=0.1)
# ┌───┐┌───┐┌───┐
# │   ││   ││   │
# └───┘└───┘└───┘
plt.subplots_adjust(wspace=1)
# ┌───┐     ┌───┐     ┌───┐
# │   │     │   │     │   │
# └───┘     └───┘     └───┘
```
**Ex2**
```python
plt.subplots_adjust(hspace=0.1)
# ┌───┐
# │   │
# └───┘
# ┌───┐
# │   │
# └───┘
plt.subplots_adjust(hspace=1)
# ┌───┐
# │   │
# └───┘
# ┌───┐
# │   │
# └───┘
```
# figure() (Cài đặt kích thước của một khung hình)
**Ex**
```python
import matplotlib.pyplot as plt
from sklearn.datasets import load_digits

digits = load_digits()

plt.figure(figsize=(10,4)) # cài đặt khung hình với kích thước 10x4 inches

plt.imshow(digits.images[0], cmap='gray')
plt.show()
```
## tight_layout() (Để các biểu đồ không bị chồng lên nhau nếu một giao diện có nhiều biểu đồ)
**Syn**
```bash
plt.tight_layout()
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
# .legend() (Hiển thị chú thích)
```bash
Dùng khi có nhiều đường biểu diễn, để biết mỗi đường là gì
```
**Ex: so sánh doanh thu hai cửa hàng**
```python
import matplotlib.pyplot as plt

days = [1, 2, 3, 4]
store_A = [10, 12, 15, 18]
store_B = [8, 11, 13, 17]

plt.plot(days, store_A, marker='o', label='Cửa hàng A')
plt.plot(days, store_B, marker='s', label='Cửa hàng B')

plt.legend()

plt.show()
# Doanh thu

# 18 |                 ● A
# 17 |                 ■ B
# 15 |            ●
# 13 |            ■
# 12 |       ●
# 11 |       ■
# 10 |  ●
#  8 |  ■
#    +----------------
#      1  2  3  4

# Legend:
# ● Cửa hàng A
# ■ Cửa hàng B
```
# .grid() (Hiện lưới)
```bash
Dùng để đọc giá trị dễ hơn
```
**Ex**
```python
import matplotlib.pyplot as plt

months = [1, 2, 3, 4]
temperature = [20, 24, 28, 26]

plt.plot(months, temperature, marker='o')

plt.grid(True)

plt.show()
# Nhiệt độ

# 30 |
# 28 |----------------●---------
# 26 |----------------------●---
# 24 |---------●---------------
# 22 |
# 20 |●------------------------
#    +-------------------------
#      1    2    3    4
```
# Save (Nhóm lưu)
## plt.savefig() (lưu lại biểu đồ)
**Syn**
```bash
plt.savefig(
    "ten_file.png",
    dpi=300
)

- Input:
    + dpi   : Chỉ định độ phân giải (tốt cho báo cáo/paper)
```