- [Logistic Regression Introduction](#logistic-regression-introduction)
  - [Ask (các câu hỏi liên quan đến chủ đề logistic)](#ask-các-câu-hỏi-liên-quan-đến-chủ-đề-logistic)
- [Practices](#practices)
  - [Demo Pipeline Logistic bằng 2 cách](#demo-pipeline-logistic-bằng-2-cách)
  - [Demo logistic với numpy](#demo-logistic-với-numpy)
  - [Demo Logistic với pytorch](#demo-logistic-với-pytorch)
---
# Logistic Regression Introduction
## Ask (các câu hỏi liên quan đến chủ đề logistic)
**Tại sao logistion phân loại 2 lớp lại chỉ có 2 weight đánh ra phải là 4 weight nếu theo ý tưởng mạng neural**
```bash
Thực ra có hai cách làm nên mới gây nhầm:
    Cách 1: Binary Logistic Regression "kinh điển"
        Có 2 lớp:
            - Class 0
            - Class 1

        Nhưng ta không tạo 2 neuron. Ta chỉ tạo 1 neuron:
            x1
            x2
             │
             ▼
            Linear(2 → 1)
             │
             ▼
            z
             │
            sigmoid
             │
             ▼
            P(class1)
        
        nghĩa là
            - P(class1)=0.96
            - P(class0)=1−0.96=0.04
            - Ta không cần neuron thứ hai vì P(class0)=1−P(class1)

    Cách 2: Viết giống Multi-class
        Ta vẫn có 2 lớp:
            - Class0
            - Class1

        Nhưng tạo 2 neuron:
            x1,x2
            ↓
            Linear(2→2)
            ↓
            [z0,z1]
            ↓
            softmax

        Lúc này
            - z0 = score class0
            - z1 = score class1
```
# Practices
## Demo Pipeline Logistic bằng 2 cách
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
**CÁCH 1: DÙNG BINARY CROSS-ENTROPY (BCE) - MÔ HÌNH 1 ĐẦU RA**
```bash
Bước 1: Khởi tạo trọng số:
    w1 = 0.1, w2 = 0.1, w3 = 0.1, b=0

Bước 2: Forward (tính dự đoán)
    Ứng viện 1: (1, 5, 2), y = 0
        + z1 = w1.x1 + w2.x2 + w3.x3 + b = 0.1(1) + 0.1(5) + 0.1(2) = 0.8
        + y_pred = σ(z1​) = 1/(1+e^-z1) = 1/(1+e^-0.8) ≈ 0.69
    
    Ứng viên 2: (2, 6, 3), y = 0    
        + z2 = 1.1 ⇒ y_pred ≈ 0.75
    
    Ứng viên 3: (3, 7, 4), y = 1
        + z3 = 1.4 ⇒ y_pred ≈ 0.80
    
    ...

Bước 3: Tính Loss (BCE)
    L1 = −(ylog(y_pred))+(1−y)log(1−y_pred)) = −(0⋅log(0.69)+(1−0)log(1−0.69))=−log(0.31) ⇒ L1 ≈ 1.17
    ...
    
    => Loss = 1/6 . (L1 + L2 + ... + L6) = 0.69
    - Nhận xét: Model đang đoán quá cao cho các mẫu rớt (0) → sai khá nhiều

Bước 4: Backpropagation (Tính gradient)
    Tính cho Ứng viên 1:
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
    
    => Tổng gradient (trung bình toàn bộ dataset)
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
**CÁCH 2: Ý TƯỞNG MULTI-CLASS (SOFTMAX + CE) - MÔ HÌNH 2 ĐẦU RA**
```bash
Để chuyển sang đa lớp, nhãn thực tế y sẽ được mã hóa dạng One-hot vector:
    - Ứng viên rớt (y=0) → Vector nhãn: Y=[1,0] (Lớp rớt có giá trị 1, lớp đậu có giá trị 0).
    - Ứng viên đậu (y=1) → Vector nhãn: Y=[0,1].

Vì có 2 lớp độc lập, ta cần 2 bộ trọng số riêng biệt:
    - Bộ dự đoán Rớt (Lớp 0): W(0) = [w1(0), w2(0), w3(0)] và bias b(0)
    - Bộ dự đoán Đậu (Lớp 1): W(1) = [w1(1), w2(1), w3(1)] và bias b(1)
 

Bước 1: Khởi tạo trọng số (Giả định tất cả bằng 0.1, bias = 0)
    - Lớp 0 (Rớt): w1(0) = 0.1, w2(0) = 0.1, w3(0) = 0.1, b(0) = 0
    - Lớp 1 (Đậu): w1(1) = 0.1, w2(1) = 0.1, w3(1) = 0.1, b(1) = 0

Bước 2: Forward (Tính toán dự đoán qua Softmax)
    Xét Ứng viên 1: X=(1,5,2), nhãn mã hóa Y=[1,0].
        Tính điểm số (Logits) cho từng lớp:
            - z0 = 0.1*1 + 0.1*5 + 0.1*2 + 0 = 0.8
            - z1 = 0.1*1 + 0.1*5 + 0.1*2 + 0 = 0.8

        Kích hoạt Softmax để đưa về phân phối xác suất tổng bằng 1:
            - ypred0 = e**z0/(e**z0 + e**z1) = e**0.8/(e**0.8+e**0.8) = 0.5 (Xác suất đoán rớt)
            - ypred1 = e**z1/(e**z1 + e**z1) = e**0.8/(e**0.8+e**0.8) = 0.5 (Xác suất đoán đậu)
        
        Vector dự đoán: Ypred = [0.5, 0.5]

Bước 3: Tính Loss (Categorical Cross-Entropy)
    Công thức: L=−∑(Y⋅log(Ypred))

    Mất mát của Ứng viên 1:
        L1 = −[1⋅log(0.5)+0⋅log(0.5)] = −log(0.5) ≈ 0.301

Bước 4: Backpropagation (Đạo hàm cho từng bộ trọng số)
    Độ lệch đầu ra đối với mô hình Softmax vẫn có dạng rất đẹp là (Ypred −Y ) cho từng lớp tương ứng:
        Với lớp 0 (Rớt): error0 = ypred0 − Y0 = 0.5−1 = −0.5
            - ∂L1/∂w1(0) = −0.5⋅x1 = −0.5⋅1 = −0.5
            - ∂L1/∂w2(0) = −0.5⋅x2 = −0.5⋅5 = −2.5
            - ∂L1/∂w3(0) = −0.5⋅x3 = −0.5⋅2 = −1.0
            - ∂L1/∂b(0) = −0.5

        Với lớp 1 (Đậu): error1 = ypred1 − Y1 = 0.5 − 0 = 0.5
            - ∂L1/∂w1(1) = 0.5⋅x1 = 0.5⋅1 = 0.5
            - ∂L1/∂w2(1) = 0.5⋅x2 = 0.5⋅5 = 2.5
            - ∂L1/∂w3(1) = 0.5⋅x3 = 0.5⋅2 = 1.0
            - ∂L1/∂b(1) = 0.5

Bước 5: Update Weights (Cập nhật song song cả 2 bộ trọng số)
    Dùng Learning Rate = 0.05 kết hợp với trung bình cộng gradient của cả tập dữ liệu để tối ưu hóa đồng thời cả bộ tham số lớp 0 và lớp 1.
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
[Link github research code](https://github.com/thang170725/02RS-Logistic-Regression/blob/main/logistic_torch.py)