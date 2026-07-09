- [Introduction](#introduction)
- [Regression (nhóm mô hình hồi quy)](#regression-nhóm-mô-hình-hồi-quy)
  - [mean\_squared\_error()](#mean_squared_error)
  - [r2\_score](#r2_score)
- [Classifier (Nhóm mô hình phân loại)](#classifier-nhóm-mô-hình-phân-loại)
  - [accuracy\_score()](#accuracy_score)
  - [classification\_report](#classification_report)
---
# Introduction
```bash
- Khi bạn gọi .predict() của các mô hình ML, nó chỉ dự đoán ra kết quả y_pred thôi. Nhưng để đánh giá mô hình có tốt hay không, bạn cần so sánh y_pred (dự đoán) với y_test (giá trị thật) và tính ra sai số như MSE, MAE, r2 score.
- Nếu chỉ .predict() mà không tính toán gì, thì chỉ thấy ra một mớ số dự đoán, không biết mô hình giỏi hay dở, không đủ chứng minh cho người khác là mô hình mình tốt hay xấu.
```
# Regression (nhóm mô hình hồi quy)
## mean_squared_error()
```bash
- Là một hàm đánh giá sai số phổ biến trong học máy, đặc biệt dùng trong các bài toán hồi quy (regression).
- Để đo lường độ chính xác của mô hình hồi quy. MSE càng nhỏ -> mô hình càng dự đoán sát với dữ liệu thực tế. 
- Được dùng làm hàm mất mát (cost function) trong huấn luyện mô hình
```
**Syn**
```bash
from sklearn.metrics import mean_squared_error
mse = mean_squared_error(y_true, y_pred)

- ytrue: Giá trị thực tế
- ypred: giá trị dự đoán
```
## r2_score
```bash
- Đánh giá độ phù hợp của mô hình hồi quy, còn được gọi là hệ số xác định (coefficient of determination).
- r-squared đo mức độ mà mô hình giải thích được phương sai của dữ liệu thực tế.
- Nó phản ánh mức độ liên hệ tuyến tính giữa giá trị dự đoán và giá trị thực.
- Nếu:
    + =1: Mô hình dự đoán chính xác hoàn toàn.
    + =0: Mô hình dự đoán kém, không hơn trung bình.
    + <0: Mô hình tệ hơn cả việc đoán trung bình.
```
**Ex**
```python
from sklearn.metrics import r2_score

y_true = [3, -0.5, 2, 7]
y_pred = [2.5, 0.0, 2, 8]

r2 = r2_score(y_true, y_pred)
print("R2 Score:", r2) # R2 Score: 0.9486081370449679
```
# Classifier (Nhóm mô hình phân loại)
## accuracy_score()
```bash
- Để đánh giá độ chính xác cho mô hình cho mô hình phân nhãn rời rạc, thường đành cho logistic. 
- Ví dụ: Nếu có 10 câu đầu vào và mô hình đoán đúng 7 câu → accuracy = 0.7
```
**Syn**
```bash
accuracy_score(y_test, y_pred))
```
## classification_report
```bash
Được dùng để đánh giá hiệu suất của mô hình phân loại. Nó hiển thị các chỉ số quan trọng cho từng lớp như:
    • Precision: Độ chính xác (đo xem trong các dự đoán đúng cho lớp đó thì bao nhiêu là đúng thật).
    • Recall: Độ bao phủ (đo xem trong tất cả các mẫu thực sự thuộc lớp đó thì bao nhiêu được dự đoán đúng).
    • F1-score: Trung bình hài hòa giữa precision và recall.
    • Support: Số lượng mẫu thật sự thuộc mỗi lớp.
```
**Ex**
```python
from sklearn.metrics import classification_report

y_true = [0, 1, 2, 2, 1]
y_pred = [0, 0, 2, 2, 1]

print(classification_report(y_true, y_pred))

#   precision        recall  f1-score   support

#            0       0.50      1.00      0.67         1
#            1       1.00      0.50      0.67         2
#            2       1.00      1.00      1.00         2

#     accuracy                           0.80         5
#    macro avg       0.83      0.83      0.78         5
# weighted avg       0.90      0.80      0.80         5
```