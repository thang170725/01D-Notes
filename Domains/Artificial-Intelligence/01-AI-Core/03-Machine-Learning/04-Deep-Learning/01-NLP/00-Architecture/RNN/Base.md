- [Introduction](#introduction)
---
# Introduction
```bash
RNN (Recurrent Neural Network) Là một kiến trúc mạng neural dùng để xử lý dữ liệu tuần tự (sequential data). 

RNN hoạt động dựa trên ý tưởng: 
    - thông tin ở bước t−1 sẽ được kết hợp với đầu vào ở bước t để tạo ra trạng thái mới.
    - Điều này rất phù hợp với: 
        + Chuỗi văn bản
        + Dữ liệu thời gian (time series)
        + Chuỗi tín hiệu âm thanh, video, …

Vấn đề: 
    - RNN quên rất nhanh.
    - Không nhớ được thông tin xa.
    - Bị vanishing gradient khi chuỗi dài.
    - Bạn đọc câu: "Tôi ăn cơm lúc 7h sáng, và đến chiều thì tôi đói." 
        + RNN có thể không nhớ phần trước (7h sáng) vì quá xa → mất ngữ cảnh 
→ RNN phù hợp với chuỗi ngắn, hoặc tác vụ đơn giản.
```
**Kiến trúc RNN**
```bash
- Một RNN đơn giản có 3 tham số chính:
Wxh  (input → hidden)
Whh  (hidden → hidden)
Why  (hidden → output)

- Giả sử:
input size = 8
hidden size = 4
output size = 8
```
**Công thức RNN**
```bash
- Hidden state: ℎ𝑡 = 𝑡𝑎𝑛ℎ(𝑊𝑥ℎ.𝑥𝑡 + 𝑊ℎℎ.ℎ𝑡−1 + 𝑏ℎ)
- Output: 𝑦𝑡 = 𝑠𝑜𝑓𝑡𝑚𝑎𝑥(𝑊ℎ𝑦.ℎ𝑡 + 𝑏𝑦)
```
**Work flow của RNN**
```bash
Bài toán dự đoán từ tiếp theo trong câu (Next Word Prediction)
    Cho một câu chưa hoàn chỉnh: "I love deep _" mô hình phải dự đoán từ tiếp theo "learning"
    Input: I love deep
    Output: learning
```
**Dataset**
```bash
| Sentence                 |
| ------------------------ |
| I love deep learning     |
| I love machine learning  |
| I love natural language  |
| I enjoy deep learning    |
| I enjoy machine learning |
| ...                      |
```
```bash
1. Tokenization: chuyển câu thành token
    I love deep learning -> [I, love, deep, learning]

2. Vocabulary: tạo từ điển
```bash
| Word     | ID |
| -------- | -- |
| I        | 1  |
| love     | 2  |
| enjoy    | 3  |
| deep     | 4  |
| machine  | 5  |
| natural  | 6  |
| language | 7  |
| learning | 8  |
-> Vocabulary size: V = 8

3. Tạo Training Samples: RNN học theo sequence → next token
    I love deep learning

    Ta tạo các sample:
    | Input       | Target   |
    | ----------- | -------- |
    | I           | love     |
    | I love      | deep     |
    | I love deep | learning |

4. Encode: One hot
    Ví dụ từ deep vector one-hot: deep = [0 0 0 1 0 0 0 0]
    Dimension: V = 8


**Ví dụ Forward Pass**
```bash
Giả sử input sequence: I love deep
Step 1: word = "I"
- One-hot: x1 = [1 0 0 0 0 0 0 0]
- Giả sử trọng số: Wxh = [0.2 0.1 0.0 ...] ...
- Giả sử hidden state ban đầu: h0 = [0 0 0 0]
- Tính: ℎ1 = 𝑡𝑎𝑛ℎ(𝑊𝑥ℎ.𝑥1 + 𝑊ℎℎ.ℎ0) = [0.21, -0.13, 0.45, 0.10]
Step 2: word = "love"
- x2 = [0 1 0 0 0 0 0 0]
- ℎ2 = 𝑡𝑎𝑛ℎ(𝑊𝑥ℎ.𝑥2 + 𝑊ℎℎ.ℎ1) = [0.35, 0.10, 0.41, 0.22]
Step 3: word = "deep"
- x3 = [0 0 0 1 0 0 0 0]
- ℎ3 = 𝑡𝑎𝑛ℎ(𝑊𝑥ℎ.𝑥3 + 𝑊ℎℎ.ℎ2) = [0.52, 0.11, 0.33, 0.40]
```
**Output Layer**
```bash
- 𝑦3 = 𝑠𝑜𝑓𝑡𝑚𝑎𝑥(𝑊ℎ𝑦.ℎ3) = [0.02, 0.01, 0.03, 0.04, 0.02, 0.03, 0.05, 0.80]
- Mapping lại từ: learning -> 0.80 → dự đoán: learning
```
**Loss Function: Dùng Cross Entropy**
```bash
- Target vector: learning = [0 0 0 0 0 0 0 1]
- Loss: 𝐿 = −∑𝑦𝑡𝑟𝑢𝑒.log(𝑦𝑝𝑟𝑒𝑑) = −log(0.80) = 0.223
```
**Backpropagation Through Time (BPTT): Gradient được lan truyền ngược theo thời gian**
```bash
- Chuỗi: I → love → deep
- Gradient flow: loss -> h3 -> h2 -> h1
- Update: Wxh, Whh, Why
```
**Training Loop: Toàn bộ pipeline**
```bash

for epoch:
  for sentence in dataset:
     tokenize
     convert to one-ho
     forward pass (RNN)
     compute loss
     BPTT
     update weights
```