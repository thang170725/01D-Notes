- [Cấu trúc thư mục](#cấu-trúc-thư-mục)
- [Installation](#installation)
- [__version__](#version)
- [.tolist()](#tolist)
- [xác suất xuất hiện mặt 6 chấm khi tung 5 lượt mỗi lượt lại tung 10 lần](#xác-suất-xuất-hiện-mặt-6-chấm-khi-tung-5-lượt-mỗi-lượt-lại-tung-10-lần)
- [trả về phương sai tổng thể](#trả-về-phương-sai-tổng-thể)
- [Tổng số điểm](#tổng-số-điểm)
- [Sinh ngẫu nhiên (x, y) trong \[-1, 1\]](#sinh-ngẫu-nhiên-x-y-trong--1-1)
- [Đếm số điểm nằm trong đường tròn](#đếm-số-điểm-nằm-trong-đường-tròn)
- [Tính tỉ lệ và xấp xỉ pi](#tính-tỉ-lệ-và-xấp-xỉ-pi)
---
# Cấu trúc thư mục
```bash
Numpy/
├── base.md
├── Creation_Initialization.md  # khởi tạo
├── Linalg_Advanced.md          # vector / ma trận
├── Logic_Searching.md          # điều kiện
├── Math_Statistics.md          # tính toán
├── Practices_Case.md           # code mẫu
└── Shape_Manipulation.md       # hình dạng
```
# Installation
```bash
1. pip install numpy.
```
# __version__
```bash
Để kiểm tra version của thư viện numpy.
```
**Ex**
```python
import numpy as np
print(np.__version__) # 2.2.3
```



Random
Rand()
Dùng để sinh số ngẫu nhiên trong khoảng [0, 1). Theo phân phối đều.
Cú pháp:
    1. np.random.rand() # sinh ngẫu nhiên 1 số
    2. np.random.rand(5) # sinh ngẫu nhiên 1 mảng 5 số
    3. np.random.rand(3,4) # sinh ngẫu nhiên mảng 2 chiều 3x4
    4. 10 + (20-10)*np.random.rand(10)) # sinh ngẫu nhiên số từ 10 đến 20
Randint()
Tạo ra số nguyên ngẫu nhiên trong một khoảng xác định.
Cú pháp:
 np.random.randint(low, high=None, size=None, dtype=int)
    • low: Giá trị nhỏ nhất.
    • high: Giá trị lớn nhất.
    • size: int hoặc tuple, là kích thước của mảng.
    • dtype: Kiểu dữ liệu.
r = np.random.randint(1, 10, size=5)
print(r)
[6 4 6 3 3]
r = np.random.randint(1, 10, size=(5,5))
print(r)
[[2 1 5 4 2]
 [9 7 1 2 5]
 [4 4 7 9 6]
 [7 4 4 1 6]
 [9 7 2 2 7]]
Uniform()
Thường dùng để tạo ra các tập dữ liệu lớn để thử nghiệm (tập dữ liệu ngẫu nhiên ở bất kỳ kích thước nào).
Cú pháp:
color = np.random.uniform(0, 1, size=(100, 3))
    • 0: số bắt đầu
    • 1: số kết thúc
    • size: kích thước
number = np.random.uniform(0, 10, 5) # tạo ra 5 số từ 0 - 10
print(number)
[5.20684506 5.6623642  3.70489081 1.98964972 0.14884213]
seed()
randn()
Được dùng để tạo ra số ngẫu nhiên tuân theo quy luật phân phối chuẩn với trung bình (mean) = 0 và độ lệch chuẩn = 1.
Cú pháp: np.random.randn(d0, d1, …, dn)
normal()
Tạo một mảng giá trị ngẫu nhiên, trong đó các giá trị tập trung xung quanh một giá trị cho trước. Loại phân phối dữ liệu này được gọi là phân phối dữ liệu chuẩn hoặc phân phối dữ liệu gauss.
Cú pháp: 
numpy.random.normal(loc=0.0,  size=None, scale=1.0)
    • loc: Trung bình (mean) của phân phối.
    • scale: Độ lệch chuẩn của phân phối.
    • size: kích thước của mảng kết quả có thể là số nguyên, tuple, hoặc None).
number = np.random.normal(0.0, scale=10, size=50)
plt.hist(number, bins=10)
plt.show()
binomial()
    • Dùng để sinh ra các giá trị ngẫu nhiên theo phân phối nhị thức (binomial distribution).
    • Phân phối nhị thức mô tả số lần thành công trong một số lần thử cố định, với xác suất thành công không đổi trong mỗi lần thử.
    • Ứng dụng là mô phỏng thử nghiệm Bernoulli lặp lại nhiều lần, tạo dữ liệu giả lập cho bài toán phân loại nhị phân. Mô phỏng kết quả của thí nghiệm có xác suất (sổ xố, trò chơi, …)
Cú pháp: numpy.random.binomial(n, p, size=None)
    • n: Số lần thử (Số nguyên dương)
    • p: Xác suất thành công trong mỗi lần thử (0 <= p <= 1)
    • size: Số lượng giá trị random muốn tạo ra (có thể là một số nguyên hoặc tuple, ví dụ (3, 3)
import numpy as np
result = np.random.binomial(n=10, p=1/6, size=5)
print(result)
# xác suất xuất hiện mặt 6 chấm khi tung 5 lượt mỗi lượt lại tung 10 lần
[2 3 6 2 1]
choice()
Là một hàm trong Python được sử dụng để chọn một phần tử ngãu nhiên từ một chuỗi (ssequence) cho trước. Chuỗi này có thể là.
    • Danh sách (list): Một tập hợp các phần tử có thứ tự, có thể thay đổi.
    • Tuple: Một tập hợp các phần tử có thứ tự, không thể thay đổi.
    • Chuỗi ký tự (string): Một dãy các ký tự.

