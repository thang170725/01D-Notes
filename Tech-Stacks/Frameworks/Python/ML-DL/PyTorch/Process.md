- [Create (Nhóm khởi tạo)](#create-nhóm-khởi-tạo)
  - [.tensor() (Để tạo tensor trong pytorch, giống với mảng số)](#tensor-để-tạo-tensor-trong-pytorch-giống-với-mảng-số)
  - [.clone()](#clone)
  - [Arange()](#arange)
  - [Zeros()](#zeros)
  - [Random](#random)
    - [.rand() (Để tạo ma trận ngẫu nhiên)](#rand-để-tạo-ma-trận-ngẫu-nhiên)
    - [randn\_like()](#randn_like)
    - [.randn() (Khởi tạo ngẫu nhiên theo phân phối chuẩn (Normal distribution))s](#randn-khởi-tạo-ngẫu-nhiên-theo-phân-phối-chuẩn-normal-distributions)
    - [Randint()](#randint)
    - [.manual\_seed()](#manual_seed)
- [Structure (chuyển đổi cấu trúc của tensor)](#structure-chuyển-đổi-cấu-trúc-của-tensor)
  - [.T](#t)
  - [\[\] (slicing)](#-slicing)
  - [.view()](#view)
  - [.reshape()](#reshape)
  - [.unsqueeze()](#unsqueeze)
  - [.unique()](#unique)
  - [.tolist()](#tolist)
  - [.zero\_() (dùng để đưa tất cả phần tử của tensor về 0)](#zero_-dùng-để-đưa-tất-cả-phần-tử-của-tensor-về-0)
- [Display (Mục đích hiển thị nhằm cung cấp thêm thông tin)](#display-mục-đích-hiển-thị-nhằm-cung-cấp-thêm-thông-tin)
  - [.size()](#size)
  - [.shape](#shape)
  - [.item()](#item)
- [Math](#math)
  - [.mean()](#mean)
  - [@ (nhân ma trận)](#-nhân-ma-trận)
  - [exp()](#exp)
  - [Tanh()](#tanh)
  - [empty()](#empty)
  - [ones()](#ones)
  - [add()](#add)
  - [add\_()](#add_)
- [Training graph (Liên quan đến huấn luyện model)](#training-graph-liên-quan-đến-huấn-luyện-model)
  - [.backward() (Lan truyền ngược (backpropagation) - tính đạo hàm của loss theo từng trọng số mô hình)](#backward-lan-truyền-ngược-backpropagation---tính-đạo-hàm-của-loss-theo-từng-trọng-số-mô-hình)
    - [.grad](#grad)
  - [.squeeze()](#squeeze)
  - [.argmax()](#argmax)
  - [.item()](#item-1)
  - [.parameters()](#parameters)
  - [.detach()](#detach)
  - [Stack()](#stack)
  - [Cat()](#cat)
  - [no\_grad()](#no_grad)
  - [softmax (chuyển tensor thành thành xác suất)](#softmax-chuyển-tensor-thành-thành-xác-suất)
  - [argmax](#argmax-1)
- [Cuda](#cuda)
  - [device()](#device)
  - [is\_available()](#is_available)
  - [get\_device\_name()](#get_device_name)
  - [.to()](#to)
  - [Utils](#utils)
- [Data (Quản lý dữ liệu bằng Pytorch)](#data-quản-lý-dữ-liệu-bằng-pytorch)
  - [Dataset (lớp đại diện cho toàn bộ dữ liệu)](#dataset-lớp-đại-diện-cho-toàn-bộ-dữ-liệu)
  - [DataLoader](#dataloader)
- [optim](#optim)
  - [SGD](#sgd)
    - [zero\_grad()](#zero_grad)
---
# Create (Nhóm khởi tạo)
```bash
Các hàm để khởi tạo
```
## .tensor() (Để tạo tensor trong pytorch, giống với mảng số)
**Syn**
```bash
import torch

X = torch.tensor(X, requires_grad=True, dtype=torch.float32)

- requires_grad=True: Cho phép PyTorch theo dõi tensor để tính gradient (W = torch.randn(3, 3, requires_grad=True))
```
**Ex**
```python
import torch

li = torch.tensor([1,2,3,4])
print(li, li[0], type(li)) # tensor([1, 2, 3, 4]) tensor(1) <class 'torch.Tensor'>
```
## .clone()
```bash
Tạo bản sao độc lập của tensor
```
**Ex**
```python
import torch

a = torch.tensor([1, 2, 3], dtype=torch.float32)
b = a.clone()

b[0] = 999

print("a:", a) # a: tensor([1., 2., 3.])
print("b:", b) # b: tensor([999., 2., 3.])
```
## Arange()
**Ex**
```python
import torch

a = torch.arange(0, 10, 2)
print(a)
tensor([0, 2, 4, 6, 8])
```
## Zeros()
**Ex**
```python
self.bh = torch.zeros(3, requires_grad=True) # (hidden_dim, )
```
## Random
### .rand() (Để tạo ma trận ngẫu nhiên)
**Ex**
```python
import torch

li = torch.rand(1,10) # random 0 - 1
li1 = int(torch.rand(1).item()*10) # nhân 10 rồi ép kiểu
print(li) # tensor([[0.6769, 0.5901, 0.8615, 0.4698, 0.7670, 0.2347, 0.0153, 0.6552, 0.3026, 0.6311]])
print(li1) # 8
```
**Ex: random 5 hàng và 3 cột**
```python
x = torch.rand(5,3)
```
### randn_like()
### .randn() (Khởi tạo ngẫu nhiên theo phân phối chuẩn (Normal distribution))s
**Syn**
```bash
X = torch.randn(32, 5, 3, device=device) 

- 32: batch size tức là 32 câu.
- 5: độ dài mỗi senquence, mỗi câu gồm 5 token.
- 3: mỗi token biểu diễn thành vector 3 chiều.
```
**Ex: Tạo 1 tensor 2x3 gồm các giá trị ngẫu nhiên ~ N(0, 1)**
```python
x = torch.randn(2, 3)
print(x) # tensor([[ 0.3272, -1.1845,  0.4821], [ 1.0063, -0.3278, -0.2205]])
```
### Randint()
**Syn**
```bash
y = torch.randint(0, 8, (32,), device=device)
```
### .manual_seed()
```bash
Để cố định random của PyTorch
```
**Ex**
```bash
import torch
torch.manual_seed(42)

print(torch.randn(3))
print(torch.randint(0, 10, (3,)))
```
# Structure (chuyển đổi cấu trúc của tensor)
## .T
**Syn**
```bash
x.T
```
## [] (slicing)
**Ex: chuyển đổi cấu trúc cuar tensor**
```python
embedding_matrix = torch.randn(10, 5)  # vocab_size=100, d_model=16
batch = [[1,2],[3,4]]
print(embedding_matrix)
out = embedding_matrix[torch.tensor(batch)]
print(out)
print(out.shape)

# tensor([[-0.0291, -1.4964,  0.5289, -0.7408, -0.9910],
#             ...
#         [-0.9508, -1.2242,  0.9311,  0.1119, -2.1378]])
# tensor([[[ 1.4053,  0.3906,  0.6657,  0.5563,  0.3010],
#          [ 0.2426, -0.1891, -1.8524,  0.7597, -0.8307]],

#         [[-0.5278,  0.8487, -0.5334, -2.0883, -0.9867],
#          [-1.0494,  0.9180, -2.0481,  0.2418,  0.0732]]])
```
## .view()
```bash
Thay đổi hình dạng của tensor. Thay đổi shape mà không sao chép dữ liệu.
```
**Ex**
```python
a = torch.tensor([[1,2], [3,4]])

print(a.shape) # torch.Size([2, 2])

b = a.view(4,1)
print(b.shape, b) # torch.Size([4, 1]) tensor([[1], [2], [3], [4]])
```
**Ex2**
```python
a = torch.tensor([[1,2], [3,4]])

print(a.shape) # torch.Size([2, 2])

b = a.view(-1,1)
c = a.view(1,-1)

print(b.shape, c.shape) # torch.Size([4, 1]) torch.Size([1, 4])
```
## .reshape()
```bash
Giống với view nhưng an toàn hơn.
```
## .unsqueeze()
```bash
Dùng khi cần biến một tensor thành dạng có thêm nhiều chiều.
```
**Ex**
```python
x = torch.tensor([1, 2, 3, 4, 5, 6])  # (6,)
x = x.unsqueeze(1)   # (6, 1)
x = x.unsqueeze(2)   # (6, 1, 1)
x = x.unsqueeze(3)   # giờ mới được: (6, 1, 1, 1)
```
## .unique()
**Ex**
```python
import torch

y = torch.tensor([1,1,2,2,3,3])
print(y) # tensor([1, 1, 2, 2, 3, 3])

new_y = torch.unique(y)
print(new_y) # tensor([1, 2, 3])
```
## .tolist() 
```bash
Chuyển tensor sang danh sách Python.
```
**Ex**
```python
import torch

arr = torch.randn(2,)
print(arr.tolist()) # [2.347059488296509, 0.8164411783218384]
x = torch.tensor([[1.0, 2.0], [3.0, 4.0]])
list_x = x.tolist()
print(list_x)
```
## .zero_() (dùng để đưa tất cả phần tử của tensor về 0)
```bash
Dấu gạch dưới _ ở cuối tên hàm có nghĩa là:
    Hàm sẽ sửa trực tiếp tensor gốc, không tạo tensor mới.


Tại sao PyTorch có zero_()?
    Trong Deep Learning, gradient sẽ được cộng dồn sau mỗi lần gọi backward().
```
**Ex1: zero_() cơ bản**
```python
import torch

x = torch.tensor([1., 2., 3.])
print(x)

x.zero_()
print(x)

# Kết quả
# tensor([1., 2., 3.])
# tensor([0., 0., 0.])
```
**Ex2: Ma trận**
```python
import torch

A = torch.tensor([
    [1., 2.],
    [3., 4.]
])
print(A)

A.zero_()
print(A)

# Kết quả
# tensor([[1., 2.],
#         [3., 4.]])
# tensor([[0., 0.],
#         [0., 0.]])
```
**Ex3**
```python
import torch

x = torch.tensor(2.0, requires_grad=True)

# Lần 1
y = x**2
y.backward()
print(x.grad) # tensor(4.)

x.grad.zero_() # Xóa gradient
print(x.grad) # tensor(0.)

y = x**2 # Tính lại
y.backward()
print(x.grad) # tensor(4.)
```
# Display (Mục đích hiển thị nhằm cung cấp thêm thông tin)
## .size()
**Ex**
```python
h_t = torch.zeros(1, 3)
Whh = torch.tensor([0.1, 0.2, 0.3], requires_grad=True)

print(h_t.size(), Whh.size()) # torch.Size([1, 3]) torch.Size([3])
```
## .shape
**Ex**
```python
import torch

a = torch.tensor([1,2,3,4])
print(a.shape)
```
## .item()
```bash
Để hiển thị giá trị của tensor. Tensor phải có duy nhất một giá trị.
```
**Ex**
```python
a = torch.tensor([1.0, 2.0, 3.0])
W = torch.tensor([0.1, 0.2, 0.3], requires_grad=True)
b = torch.tensor(1.0, requires_grad=True)

y = W*a+b
z = torch.sum(y)

print(z.item()) # 4.4
```
# Math
## .mean()
**Ex**
```python
a = torch.tensor([1.0, 2.0, 3.0, 4.0, 5.0])

print(a.mean()) # tensor(3.)
```
## @ (nhân ma trận)
```bash
Nó tương đương với torch.matmul().
```
**Ex**
```python
import torch

A = torch.tensor([
    [1, 2],
    [3, 4]
])

B = torch.tensor([
    [5, 6],
    [7, 8]
])

C = A @ B

print(C)
# tensor([[19, 22],
#         [43, 50]])

# [1 2]     [5 6]
# [3 4]  @  [7 8]
# =
# [
# 1*5 + 2*7, 1*6 + 2*8
# 3*5 + 4*7, 3*6 + 4*8
# ]
# =
# [
# 19 22
# 43 50
# ]
```
## exp()
## Tanh()
## empty()
## ones()
## add()
## add_()
# Training graph (Liên quan đến huấn luyện model)
## .backward() (Lan truyền ngược (backpropagation) - tính đạo hàm của loss theo từng trọng số mô hình)
```bash
Cập nhật trọng số mô hình theo gradient đã tính từ backward() và thuật toán tói ưu (Adam)
```
**Syn**
```bash
tensor.backward()

- tensor thường là loss.
- Sau khi gọi backward(), gradient sẽ được lưu vào thuộc tính: parameter.grad
```
**Ex**
```python
import torch

X = torch.tensor([1.0, 2.0, 3.0])
W = torch.tensor([0.1, 0.2, 0.3], requires_grad=True)
b = torch.tensor(1.0, requires_grad=True)
Y = W*X + b

print("X = ", X)
print("W = ", W)
print("b = ", b)
print("Y = ", Y)

Z = torch.sum(Y)
print("Z = ", Z)

Z.backward()
print("W.grad = ", W.grad)
print("b.grad = ", b.grad) # dz/dW, dz/db
# giải thích:
# dz/dW = (dz/dy).(dy/dW)
#   - dy/dW = X = [1.0, 2.0, 3.0]
#   - dz/dy = [1.0, 1.0, 1.0]
# dz/db = (dz/dy).(dy/db) = 1. + 1. + 1. = 3.

# X =  tensor([1., 2., 3.])
# W =  tensor([0.1000, 0.2000, 0.3000], requires_grad=True)
# b =  tensor(1., requires_grad=True)
# Y =  tensor([1.1000, 1.4000, 1.9000], grad_fn=<AddBackward0>)
# Z =  tensor(4.4000, grad_fn=<SumBackward0>)
# W.grad =  tensor([1., 2., 3.])
# b.grad =  tensor(3.)
```
### .grad
**Ex**
```python
import torch
x = torch.tensor(2.0, requires_grad=True)
y = x**2
y.backward()  # Tính đạo hàm y theo x
print(x)
print(x.grad) # gradient được lưu trong x.grad
# tensor(2., requires_grad=True)
# tensor(4.)
```
## .squeeze()
```bash
Xóa các chiều có size = 1. Mục đích là loại bỏ chiều thừa không cần thiết. Cần gán vào một biến mới
```
**Ex**
```python
x = torch.randn(1,3,1,5)

y = x.squeeze()
z = x.squeeze(2)
t = x.squeeze(3)
print(y.shape, z.shape, t.shape) # torch.Size([3, 5]) torch.Size([1, 3, 5]) torch.Size([1, 3, 1, 5])
```
## .argmax()
```bash
Lấy chỉ số của giá trị lớn nhất. Mục đích là lấy nhãn được dự đoán lớn nhất trong xác suất đầu ra.
```
## .item()
## .parameters()
## .detach()
```bash
Cắt tensor khỏi graph tính đạo hàm
```
**Ex**
```python
import torch

x = torch.tensor(2.0, requires_grad=True)
y = x * 3
z = y.detach()  # tách z khỏi graph

out = z * 5
out.backward()  # ❌ không thể tạo gradient cho x

print(x.grad) # None
Cộng, trừ, nhân, chia 
x = torch.tensor([1.0, 2.0])
y = torch.tensor([3.0, 4.0])

print(x + y)  # tensor([4., 6.])
print(x * y)  # Nhân từng phần tử: tensor([3., 8.])
```
## Stack()
```bash
Ghép (stack) nhiều tensor cùng shape lại thành 1 tensor lớn hơn, bằng cách thêm 1 dimension mới.
```
**Ex**
```python
import torch

a = torch.tensor([1, 2, 3])
b = torch.tensor([4, 5, 6])
c = torch.tensor([7, 8, 9])

out = torch.stack([a, b, c])
print(out)
print(out.shape)
tensor([
 [1, 2, 3],
 [4, 5, 6],
 [7, 8, 9]
])
torch.Size([3, 3])
out = torch.stack([a, b, c], dim=1)
print(out)
print(out.shape) # Lần này là xếp theo chiều 1 → ma trận bị đảo trục.
tensor([
 [1, 4, 7],
 [2, 5, 8],
 [3, 6, 9]
])
torch.Size([3, 3])
```
## Cat()
## no_grad()
```bash
Trong quá trình dự đoán (inference), bạn không cần tính gradient nữa (vì không học nữa). Việc tắt gradient sẽ giúp giảm tốn bộ nhớ, tăng tốc độ, tránh sai sót do vô tình .backward() khi không cần.
```
**Syn**
```bash
with torch.no_grad():
    # các câu lệnh không cần tính gradient ở đây
```
## softmax (chuyển tensor thành thành xác suất)
**Ex1: Một mẫu dữ liệu**
```python
import torch

logits = torch.tensor([2.0, 1.0, 0.1])

probs = torch.softmax(logits, dim=0)

print(probs) # tensor([0.6590, 0.2424, 0.0986])
```
## argmax
```python
import torch

probs = torch.tensor([0.6590, 0.2424, 0.0986])
pred = torch.argmax(probs)

print(pred) # tensor(0)
```
# Cuda
## device()
## is_available()
```bash
Trả về True/False. True là máy tính có thể chạy gpu.
```
**Syn**
```bash
import torch
torch.cuda.is_available()
```
## get_device_name()
```bash
Trả về tên của gpu đang sử dụng.
```
**Ex**
```bash
print(torch.cuda.get_device_name(0))
```
## .to()
```bash
Thiết lập chế độ chạy GPU hay CPU.
```
**Ex**
```python
import torch

device = torch.device("cuda" if torch.cuda.is_available() else 'cpu')
a = torch.tensor([1,2]).to(device)

print(a.device) # cuda:
```
## Utils
# Data (Quản lý dữ liệu bằng Pytorch)
## Dataset (lớp đại diện cho toàn bộ dữ liệu)
```bash
Có thể là:
    - Tập ảnh huấn luyện (train images)
    - Dữ liệu dạng bảng (CSV)
    - Các file văn bản
    - Bất cứ loại dữ liệu nào bạn muốn đưa vào mô hình

Tại sao phải dùng Dataset:
    Nếu bạn chỉ đọc file trực tiếp bằng cv2.imread() hay pandas.read_csv(), bạn sẽ phải tự quản lý việc chia batch, shuffle, và load dần vào GPU → rất rối. PyTorch tạo ra lớp Dataset để bạn chỉ cần định nghĩa 2 hàm quan trọng: 
        - __len__() → cho biết có bao nhiêu mẫu dữ liệu 
        - __getitem__(index) → khi cần lấy mẫu thứ index, thì làm thế nào để load nó. 
    + Còn việc lặp qua batch, chia batch, shuffle… sẽ do DataLoader lo.
```
**Ex**
```python
import torch
from torch.utils.data import Dataset
import pandas as pd
from typing import List

class RealEstateDataset(Dataset):
    def __init__(self, 
        data_frame: pd.DataFrame, 
        features: List[str],
        label: List[str]) -> None:

        self.data = data_frame

        self.X = torch.tensor(
            self.data[features].to_numpy(), 
            dtype=torch.float32
        )
        self.y = torch.tensor(
            self.data[label].to_numpy(), 
            dtype=torch.float32
        )
    
    def __len__(self) -> int:
        return len(self.data)
    
    def __getitem__(self, idx) -> tuple:
        return self.X[idx], self.y[idx]
    
if __name__ == "__main__":
    data = {
        'size': [850, 900, 1200, 1500],
        'bedrooms': [2, 3, 3, 4],
        'age': [10, 15, 20, 5],
        'price': [200000, 250000, 300000, 350000]
    }

    df = pd.DataFrame(data)
    
    features = ['size', 'bedrooms', 'age']
    labels = ['price']

    dataset = RealEstateDataset(df, features, labels)
    print(f'Data length: {dataset.__len__()}')
    print(f'First sample: {dataset.__getitem__(0)}')
# Data length: 4
# First sample: (tensor([850.,   2.,  10.]), tensor([200000.]))
```
## DataLoader
**Ex**
```bash
from torch.utils.data import DataLoader

train_loader = DataLoader(
    train_dataset,
    batch_size=32,
    shuffle=True
)

test_loader = DataLoader(
    test_dataset,
    batch_size=32,
    shuffle=False
)

for X_batch, y_batch in train_loader:
    print(X_batch.shape)  # (32, 10)
    print(y_batch.shape)  # (32,)
    break
```
# optim
## SGD
### zero_grad()
**Không dùng zero_grad()**
```bash
Giả sử ta có: y = x**2
```
```python
import torch

x = torch.tensor(2.0, requires_grad=True)

# Lần 1
y = x ** 2
y.backward()

print(x.grad) # tensor(4.)

# Lần 2
y = x ** 2
y.backward()

print(x.grad) # tensor(8.)
```
**Dùng zero_grad()**
```python
import torch

x = torch.tensor(2.0, requires_grad=True)

optimizer = torch.optim.SGD([x], lr=0.1)

# Lần 1
optimizer.zero_grad()

y = x ** 2
y.backward()

print(x.grad) # tensor(4.)

# Lần thứ hai
optimizer.zero_grad()
y = x ** 2
y.backward()

print(x.grad) # tensor(4.)

# vì zero_grad() đã xóa gradient cũ trước khi tính gradient mới.
```