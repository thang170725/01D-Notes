- [Linear Regression](#linear-regression)
  - [Demo code thuần không dùng thư viện Linear Regression 1 đặc trưng](#demo-code-thuần-không-dùng-thư-viện-linear-regression-1-đặc-trưng)
  - [Xây dựng model linear 2 đặc trưng](#xây-dựng-model-linear-2-đặc-trưng)
  - [Train model linear với numpy](#train-model-linear-với-numpy)
  - [Train model Linear với pytorch](#train-model-linear-với-pytorch)
---
# Linear Regression
```bash
Đầu ra dự đoán là liên tục và có độ dốc không đổi. Nó được sử dụng để dự đoán các giá trị trong một phạm vi liên tục (doanh số, giá cả) thay vì cố gắng phân loại chúng thành các danh mục nhóm (chó, mèo).
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
import torch.optim as optim

optimizer = optim.SGD([W, b], lr=0.01)

for epoch in range(5):
    y_pred = W*X + b
    loss = ((y_pred - y)**2).mean()
    
    optimizer.zero_grad()
    loss.backward()
    optimizer.step()  # cập nhật W, b tự động
```