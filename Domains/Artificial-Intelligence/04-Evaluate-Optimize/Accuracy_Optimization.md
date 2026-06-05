- [Overfitting \& Underfitting](#overfitting--underfitting)
- [Vanishing Gradient \& Exploding Gradient](#vanishing-gradient--exploding-gradient)
- [Precision \& Recall](#precision--recall)
- [Evaluate Regression (đánh giá mô hình hồi quy)](#evaluate-regression-đánh-giá-mô-hình-hồi-quy)
  - [Mean Absolute Error (MAE) (sai số tuyệt đối trung bình)](#mean-absolute-error-mae-sai-số-tuyệt-đối-trung-bình)
  - [Relative MAE (Sai số tuyệt đối trung bình tương đối)](#relative-mae-sai-số-tuyệt-đối-trung-bình-tương-đối)
  - [Mean Absolute Percentage Error (MAPE) (Trung bình sai số phần trăm tuyệt đối)](#mean-absolute-percentage-error-mape-trung-bình-sai-số-phần-trăm-tuyệt-đối)
  - [Mean Squared Error (MSE) (Bình phương sai số trung bình)](#mean-squared-error-mse-bình-phương-sai-số-trung-bình)
  - [Root Mean Squared Error (RMSE)](#root-mean-squared-error-rmse)
  - [R2 Score (r2)](#r2-score-r2)
- [Binary Cross-Entropy (Log Loss)](#binary-cross-entropy-log-loss)
  - [Demo về công thức BCE bằng math](#demo-về-công-thức-bce-bằng-math)
---
# Overfitting & Underfitting
```bash
Overfitting xảy ra khi mô hình học quá kỹ dữ liệu huấn luyện -> mất khả năng tổng quát với dữ liệu mới. Biểu hiện là accuracy trên tập huấn luyện rất cao còn trên tập test lại thấp.
- Cách xử lý:
    + Thêm dữ liệu huấn luyện
    + Giảm độ phức tạp của mô hình
    + Regularization - phạt mô hình quá phức tạp
    + Early stopping cho mạng nơ ron
    + Dropout cho deep learning
    + Cross-validation (đánh giá mô hình nhiều lần với nhiều cách chia tập train/test khác nhau để tránh ăn may.
Underfitting xảy ra khi mô hình quá đơn giản hoặc thiếu dữ liệu, không thể học ra quy luật dẫn đến hiệu suất kém.
```
# Vanishing Gradient & Exploding Gradient 
```bash
- vanishing   : Gradient biến mất
- exploding   : Gradient bùng nổ
```
# Precision & Recall 
```bash
- Dùng để đánh giá chất lượng của một mô hình phân loại (classification), đặc biệt khi dữ liệu không cân bằng.
- Precision (độ chính xác) trả lời câu hỏi:
    + Trong những gì mô hình dự đoán là đúng (positive), thì bao nhiêu cái thực sự đúng?
    + Công thức: Precision = TP / (TP + FP)
    => Đo độ “chắc chắn” của mô hình khi dự đoán positive
- Recall (độ bao phủ) trả lời câu hỏi:
    + Trong tất cả những cái thực sự là positive, mô hình bắt được bao nhiêu?
    + Công thức: Recall = TP / (TP + FN)
    + Đo khả năng không bỏ sót
```
**Ex: Precision**
```bash
- Spam detection: Model nói 100 email là spam. Nhưng chỉ 80 cái thật sự là spam
→ Precision = 80/100 = 0.8
→ Nghĩa là: model không đoán bừa nhiều
```
**Ex: Recall**
```bash
- Có 100 email spam thật
- Model chỉ phát hiện được 80 → Recall = 80/100 = 0.8
→ Nghĩa là: model không bỏ sót nhiều
```
**Khi nào dùng cái nào?**
```bash
- Ưu tiên Precision khi:
    + False positive rất nguy hiểm
    + Ví dụ:
        - Phát hiện gian lận ngân hàng
        - Chẩn đoán bệnh nghiêm trọng (không muốn báo nhầm người khỏe thành bệnh)
- Ưu tiên Recall khi:
    + False negative nguy hiểm hơn
    + Ví dụ:
        - Phát hiện ung thư (không muốn bỏ sót người bệnh)
        - Tìm kiếm tài liệu (muốn lấy đủ kết quả)
```
**Trade-off (đánh đổi)**
```bash
- Precision và Recall thường đối nghịch nhau:
    + Tăng precision → giảm recall
    + Tăng recall → giảm precision
=> Vì vậy người ta hay dùng thêm: F1-score = trung bình điều hòa của precision & recall
```
# Evaluate Regression (đánh giá mô hình hồi quy)
## Mean Absolute Error (MAE) (sai số tuyệt đối trung bình)
```bash
- MAE là một metric dùng để đánh giá mô hình hồi quy (regression).
- MAE (Mean Absolute Error) = Sai số tuyệt đối trung bình
- Nó đo xem dự đoán của mô hình lệch trung bình bao nhiêu so với giá trị thật.
- MAE trả lời câu hỏi: “Trung bình mỗi dự đoán của mô hình sai khoảng bao nhiêu đơn vị?”
    + Ví dụ: MAE = 5 → trung bình dự đoán lệch 5 đơn vị so với thực tế
```
**Formula**
```bash
MAE = (1/n).(|y1-y_pred1| + |y2-y_pred2| + ... + |yn-y_predn|)

- y             : giá trị thật
- y_pred        : giá trị dự đoán
- |y - y_pred|  : sai số tuyệt đối
```
**Ex**
```bash
y_true = [100, 200, 300]
y_pred = [90, 220, 280]
Sai số từng điểm: e = y_true - y_pred = [10, -20, 20]
=> MAE = (10+20+20)/3 = 16.67
```
## Relative MAE (Sai số tuyệt đối trung bình tương đối) 
```bash
- Được sinh ra để giải quyết một điểm yếu chí mạng của MAE truyền thống: Tính phụ thuộc vào quy mô (Scale-dependent).
- Nói một cách dễ hiểu, RMAE dùng để "bình đẳng hóa" sai số, giúp bạn đánh giá được mô hình đang dự báo tốt hay tệ trên toàn bộ 370 khách hàng có quy mô tiêu thụ điện hoàn toàn lệch nhau.
- Tại sao có MAE rồi lại cần thêm Relative MAE?
    + Hãy tưởng tượng bạn đang dự báo cho 2 đối tượng khách hàng trong tập dữ liệu UCI của bạn:
        - Khách hàng A (Hộ gia đình nhỏ): Tiêu thụ trung bình ≈10 kW. Mô hình dự báo sai lệch so với thực tế là MAE = 14 kW.
        - Khách hàng B (Nhà máy công nghiệp): Tiêu thụ trung bình ≈2000 kW. Mô hình dự báo sai lệch là MAE = 14 kW.
    + Nếu chỉ nhìn vào con số MAE tổng thể là 14.0814 mà mô hình in ra, bạn sẽ thấy sai số của hai ông này bằng nhau. Nhưng thực tế:
        - Với hộ gia đình A: Sai số 14 kW trên mức nền 10 kW là quá tệ (dự báo sai gấp đôi thực tế).
        - Với nhà máy B: Sai số 14 kW trên mức nền 2000 kW là quá xuất sắc (sai số chưa tới 1%).
    + Bằng cách lấy MAE chia cho giá trị trung bình thực tế (np.mean(y_true)), công thức Relative MAE đã triệt tiêu đơn vị gốc (kW) để biến sai số thành tỷ lệ phần trăm (%).
    + Kết quả Relative MAE = 7.54% của bạn có nghĩa là: "Tính trung bình trên toàn bộ hệ thống, dù khách hàng dùng điện nhiều hay ít, mô hình LightGBM chỉ sai lệch khoảng 7.54% so với mức tiêu thụ thực tế của họ."
```
2. Sự khác biệt giữa Relative MAE và MAPE là gì?
Bạn sẽ thắc mắc: "Ơ, thế thì nó khác gì cái MAPE = 10.10% ở ngay bên dưới?"

Đây là một câu hỏi rất sâu về mặt toán học dữ liệu mà nếu bạn chủ động đưa vào báo cáo, thầy cô sẽ đánh giá bạn cực kỳ cao:

Chỉ số	Cách tính toán học	Điểm yếu khi gặp dữ liệu điện năng
MAPE	Tính tỷ lệ phần trăm sai số cho từng dòng dữ liệu trước, rồi mới lấy trung bình cộng của các phần trăm đó.	Bị nhạy cảm quá mức với các giá trị nhỏ gần bằng 0. Nếu thực tế khách hàng chỉ dùng 1 kW mà mô hình đoán 2 kW, MAPE của dòng đó lập tức vọt lên 100%, làm kéo cả chỉ số tổng thể xấu đi một cách oan uổng.
Relative MAE	Tính tổng sai số MAE của toàn bộ tập dữ liệu trước, rồi mới chia cho mức trung bình tổng.	Khắc phục hoàn toàn lỗi chia cho số 0 hoặc số quá nhỏ. Nó cho một cái nhìn toàn cục và công bằng hơn khi tập dữ liệu dính nhiều dải số 0 hoặc dải tiêu thụ thấp.

3. Cách viết ý nghĩa của Relative MAE vào Chương 3
Bạn có thể đưa đoạn nhận xét này vào mục 3.3.1 (Kết quả dự báo trên tập kiểm thử):

"Bên cạnh các chỉ số truyền thống, nghiên cứu đưa vào chỉ số Relative MAE (7.54%) để đánh giá hiệu năng mô hình một cách khách quan trên toàn bộ 370 khách hàng. Vì bộ dữ liệu UCI bao gồm nhiều nhóm đối tượng có quy mô tiêu thụ chênh lệch lớn (từ hộ gia đình đến nhà máy), chỉ số Relative MAE giúp chuẩn hóa sai số tuyệt đối về dạng tỷ lệ phần trăm dựa trên mức nền tiêu thụ trung bình. Kết quả 7.54% chứng minh mô hình Global Model của LightGBM có khả năng kiểm soát sai số cực kỳ ổn định và đồng đều, không bị ảnh hưởng bởi sự lệch pha về quy mô giữa các khách hàng."

Hiểu được bản chất RMAE giúp bạn nắm đằng chuôi vũ khí lý thuyết, không sợ bị hội đồng hỏi vặn tại sao lại vẽ ra nhiều chỉ số sai số làm gì!
## Mean Absolute Percentage Error (MAPE) (Trung bình sai số phần trăm tuyệt đối)
```bash
- Nó là một metric dùng để đánh giá độ chính xác của mô hình dự đoán, đặc biệt trong bài toán regression / forecasting (ví dụ dự đoán điện năng mà bạn đang làm với LightGBM).
- Nó trả lời câu hỏi: Trung bình mô hình dự đoán lệch bao nhiêu % so với giá trị thật?
- Càng nhỏ càng tốt.
    + < 10% → rất tốt
    + 10–20% → khá ổn
    + 20–50% → tạm được
    + > 50% → mô hình kém
    (chỉ là rule of thumb, tùy domain; dự báo thời tiết / điện năng tương lai thường chấp nhận cao hơn)
```
**Formula**
```bash
MAPE = (1/n)*(|(y1 - y_pred1)/y1|+ |(y2 - y_pred2)/y2| + |...|)*100
	​
- Input:
    + y1 -> yn  : giá trị thật
    + y_pred    : giá trị dự đoán
    + n         : số mẫu
    + ∣...∣     : lấy trị tuyệt đối (bỏ dấu âm)
- Output: Một số float, đơn vị %
```
**Ex**
```bash
Giá trị thật y  	Dự đoán p_pred  	Sai số %
100	                    90	            +10
200	                    220         	-20
50	                    40	            +10

MAPE = (10+10+20)/3 = 13.33% => Mô hình sai trung bình 13.33%
```
```python
from sklearn.metrics import mean_absolute_percentage_error

y_true = [100, 200, 50]
y_pred = [90, 220, 40]

mape = mean_absolute_percentage_error(y_true, y_pred)

print(mape)        # 0.1333
print(mape * 100)  # 13.33%
# sklearn trả về dạng thập phân
```
**Điểm khác nhau giữa MAE và MAPE**
```bash
- MAE phụ thuộc scale dữ liệu
- Ví dụ: Sai 10 đơn vị:
    + với giá trị 100 → sai 10%
    + với giá trị 10,000 → sai 0.1%
    + Nhưng MAE đều coi là “10”.
- MAPE chuẩn hóa theo %
    + Nó quan tâm: “Sai này lớn bao nhiêu so với giá trị thật?”
    + Nên cùng sai 10 => MAPE thấy 2 trường hợp này rất khác nhau.
```
## Mean Squared Error (MSE) (Bình phương sai số trung bình)
```bash
Ý nghĩa: Phạt lỗi lớn mạnh
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
## Root Mean Squared Error (RMSE)
**Vì sao dùng RMSE**
```bash
- Vì mse là đơn vị bình phương gây khó hiểu
- Ví dụ: MSE = kWh² cần chuyển sang RMSE = kWh (quay lại đơn vị gốc)
```
```bash
RMSE = sqrt((1/n).((y1-y_pred1)**2 + ... + (yn-y_predn)))
```
## R2 Score (r2)
```bash
- Là hệ số xác định dùng cho regression. 
- Model giải thích được bao nhiêu % biến thiên của dữ liệu 
    + Ví dụ:
        | Nhà | Giá thật |
        | --- | -------- |
        | A   | 1 tỷ     |
        | B   | 2 tỷ     |
        | C   | 3 tỷ     |
    => Dữ liệu thật dao động mạnh (1 → 3 tỷ) → đó là “biến thiên
- Có 2 cách đoán
    Cách 1: mô hình tốt. Dự đoán:
        1.1
        1.9
        3.1
    → nó “bắt được xu hướng tăng giảm”
    Cách 2: mô hình tệ. Dự đoán:
        2
        2
        2
    → chỉ đoán trung bình, không quan tâm gì cả
- R² đang đo cái gì?
    + Nó hỏi: “Model của bạn giải thích được bao nhiêu phần sự lên xuống (dao động) của giá thật?”
- Trực giác dễ hiểu nhất
    + Nếu R² = 0 → model không hiểu gì cả
        → chỉ đoán trung bình
        📌 Nếu R² = 1
        → model hiểu toàn bộ xu hướng tăng giảm
    + Nếu R² = 0.8 → model hiểu được 80% sự dao động, còn 20% là sai số
- Một cách nói “đời thường hơn”
- Câu đó có thể hiểu lại thành: “Model của bạn bắt được bao nhiêu % pattern của dữ liệu thật”
    + Ví dụ trực giác mạnh
        - Giả sử dữ liệu thật lên xuống như sóng:
            + Model tốt: vẽ lại gần giống sóng thật → R² cao
            + Model tệ: đường thẳng ngang → R² thấp
```
**Formula**
```bash
R2 = 1 - ((y1-y_pred1)**2 + ... + (yn-y_predn)**2)/((y1-y_tb)**2 + ... + (yn-y_tb)**2)

- Input: 
    + y1 -> yn  : giá trị thật
    + y_pred    : giá trị dự đoán
    + y_tb  : Giá trị trung bình của toàn bộ y thật
```
# Binary Cross-Entropy (Log Loss)
```bash
BCE (Binary Cross Entropy) là hàm mất mát (loss function) phổ biến nhất cho bài toán phân loại nhị phân (0 hoặc 1).
```
**Syn**
```bash
1. Công thức cho 1 mẫu: BCE(y_true, y_pred) = −[y_true.log(y_pred) + (1-y_true).log(1−y_pred)]
    - với log cơ số e
2. Công thức cho batch (N mẫu): BCE = −(1/n).∑[yi_true . log(yi_pred) + (1-yi_true) . log(1−yi_pred)]
```
**Đạo hàm BCE**
```bash
L = BCE = −[y_true.log(y_pred) + (1-y_true).log(1−y_pred)]
    dL/dy_pred = -y_true/y_pred + (1-y_true)/(1-y_pred) = (y_pred-y_true)/(y_pred.(1-y_pred))

Đạo hàm sigmoid
    dy_pred/dz = y_pred.(1-y_pred)

Đạo hàm BCE theo z
    dL/dz = (dL/dy_pred).(dy_pred/dz) = (y_pred-y_true)/(y_pred.(1-y_pred)).y_pred.(1-y_pred) = y_pred - y_true

=> dL/dw = (y-pred – y_true).x
=> dL/db = (y_pred - y_true)
```
## Demo về công thức BCE bằng math
```python
import math

def bce(y, y_hat):
    return -(y*math.log(y_hat) + (1-y)*math.log(1-y_hat))

print(bce(1, 0.9))
print(bce(1, 0.1))
```