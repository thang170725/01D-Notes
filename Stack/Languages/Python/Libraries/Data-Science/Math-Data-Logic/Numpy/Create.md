- [np.array() \& empty \& .zeros()](#nparray--empty--zeros)
- [.zeros\_like()](#zeros_like)
- [.astype()](#astype)
- [frombuffer](#frombuffer)
- [.tobytes()](#tobytes)
- [linspace()](#linspace)
- [Asarray()](#asarray)
- [.view() \& .copy()](#view--copy)
- [Random (Tạo ngẫu nhiên)](#random-tạo-ngẫu-nhiên)
  - [Rand()](#rand)
  - [Randint()](#randint)
  - [Uniform()](#uniform)
  - [.seed()](#seed)
  - [randn()](#randn)
  - [normal()](#normal)
  - [binomial()](#binomial)
  - [.choice()](#choice)

---

# np.array() & empty & .zeros()

```bash
- array     : Tạo mảng có sẵn giá trị.
- empty     : Tạo mảng không quan tâm giá trị (rất nhanh).
- zeros     : Tạo mảng có kích thước có sẵn.
```

**Syn: array**

```bash
arr = np.array([1,2,3,4,5], dtype=float)

- dtype: chỉ định kiểu dữ liệu của mảng
    + i4 : là kiểu dữ liệu integer có kích thước 4 bytes
```

**Syn: empty**

```bash
import numpy as np

arr = np.empty((h, w))   # h, w là kích thước đã biết
```

**Syn: zeros**

```bash
out = np.zeros(
   (out_h, out_w, chanels),
   dtype=np.uint8
)
```

# .zeros_like()

```bash
- Để tạo một mảng mới có cùng hình dạng (shape) và kiểu dữ liệu (dtype) với mảng gốc, nhưng tất cả các phần tử đều bằng 0.
```

**Syn**

```bash
np.zeros_like(a, dtype=None)

- a: mảng gốc muốn “bắt chước” shape và dtype.
- dtype: (tuỳ chọn) nếu muốn đổi kiểu dữ liệu, có thể truyền thêm vào.
```

**Ex**

```python
a = np.array([[1, 2, 3], [4, 5, 6]])
b = np.zeros_like(a)

print("a:\n", a)
print("b:\n", b)

# a:
#  [[1 2 3]
#   [4 5 6]]
# b:
#  [[0 0 0]
#   [0 0 0]]
```

# .astype()

```bash
- Dùng để chuyển kiểu dữ liệu của mảng sang kiểu khác.
```

**Syn**

```bash
a = array.astype(dtype)

- dtype: là kiểu dữ liệu bạn muốn chuyển sang, ví dụ: int, float, bool, str, np.int32, np.float64, …
```

**Ex1**

```python
arr = np.array([1.1, 2.1, 3.1])
newarr = arr.astype('i')
print(newarr) # [1 2 3]
print(newarr.dtype) # int32
```

**Ex2**

```python
arr = np.array([1.1, 2.1, 3.1])
newarr = arr.astype(int)
print(newarr) # [1 2 3]
print(newarr.dtype) # int64
```

**Ex3**

```python
arr = np.array([1, 0, 3])
newarr = arr.astype(bool)
print(newarr) # [ True False True]
print(newarr.dtype) # bool
```

# frombuffer

- Chuyển bytes → numpy array 1 chiều.
- Thường dùng kèm với cv2.imdecode
**Syn**

```bash
np.frombuffer(buffer, dtype=np.uint8, count=-1, offset=0)
```

**Ex**

```python
np_arr = np.frombuffer(image_bytes, np.uint8)
# np_arr = [137, 80, 78, 71, ...]
# CHƯA phải ảnh, chỉ là byte stream
```

# .tobytes()

Chuyển np.ndarray → bytes (gửi HTTP)
**Syn**

```bash
ndarray.tobytes(order='C')
```

# linspace()

```bash
Để tạo một mảng số cách đều nhau trên một khoảng xác định.
```

**Syn** 

```bash
numpy.linspace(start, stop, num=50, endpoint=True, retstep=False, dtype=None, axis=0)

- start: Giá trị bắt đầu của dãy số.
- stop: Giá trị kết thúc của dãy số.
- num: Số lượng phần tử trong dãy số (mặc định là 50).
- endpoint: Nếu là True (mặc định), stop là phần tử cuối cùng của dãy số. Nếu là false, stop không được bao gồm.
- retstep: Nếu là True, hàm này trả về một tuple gồm mảng và khoảng cách giữa các phần tử.
- dtype: Kiểu dữ liệu của các phần tử trong mảng.
- axis: Trục để lưu kết quả.
```
**Ex**
```python
import numpy as np

res = np.linspace(0, 10, num=10, endpoint=False)
print(res) # [0. 1. 2. 3. 4. 5. 6. 7. 8. 9.]
```
# Asarray()
```bash
Dùng để chuyển dữ liệu bất kỳ (list, tuple, list lồng nhau, …) thành mảng NumPy (ndarray) nhưng không tạo bản sao (copy) nếu không cần thiết — tức là nếu đầu vào đã là ndarray rồi thì nó trả về chính nó, không tạo mảng mới.
```
**Ex**
```python
arr = np.asarray(lst, dtype=float)
import numpy as np

arr1 = np.array([1, 2, 3])
arr2 = np.asarray(arr1)

print(arr1 is arr2)  # True -> cùng vùng nhớ
np.asarray() không tạo copy → tiết kiệm bộ nhớ.
```
# .view() & .copy()
```bash
- view  : Tạo một chế độ xem focus vào mảng gốc.
- copy  : Để sao chép một mảng.
```
**Ex1: view**
```python
arr = np.array([1, 2, 3, 4, 5])
x = arr.view()

arr[0] = 42

print(arr) # [42 2 3 4 5]
print(x) # [42 2 3 4 5]
```
**Ex2: copy**
```python
arr = np.array([1, 2, 3, 4, 5])
x = arr.copy()
arr[0] = 42
print(arr) # [42 2 3 4 5]
print(x) # [1 2 3 4 5]
```
# Random (Tạo ngẫu nhiên)
## Rand()
```bash
Dùng để sinh số ngẫu nhiên trong khoảng [0, 1). Theo phân phối đều.
```
**Syn**
```bash
1. np.random.rand() # sinh ngẫu nhiên 1 số
2. np.random.rand(5) # sinh ngẫu nhiên 1 mảng 5 số
3. np.random.rand(3,4) # sinh ngẫu nhiên mảng 2 chiều 3x4
4. 10 + (20-10)*np.random.rand(10)) # sinh ngẫu nhiên số từ 10 đến 20
```
## Randint()
```bash
Tạo ra số nguyên ngẫu nhiên trong một khoảng xác định.
```
**Syn**
```bash
np.random.randint(low, high=None, size=None, dtype=int)

- low: Giá trị nhỏ nhất.
- high: Giá trị lớn nhất.
- size: int hoặc tuple, là kích thước của mảng.
- dtype: Kiểu dữ liệu.
```
**Ex**
```python
r1 = np.random.randint(1, 10, size=5)

print(r1) # [6 4 6 3 3]

r2 = np.random.randint(1, 10, size=(5,5))

print(r2)

# [[2 1 5 4 2]
#  [9 7 1 2 5]
#  [4 4 7 9 6]
#  [7 4 4 1 6]
#  [9 7 2 2 7]]
```
## Uniform()
```bash
Thường dùng để tạo ra các tập dữ liệu lớn để thử nghiệm (tập dữ liệu ngẫu nhiên ở bất kỳ kích thước nào).
```
**Syn**
```bash
color = np.random.uniform(0, 1, size=(100, 3))

- 0: số bắt đầu
- 1: số kết thúc
- size: kích thước
```
**Ex**
```python
number = np.random.uniform(0, 10, 5) # tạo ra 5 số từ 0 - 10

print(number) # [5.20684506 5.6623642  3.70489081 1.98964972 0.14884213]
```
## .seed()
## randn()
```bash
Được dùng để tạo ra số ngẫu nhiên tuân theo quy luật phân phối chuẩn với trung bình (mean) = 0 và độ lệch chuẩn = 1.
```
**Syn** 
```bash
np.random.randn(d0, d1, …, dn)
```
## normal()
```bash
Tạo một mảng giá trị ngẫu nhiên, trong đó các giá trị tập trung xung quanh một giá trị cho trước. Loại phân phối dữ liệu này được gọi là phân phối dữ liệu chuẩn hoặc phân phối dữ liệu gauss.
```
**Syn**
```bash
numpy.random.normal(loc=0.0,  size=None, scale=1.0)

- loc: Trung bình (mean) của phân phối.
- scale: Độ lệch chuẩn của phân phối.
- size: kích thước của mảng kết quả có thể là số nguyên, tuple, hoặc None).
```
## binomial()
```bash
- Dùng để sinh ra các giá trị ngẫu nhiên theo phân phối nhị thức (binomial distribution).
- Phân phối nhị thức mô tả số lần thành công trong một số lần thử cố định, với xác suất thành công không đổi trong mỗi lần thử.
- Ứng dụng là mô phỏng thử nghiệm Bernoulli lặp lại nhiều lần, tạo dữ liệu giả lập cho bài toán phân loại nhị phân. Mô phỏng kết quả của thí nghiệm có xác suất (sổ xố, trò chơi, …)
```
**Syn**
```bash
numpy.random.binomial(n, p, size=None)

- n: Số lần thử (Số nguyên dương)
- p: Xác suất thành công trong mỗi lần thử (0 <= p <= 1)
- size: Số lượng giá trị random muốn tạo ra (có thể là một số nguyên hoặc tuple, ví dụ (3, 3)
```
**Ex: xác suất xuất hiện mặt 6 chấm khi tung 5 lượt mỗi lượt lại tung 10 lần**
```python
import numpy as np
result = np.random.binomial(n=10, p=1/6, size=5)
print(result) # [2 3 6 2 1]
```
## .choice()
```bash
Dùng để chọn ngẫu nhiên phần tử từ một tập hợp.
```
**Syn**
```bash
np.random.choice(a, size=None, replace=True, p=None)

- Input:
  + a:
    - Nếu là số nguyên n → chọn từ 0 đến n-1
    - Nếu là list/array → chọn từ các phần tử đó
  + size: Số lượng phần tử muốn lấy
  + replace=True:
    - True: lấy có hoàn lại (có thể trùng)
    - False: không hoàn lại (không trùng)
  + p: Xác suất chọn từng phần tử
```
**Ex1: Chọn 1 phần tử ngẫu nhiên**
```python
import numpy as np

x = np.random.choice([10,20,30,40])
print(x) # 30
```
**Ex2: Chọn nhiều phần tử**
```python
np.random.choice([10,20,30,40], size=3) ## array([20, 20, 40]) (vì mặc định cho phép lặp)

# Không cho trùng
np.random.choice([10,20,30,40], size=3, replace=False) # array([40,10,30])
```
**Ex3: Chọn theo xác suất**

```python
np.random.choice(
    ['A','B','C'],
    size=10,
    p=[0.7,0.2,0.1]
)

# A có 70% khả năng xuất hiện.
# Ví dụ: ['A' 'A' 'B' 'A' ...]
```