- [Linear](#linear)
- [ReLu](#relu)
- [LeakyReLU](#leakyrelu)
- [GELU](#gelu)
- [Sigmoid](#sigmoid)
- [Tanh](#tanh)
- [Softmax](#softmax)
---
# Linear
**Formula**
```bash
1. z = W·X + b # Cách viết phổ biến trong machine learning lý thuyết, đặc biệt trong sách Deep Learning
    + X: vector input kích thước (n, 1)
    + W: ma trận trọng số kích thước (m, n)
    + b: vector bias (m, 1)
2. z = X·W + b # Phổ biến trong framework dạng batch, như TensorFlow, PyTorch, sklearn.
    + X: dạng hàng (row vector) hoặc batch (batch_size, n)
    + W: ma trận trọng số (n, m)
    + b: vector bias (m,)
```
# ReLu
```bash
Hàm kích hoạt ReLU giúp phá vỡ tính tuyến tính, cho phép mạng học được các hàm số phức tạp hơn.
    - ít bị vanishing gradient
    - có thể gây exploding
```
**Formula**
```bash
f(x) = max(0, x)
```
# LeakyReLU
```bash
- ít bị vanishing gradient
- có thể gây exploding gradient
```
**Ex**
```bash
f(x) = x (​x>0) and 0.01*x (x<0​)
```
# GELU
```bash
- ít bị vanishing gradient
- có thể gây exploding gradient

Được dùng trong:
    - OpenAI GPT
    - Google BERT
    - Transformer hiện đại
Đồ thị giống ReLU nhưng mượt hơn.
```
**Fomula**
```bash
GELU(x)=x⋅Φ(x)

- Φ(x): là hàm phân phối tích lũy (CDF) của phân phối chuẩn.

Công thức xấp xỉ thường dùng. Trong code thực tế thường dùng:

GELU(x) = 0.5*x*(1+tanh(sqrt(2/π)*(x+0.044715*x**3)))
```
# Sigmoid
```bash
Rất dễ gây vanishing gradient, không gây exploding gradient đáng kể
```
**Formula**
```bash
f(z) = 1 / (1+e**-z) # chỉ áp dụng lên 1 giá trị của z = W*x + b
```
# Tanh
```bash
Giống sigmoid, giúp mô hình học các quan hệ phi tuyến.
    - có gây vanishing gradient
    - gây exploding gradient không đáng kể

- Giá trị nằm giữa -1 và 1 → giúp gradient descent ổn định hơn so với sigmoid (giảm bias về chiều dương).
- Ứng dụng:
    1. Hidden layer trong mạng nơ-ron
        1. Trước đây, thường dùng trong MLP, RNN.
        2. Ví dụ: h_t = tanh(Wx_t + Uh_{t-1}) trong RNN.
    2. Chuỗi thời gian và ngôn ngữ
        1. Trong RNN / LSTM / GRU, tanh thường dùng để:
            1. Biểu diễn trạng thái ẩn (hidden state)
            2. Điều chỉnh thông tin truyền xuống các bước thời gian.
    3. Chuẩn hóa dữ liệu đầu ra
        1. Khi dữ liệu cần nằm trong khoảng [-1, 1]
    4. Phi tuyến hóa đầu ra
        1. Trong một số bài toán hồi quy giới hạn đầu ra.
```
**Formula**
```bash
tanh(x) = (e**x – e**-x) / (e**x + e**-x) # nằm trong đợn -1 đến 1
```
# Softmax
```bash
Thường được dùng ở output layer của mô hình phân loại nhiều lớp (multi-class classification). Nó biến vector đầu ra thô (logits) của mô hình thành xác suất, sao cho tổng các xác suất = 1.
```
**Formula**
```bash
# Giả sử đầu ra của mô hình là một vector: z = [z1, z2, z3, z4, … , zn]
softmax(z1) = e^z1 / (e^z1 + … + e^zn)
```
**Ex**
```python
import numpy as np

def softmax(x):
    exp_x = np.exp(x – np.max(x)) # Trừ max(x) để tránh tràn số khi e^x quá lớn
    return exp_x / np.sum(exp_x)

# Ví dụ:
logits = np.array([2.0, 1.0, 0.1])
probs = softmax(logits)
print("Xác suất:", probs)
print("Tổng:", np.sum(probs))
```