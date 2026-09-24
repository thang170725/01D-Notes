Scipy
    • Là thư viện để tính toán khoa học và toán học phức tạp. Được xây dựng trên numpy.
    • Là công cụ tính toán khoa học cao cấp hơn để tối ưu hóa, tích phân, giải hệ phương trình vi phân, xử lý tín hiệu.
6.2.1 Kiến thức cơ sở
Cài đặt thư viện Scipy
Gõ lệnh: pip install scipy
6.2.2 Thư viện stats
Là một module cung cấp một lượng lớn các hàm và phân phối thống kê. Nó là một công cụ mạnh mẽ để thực hiện các phân tích thống kê trong python.
6.2.2.1
mode()
Trả về giá trị xuất hiện nhiều lần nhất.
from scipy import stats
def main():
    speed = [90, 105, 55, 60, 75, 80, 55]
    print(stats.mode(speed))
main()
ModeResult(mode=np.int64(55), count=np.int64(2))
from scipy import stats
def main():
    speed = [90, 105, 60, 75, 80]
    print(stats.mode(speed))
main()
ModeResult(mode=np.int64(60), count=np.int64(1))
linregress()
Là phương thức ứng dụng cho thuật toán hồi quy tuyến tính (linear regression).
Trả về 5 giá trị:
    1. slope
    2. intercept ( y = slope*x + intercept)
    3. r – hệ số tương quan
    4. p  - Biểu thị mối quan hệ tuyến tính quan sát được giữa x và y xảy ra một cách ngẫu nhiên
    5. std_err – Sai số chuẩn
Ứng dụng thuật toán chiều cao, cân nặng bằng hồi quy tuyến tính sử dụng stas.linregress()
import pandas as pd
import scipy.stats as stats
import matplotlib.pyplot as plt
# hàm tính toán y dựa và x
def predict(x, slope, intercept):
    return slope * x + intercept

def main():
    # đọc file csv để  lấy dữ liệu
    li = pd.read_csv("D:\workspace\Python_box\danhSach.csv")
    # khởi tạo 2 mảng x và y để lưu dữ liệu
    x = li.values[:, 0] # cột chiều cao
    y = li.values[:, 1] # cột cân nặng
    # áp dụng phương thức stats.linregress để tính toán
    slope, intercept, r_value, p_value, std_err = stats.linregress(x, y)
    # mảng lưu y khi áp dụng hàm predict
    # vì map() chỉ mong muốn hàm có 1 tham số nên ta sử dụng lambda để truyền thêm 2 tham số slope và intercept
    yNew = list(map(lambda x_val : predict(x_val, slope, intercept), x))
    # kiểm tra giá trị của yNew
    print(yNew)
    # vẽ đồ thị
    plt.scatter(x, y)
    plt.plot(x, yNew,)
    plt.show()
main()

6.2.2.2 Thư viện skewnorm
    • Nó để cập đến phân phối chuẩn lệch, và nó được triển khai thông qua thư viện scipy.stats.
    • Phân phối chuẩn lệch là một mở rộng của phân phối chuẩn. Nó cho phép mô hình hóa dữ liệu không đối xứng, tức là dữ liệu có thể bị lệch về bên trái hoặc bên phải.
    • Trong khhi phân phối chuẩn có độ lệch bằng 0 (đối xứng), phân phối chuẩn lệch có thể có độ lệch dương hoặc âm.
rvs()
Là một hàm trong Python được sử dụng để tạo ra các giá trị ngẫu nhiên từ phân phối chuẩn lệch. Nó nằm trong module scipy.stas.
Cú pháp: stats.skewnorm.rvs(a, loc=0, scale=1, size=1, random_state=None)
    • a (tham số hình dạng): Đây là tham số quan trọng nhất, quyết định độ lệch của phân phối. Giá trị dương tạo ra độ lệch dương (đuôi dài về bên phải), giá trị âm tạo ra độ lệch âm (đuôi dài về bên trái), và giá trị 0 tạo ra phân phối chuẩn thông thường.
    • loc (tham số vị trí, mặc định là 0): Xác định vị trí của đỉnh phân phối, tương tự như trung bình trong phân phối chuẩn.
    • scale (tham số tỷ lệ, mặc định là 1): Xác định độ rộng của phân phối, tương tự như độ lệch chuẩn trong phân phối chuẩn.
    • size (kích thước, mặc định là 1): Xác định số lượng giá trị ngẫu nhiên cần tạo ra. Có thể là một số nguyên hoặc một tuple để tạo ra một mảng đa chiều.
    • random_state (trạng thái ngẫu nhiên, mặc định là None): Sử dụng để kiểm soát tính ngẫu nhiên. Nếu được cung cấp một số nguyên, nó sẽ đảm bảo rằng các giá trị ngẫu nhiên được tạo ra là nhất quán mỗi khi chạy mã.
