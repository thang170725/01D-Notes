Matplotlib
Là một thư viện vẽ đồ thị cấp thấp
pip install matplotlib
__version__
Để kiểm tra version của thư viện mathplotlib.
Cú pháp:
import matplotlib as mat
 print(mat.__version__) # 3.10.1
Pyplot
Hầu hết các tiện ích matplotlib nằm trong module con pyplot và thường được nhập dưới bí danh plt.
import matplotlib.pyplot as plt
Title() & set_title() 
Thiết lập tiêu đề của khung hình, khi cửa sổ đó chỉ có một hình ảnh.
gca()
Để lấy ra axes hiện tại.
# take axes current
ax = plt.gca()
# có phương thức này mới có thể sử dụng được set_title, …
Xlabel() & ylabel() &  set_ylabel() & set_xlabel()
Thiết lập tiêu đề cho trục x, y của đồ thị, khi trong cửa sổ đó chỉ có một đồ thị.
Cú pháp:
plt.xlabel("Intent") hoặc plt.ylabel("Số lượng")
Axis()

Tắt hoặc hiển thị trục X,Y trên hình ảnh (ẩn các số và vạch trục)
Cú pháp: plt.axis(‘on | off’)
plot()
    • Được sử dụng để vẽ các điểm (điểm đánh dấu) trong sơ đồ nhưng thường được sử dụng để vẽ đường thẳng.
    • Theo mặc định, hàm plot() vẽ một đường thẳng từ điểm này đến điểm kia.
import matplotlib.pyplot as plt
import numpy as np
def main():
    x = np.array([3,4])
    y = np.array([7,8])

    plt.plot(x,y)
    plt.show()
main()

import matplotlib.pyplot as plt
import numpy as np
def main():
    x = np.array([3,4])
    y = np.array([7,8])

    plt.plot(x,y, 'x')
    plt.show()
main()

linestyle || ls
Để thay đổi kiểu hiển thị của đường biểu diễn đồ thị.
Style:
    • solid
    • dotted
    • dashed
    • dashdot
    • none
import matplotlib.pyplot as plt
import numpy as np

ypoints = np.array([3, 8, 1, 10])

plt.plot(ypoints, linestyle = 'dotted')
plt.show()

marker
Để đánh dấu các điểm trong đồ thị.
import matplotlib.pyplot as plt
import numpy as np
def main():
    x = np.array([3,4])
    y = np.array([7,8])

    plt.plot(x,y, marker = 'o')
    plt.show()
main()

Show() & imshow()
    • Để hiển thị lên màn hình.
    • matshow là hàm dùng để hiển thị ma trận dưới dạng hình ảnh. Nó được thiết kế đặc biệt để hiển thị dữ liệu 2d như ma trận, bảng, ảnh, … và tự động đặt tỷ lệ trục sao cho các ô vuông vức (không bị méo). Chỉ hiện thị được 1 hình ảnh trên một khung hình.

Cú pháp:
plt.show()
ax.imshow(wordcloud, interpolation="bilinear")
plt.matshow(digits.images[0], cmap='gray')


import matplotlib.pyplot as plt
from sklearn.datasets import load_digits
digits = load_digits()
plt.matshow(digits.images[0], cmap='gray')
plt.show() # một hình ảnh đen trắng số 0 kích thước 8x8 px sẽ được hiện ra
subplots() & subplot()
Chức năng giống subplot nhưng dùng khi vẽ phức tạp, nhiều axes, muốn quản lý dễ dàng.
Cú pháp:
self.fig, self.ax = plt.subplots(2, 2, figsize=(12, 5))
    • fig: <class 'matplotlib.figure.Figure'>
    • ax: là mảng numy 2d gồm các axes
plt.subplot(nrows, ncols, index)
    • nrows: Số hàng trong lưới.
    • ncols: Số cột trong lưới.
    • index: Vị trí con trỏ hiện tại
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



tight_layout()
Nếu một giao diện có nhiều biểu đồ thì hãy sử dụng phương thức này để các biểu đồ không bị chồng lên nhau.
Cú pháp: 
plt.tight_layout()
Xticks()
Cú pháp:
plt.xticks(rotation=45)


scatter()
Thường để vẽ các điểm.
Cú pháp: 
import matplotlib.pyplot as plt
plt.scatter(x, y, s=None, c=None, marker=None, alpha=None, cmap=None, edgecolors=None, linewidths=None)
    • x: danh sách hoặc mảng tọa độ trục x.
    • y: danh sách hoặc mảng tọa độ trục y.
    • s: kích thước của các điểm (có thể là một số hoặc danh sách).
    • c: màu của các điểm (có thể là một màu hoặc danh sách màu).
    • marker: kiểu đánh dấu (ví dụ: 'o', 'x', '^', 's', …).
    • alpha: độ trong suốt (giá trị từ 0 đến 1).
    • cmap: bản đồ màu nếu c là một mảng giá trị.
    • edgecolors: màu viền của các điểm.
    • inewidths: độ dày của viền.
import numpy as np
import matplotlib.pyplot as plt
def main():
    x = [2,4,6,8]
    y = [10,23,14,18]
    plt.scatter(x,y)
    plt.show()
main()

figure()
Cài đặt kích thước của một khung hình.
import matplotlib.pyplot as plt
from sklearn.datasets import load_digits
digits = load_digits()
plt.figure(figsize=(10,4))
plt.imshow(digits.images[0], cmap='gray')
plt.show()
# khung hình với kích thước 10x4 inches sẽ được hiển thị lên màn hình

Hist()
Để tạo biểu đồ histogram. Nó được chia thành các bin (khoảng giá trị) và hiển thị tần suất (số lượng) các điểm dữ liệu rơi vào mỗi bin.
Cú pháp:
plt.hist(x, bins=10, density=False, cumulative=False, color='blue', edgecolor='black', anpha=””…)
    • x: Dữ liệu đầu vào.
    • bins: Số lượng cột, chia dữ liệu thành bao nhiêu khoảng.
    • density: Mặc định False (hiển thị tần suất), nếu True biểu đồ sẽ chuẩn hóa thành xác suất. (False: trục y = số lượng, True: trục y = xác suất).
    • cumulative: Nếu True, sẽ vẽ biểu đồ tích lũy (cộng dồn từ trái sang phải).
    • color: Màu của các cột.
    • edgecolor: Màu đường viền của cột, giúp phân biệt dễ dàng hơn, thường là black hoặc white.
    • anpha: Mức độ trong suốt (opacity) của biểu đồ
import numpy as np
import matplotlib.pyplot as plt
number = np.random.uniform(0.0, 10, 100)
plt.hist(number, 100)
plt.show()
bar()
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

pie()
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

tick_params()
import seaborn as sns
import matplotlib.pyplot as plt
import pandas as pd

df = pd.DataFrame({
    "intent": ["play_music", "stop_music", "open_door", "close_door", "open_fan"],
    "length": [4, 5, 6, 7, 3]
})

plt.figure(figsize=(6,4))
sns.boxplot(x="intent", y="length", data=df, palette="Set2")

# Tinh chỉnh tick bằng matplotlib
plt.tick_params(axis='x', rotation=45, labelsize=10, colors='blue')
plt.tick_params(axis='y', labelsize=9, colors='red')

plt.title("Độ dài câu lệnh theo intent", fontsize=12)
plt.show()
