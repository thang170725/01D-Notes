- [MLP Introduction (Multi-layer Perceptron)](#mlp-introduction-multi-layer-perceptron)
- [Practices](#practices)
  - [Demo cách hoạt động của MLP](#demo-cách-hoạt-động-của-mlp)
- [Practices](#practices-1)
  - [Demo MLP classificial](#demo-mlp-classificial)
---
# MLP Introduction (Multi-layer Perceptron)
```bash
MLP, còn được gọi là mạng truyền thẳng (Feedforward Network), được cấu tạo từ các lớp (layer): Lớp đầu vào, một hoặc nhiều lớp ẩn, và lớp đầu ra

Ứng dụng:
    - Phần loại hình ảnh, văn bản.
    - Dự đoán giá trị (hồi quy).
    - Dự đoán chuỗi thời gian.
```
**Cấu trúc cơ bản**
```bash
1. Input layers: Nhận dữ liệu đầu vào dạng vector.

2. Hidden layers (1 hoặc nhiều): 
    Mỗi lớp gồm nhiều nơ ron, mỗi neuron tính tổng có trọng số của đầu vào rồi áp dụng activation function như ReLU, sigmoid, tanh …

3. Output layer: Trả về kết quả cuối cừng, có thể là phần loại, hồi quy, …
```
**Cơ chế hoạt động**
```bash
1. Phép nhân Ma trận (Matrix Multiplication):
    Đây là cơ chế cốt lõi để tính toán đầu ra của một nơ-ron trong lớp tiếp theo.
    
    Đối với mỗi nơ-ron trong lớp ẩn, đầu vào của nó là tổng có trọng số của đầu ra từ tất cả các nơ-ron trong lớp trước.
    
    Công thức tổng quát cho tính toán tuyến tính (linear combination) trong một lớp là: Z=XW+B
        - X: Ma trận đầu vào từ lớp trước (hoặc lớp đầu vào).
        - W: Ma trận trọng số (Weights) của lớp hiện tại. Đây là các tham số mà mô hình học được.
        - B: Vector độ lệch (Bias) của lớp hiện tại.
        - Z: Đầu ra tuyến tính.

2. Hàm Kích Hoạt Phi Tuyến tính (Non-linear Activation Function)
    Sau khi tính toán tuyến tính (Z), kết quả này sẽ được truyền qua một hàm kích hoạt (ví dụ: Sigmoid, ReLU, Tanh).
    
    Công thức: A=f(Z)
        - A: Đầu ra đã được kích hoạt (activation), đây chính là đầu vào cho lớp tiếp theo.
        - f: Hàm kích hoạt phi tuyến tính.
```
# Practices
## Demo cách hoạt động của MLP
```bash
Cho input là [1,2,3,4,5] và mạng nơ ron 2 lớp 3x2. Demo cách hoạt động của mạng nơ ron này
```
```bash
1. Khởi tạo tham số ban đầu:
    w11 = [0.1, 0.2, 0.3, 0.4, 0.5], b11 = 0.01
    w12 = [0.11, 0.22, 0.33, 0.44, 0.55], b12 = 0.01
    w13 = [0.15, 0.25, 0.35, 0.45, 0.55], b13 = 0.01
    
    w21 = [0.1, 0.2, 0.3], b21 = 0.01
    w22 = [0.05, 0.15, 0.2], b21 = 0.01

2. Tíng giá trị z của mỗi nơ ron:
    z11 = 1x0.1 + 2x0.2 + 3x0.3 + 4x0.4 + 5.0.5 + 0.01 = 5.51
    z12 = 6
    z13 = 6.4

3. Áp dụng hàm kích hoạt ReLU cho layer 1:
    h11 = 5.51
    h12 = 6
    h13 = 6.4

4. Tính giá trị z cho mỗi nơ ron ở layer 2:
    z21 = 0.1x5.51 + 0.2x6 + 0.3x6.4 = 3.67
    z22 = 2.58

5. Áp dụng softmax cho layer 2: 
    softmax = [0.748, 0.252]

6. Tính độ mất mát (loss) bằng Categorical Cross-Entropy với nhãn thật là [1,0]:
       L = -(1.log(0.748) + 0.log(252)) = 0.126

7. Backpropagation:
       dL/dz2k = d2k = pk – yk
       …

8. Cập nhật lại trọng số và bias
       w := w -alpha*&w
       b := b – alpha*&b
```
# Practices
## Demo MLP classificial
```bash
'''
==============================
====== PHÂN LOẠI CẢM XÚC =====
==============================
'''
import torch
import torch.optim as optim, torch.nn as nn
from torch.utils.data import DataLoader, Dataset
import pandas as pd
from sklearn.feature_extraction.text import CountVectorizer
from sklearn.preprocessing import LabelEncoder
from sklearn.model_selection import train_test_split
from sklearn.metrics import accuracy_score
import tqdm

class MyDataset(Dataset):
    def __init__(self, X, y):
        super(MyDataset, self).__init__()

        self.X = X
        self.y = y
    
    def __len__(self):
        return len(self.X)
    
    def __getitem__(self, idx):
        return self.X[idx], self.y[idx]


class SentimentClassification(nn.Module):
    def __init__(self, input_size, num_classes):
        super(SentimentClassification, self).__init__()

        self.model = nn.Sequential(
            nn.Linear(input_size, 128),
            nn.ReLU(),
            nn.Linear(128,64),
            nn.ReLU(),
            nn.Linear(64, num_classes)
        )
        return self.model
    
    def forward(self, x):
        return self.model(x)

class Model:
    def __init__(self, df, lr=0.01, epochs=10):
        X, input_size, _ = self.bow(df)
        y, num_classes = self.label_encoder(df)

        X_train, X_test, y_train, y_test = self.split(X, y)

        train_dataset = MyDataset(X_train, y_train)
        test_dataset = MyDataset(X_test, y_test)
        self.train_loader = DataLoader(train_dataset, batch_size=1, shuffe=True)
        self.test_loader = DataLoader(test_dataset, batch_size=1, shuffe=True)

        self.model = SentimentClassification(input_size, num_classes)
        self.optimizer = optim.Adam(model.parameters(), lr=lr)
        self.criterion = nn.CrossEntropyLoss()

        self.epochs = epochs
        
    def bow(self, df):
        vectorizer = CountVectorizer()
        X = vectorizer.fit_transform(self.df["texts"]).toarray()

        input_size = self.X.shape[1]

        feature_name = self.X.get_feature_names_out()
        return X, input_size, feature_name
    
    def label_encoder(self, df):
        le = LabelEncoder()
        y = le.fit_transform(df["labels"]).toarray()

        num_classes = y.class_
        return y, num_classes

    def split(self, X, y, test_size=0.2):
        X_train, X_test, y_train, y_test = train_test_split(X, y, test_size)
        return X_train, X_test, y_train, y_test
    
    def train(self):
        self.model.train()
        for epoch in range(self.epochs):
            total_loss = 0
            for X_batch, y_batch in tqdm(self.train_loader, desc=f"Epoch {epoch+1}/{self.epochs}"):
                X_batch, y_batch = X_batch.to(self.device), y_batch.to(self.device)
                self.optimizer.zero_grad()
                outputs = self.model(X_batch)
                loss = self.criterion(outputs, y_batch)
                loss.backward()
                self.optimizer.step()
                total_loss += loss.item()
            print(f"Epoch {epoch+1}/{self.epochs} - Loss: {total_loss/len(self.train_loader):.4f}")

    def evaluate(self):
        self.model.eval()
        y_true, y_pred = [], []
        with torch.no_grad():
            for X_batch, y_batch in self.test_loader:
                X_batch = X_batch.to(self.device)
                outputs = self.model(X_batch)
                preds = torch.argmax(outputs, dim=1)
                y_true.extend(y_batch.numpy())
                y_pred.extend(preds.cpu().numpy())

        acc = accuracy_score(y_true, y_pred)
        print("=== ĐÁNH GIÁ MÔ HÌNH ===")
        print("Độ chính xác:", acc)
        print(classification_report(y_true, y_pred, target_names=self.label_encoder.classes_))

    # ---------------- LƯU MÔ HÌNH ----------------
    def save_model(self, model_path="intent_model.pt", vec_path="vectorizer.pkl", encoder_path="label_encoder.pkl"):
        torch.save(self.model.state_dict(), model_path)
        joblib.dump(self.vectorizer, vec_path)
        joblib.dump(self.label_encoder, encoder_path)
        print(f"✅ Đã lưu mô hình vào {model_path}")
        print(f"✅ Các nhãn: {list(self.label_encoder.classes_)}")

    # ---------------- DỰ ĐOÁN ----------------
    def predict(self, text, model_path="intent_model.pt", vec_path="vectorizer.pkl", encoder_path="label_encoder.pkl"):
        # Load model & encoder
        self.model.load_state_dict(torch.load(model_path, map_location=self.device))
        self.model.eval()
        self.vectorizer = joblib.load(vec_path)
        self.label_encoder = joblib.load(encoder_path)

        x = self.vectorizer.transform([text]).toarray()
        x_tensor = torch.tensor(x, dtype=torch.float32).to(self.device)

        with torch.no_grad():
            output = self.model(x_tensor)
            pred_id = torch.argmax(output, dim=1).item()
            intent = self.label_encoder.inverse_transform([pred_id])[0]

        print(f"👉 Câu: {text}")
        print(f"🎯 Ý định dự đoán: {intent}")
        return intent



if __name__ == "__main__":
    # fake data
    data = {
        "texts": ["i am very happy", "i am bad today", "i am normal"],
        "labels": ["happy", "bad", "normal"]
    }
    df = pd.DataFrame(data)
    
    model = Model(df)

```