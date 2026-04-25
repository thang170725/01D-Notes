- [Loss\_Function](#loss_function)
- [Cost\_Function](#cost_function)
  - [Regression (Nhóm hồi quy)](#regression-nhóm-hồi-quy)
    - [Mean Squared Error (MSE)](#mean-squared-error-mse)
    - [Mean Absolute Error](#mean-absolute-error)
    - [Root Mean Squared Error (RMSE)](#root-mean-squared-error-rmse)
    - [R2 Score](#r2-score)
  - [Binary Cross-Entropy (Log Loss)](#binary-cross-entropy-log-loss)
  - [Demo về công thức BCE bằng math](#demo-về-công-thức-bce-bằng-math)
---
# Loss_Function
```bash
Tính cho 1 sample (1 dòng).
```
# Cost_Function
```bash
Tính trên toàn bộ dataset
```
## Regression (Nhóm hồi quy)
### Mean Squared Error (MSE)
```bash
Bình phương sai số trung bình -> Ý nghĩa: Phạt lỗi lớn mạnh
```
**Formula**
```bash
1. MSE = 1/n . [(y1_true - y1_pred)^2 + (y2_true - y2_pred)^2 + … ]
  - Output: càng gần 0 càng 
2.
  - Gradient theo w: dL/dw = (−2/𝑚).𝑋𝑇.(𝑦−𝑦^)
  - Gradient theo b: dL/db = (−2/𝑚).∑(𝑦−𝑦^)
```
**Tại sao trong công thức mse là có bình phương**
```bash
- y_true − y_pred: đúng là “sai số” (error) nhưng chưa đủ để đo độ sai tốt
- Vấn đề nếu KHÔNG bình phương. Nếu bạn dùng:
  + y_true − y_pred thì sẽ có chuyện:
    - Sai dương: +10
    - Sai âm: -10
    👉 Cộng lại = 0 ➡️ Model sai rất nhiều nhưng lại nhìn như “không sai” 😅
✅ Vì vậy mới cần bình phương Ý nghĩa:
  - Bình phương → mọi sai số đều dương
  - Không bị triệt tiêu nhau. Đo được “độ lớn sai số” thật
🔥 Lý do quan trọng hơn (ít người để ý)
  1. Phạt mạnh lỗi lớn
    - Sai 1 → 1**2 = 1
    - Sai 10 → 10**2 = 100
    👉 lỗi lớn bị phạt nặng hơn nhiều ➡️ Model sẽ cố tránh sai lớn
  2. Dễ tối ưu (rất quan trọng)
    - Hàm bình phương:
      + smooth (trơn)
      + có đạo hàm đẹp
      👉 dùng được với gradient descent (cực kỳ quan trọng cho ML)
```
**Ex: bình phương và không bình phương**
```bash
y_true	y_pred	error
10	    8	      +2
10	    12      -2
❌ Không bình phương: 2+(−2)=0 → tưởng model hoàn hảo 😑
✅ Có bình phương: 2**2+(−2)**2 = 4+4 = 8 → phản ánh đúng là đang sai
```
### Mean Absolute Error
```bash
Sai số tuyệt đối trung bình
```
**Formula**
```bash
MAE = (1/n).(|y1-y_pred1| + |y2-y_pred2| + ... + |yn-y_predn|)
```
**Ex**
```bash
y_true = [100, 200, 300]
y_pred = [90, 220, 280]
Sai số từng điểm: e = y_true - y_pred = [10, -20, 20]
=> MAE = (10+20+20)/3 = 16.67
```
### Root Mean Squared Error (RMSE)
**Vì sao dùng RMSE**
```bash
- Vì mse là đơn vị bình phương gây khó hiểu
- Ví dụ: MSE = kWh² cần chuyển sang RMSE = kWh (quay lại đơn vị gốc)
```
```bash
RMSE = sqrt((1/n).((y1-y_pred1)**2 + ... + (yn-y_predn)))
```
### R2 Score
```bash
- Là hệ số xác định. Đo model giải thích được bao nhiêu biến thiên
```
**Formula**
```bash
R2 = 1 - ((y1-y_pred1)**2 + ... + (yn-y_predn)**2)/((y1-y_tb)**2 + ... + (yn-y_tb)**2)

- Input: 
  + y_tb  : Giá trị trung bình của toàn bộ y thật
```
## Binary Cross-Entropy (Log Loss)
```bash
Dùng cho phân loại nhị phân.
```
**Syn**
```bash
1. Công thức cho 1 mẫu: BCE(y_true, y_pred) = −[y_true.log(y_pred) + (1-y_true).log(1−y_pred)]
2. Công thức cho batch (N mẫu): BCE = −(1/n) . [yi_true . log(yi_pred) + (1-yi_true) . log(1−yi_pred)]
3. dL/dw = (y-pred – y_true).x
4. dL/db = (y_pred - y_true)
```
## Demo về công thức BCE bằng math
```python
import math

def bce(y, y_hat):
    return -(y*math.log(y_hat) + (1-y)*math.log(1-y_hat))

print(bce(1, 0.9))
print(bce(1, 0.1))
```