Tham số đầu ra: Một mảng NumPy chứa các giá trị ngẫu nhiên được tạo ra từ phân phối chuẩn lệch.
from scipy.stats import skewnorm
def main():
    # create 100 random numbers
    data = skewnorm.rvs(4, size=100)
    # tạo ra 100 giá trị với đồ trị lệch trái
    print(data)
main()

[ 0.84770489  0.4501669  -0.1227352   0.49589245  0.93022384  3.22838968
  0.67146618  0.07334712  0.83055938  0.09659893  1.78585693  0.42485826
  0.70010012  1.03704254  0.2309022   1.38644932  1.16320305  1.44914808
  0.05609088  0.0843087   0.64471609 -0.02720244  0.13741172  2.33860118
  0.74360182  0.74755344 -0.06206227  1.44847973  0.45612282  0.37292896
  1.83735154  2.37184891  0.62020115  0.44811688  0.17479848  0.44227136
  0.6318813  -0.23830048  1.01790808  1.59318216  0.27927275  0.09151898
  0.6974189   1.64012235  1.13004769  1.17602352  0.78411231  1.4837838
  1.66473239  0.87052737  1.61517659  1.0271452   0.72088634  0.83490107
  0.18080852  1.22825258  0.82633184  0.83511088  2.28277042  1.58215873
  1.8214195   0.61429786  0.85449373  1.52146748  0.28031991  0.05068064
  0.01245932  0.34361952  1.75131734  2.44344304  0.36418092  0.35899311
  1.02018362  0.36920488  0.64772422  0.7898239   1.58372313  1.18781929
  0.15887835  0.88253347  0.13342374  0.18563885  0.53903796 -0.50987176
  0.48246609  0.52068334  0.92592464  1.76808875  0.65734475  0.67546101
  0.39304084  0.67473907  1.70859361  1.40792272  0.66010746 -0.07494275
  0.82308123  1.18293283  0.848569    0.28524023]

from scipy.stats import skewnorm
import matplotlib.pyplot as plt

a = 4 #Độ lệch của phân phối
x = skewnorm.rvs(a,size=3000) + 0.5
x = x[x>0]

nhiet_do = [85, 87, 75, 88, 80, 86, 90, 94, 93, 92, 90, 92, 94,
93, 97, 90, 95, 96, 96, 95, 92, 70, 79, 73, 88, 92, 94, 93, 95,
76, 78, 86, 81, 95, 77, 71, 69, 88, 86, 89, 84, 82, 77, 84, 81,
79, 75, 75, 91, 86, 86, 84, 82, 68, 75, 78, 82, 83, 85]

fig,ax = plt.subplots(1,2,figsize=(12,12))
ax[0].hist(x,bins=30)
ax[0].set_title("Bieu do tan suat ")
ax[0].set_xlabel("Gia tri")
ax[0].set_ylabel("Tan suat")

ax[1].hist(nhiet_do,bins=7)
ax[1].set_title("Bieu do tan suat nhiet do ")
ax[1].set_xlabel("Gia tri")
ax[1].set_ylabel("Tan suat")

plt.show()

from scipy.stats import skewnorm
import matplotlib.pyplot as plt

a = -4
b = 0
c = 4

x = skewnorm.rvs(a,size=5000) + 0.5
y = skewnorm.rvs(b,size=5000) + 0.5
z = skewnorm.rvs(c,size=5000) + 0.5

fig,ax = plt.subplots(1,3,figsize=(12,5))
ax[0].set_title("Bieu do 1")
ax[0].set_xlabel("Gia tri")
ax[0].set_ylabel("Tan suat")
ax[0].hist(x,bins=30)

ax[1].set_title("Bieu do 2")
ax[1].set_xlabel("Gia tri")
ax[1].set_ylabel("Tan suat")
ax[1].hist(y,bins=30)

ax[2].set_title("Bieu do 2")
ax[2].set_xlabel("Gia tri")
ax[2].set_ylabel("Tan suat")
ax[2].hist(z,bins=30)

plt.show()


