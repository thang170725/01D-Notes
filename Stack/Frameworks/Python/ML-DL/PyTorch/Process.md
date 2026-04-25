- [Create (Nhóm khởi tạo)](#create-nhóm-khởi-tạo)
  - [.tensor()](#tensor)
  - [.clone()](#clone)
  - [Arange()](#arange)
  - [Zeros()](#zeros)
  - [Random](#random)
    - [.rand()](#rand)
    - [randn\_like()](#randn_like)
    - [.randn()](#randn)
    - [Randint()](#randint)
    - [.manual\_seed()](#manual_seed)
- [Structure](#structure)
  - [\[\]](#)
  - [.view()](#view)
  - [.reshape()](#reshape)
  - [.unsqueeze()](#unsqueeze)
  - [.tolist()](#tolist)
- [Display](#display)
  - [.size()](#size)
  - [.shape](#shape)
  - [.item()](#item)
- [Math](#math)
  - [.mean()](#mean)
  - [exp()](#exp)
  - [Tanh()](#tanh)
  - [empty()](#empty)
  - [ones()](#ones)
  - [add()](#add)
  - [add\_()](#add_)
- [Training](#training)
  - [.backward()](#backward)
  - [.grad](#grad)
  - [.zero\_()](#zero_)
  - [.squeeze()](#squeeze)
  - [.argmax()](#argmax)
  - [.item()](#item-1)
  - [.parameters()](#parameters)
  - [.detach()](#detach)
  - [Stack()](#stack)
  - [Cat()](#cat)
  - [no\_grad()](#no_grad)
- [Cuda](#cuda)
  - [device()](#device)
  - [is\_available()](#is_available)
  - [get\_device\_name()](#get_device_name)
  - [.to()](#to)
  - [Utils](#utils)
- [Dataset](#dataset)
- [DataLoader](#dataloader)
---
# Create (Nhóm khởi tạo)
```bash
Các hàm để khởi tạo
```
## .tensor()
```bash
Để tạo tensor trong pytorch, giống với mảng số.
```
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
### .rand()
```bash
Để tạo ma trận ngẫu nhiên.
```
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
### .randn()
```bash
Khởi tạo ngẫu nhiên theo phân phối chuẩn (Normal distribution).
```
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
# Structure
```bash
Hàm làm chuyển đổi cấu trúc của tensor
``` 
## []
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
# Display
```bash
Mục đích hiển thị nhằm cung cấp thêm thông tin
``` 
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
## exp()
## Tanh()
## empty()
## ones()
## add()
## add_()
# Training
```bash
Liên quan đến huấn luyện model
```
## .backward() 
    • Lan truyền ngược (backpropagation) - tính đạo hàm của loss theo từng trọng số mô hình.
    • Cập nhật trọng số mô hình theo gradient đã tính từ backward() và thuật toán tói ưu (Adam)
## .grad
**Ex**
```python
import torch
x = torch.tensor(2.0, requires_grad=True)
y = x**2
y.backward()  # Tính đạo hàm y theo x
print(x)
print(x.grad) # gradient được lưu trong x.grad
tensor(2., requires_grad=True)
tensor(4.)
a = torch.tensor([1.0, 2.0, 3.0])
W = torch.tensor([0.1, 0.2, 0.3], requires_grad=True)
b = torch.tensor(1.0, requires_grad=True)
y = W*a+b
z = torch.sum(y)
z.backward()
print(W.grad, b.grad) # dz/dW, dz/db
# dz/dW = (dz/dy).(dy/dW)
# dy/dW = a = [1.0, 2.0, 3.0]

# dz/db = (dz/dy).(dy/db) = 1. + 1. + 1. = 3.

tensor([1., 2., 3.]) tensor(3.)
```
## .zero_()
```bash
Xóa gradient cũ trước vòng tiếp theo.
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
Cú pháp: 
with torch.no_grad():
    # các câu lệnh không cần tính gradient ở đây
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
# Dataset
```bash
- Là lớp đại diện cho toàn bộ dữ liệu. Tập ảnh huấn luyện (train images), Dữ liệu dạng bảng (CSV), Các file văn bản, Bất cứ loại dữ liệu nào bạn muốn đưa vào mô hình
- Tại sao phải dùng Dataset:
    + Nếu bạn chỉ đọc file trực tiếp bằng cv2.imread() hay pandas.read_csv(), bạn sẽ phải tự quản lý việc chia batch, shuffle, và load dần vào GPU → rất rối. PyTorch tạo ra lớp Dataset để bạn chỉ cần định nghĩa 2 hàm quan trọng: 
    + __len__() → cho biết có bao nhiêu mẫu dữ liệu 
    + __getitem__(index) → khi cần lấy mẫu thứ index, thì làm thế nào để load nó. 
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
Data length: 4
First sample: (tensor([850.,   2.,  10.]), tensor([200000.]))
```
# DataLoader
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