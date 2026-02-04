- [Directory structure](#directory-structure)
- [Introduction](#introduction)
- [Installation](#installation)
- [dz/dW = (dz/dy).(dy/dW)](#dzdw--dzdydydw)
- [dy/dW = a = \[1.0, 2.0, 3.0\]](#dydw--a--10-20-30)
- [dz/db = (dz/dy).(dy/db) = 1. + 1. + 1. = 3.](#dzdb--dzdydydb--1--1--1--3)
- [Tạo 1 tensor 2x3 gồm các giá trị ngẫu nhiên ~ N(0, 1)](#tạo-1-tensor-2x3-gồm-các-giá-trị-ngẫu-nhiên--n0-1)
- [tensor đầu ra của mô hình](#tensor-đầu-ra-của-mô-hình)
---
# Directory structure
```bash
PyTorch/
    ├── 01_Tensors.md         # Khởi tạo, Thao tác mảng, tính toán GPU
    ├── 02_Autograd.md        # Đạo hàm tự động (Backpropagation)
    ├── 03_NN_Modules.md      # Xây dựng Layer, Model (nn.Module)
    ├── 04_Data_Pipeline.md   # DataLoader, Dataset (Xử lý dữ liệu)
    └── 05_Optimization.md    # Loss functions, Optimizers (SGD, Adam)Torch
```
# Introduction
```bash
- PyTorch là một thư viện của python nhưng nhiều người gọi nó là framework vì đầy đủ sức mạnh của một framework (end-to-end)
- PyTorch dùng để xây dựng và huấn luyện mô hình học sâu (deep learning).
```
# Installation
```bash
pip install torch
```
Tensor()
Để tạo tensor trong pytorch, giống với mảng số.
Cú pháp:
X = torch.tensor(X, requires_grad=True, dtype=torch.float32)
    • requires_grad=True: Cho phép PyTorch theo dõi tensor để tính gradient (W = torch.randn(3, 3, requires_grad=True))
import torch

li = torch.tensor([1,2,3,4])
print(li, li[0], type(li)) # tensor([1, 2, 3, 4]) tensor(1) <class 'torch.Tensor'>
[]
    embedding_matrix = torch.randn(10, 5)  # vocab_size=100, d_model=16
    batch = [[1,2],[3,4]]
    print(embedding_matrix)
    out = embedding_matrix[torch.tensor(batch)]
    print(out)
    print(out.shape)
tensor([[-0.0291, -1.4964,  0.5289, -0.7408, -0.9910],
        [ 1.4053,  0.3906,  0.6657,  0.5563,  0.3010],
        [ 0.2426, -0.1891, -1.8524,  0.7597, -0.8307],
        [-0.5278,  0.8487, -0.5334, -2.0883, -0.9867],
        [-1.0494,  0.9180, -2.0481,  0.2418,  0.0732],
        [-0.0869,  0.5328,  0.4544, -1.5288, -0.9604],
        [ 0.8380, -2.1501,  0.6361,  0.0210, -0.5974],
        [-0.1633, -0.1661,  1.0151, -0.9994, -1.8404],
        [ 0.0644, -1.3434, -1.8502, -0.8763,  0.0859],
        [-0.9508, -1.2242,  0.9311,  0.1119, -2.1378]])
tensor([[[ 1.4053,  0.3906,  0.6657,  0.5563,  0.3010],
         [ 0.2426, -0.1891, -1.8524,  0.7597, -0.8307]],

        [[-0.5278,  0.8487, -0.5334, -2.0883, -0.9867],
         [-1.0494,  0.9180, -2.0481,  0.2418,  0.0732]]])
torch.Size([2, 2, 5])
import torch

a = torch.arange(0, 40).reshape(10, 4)
print(a)
print(a[:, 0::2])
tensor([[ 0,  1,  2,  3],
        [ 4,  5,  6,  7],
        [ 8,  9, 10, 11],
        [12, 13, 14, 15],
        [16, 17, 18, 19],
        [20, 21, 22, 23],
        [24, 25, 26, 27],
        [28, 29, 30, 31],
        [32, 33, 34, 35],
        [36, 37, 38, 39]])
tensor([[ 0,  2],
        [ 4,  6],
        [ 8, 10],
        [12, 14],
        [16, 18],
        [20, 22],
        [24, 26],
        [28, 30],
        [32, 34],
        [36, 38]])

.item()
Để hiển thị giá trị của tensor. Tensor phải có duy nhất một giá trị.
Cú pháp:
a = torch.tensor([1.0, 2.0, 3.0])
W = torch.tensor([0.1, 0.2, 0.3], requires_grad=True)
b = torch.tensor(1.0, requires_grad=True)
y = W*a+b
z = torch.sum(y)
print(z.item()) # 4.4
empty()
ones()
.shape
import torch

device = torch.device("cuda" if torch.cuda.is_available() else 'cpu')
a = torch.tensor([1,2,3,4]).to(device)
print(a.shape)
torch.Size([4])
.size()
h_t = torch.zeros(1, 3)
Whh = torch.tensor([0.1, 0.2, 0.3], requires_grad=True)
print(h_t.size(), Whh.size()) # torch.Size([1, 3]) torch.Size([3])

add()
add_()
.mean()
Cú pháp:
a = torch.tensor([1.0, 2.0, 3.0, 4.0, 5.0], dtype=)
print(a.mean()) # tensor(3.)
.view()
Thay đổi hình dạng của tensor. Thay đổi shape mà không sao chép dữ liệu.
Cú pháp:
device = torch.device("cuda" if torch.cuda.is_available() else 'cpu')
a = torch.tensor([[1,2], [3,4]]).to(device)
print(a.shape)
b = a.view(4,1)
print(b.shape, b)
torch.Size([2, 2]) torch.Size([4, 1]) tensor([[1], [2], [3], [4]], device='cuda:0')
device = torch.device("cuda" if torch.cuda.is_available() else 'cpu')
a = torch.tensor([[1,2], [3,4]]).to(device)
print(a.shape)
b = a.view(-1,1)
c = a.view(1,-1)
print(b.shape, c.shape)
torch.Size([2, 2]) torch.Size([4, 1]) torch.Size([1, 4])

.backward() & .grad
    • Lan truyền ngược (backpropagation) - tính đạo hàm của loss theo từng trọng số mô hình.
    • Cập nhật trọng số mô hình theo gradient đã tính từ backward() và thuật toán tói ưu (Adam)
Cú pháp:
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
.zero_()
Xóa gradient cũ trước vòng tiếp theo.

.reshape()
Giống với view nhưng an toàn hơn.
.squeeze()
Xóa các chiều có size = 1. Mục đích là loại bỏ chiều thừa không cần thiết. Cần gán vào một biến mới
Cú pháp:
x = torch.randn(1,3,1,5)

y = x.squeeze()
z = x.squeeze(2)
t = x.squeeze(3)
print(y.shape, z.shape, t.shape) # torch.Size([3, 5]) torch.Size([1, 3, 5]) torch.Size([1, 3, 1, 5])
.unsqueeze()
Dùng khi cần biến một tensor thành dạng có thêm nhiều chiều.
Cú pháp:
x = torch.tensor([1, 2, 3, 4, 5, 6])  # (6,)
x = x.unsqueeze(1)   # (6, 1)
x = x.unsqueeze(2)   # (6, 1, 1)
x = x.unsqueeze(3)   # giờ mới được: (6, 1, 1, 1)

argmax()
Lấy chỉ số của giá trị lớn nhất. Mục đích là lấy nhãn được dự đoán lớn nhất trong xác suất đầu ra.
item()
parameters()
.tolist() 
Chuyển tensor sang danh sách Python.
Cú pháp:
import torch

arr = torch.randn(2,)
print(arr.tolist()) # [2.347059488296509, 0.8164411783218384]
x = torch.tensor([[1.0, 2.0], [3.0, 4.0]])
list_x = x.tolist()
print(list_x)
.clone()
Tạo bản sao độc lập của tensor
Cú pháp:
import torch

a = torch.tensor([1, 2, 3], dtype=torch.float32)
b = a.clone()

b[0] = 999

print("a:", a)
print("b:", b)
a: tensor([1., 2., 3.])
b: tensor([999., 2., 3.])
.detach()
Cắt tensor khỏi graph tính đạo hàm
Cú pháp:
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

Arange()
import torch

a = torch.arange(0, 10, 2)
print(a)
tensor([0, 2, 4, 6, 8])

Zeros()
self.bh = torch.zeros(3, requires_grad=True) # (hidden_dim, )

exp()
Tanh()
Stack()
Ghép (stack) nhiều tensor cùng shape lại thành 1 tensor lớn hơn, bằng cách thêm 1 dimension mới.
Cú pháp:
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
Cat()
Random
rand()
Để tạo ma trận ngẫu nhiên.
import torch

li = torch.rand(1,10) # random 0 - 1
li1 = int(torch.rand(1).item()*10) # nhân 10 rồi ép kiểu
print(li)
print(li1)
tensor([[0.6769, 0.5901, 0.8615, 0.4698, 0.7670, 0.2347, 0.0153, 0.6552, 0.3026, 0.6311]])
8
x = torch.rand(5,3) # 5 hàng và 3 cột

randn_like()
Randn()
Khởi tạo ngẫu nhiên theo phân phối chuẩn (Normal distribution).
Cú pháp:
X = torch.randn(32, 5, 3, device=device) 
    • 32: batch size tức là 32 câu.
    • 5: độ dài mỗi senquence, mỗi câu gồm 5 token.
    • 3: mỗi token biểu diễn thành vector 3 chiều.
# Tạo 1 tensor 2x3 gồm các giá trị ngẫu nhiên ~ N(0, 1)
x = torch.randn(2, 3)
print(x)
tensor([[ 0.3272, -1.1845,  0.4821],
        [ 1.0063, -0.3278, -0.2205]])
Randint()
y = torch.randint(0, 8, (32,), device=device)
manual_seed()
Để cố định random của PyTorch
Cú pháp:
import torch

torch.manual_seed(42)

print(torch.randn(3))
print(torch.randint(0, 10, (3,)))
no_grad()
Trong quá trình dự đoán (inference), bạn không cần tính gradient nữa (vì không học nữa). Việc tắt gradient sẽ giúp giảm tốn bộ nhớ, tăng tốc độ, tránh sai sót do vô tình .backward() khi không cần.
Cú pháp: 
with torch.no_grad():
    # các câu lệnh không cần tính gradient ở đây
Cuda
device()
is_available()
Trả về True/False. True là máy tính có thể chạy gpu.
Cú pháp:
torch.cuda.is_available()
get_device_name()
Trả về tên của gpu đang sử dụng.
Cú pháp:
print(torch.cuda.get_device_name(0))
.to()
Thiết lập chế độ chạy GPU hay CPU.
Cú pháp:
import torch

device = torch.device("cuda" if torch.cuda.is_available() else 'cpu')
a = torch.tensor([1,2]).to(device)
print(a.device) # cuda:0
Utils
Data
Dataset
Là lớp đại diện cho toàn bộ dữ liệu. Tập ảnh huấn luyện (train images), Dữ liệu dạng bảng (CSV), Các file văn bản, Bất cứ loại dữ liệu nào bạn muốn đưa vào mô hình
Tại sao phải dùng Dataset:
Nếu bạn chỉ đọc file trực tiếp bằng cv2.imread() hay pandas.read_csv(), bạn sẽ phải tự quản lý việc chia batch, shuffle, và load dần vào GPU → rất rối. PyTorch tạo ra lớp Dataset để bạn chỉ cần định nghĩa 2 hàm quan trọng: 
    • __len__() → cho biết có bao nhiêu mẫu dữ liệu 
    • __getitem__(index) → khi cần lấy mẫu thứ index, thì làm thế nào để load nó. 
Còn việc lặp qua batch, chia batch, shuffle… sẽ do DataLoader lo.
Cú pháp:
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