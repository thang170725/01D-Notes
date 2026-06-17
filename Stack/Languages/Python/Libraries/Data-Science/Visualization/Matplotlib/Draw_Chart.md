- [Show()](#show)
- [plt.close()](#pltclose)
- [imshow()](#imshow)
- [matshow()](#matshow)
- [plot()](#plot)
- [marker](#marker)
- [scatter()](#scatter)
- [Hist()](#hist)
- [bar()](#bar)
- [pie()](#pie)
- [take axes current](#take-axes-current)
- [có phương thức này mới có thể sử dụng được set\_title, …](#có-phương-thức-này-mới-có-thể-sử-dụng-được-set_title-)
- [.axvline() (Vẽ đường thẳng đứng)](#axvline-vẽ-đường-thẳng-đứng)
---
# Show()
```bash
Để hiển thị chart
```
# plt.close() 
```bash
Nó dùng để đóng figure (biểu đồ).
```
**Syn**
```bash
import matplotlib.pyplot as plt

plt.close()
```
**Ex1: Đóng figure hiện tại**
```python
import matplotlib.pyplot as plt

plt.plot([1,2,3],[4,5,6])
plt.show()

plt.close()
```
**Ex2: Đóng một figure cụ thể**
```python
fig = plt.figure()

plt.plot([1,2,3])

plt.close(fig)
```
**Ex3: Đóng tất cả figure**
```python
plt.close('all') # Rất hay dùng.
```
**Tại sao phải dùng?**
```bash
- Tránh tốn bộ nhớ. Nếu loop vẽ hàng trăm biểu đồ:
    for col in df.columns:

        plt.plot(df[col])
        plt.savefig(f"{col}.png")

        plt.close()
- Nếu không close():
    + figure chồng chất trong memory
    + có thể warning:
```
# imshow()
```bash
- Dùng để hiển thị ma trận như một ảnh.
- Ma trận 2D (100×100) → được hiểu là ảnh grayscale
```
# matshow()
```bash
- Dùng để hiển thị ma trận dưới dạng hình ảnh. 
- Nó được thiết kế đặc biệt để hiển thị dữ liệu 2d như ma trận, bảng, ảnh, … và tự động đặt tỷ lệ trục sao cho các ô vuông vức (không bị méo). 
- Chỉ hiện thị được 1 hình ảnh trên một khung hình.
```
**Ex1**
```python
import matplotlib.pyplot as plt
from sklearn.datasets import load_digits

digits = load_digits()

plt.matshow(digits.images[0], cmap='gray')
plt.show() # một hình ảnh đen trắng số 0 kích thước 8x8 px sẽ được hiện ra
```
# plot()
```bash
- Theo mặc định, hàm plot() vẽ một đường thẳng từ điểm này đến điểm kia.
```
**Syn**
```bash
plt.plot(x, y, 'x', linestyle='dotted')

- Input:
    + linestyle: thay đổi kiểu hiển thị của đường biểu diễn đồ thị
        - solid
        - dotted
        - dashed
        - dashdot
        - none
```
**Ex**
```python
import matplotlib.pyplot as plt
import numpy as np

x = np.array([3,4])
y = np.array([7,8])

plt.plot(x,y)
plt.show()
```
# marker
```bash
Để đánh dấu các điểm trong đồ thị.
```
**Ex**
```python
import matplotlib.pyplot as plt
import numpy as np

x = np.array([3,4])
y = np.array([7,8])

plt.plot(x,y, marker = 'o')
plt.show()
```
# scatter()
```bash
Thường để vẽ các điểm.
```
**Syn**
```bash
import matplotlib.pyplot as plt
plt.scatter(x, y, s=None, c=None, marker=None, alpha=None, cmap=None, edgecolors=None, linewidths=None)

- x: danh sách hoặc mảng tọa độ trục x.
- y: danh sách hoặc mảng tọa độ trục y.
- s: kích thước của các điểm (có thể là một số hoặc danh sách).
- c: màu của các điểm (có thể là một màu hoặc danh sách màu).
- marker: kiểu đánh dấu (ví dụ: 'o', 'x', '^', 's', …).
- alpha: độ trong suốt (giá trị từ 0 đến 1).
- cmap: bản đồ màu nếu c là một mảng giá trị.
- edgecolors: màu viền của các điểm.
- inewidths: độ dày của viền.
```
**Ex**
```python
import numpy as np
import matplotlib.pyplot as plt

x = [2,4,6,8]
y = [10,23,14,18]
plt.scatter(x,y)
plt.show()
```
# Hist()
```bash
Để tạo biểu đồ histogram. Nó được chia thành các bin (khoảng giá trị) và hiển thị tần suất (số lượng) các điểm dữ liệu rơi vào mỗi bin.
```
**Syn**
```bash
plt.hist(x, bins=10, density=False, cumulative=False, color='blue', edgecolor='black', anpha=””…)

- x: Dữ liệu đầu vào.
- bins: Số lượng cột, chia dữ liệu thành bao nhiêu khoảng.
- density: Mặc định False (hiển thị tần suất), nếu True biểu đồ sẽ chuẩn hóa thành xác suất. (False: trục y = số lượng, True: trục y = xác suất).
- cumulative: Nếu True, sẽ vẽ biểu đồ tích lũy (cộng dồn từ trái sang phải).
- color: Màu của các cột.
- edgecolor: Màu đường viền của cột, giúp phân biệt dễ dàng hơn, thường là black hoặc white.
- anpha: Mức độ trong suốt (opacity) của biểu đồ
```
**Ex**
```python
import numpy as np
import matplotlib.pyplot as plt

number = np.random.uniform(0.0, 10, 100)
plt.hist(number, 100)
plt.show()
```
# bar()
Để tạo biểu đồ cột (bar chart). Biểu đồ cột là một cách trực quan để so sánh các giá trị giữa các danh mục khác nhau.
Cú pháp: matplotlib.pyplot.bar(x, height, width=0.8, bottom=None, align='center', data=None, **kwargs)
    • x: Vị trí của các cột trên trục x. Đây thường là một danh sách hoặc mảng chứa các giá trị số hoặc chuỗi đại diện cho các danh mục. 
    • height: Chiều cao của các cột. Đây là một danh sách hoặc mảng chứa các giá trị số tương ứng với chiều cao của mỗi cột. 
    • width: Độ rộng của các cột. Giá trị mặc định là 0.8. 
    • bottom: Vị trí cơ sở của các cột trên trục y. Giá trị mặc định là 0. 
    • align: Căn chỉnh các cột so với vị trí x. Có thể là 'center' (mặc định) hoặc 'edge'. 
    • color: Màu sắc của các cột. 
    • label: Nhãn cho biểu đồ, được sử dụng trong chú giải.
import matplotlib.pyplot as plt
def main():
    brand = ["Mercedes", "BMW", "Audi", "Porsche", "Rolls Royce"] # y-axis
    quantity = [100, 50, 75, 25, 10] # x-axis
    # bar chart
    plt.bar(brand, quantity, width=0.5, bottom=None, align="center", color="black", alpha=0.5)
    # take axes current
    ax = plt.gca()
    ax.set_title("Bar Chart")
    ax.set_xlabel("Brand")
    ax.set_ylabel("Quantity")
    plt.show()

main()


import matplotlib.pyplot as plt

mau_xe = ['Đỏ', 'Xanh', 'Đen', 'Trắng']
so_luong = [12, 18, 9, 15]

muc_do = ['Rất tệ', 'Tệ', 'Bình thường', 'Tốt', 'Rất tốt']
sl = [5, 8, 15, 20, 25]

fig,ax = plt.subplots(1,2,figsize=(12,5))

ax[0].set_title("Bieu do 1 ")
ax[0].set_xlabel("Mau xe")
ax[0].set_ylabel("So luong")
ax[0].bar(mau_xe,so_luong)

ax[1].set_title("Bieu do 2")
ax[1].set_xlabel("Muc do")
ax[1].set_ylabel("So luong")
ax[1].bar(muc_do,sl)

plt.show()
# pie()
Là một hàm thuộc thư viện matplotlib.pyplot dùng để vẽ biểu đồ hình tròn (pie chart). Biểu đồ hình tròn thể hiện dữ liệu dưới dạng các phần của một hình tròn, mỗi phần có kích thước tỷ lệ với giá trị dữ liệu tương ứng.
Cú pháp: matplotlib.pyplot.pie(x, explode=None, labels=None, colors=None, autopct=None, shadow=False, startangle=0)
    • x: Mảng các giá trị số liệu, mỗi giá trị đại diện cho kích thước của một phần trong biểu đồ. 
    • explode: Mảng các giá trị số liệu, mỗi giá trị đại diện cho khoảng cách "nổ tung" của một phần khỏi tâm hình tròn. Giá trị càng lớn, phần đó càng xa tâm. 
    • labels: Danh sách các chuỗi, mỗi chuỗi đại diện cho nhãn của một phần trong biểu đồ. 
    • colors: Danh sách các màu, mỗi màu đại diện cho màu sắc của một phần trong biểu đồ. 
    • autopct: Chuỗi định dạng để hiển thị phần trăm giá trị của mỗi phần. Ví dụ: %1.1f%% hiển thị phần trăm với một chữ số thập phân. 
    • shadow: Giá trị boolean, nếu True sẽ thêm bóng đổ cho biểu đồ. 
    • startangle: Góc bắt đầu của phần đầu tiên trong biểu đồ (tính theo độ, mặc định là 0).
import matplotlib.pyplot as plt
def main():
    # Dữ liệu
    labels = 'Ếch', 'Heo', 'Chó', 'Gà'
    sizes = [15, 30, 45, 10]
    explode = (0, 0.1, 0, 0)  # "nổ tung" phần "Heo"

    # Vẽ biểu đồ
    fig1, ax1 = plt.subplots()
  ax1.pie(sizes, explode=explode, labels=labels, autopct='%1.1f%%', shadow=True, startangle=90)
    ax1.axis('equal')  # Đảm bảo hình tròn có dạng tròn

    plt.show()
main()


import matplotlib.pyplot as plt

khoa = ['CNTT', 'Kinh tế', 'Y dược', 'Kỹ thuật', 'Ngoại ngữ']
sl = [350, 420, 250, 300, 280]

plt.pie(sl,labels = khoa,autopct='%1.1f%%')
plt.show()


gca()
Để lấy ra axes hiện tại.
# take axes current
ax = plt.gca()
# có phương thức này mới có thể sử dụng được set_title, …
Biểu đồ cơ bản (phải biết)
1. plt.plot()
Dùng để làm gì

Vẽ biểu đồ đường.

Ứng dụng
Xu hướng theo thời gian
Giá cổ phiếu
Doanh thu
Cú pháp
plt.plot(x, y)
Ví dụ
plt.plot([1,2,3], [2,5,4])
2. plt.scatter()
Dùng để làm gì

Biểu đồ phân tán.

Ứng dụng
Mối quan hệ giữa 2 biến
Correlation
Cú pháp
plt.scatter(x, y)
Ví dụ
plt.scatter(height, weight)
3. plt.bar()
Dùng để làm gì

Biểu đồ cột đứng.

Ứng dụng
So sánh giữa các nhóm.
Cú pháp
plt.bar(x, height)
Ví dụ
plt.bar(["A","B","C"], [10,20,15])
4. plt.barh()
Dùng để làm gì

Biểu đồ cột ngang.

Ứng dụng
Top N
Ranking.
Cú pháp
plt.barh(y, width)
Ví dụ
plt.barh(names, scores)
5. plt.hist()
Dùng để làm gì

Histogram.

Ứng dụng
Phân bố dữ liệu.
Cú pháp
plt.hist(x)
Ví dụ
plt.hist(scores, bins=10)
6. plt.pie()
Dùng để làm gì

Biểu đồ tròn.

Ứng dụng
Tỷ lệ thành phần.
Cú pháp
plt.pie(x)
Ví dụ
plt.pie([30,40,30],
        labels=["A","B","C"])
II. Biểu đồ trung cấp
7. plt.boxplot()
Dùng để làm gì

Boxplot.

Ứng dụng
Outlier
Median.
Cú pháp
plt.boxplot(x)
Ví dụ
plt.boxplot(scores)
8. plt.violinplot()
Dùng để làm gì

Violin plot.

Ứng dụng
Hình dạng phân bố.
Cú pháp
plt.violinplot(dataset)
Ví dụ
plt.violinplot([classA,classB])
9. plt.stem()
Dùng để làm gì

Biểu đồ thân-cành.

Ứng dụng
Xử lý tín hiệu số.
Cú pháp
plt.stem(x,y)
Ví dụ
plt.stem([1,2,3],[2,5,4])
10. plt.step()
Dùng để làm gì

Biểu đồ bậc thang.

Ứng dụng
Giá điện
Dữ liệu thay đổi theo mức.
Cú pháp
plt.step(x,y)
Ví dụ
plt.step(time, level)
11. plt.errorbar()
Dùng để làm gì

Vẽ sai số.

Ứng dụng
Kết quả thí nghiệm.
Cú pháp
plt.errorbar(x,y,yerr=error)
Ví dụ
plt.errorbar(x,y,yerr=std)
III. Biểu đồ nâng cao
12. plt.stackplot()
Dùng để làm gì

Area chart chồng.

Ứng dụng
Thành phần thay đổi theo thời gian.
Cú pháp
plt.stackplot(x,y1,y2,...)
Ví dụ
plt.stackplot(year, ios, android)
13. plt.fill_between()
Dùng để làm gì

Tô vùng giữa các đường.

Ứng dụng
Confidence interval.
Cú pháp
plt.fill_between(x,y1,y2)
Ví dụ
plt.fill_between(x, lower, upper)
14. plt.eventplot()
Dùng để làm gì

Biểu diễn các sự kiện.

Ứng dụng
Spike train.
Event timeline.
Cú pháp
plt.eventplot(events)
Ví dụ
plt.eventplot([1,3,5,8])
15. plt.hexbin()
Dùng để làm gì

Scatter mật độ cao.

Ứng dụng
Dataset rất lớn.
Cú pháp
plt.hexbin(x,y)
Ví dụ
plt.hexbin(x,y, gridsize=20)
IV. Biểu đồ ma trận và ảnh
16. plt.imshow()
Dùng để làm gì

Hiển thị ảnh hoặc ma trận.

Ứng dụng
Computer Vision
Heatmap đơn giản.
Cú pháp
plt.imshow(data)
Ví dụ
plt.imshow(image)
17. plt.matshow()
Dùng để làm gì

Hiển thị ma trận.

Ứng dụng
Ma trận tương quan.
Cú pháp
plt.matshow(matrix)
Ví dụ
plt.matshow(df.corr())
V. Biểu đồ vector
18. plt.quiver()
Dùng để làm gì

Biểu diễn vector.

Ứng dụng
Vật lý.
Trường lực.
Cú pháp
plt.quiver(X,Y,U,V)
Ví dụ
plt.quiver(x,y,u,v)
19. plt.streamplot()
Dùng để làm gì

Đường dòng.

Ứng dụng
Dòng chảy chất lỏng.
Cú pháp
plt.streamplot(X,Y,U,V)
Ví dụ
plt.streamplot(X,Y,U,V)
VI. Biểu đồ 3D (mpl_toolkits.mplot3d)
20. ax.plot3D()

Đường 3D.

Ví dụ:

ax.plot3D(x,y,z)
21. ax.scatter3D()

Scatter 3D.

Ví dụ:

ax.scatter3D(x,y,z)
22. ax.bar3d()

Cột 3D.

Ví dụ:

ax.bar3d(x,y,z,dx,dy,dz)
23. ax.plot_surface()

Surface plot.

Ứng dụng:

Hàm số 3D.

Ví dụ:

ax.plot_surface(X,Y,Z)
24. ax.contour3D()

Contour 3D.

Ví dụ:

ax.contour3D(X,Y,Z)
VII. Biểu đồ thống kê đặc biệt
25. plt.contour()

Contour 2D.

Ứng dụng:

Đường đồng mức.
plt.contour(X,Y,Z)
26. plt.contourf()

Contour tô màu.

plt.contourf(X,Y,Z)
27. plt.specgram()

Spectrogram.

Ứng dụng:

Phân tích âm thanh.
plt.specgram(signal)
# .axvline() (Vẽ đường thẳng đứng)
```bash
Dùng khi muốn đánh dấu một mốc đặc biệt trên trục X.
```
**Ex: doanh thu 7 ngày, và đánh dấu ngày bắt đầu khuyến mãi**
```python
import matplotlib.pyplot as plt

days = [1, 2, 3, 4, 5, 6, 7]
sales = [10, 12, 11, 20, 22, 21, 23]

plt.plot(days, sales, marker='o')

# Đánh dấu ngày thứ 4
plt.axvline(x=4, color='red', linestyle='--')

plt.title("Doanh thu 7 ngày")
plt.xlabel("Ngày")
plt.ylabel("Doanh thu")
plt.show()
# Doanh thu
# 23 |                       ●
# 22 |                    ●
# 21 |                  ●
# 20 |             ●
# 12 |      ●
# 11 |         ●
# 10 |   ●
#    +----------------------------
#       1  2  3 |4| 5  6  7
#               ↑
#       Đường đỏ đánh dấu ngày khuyến mãi
```