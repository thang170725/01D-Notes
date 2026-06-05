- [Demo code thuần không dùng thư viện Linear Regression 1 đặc trưng](#demo-code-thuần-không-dùng-thư-viện-linear-regression-1-đặc-trưng)
  - [Xây dựng model linear 2 đặc trưng](#xây-dựng-model-linear-2-đặc-trưng)
- [Xây dựng model linear với numpy](#xây-dựng-model-linear-với-numpy)
  - [Train model Linear với pytorch](#train-model-linear-với-pytorch)
---
# Demo code thuần không dùng thư viện Linear Regression 1 đặc trưng
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
# Xây dựng model linear với numpy
```bash
Dự đoán điểm dựa vào thời gian học, số bài tập đã làm, số buổi đi học.
```
**Batch Gradient Decent (sử dụng tất cả dữ liệu trong dataset rồi mới cập nhật trọng số**
```python
import pandas as pd
import numpy as np
from typing import Tuple

np.random.seed(42)

class LinearRegression:
    def __init__(self, dataset: pd.DataFrame, target: str = "points", lr=0.001, epochs=1000) -> None:
        self.X = dataset.drop(target, axis=1).to_numpy() # (30, 3)
        self.y = dataset[target].to_numpy() # (30, )
        self.n = len(self.y)
        
        self.W = np.random.rand(self.X.shape[1])
        self.b = 0

        self.lr = lr
        self.epochs = epochs

    # hàm kích hoạt
    def activate_function(self) -> np.ndarray: # (30, )
        return np.dot(self.X, self.W) + self.b

    # tính sai số
    def cost_function(self) -> float:
        y_pred = self.activate_function()
        return np.mean(np.power(self.y - y_pred, 2))

    def backprop(self) -> None:
        y_pred = self.activate_function()
        error = self.y -y_pred
        
        dw = -2/self.n * np.dot(self.X.T, error)
        db = -2/self.n * np.sum(error)

        self.W = self.W - dw*self.lr
        self.b = self.b - db*self.lr

    def train(self) -> None:
        for i in range(self.epochs):
            self.backprop()
        
            if i%100 == 0:
                print("epoch: ", i, "cost: ", self.cost_function())

    def predict(self, new_X: np.ndarray) -> float:
        return np.dot(new_X, self.W) + self.b

if __name__ == "__main__":
    # ====== Bước 1: Tạo bộ dữ liệu ======
    times = np.random.randint(low=5, high=30, size=30, dtype=int)
    number_exercises = np.random.randint(low=3, high=20, size=30, dtype=int)
    number_schools = np.random.randint(low=2, high=8, size=30, dtype=int)
    points = 2*times + 3*number_exercises + 2*number_schools + np.random.normal(loc=0, scale=5, size=30)

    df = pd.DataFrame({
        "times": times,
        "number_exercises": number_exercises,
        "number_schools": number_schools,
        "points": points
    })
    
    # ===== Bước 2: Train model ========
    linear_regression = LinearRegression(dataset=df, target="points", lr=0.0001, epochs=1000)
    linear_regression.train()
```
**Mini Batch Size**
```python
import pandas as pd
import numpy as np
from typing import Tuple

np.random.seed(42)

class LinearRegression:
    def __init__(self, dataset: pd.DataFrame, target: str = "points", lr=0.001, epochs=1000) -> None:
        self.X = dataset.drop(target, axis=1).to_numpy() # (30, 3)
        self.y = dataset[target].to_numpy() # (30, )
        self.n = len(self.y)
        
        self.W = np.random.rand(self.X.shape[1])
        self.b = 0

        self.lr = lr
        self.epochs = epochs

    # hàm kích hoạt
    def activate_function(self) -> np.ndarray: # (30, )
        return np.dot(self.X, self.W) + self.b

    # tính sai số
    def cost_function(self) -> float:
        y_pred = self.activate_function()
        return np.mean(np.power(self.y - y_pred, 2))

    def backprop(self, X_batch, y_batch) -> None:
        m = len(y_batch)
        y_pred = np.dot(X_batch, self.W) + self.b
        error = y_batch - y_pred

        dw = -2/m * np.dot(X_batch.T, error)
        db = -2/m * np.sum(error)

        self.W = self.W - dw*self.lr
        self.b = self.b - db*self.lr

    def train(self, batch_size=10) -> None:
        for epoch in range(self.epochs):

            # 🔀 shuffle dữ liệu mỗi epoch (rất quan trọng)
            indices = np.random.permutation(self.n)
            X_shuffled = self.X[indices]
            y_shuffled = self.y[indices]

            # chia batch
            for i in range(0, self.n, batch_size):
                X_batch = X_shuffled[i:i+batch_size]
                y_batch = y_shuffled[i:i+batch_size]

                self.backprop(X_batch, y_batch)

            if epoch % 100 == 0:
                print("epoch:", epoch, "cost:", self.cost_function())

    def predict(self, new_X: np.ndarray) -> float:
        return np.dot(new_X, self.W) + self.b

if __name__ == "__main__":
    # ====== Bước 1: Tạo bộ dữ liệu ======
    times = np.random.randint(low=5, high=30, size=30, dtype=int)
    number_exercises = np.random.randint(low=3, high=20, size=30, dtype=int)
    number_schools = np.random.randint(low=2, high=8, size=30, dtype=int)
    points = 2*times + 3*number_exercises + 2*number_schools + np.random.normal(loc=0, scale=5, size=30)

    df = pd.DataFrame({
        "times": times,
        "number_exercises": number_exercises,
        "number_schools": number_schools,
        "points": points
    })
    
    # ===== Bước 2: Train model ========
    linear_regression = LinearRegression(dataset=df, target="points", lr=0.0001, epochs=1000)
    linear_regression.train(batch_size=10)
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