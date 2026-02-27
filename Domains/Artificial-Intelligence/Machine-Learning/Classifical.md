- [Logistic Regression](#logistic-regression)
  - [Demo logistic với numpy](#demo-logistic-với-numpy)
  - [Demo Logistic với pytorch](#demo-logistic-với-pytorch)
- [Decision Tree](#decision-tree)
- [Random Forest](#random-forest)
- [XGBoost](#xgboost)
- [LightGBM](#lightgbm)
- [CatBoost](#catboost)
---
# Logistic Regression
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
# Decision Tree
```bash
- Decision Tree (ví dụ: CART) là một cây duy nhất chia dữ liệu theo rule.
- Ưu điểm
    + Rất dễ hiểu và dễ giải thích
    + Trực quan (có thể vẽ cây)
    + Chạy nhanh
Phù hợp khi:
    + Dataset nhỏ
    + Cần explainability cao (y tế, tài chính, luật)
    + Prototype nhanh
    + Nhược điểm
    + Dễ overfit
    + Độ chính xác thường thấp hơn ensemble methods
    + Nhạy với nhiễu
```
# Random Forest
```bash
Random Forest là bagging ensemble:
    + Train nhiều cây độc lập song song
    + Mỗi cây dùng bootstrap sample
    + Random subset features mỗi split
    + Kết quả = average / majority vote
    → Mục tiêu: giảm variance
Random Forest tốt cho:
    1. Dataset nhỏ – vừa
    2. Data noisy: RF trung bình hóa → ổn định hơn
    3. Muốn model ổn định, ít tuning
        RF: Chỉ cần chỉnh n_estimators. Ít nhạy hyperparameter
    4. Cần train nhanh & song song
        RF tận dụng multi-core rất tốt.
```
# XGBoost
```bash
- Ý tưởng cốt lõi là "sai -> học thêm cây mới để sửa sai"
- Có thể phân loại và dự đoán
- XGBoost mạnh vì:
    + chạy nhanh
    + Xử lý dữ liệu lớn tốt
    + Tự xử lý missing value
    + phổ biến trong production
- XGBoost tốt cho:
    1. Dataset lớn, phức tạp. Boosting bắt nonlinear pattern tốt hơn.
    2. Muốn squeeze từng % accuracy. Competition / production high-stakes.
    3. Feature engineering chưa hoàn hảo. Boosting có thể học interaction tốt hơn.
    4. Tabular data structured. Trong 80% bài toán tabular → XGBoost thường thắng RF.
```
# LightGBM
LightGBM (Light Gradient Boosting Machine) là một thư viện gradient boosting dựa trên decision tree, do Microsoft phát triển.

Nó cùng “họ” với:

XGBoost

CatBoost

⚙️ LightGBM khác XGBoost ở điểm nào?
1️⃣ Cách xây cây

XGBoost: grow theo level-wise (từng tầng một)

LightGBM: grow theo leaf-wise (chọn leaf có gain lớn nhất để tách tiếp)

👉 Leaf-wise thường:

Giảm loss nhanh hơn

Có thể chính xác hơn

Nhưng dễ overfit nếu dataset nhỏ

2️⃣ Tốc độ

LightGBM:

Dùng histogram-based algorithm

Thường train nhanh hơn XGBoost

Tốn ít memory hơn

❓ LightGBM có mạnh hơn XGBoost trong đa số trường hợp?

Câu trả lời trung thực:

👉 Không có cái nào luôn thắng.

Thực tế:

Dataset lớn (100k+ rows): LightGBM thường nhanh và có thể tốt hơn

Dataset nhỏ – vừa (vài nghìn → vài chục nghìn): XGBoost thường ổn định hơn

Nhiều categorical feature: CatBoost có thể thắng cả hai
# CatBoost
CatBoost là gì?

CatBoost là thư viện gradient boosting do Yandex phát triển, đặc biệt mạnh khi:

Có nhiều categorical feature

Không muốn encoding thủ công

Dataset không quá lớn

🎯 CatBoost khác XGBoost & LightGBM ở đâu?

Nó giải quyết 2 vấn đề lớn của boosting:

1️⃣ Xử lý categorical thông minh

Trong:

XGBoost

LightGBM

Bạn thường phải:

One-hot encoding

Target encoding

Hoặc label encoding

CatBoost:

Encode nội bộ bằng kỹ thuật ordered target encoding

Giảm leakage

Ít overfit hơn

👉 Nếu dataset bạn có nhiều cột dạng category → CatBoost rất đáng thử.

2️⃣ Ít overfit hơn trong dataset nhỏ – vừa

Với 10k sample:

LightGBM (leaf-wise) có thể hơi aggressive

XGBoost ổn định

CatBoost thường khá “smooth”

📊 So sánh nhanh cho dataset 10k tabular
	XGBoost	LightGBM	CatBoost
Ổn định	✅	⚠️	✅
Tốc độ	Trung bình	Nhanh	Trung bình
Categorical	Cần encode	Cần encode	⭐ Tốt nhất
Dễ tuning	Trung bình	Khó hơn	Dễ
Overfit	Trung bình	Dễ hơn	Thấp