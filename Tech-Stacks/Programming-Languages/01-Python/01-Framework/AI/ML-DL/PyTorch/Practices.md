- [Demo quản lý Data băng pytorch](#demo-quản-lý-data-băng-pytorch)
---
# Demo quản lý Data băng pytorch
```python
import numpy as np
import torch
from torch.utils.data import DataLoader, Dataset

# ---------------------------------------------------------
# BƯỚC 1: KHỞI TẠO DỮ LIỆU GIẢ LẬP (5 cột, 20 hàng)
# ---------------------------------------------------------
# Giả sử 4 cột đầu là Đặc trưng (Features - X), cột cuối là Nhãn (Label - y)
np.random.seed(42)  # Cố định dữ liệu để mỗi lần chạy đều ra kết quả giống nhau
raw_data = np.random.rand(20, 5)  # Tạo ma trận 20 dòng, 5 cột ngẫu nhiên

X_raw = raw_data[:, :4]  # Lấy 4 cột đầu (Kích thước: 20x4)
y_raw = raw_data[:, 4]  # Lấy cột cuối cùng (Kích thước: 20,)

print("=== DỮ LIỆU THÔ BAN ĐẦU ===")
print(f"Kích thước X thô: {X_raw.shape} | Kích thước y thô: {y_raw.shape}")
print(f"Dòng đầu tiên của X: {X_raw[0]}")
print(f"Nhãn của dòng đầu tiên: {y_raw[0]}")
print("-" * 60)


# ---------------------------------------------------------
# BƯỚC 2: TẠO CLASS DATASET CHUYÊN BIỆT (Custom Dataset)
# ---------------------------------------------------------
class MyCustomDataset(Dataset):

    def __init__(self, features, labels):
        # Chuyển đổi dữ liệu từ numpy array sang PyTorch Tensor (kiểu float32)
        self.features = torch.tensor(features, dtype=torch.float32)
        self.labels = torch.tensor(labels, dtype=torch.float32)

    def __len__(self):
        # Bắt buộc: Trả về tổng số lượng mẫu trong dataset (ở đây là 20)
        return len(self.features)

    def __getitem__(self, idx):
        # Bắt buộc: Trả về 1 mẫu dữ liệu (gồm features và label tương ứng) dựa vào chỉ số idx
        return self.features[idx], self.labels[idx]


# Khởi tạo đối tượng dataset của chúng ta
my_dataset = MyCustomDataset(X_raw, y_raw)


# ---------------------------------------------------------
# BƯỚC 3: CẤU HÌNH DATALOADER
# ---------------------------------------------------------
# Cấu hình: Mỗi lần nạp dữ liệu sẽ lấy ra 5 dòng (batch_size=5)
# Shuffle=True giúp xáo trộn thứ tự các dòng sau mỗi Epoch (chu kỳ học)
custom_dataloader = DataLoader(my_dataset, batch_size=5, shuffle=True)


# ---------------------------------------------------------
# BƯỚC 4: MÔ PHỎNG QUY TRÌNH HUẤN LUYỆN (Training Loop)
# ---------------------------------------------------------
print("\n=== BẮT ĐẦU QUY TRÌNH DUYỆT DATALOADER (MÔ PHỎNG TRAINING) ===")

epochs = 2  # Chạy thử 2 chu kỳ học thử nghiệm
for epoch in range(epochs):
    print(f"\n🔄 CHI TIẾT EPOCH {epoch + 1}:")

    # DataLoader tự động gom dữ liệu thành các batch và xáo trộn chúng
    for batch_idx, (batch_X, batch_y) in enumerate(custom_dataloader):
        print(f"\n  ↳ [Batch {batch_idx + 1}]")
        print(f"    - Kích thước tensor X: {list(batch_X.shape)} (5 mẫu, mỗi mẫu 4 đặc trưng)")
        print(f"    - Kích thước tensor y: {list(batch_y.shape)} (5 nhãn)")
        print(f"    - Giá trị X trong batch này:\n{batch_X.numpy()}")

print("\n" + "=" * 60)
print("Quá trình quản lý và nạp dữ liệu hoàn tất thành công!")
```
```bash
=== DỮ LIỆU THÔ BAN ĐẦU ===
Kích thước X thô: (20, 4) | Kích thước y thô: (20,)
Dòng đầu tiên của X: [0.37454012 0.95071431 0.73199394 0.59865848]
Nhãn của dòng đầu tiên: 0.15601864044243652
------------------------------------------------------------

=== BẮT ĐẦU QUY TRÌNH DUYỆT DATALOADER (MÔ PHỎNG TRAINING) ===

🔄 CHI TIẾT EPOCH 1:

  ↳ [Batch 1]
    - Kích thước tensor X: [5, 4] (5 mẫu, mỗi mẫu 4 đặc trưng)
    - Kích thước tensor y: [5] (5 nhãn)
    - Giá trị X trong batch này:
[[0.80839735 0.30461377 0.09767211 0.684233  ]
 [0.02058449 0.96990985 0.83244264 0.21233912]
 [0.3886773  0.27134904 0.8287375  0.35675332]
 [0.54269606 0.14092423 0.802197   0.07455064]
 [0.6118529  0.13949387 0.29214466 0.36636186]]

  ↳ [Batch 2]
    - Kích thước tensor X: [5, 4] (5 mẫu, mỗi mẫu 4 đặc trưng)
    - Kích thước tensor y: [5] (5 nhãn)
    - Giá trị X trong batch này:
[[0.15599452 0.05808361 0.8661761  0.601115  ]
 [0.11959425 0.7132448  0.76078504 0.5612772 ]
 [0.32518333 0.72960615 0.63755745 0.88721275]
 [0.86310345 0.6232981  0.33089802 0.06355835]
 [0.1834045  0.30424225 0.52475643 0.43194503]]

  ↳ [Batch 3]
    - Kích thước tensor X: [5, 4] (5 mẫu, mỗi mẫu 4 đặc trưng)
    - Kích thước tensor y: [5] (5 nhãn)
    - Giá trị X trong batch này:
[[0.96958464 0.77513283 0.93949896 0.89482737]
 [0.12203824 0.4951769  0.03438852 0.9093204 ]
 [0.37454012 0.9507143  0.7319939  0.5986585 ]
 [0.77224475 0.19871569 0.00552212 0.81546146]
 [0.9218742  0.08849251 0.19598286 0.04522729]]

  ↳ [Batch 4]
    - Kích thước tensor X: [5, 4] (5 mẫu, mỗi mẫu 4 đặc trưng)
    - Kích thước tensor y: [5] (5 nhãn)
    - Giá trị X trong batch này:
[[0.7290072  0.77127033 0.07404465 0.35846573]
 [0.785176   0.19967379 0.5142344  0.59241456]
 [0.60754484 0.17052412 0.06505159 0.94888556]
 [0.66252226 0.31171107 0.52006805 0.54671025]
 [0.4937956  0.52273285 0.42754102 0.02541913]]

🔄 CHI TIẾT EPOCH 2:

  ↳ [Batch 1]
    - Kích thước tensor X: [5, 4] (5 mẫu, mỗi mẫu 4 đặc trưng)
    - Kích thước tensor y: [5] (5 nhãn)
    - Giá trị X trong batch này:
[[0.6118529  0.13949387 0.29214466 0.36636186]
 [0.96958464 0.77513283 0.93949896 0.89482737]
 [0.66252226 0.31171107 0.52006805 0.54671025]
 [0.02058449 0.96990985 0.83244264 0.21233912]
 [0.4937956  0.52273285 0.42754102 0.02541913]]

  ↳ [Batch 2]
    - Kích thước tensor X: [5, 4] (5 mẫu, mỗi mẫu 4 đặc trưng)
    - Kích thước tensor y: [5] (5 nhãn)
    - Giá trị X trong batch này:
[[0.77224475 0.19871569 0.00552212 0.81546146]
 [0.3886773  0.27134904 0.8287375  0.35675332]
 [0.15599452 0.05808361 0.8661761  0.601115  ]
 [0.9218742  0.08849251 0.19598286 0.04522729]
 [0.37454012 0.9507143  0.7319939  0.5986585 ]]

  ↳ [Batch 3]
    - Kích thước tensor X: [5, 4] (5 mẫu, mỗi mẫu 4 đặc trưng)
    - Kích thước tensor y: [5] (5 nhãn)
    - Giá trị X trong batch này:
[[0.7290072  0.77127033 0.07404465 0.35846573]
 [0.60754484 0.17052412 0.06505159 0.94888556]
 [0.80839735 0.30461377 0.09767211 0.684233  ]
 [0.86310345 0.6232981  0.33089802 0.06355835]
 [0.54269606 0.14092423 0.802197   0.07455064]]

  ↳ [Batch 4]
    - Kích thước tensor X: [5, 4] (5 mẫu, mỗi mẫu 4 đặc trưng)
    - Kích thước tensor y: [5] (5 nhãn)
    - Giá trị X trong batch này:
[[0.785176   0.19967379 0.5142344  0.59241456]
 [0.32518333 0.72960615 0.63755745 0.88721275]
 [0.11959425 0.7132448  0.76078504 0.5612772 ]
 [0.12203824 0.4951769  0.03438852 0.9093204 ]
 [0.1834045  0.30424225 0.52475643 0.43194503]]

============================================================
Quá trình quản lý và nạp dữ liệu hoàn tất thành công!
```
Dưới đây là ví dụ đơn giản nhất để xây dựng một mô hình Linear Regression bằng nn.Linear trong PyTorch.

1. Import thư viện
import torch
import torch.nn as nn
import torch.optim as optim
2. Tạo dữ liệu

Giả sử ta có công thức

y=2x+1
# x có dạng (batch_size, input_features)
X = torch.tensor([
    [1.0],
    [2.0],
    [3.0],
    [4.0],
    [5.0]
])

Y = torch.tensor([
    [3.0],
    [5.0],
    [7.0],
    [9.0],
    [11.0]
])

Lưu ý:

X.shape = (5, 1)

5 mẫu dữ liệu
1 đặc trưng (feature)
3. Xây dựng model
class LinearRegression(nn.Module):

    def __init__(self):
        super().__init__()

        self.linear = nn.Linear(
            in_features=1,
            out_features=1
        )

    def forward(self, x):
        return self.linear(x)

Khởi tạo model

model = LinearRegression()
4. Xem trọng số ban đầu
print(model.linear.weight)
print(model.linear.bias)

Ví dụ

Parameter containing:
tensor([[0.3145]], requires_grad=True)

Parameter containing:
tensor([0.1052], requires_grad=True)

Ban đầu PyTorch sinh ngẫu nhiên.

5. Hàm mất mát và Optimizer
criterion = nn.MSELoss()

optimizer = optim.SGD(
    model.parameters(),
    lr=0.01
)
6. Huấn luyện
epochs = 1000

for epoch in range(epochs):

    # Forward
    prediction = model(X)

    loss = criterion(prediction, Y)

    # Xóa gradient cũ
    optimizer.zero_grad()

    # Tính gradient
    loss.backward()

    # Cập nhật weight
    optimizer.step()

    if epoch % 100 == 0:
        print(f"Epoch {epoch}, Loss = {loss.item():.4f}")
7. Kết quả

Sau khi train

print("Weight:", model.linear.weight.item())
print("Bias:", model.linear.bias.item())

Sẽ gần

Weight: 2.00
Bias: 1.00
8. Dự đoán
x = torch.tensor([[10.0]])

y = model(x)

print(y)

Kết quả

tensor([[21.0]])

vì

2 × 10 + 1 = 21
Toàn bộ chương trình
import torch
import torch.nn as nn
import torch.optim as optim

# -------------------------
# Data
# -------------------------
X = torch.tensor([
    [1.0],
    [2.0],
    [3.0],
    [4.0],
    [5.0]
])

Y = torch.tensor([
    [3.0],
    [5.0],
    [7.0],
    [9.0],
    [11.0]
])

# -------------------------
# Model
# -------------------------
class LinearRegression(nn.Module):

    def __init__(self):
        super().__init__()

        self.linear = nn.Linear(1, 1)

    def forward(self, x):
        return self.linear(x)

model = LinearRegression()

# -------------------------
# Loss & Optimizer
# -------------------------
criterion = nn.MSELoss()

optimizer = optim.SGD(
    model.parameters(),
    lr=0.01
)

# -------------------------
# Train
# -------------------------
for epoch in range(1000):

    prediction = model(X)

    loss = criterion(prediction, Y)

    optimizer.zero_grad()

    loss.backward()

    optimizer.step()

    if epoch % 100 == 0:
        print(epoch, loss.item())

# -------------------------
# Result
# -------------------------
print("\nWeight =", model.linear.weight.item())
print("Bias =", model.linear.bias.item())

# -------------------------
# Predict
# -------------------------
x = torch.tensor([[10.0]])

print(model(x))
nn.Linear thực chất làm gì?

Lệnh:

self.linear = nn.Linear(1, 1)

tự tạo hai tham số cần học:

weight (W)
bias   (b)

và trong hàm forward, khi gọi:

y = self.linear(x)

PyTorch sẽ tự động tính:

y = xW + b

Ví dụ:

W = 2
b = 1
x = 5

↓

y = 5 × 2 + 1 = 11

Đây chính là bản chất của một lớp tuyến tính (Linear layer). Trong các mạng nơ-ron nhiều tầng, nhiều lớp nn.Linear sẽ được ghép lại với các hàm kích hoạt (ReLU, Sigmoid, Tanh, ...) để học các quan hệ phức tạp hơn.