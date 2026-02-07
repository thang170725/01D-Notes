- [np.array() \& empty \& .zeros()](#nparray--empty--zeros)
- [.zeros\_like()](#zeros_like)
- [.astype()](#astype)
- [frombuffer](#frombuffer)
- [.tobytes()](#tobytes)
- [linspace()](#linspace)
- [.tolist()](#tolist)
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
```python
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
# .tolist()
Để chuyển từ mảng numpy sang mảng thường.
**Cú pháp**
```text
arr.tolist()
```
Asarray()
Dùng để chuyển dữ liệu bất kỳ (list, tuple, list lồng nhau, …) thành mảng NumPy (ndarray) nhưng không tạo bản sao (copy) nếu không cần thiết — tức là nếu đầu vào đã là ndarray rồi thì nó trả về chính nó, không tạo mảng mới.
Cú pháp:
arr = np.asarray(lst, dtype=float)
import numpy as np

arr1 = np.array([1, 2, 3])
arr2 = np.asarray(arr1)

print(arr1 is arr2)  # True -> cùng vùng nhớ
np.asarray() không tạo copy → tiết kiệm bộ nhớ.