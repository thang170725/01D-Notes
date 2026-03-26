- [Linear Regression](#linear-regression)
  - [Thuật toán Linear Regression](#thuật-toán-linear-regression)
  - [Demo code thuần không dùng thư viện Linear Regression 1 đặc trưng](#demo-code-thuần-không-dùng-thư-viện-linear-regression-1-đặc-trưng)
  - [Xây dựng model linear 2 đặc trưng](#xây-dựng-model-linear-2-đặc-trưng)
  - [Train model linear với numpy](#train-model-linear-với-numpy)
  - [Train model Linear với pytorch](#train-model-linear-với-pytorch)
---
# Linear Regression
```bash
Đầu ra dự đoán là liên tục và có độ dốc không đổi. Nó được sử dụng để dự đoán các giá trị trong một phạm vi liên tục (doanh số, giá cả) thay vì cố gắng phân loại chúng thành các danh mục nhóm (chó, mèo).
```   
## Thuật toán Linear Regression
```bash
Bạn có dataset đã được scale sẵn (Z-score), gồm:
| x₁ | x₂ | x₃ | y  |
| -- | -- | -- | -- |
| 1  | 0  | -1 | 2  |
| 0  | 1  | 1  | 3  |
| -1 | -1 | 0  | -1 |

Yêu cầu:
1. Viết mô hình: 𝑦 = 𝑤1.𝑥1 + 𝑤2.𝑥2 + 𝑤3.𝑥3 + 𝑏 
2. Dùng dạng ma trận: 𝑦 = w𝑋 + 𝑏
3. Tìm: 𝑤1,𝑤2,𝑤3, w1
```
```bash
---- Loop 1 ------
Step 1: Tính y
    - Tự chọn w1 = 0.1, w2 = 0.2, w3 = 0.15, b = 0
    - y1 = 𝑤1.𝑥1 + 𝑤2.𝑥2 + 𝑤3.𝑥3 + 𝑏 = 0.1x1 + 0.2x0 + 0.15x2 = 0.4
    - y2 = 0.5
    - y3 = 0.2
    - ... (nếu data co nhiều dòng)
Step 2: Tính loss (MSE)
    MSE = (1/n) [(y1_true - y2_pred)**2 + ...] = 3.4
Step 3: BackProp (đạo hàm)
    dL/dw = -(2/n).(Y_true - (W.X + b)).X = [1.2, 3.0, 2]
    dL/db = -(2/n).(Y_true - (W.X + b)) = 1
Step 3: Update (cập nhật trọng số)
    - Tự chọn learning rate = 0.002
    W = W - (dL/dw).lr = [1, 2.8, 1]
    b = b - (dL/db).lr = 1

---- Loop 2 -----
...
```
## Demo code thuần không dùng thư viện Linear Regression 1 đặc trưng
```python
def predict(X, W, b):
    return W * X + b

def mse(X, y, W, b):
    n = len(X)
    total = 0
    for i in range(n):
        y_pred = predict(X[i], W, b)
        total += (y_pred - y[i])**2
    return total / n

def train(X, y, W, b, epochs, lr):
    n = len(X)

    for epoch in range(epochs):
        dw = 0
        db = 0

        # Gradient tính đúng
        for i in range(n):
            y_pred = predict(X[i], W, b)
            dw += (2/n) * X[i] * (y_pred - y[i])
            db += (2/n) * (y_pred - y[i])

        # Cập nhật W, b
        W = W - lr * dw
        b = b - lr * db

        if epoch % 100 == 0:
            m = mse(X, y, W, b)
            print(f"Epoch {epoch} - MSE: {m}")

    return W, b

# Dataset
X = [150, 155, 160, 165, 170, 180, 185, 190]
y = [50, 55, 60, 65, 70, 80, 85, 90]

# Khởi tạo
W = 0
b = 0

# Learning rate nên rất nhỏ
W, b = train(X, y, W, b, epochs=5000, lr=0.0000001)

print("Final W =", W)
print("Final b =", b)
print(f"Weight of human 1m76: {predict(176, W, b)}")
```
## Xây dựng model linear 2 đặc trưng
```python
X = [
    [150, 20],
    [155, 22],
    [160, 23],
    [165, 25],
    [170, 27],
    [180, 29],
    [185, 30],
    [190, 32]
]
y = [50, 55, 60, 65, 70, 80, 85, 90]
W = [0, 0]
b = 0

def predict(X, W, b):
    y_pred = 0
    for i in range(len(X)):
        y_pred += W[i]*X[i]
    return y_pred+b

def mse(X, y, W, b):
    n = len(X)
    m = 0
    for i in range(len(y)):
        y_pred = predict(X[i], W, b)
        m = (y_pred-y[i])**2
    return m/n

def train(X, y, W, b, epochs, lr):
    n = len(X)
    d = len(W)
    for epoch in range(epochs):
        dw = [0]*d
        db = 0 
        for i in range(n):
            y_pred = predict(X[i], W, b)
            for j in range(d):
                dw[j] += (2/n)*X[i][j]*(y_pred-y[i])
            db += (2/n)*(y_pred-y[i])
        
        for i in range(d):
            W[i] = W[i] - lr*dw[i]
        b = b - lr*db
        m = mse(X, y, W, b)
        if epoch%1000==0:
            print(f"epoch {epoch}, mse {m}, W {W}, b {b}") 
    return W, b

W, b = train(X, y, W, b, epochs=5000, lr=0.000001)

print("\n===== RESULT =====")
print("Final W:", W)
print("Final b:", b)
test = [176, 28]   # chiều cao 176cm, tuổi 28
print(f"Predict weight for height={test[0]}, age={test[1]} → {predict(test, W, b)} kg")
```
## Train model linear với numpy
```python
import pandas as pd
import numpy as np

# ====== Bước 1: Tạo bộ dữ liệu ======
np.random.seed(42)
thoi_gian = np.random.randint(low=5, high=30, size=30, dtype=int)
so_bai_tap = np.random.randint(low=3, high=20, size=30, dtype=int)
so_buoi_di_hoc = np.random.randint(low=2, high=8, size=30, dtype=int)

# ====== Bước 2: khởi tạo w, b đầu tiên ======
diem = 2*thoi_gian + 3*so_bai_tap + 2*so_buoi_di_hoc + np.random.normal(loc=0, scale=5, size=30)

df = pd.DataFrame({
    "thoi_gian": thoi_gian,
    "so_bai_tap": so_bai_tap,
    "so_buoi_di_hoc": so_buoi_di_hoc,
    "diem": diem
})

# ====== Bước 3: Thuật toán Linear =======
def activate_function(X, w, b):
    return np.dot(X, w) + b # x1*w1 + x2*w2 + x3*w3 + … + b

def cost_function(X, y, w, b):
    m = len(y)
    mse = 0
    for i in range(m):
        y_pred = sum([X[i][j]*w[j] for j in range(len(w))]) + b
        loss = (y[i] - y_pred)**2
        mse += loss
    return mse/m

def update_w_b(X, y, w, b, learning_rate):
    m = len(y)
    y_pred = np.dot(X, w) + b
    error = y - y_pred
    dw = -2/m * np.dot(X.T, error)
    db = -2/m * np.sum(error)

    w = w - dw*learning_rate
    b = b - db*learning_rate
    return w,b

def train(X, y, w, b, learning_rate, epoch):
    for i in range(epoch):
        w, b = update_w_b(X,y,w,b,learning_rate=learning_rate)
        if i%100 == 0:
            print("epoch: ", i, "cost: ", cost_function(X,y,w,b))
    return w, b

# ======= Bước 4: Đánh giá ======
X = df.drop('diem', axis=1).values
y = df['diem'].values
w1 = np.zeros(X.shape[1])
w, b = train(X, y, w1, 0.1, 0.0001, 1000)
print(activate_function([15, 10, 3], w, b))
```
## Train model Linear với pytorch
**Ex1**
```python
import pandas as pd
import torch

data = {
    'weight': [50, 60, 70, 80, 90],
    'high': [160, 170, 172, 185, 190]
}
df = pd.DataFrame(data)

X = torch.tensor(df['weight'])
y = torch.tensor(df['high'])
W = torch.tensor(0.5, requires_grad=True)
b = torch.tensor(0.0, requires_grad=True)
lr = 0.01

for epoch in range(5):
  y_pred = W*X+b
  loss = ((y_pred-y)**2).mean()

  loss.backward()
  with torch.no_grad():
    W -= lr*W.grad
    b -= lr*b.grad

  W.grad.zero_()
  b.grad.zero_()

  print(f"Epoch {epoch}, Loss: {loss.item():.4f}, W: {W.item():.4f}, b: {b.item():.4f}")
```
**Ex2**
```python
import torch.optim as optim

optimizer = optim.SGD([W, b], lr=0.01)

for epoch in range(5):
    y_pred = W*X + b
    loss = ((y_pred - y)**2).mean()
    
    optimizer.zero_grad()
    loss.backward()
    optimizer.step()  # cập nhật W, b tự động
```
**Ex3**
```python
import pandas as pd
import torch

class LinearTorchDetailCode:
    def __init__(self, data: dict, epochs=10, lr=0.01):
        df = pd.DataFrame(data)
            
        self.X = torch.tensor(df['weight'].values, dtype=torch.float32)
        self.y = torch.tensor(df['high'].values, dtype=torch.float32)

        self.W = torch.tensor(0.5, dtype=torch.float32, requires_grad=True)
        self.b = torch.tensor(0.0, dtype=torch.float32, requires_grad=True)

        self.lr = lr
        self.epochs = epochs

        self.train()   # gọi đúng

    def train(self):
        for ep in range(self.epochs):
            y_pred = self.W * self.X + self.b
            loss = ((y_pred - self.y) ** 2).mean()

            loss.backward()

            with torch.no_grad():
                self.W -= self.lr * self.W.grad
                self.b -= self.lr * self.b.grad

            self.W.grad.zero_()
            self.b.grad.zero_()

            print(f"Epoch {ep}, Loss: {loss.item():.4f}, W: {self.W.item():.4f}, b: {self.b.item():.4f}")

class LinearTorchWithOptim:
    def __init__(self, data: dict, epochs=10, lr=0.01):
        df = pd.DataFrame(data)
            
        self.X = torch.tensor(df['weight'].values, dtype=torch.float32)
        self.y = torch.tensor(df['high'].values, dtype=torch.float32)

        self.W = torch.tensor(0.5, dtype=torch.float32, requires_grad=True)
        self.b = torch.tensor(0.0, dtype=torch.float32, requires_grad=True)

        self.lr = lr
        self.epochs = epochs

        self.optimizer = torch.optim.Adam([self.W, self.b], lr=lr)

        self.train()   # gọi đúng

    def train(self):
        for ep in range(self.epochs):
            y_pred = self.W * self.X + self.b
            loss = ((y_pred - self.y) ** 2).mean()

            self.optimizer.zero_grad()
            loss.backward()
            self.optimizer.step()

            print(f"Epoch {ep}, Loss: {loss.item():.4f}, W: {self.W.item():.4f}, b: {self.b.item():.4f}")

if __name__ == "__main__":
    data = {
        'weight': [50, 60, 70, 80, 90],
        'high': [160, 170, 172, 185, 190]
    }

    model = LinearTorchDetailCode(data)
```