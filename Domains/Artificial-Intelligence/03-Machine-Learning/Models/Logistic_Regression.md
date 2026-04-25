- [Logistic Regression](#logistic-regression)
  - [Demo Pipeline Logistic](#demo-pipeline-logistic)
  - [Demo logistic với numpy](#demo-logistic-với-numpy)
  - [Demo Logistic với pytorch](#demo-logistic-với-pytorch)
---
# Logistic Regression
## Demo Pipeline Logistic
```bash
Bài toán: Dự đoán đậu/rớt phỏng vấn
Một công ty muốn dự đoán xem ứng viên có đậu phỏng vấn (1) hay rớt (0) dựa trên 3 đặc trưng:
    - 𝑥1: Số năm kinh nghiệm
    - 𝑥2: Điểm test kỹ thuật (0–10)
    - 𝑥3: Số dự án đã làm

Dataset mẫu
Ứng viên    𝑥1(exp)    𝑥2(score)    𝑥3(projects)    y(kết quả)
1	        1	        5	        2	            0
2	        2	        6	        3	            0
3	        3	        7	        4	            1
4	        4	        8	        5	            1
5	        5	        6	        6	            1
6	        1	        4	        1	            0

Yêu cầu bài toán: Huấn luyện mô hình logistic regression với dataset trên
Tìm các trọng số: 𝑤0, 𝑤1, 𝑤2, 𝑤3
```
```bash
Bước 1: Khởi tạo trọng số:
    - w1 = 0.1, w2 = 0.1, w3 = 0.1, b=0
Bước 2: Forward (tính dự đoán)
    - Ứng viện 1: (1, 5, 2), y = 0
        + z1 = w1.x1 + w2.x2 + w3.x3 + b = 0.1(1) + 0.1(5) + 0.1(2) = 0.8
        + y_pred = σ(z1​) = 1/(1+e^-z1) = 1/(1+e^-0.8) ≈ 0.69
    - Ứng viên 2: (2, 6, 3), y = 0    
        + z2 = 1.1 ⇒ y_pred ≈ 0.75
    - Ứng viên 3: (3, 7, 4), y = 1
        + z3 = 1.4 ⇒ y_pred ≈ 0.80
    - ...
Bước 3: Tính Loss (BCE – giả định)
    - L1 = −(ylog(y_pred))+(1−y)log(1−y_pred)) = −(0⋅log(0.69)+(1−0)log(1−0.69))=−log(0.31) ⇒ L1≈1.17
    - ...
    => Loss = 1/6 . (L1 + L2 + ... + L6) = 0.69
    - Nhận xét: Model đang đoán quá cao cho các mẫu rớt (0) → sai khá nhiều
Bước 4: Backprop (đạo hàm – giả định)
    - Tính cho Ứng viên 1:
        + ∂L1/∂z1 = y_pred1 - y1 = 0.69−0 = 0.69
        + Gradient theo từng trọng số:
            - ∂L/∂w1 = (y_pred1 - y)⋅x1
            - ∂L/∂w2 = (y_pred1 − y)⋅x2
	​        - ∂L/∂w3 = (y_pred1 − y)⋅x3
	​        - ∂L/∂b = (y_pred1 − y)
        + Thay số cho Ứng viên 1:
            - dL/dw1 = 0.69⋅1 = 0.69
            - dL/dw2 = 0.69⋅5 = 3.45
            - dL/dw3 = 0.69⋅2 = 1.38
            - dL/db=0.69
    => Tổng gradient (trung bình toàn bộ dataset – giả định)
        + dL/dw1≈0.9
        + dL/dw2≈1.5
        + dL/dw3≈1.0
        + dL/db≈0.8
Bước 5: Update (Learning rate = 0.05)
    - w1 = 0.1 − 0.05(0.9)=0.055
    - w2 = 0.1 − 0.05(1.5)=0.025
    - w3 = 0.1 − 0.05(1.0)=0.05
    - b = 0−0.05(0.8)=−0.04
Bước 6: Quay lại bước 1
```
## Demo logistic với numpy
```python
import numpy as np

class LogisticRegression:
    def __init__(self):
        self.W, self.b = 0, 0
    
    def sigmoid(self, z):
        return 1/(1+np.exp(-z))
    
    def linear(self, X, W, b):
        return W*X+b
    
    def bce(self, y_true, y_pred):
        return y_true*np.log(y_pred)+(1-y_true)*np.log(1-y_pred)
    
    def accuracy(self, y_true, y_pred):
        y_true = np.asarray(y_true)
        y_pred = np.asarray(y_pred)
        return np.mean(y_true == y_pred)


    def train(self, X, y, epochs, lr=0.00001):
        for ep in range(epochs):
            dw, db = 0, 0
            y_pred = 0
            for i in range(len(X)):
                z = self.linear(X[i], self.W, self.b)
                y_pred = self.sigmoid(z)

                dw += (y_pred - y[i])*X[i]
                db += (y_pred - y[i])
            self.W -= lr*dw
            self.b -= lr*db
            if ep%1000 == 0:
                y_hat = self.predict(X)
                a = self.accuracy(y, y_hat)
                print(f"epoch {ep}, acc {a}")
    
    def predict(self, X):
        y_pred = self.sigmoid(self.W * X + self.b)
        return (y_pred >= 0.5).astype(int)
    
if __name__ == "__main__":
    dataset = np.array([
        [-10, 0],
        [-5, 0],
        [-7, 0],
        [0, 0],
        [-2, 0],
        [5, 1],
        [7, 1],
        [6, 1],
        [10, 1],
        [15, 1],
        [9, 1]
    ])

    X = dataset[:, 0]
    y = dataset[:, 1]

    model = LogisticRegression()
    model.train(X, y, 5000)

    print("W:", model.W)
    print("b:", model.b)
    print("pred:", model.predict(X))
```
## Demo Logistic với pytorch
```python
import torch
import torch.nn as nn
import pandas as pd

class LogisticTorch:
    def __init__(self):
        self.w = torch.randn(1, requires_grad=True)
        self.b = torch.zeros(1, requires_grad=True)
        self.loss_fn = nn.BCELoss()
        self.sigmoid = nn.Sigmoid()
    
    def forward(self, X, y, lr=0.01, epochs=5):
        X = torch.tensor(X, dtype=torch.float32)
        y = torch.tensor(y, dtype=torch.float32)

        for epoch in range(epochs):
            logits = self.w*X + self.b # linear
            y_pred = self.sigmoid(logits) # sigmoid

            loss = self.loss_fn(y_pred, y)
            loss.backward()

            with torch.no_grad():
                self.w -= lr*self.w.grad
                self.b -= lr*self.b.grad
        
            self.w.grad.zero_()
            self.b.grad.zero_()

            print(f'epoch {epoch+1}: Loss: {loss.item()}, Weight: {self.w.item()}, bias: {self.b.item()}')

class LogisticRegression:
    def __init__(self, n_features, n_classes):
        # Khởi tạo trọng số thủ công
        self.W = torch.randn(n_features, n_classes, requires_grad=True)
        self.b = torch.zeros(n_classes, requires_grad=True)

    def forward(self, X):
        logits = X @ self.W + self.b
        return logits

    def train(self, X, y, lr=0.1, epochs=100):
        criterion = nn.CrossEntropyLoss()

        for epoch in range(epochs):
            logits = self.forward(X)

            loss = criterion(logits, y)

            # Backprop
            loss.backward()

            # Update W, b
            with torch.no_grad():
                self.W -= lr * self.W.grad
                self.b -= lr * self.b.grad

            # Reset gradient
            self.W.grad.zero_()
            self.b.grad.zero_()

            if (epoch + 1) % 10 == 0:
                print(f"Epoch {epoch+1}, Loss = {loss.item():.4f}")

    def predict(self, X):
        logits = self.forward(X)
        probs = torch.softmax(logits, dim=1)
        preds = torch.argmax(probs, dim=1)
        return preds


# ======================
#       DATASET
# ======================

# X: 2 đặc trưng
X = torch.tensor([
    [1.0, 2.0],
    [1.5, 1.8],
    [5.0, 8.0],
    [6.0, 9.0],
    [1.0, 0.5],
    [2.0, 1.0]
], dtype=torch.float32)

# y: 3 lớp (0, 1, 2)
y = torch.tensor([0, 0, 1, 1, 2, 2], dtype=torch.long)

# ======================
#       TRAIN MODEL
# ======================

model = LogisticRegression(n_features=2, n_classes=3)
model.train(X, y, lr=0.05, epochs=100)

# ======================
#       TEST
# ======================
test_sample = torch.tensor([[1.2, 1.8]], dtype=torch.float32)
pred = model.predict(test_sample)

print("Prediction:", pred.item())

if __name__ == '__main__':
    data = {
        'input': [1,2,3,4,5,6],
        'output': [1,1,1,0,0,0]
    }
    df = pd.DataFrame(data)
    X = df['input']
    y = df['output']
    model = LogisticTorch()
    model.forward(X, y)
```