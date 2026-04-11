- [Logistic Regression](#logistic-regression)
  - [Demo Pipeline Logistic](#demo-pipeline-logistic)
- [𝑦](#𝑦)
- [)](#)
- [1](#1)
- [2](#2)
- [3](#3)
  - [Demo logistic với numpy](#demo-logistic-với-numpy)
  - [Demo Logistic với pytorch](#demo-logistic-với-pytorch)
---
# Logistic Regression
## Demo Pipeline Logistic
Bài toán: Dự đoán đậu/rớt phỏng vấn

Một công ty muốn dự đoán xem ứng viên có đậu phỏng vấn (1) hay rớt (0) dựa trên 3 đặc trưng:

𝑥
1
x
1
	​

: Số năm kinh nghiệm
𝑥
2
x
2
	​

: Điểm test kỹ thuật (0–10)
𝑥
3
x
3
	​

: Số dự án đã làm
📊 Dataset mẫu
Ứng viên	
𝑥
1
x
1
	​

 (exp)	
𝑥
2
x
2
	​

 (score)	
𝑥
3
x
3
	​

 (projects)	y (kết quả)
1	1	5	2	0
2	2	6	3	0
3	3	7	4	1
4	4	8	5	1
5	5	6	6	1
6	1	4	1	0
🧠 Mô hình logistic regression

Xác suất đậu được tính bằng:

𝑃
(
𝑦
=
1
∣
𝑥
)
=
1
1
+
𝑒
−
(
𝑤
0
+
𝑤
1
𝑥
1
+
𝑤
2
𝑥
2
+
𝑤
3
𝑥
3
)
P(y=1∣x)=
1+e
−(w
0
	​

+w
1
	​

x
1
	​

+w
2
	​

x
2
	​

+w
3
	​

x
3
	​

)
1
	​


🎯 Yêu cầu bài toán
Huấn luyện mô hình logistic regression với dataset trên
Tìm các trọng số 
𝑤
0
,
𝑤
1
,
𝑤
2
,
𝑤
3
w
0
	​

,w
1
	​

,w
2
	​

,w
3
	​

Dự đoán cho ứng viên mới:
𝑥
1
=
2
x
1
	​

=2, 
𝑥
2
=
7
x
2
	​

=7, 
𝑥
3
=
3
x
3
	​

=3
Xác định:
Xác suất đậu
Nhãn dự đoán (ngưỡng 0.5)
💡 Gợi ý
Có thể dùng:
Gradient Descent (tự code)
Hoặc sklearn.linear_model.LogisticRegression
Chuẩn hóa dữ liệu sẽ giúp học nhanh hơn

Nếu bạn muốn, mình có thể:

Giải tay từng bước (gradient descent)
Hoặc viết code PyTorch / NumPy / sklearn cho bài này 🚀 
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