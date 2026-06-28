- [Underfitting (học quá kỹ dữ liệu huấn luyện, mất khả năng tổng quát với dữ liệu mới)](#underfitting-học-quá-kỹ-dữ-liệu-huấn-luyện-mất-khả-năng-tổng-quát-với-dữ-liệu-mới)
- [Overfitting (học quá kỹ dữ liệu huấn luyện, mất khả năng tổng quát với dữ liệu mới)](#overfitting-học-quá-kỹ-dữ-liệu-huấn-luyện-mất-khả-năng-tổng-quát-với-dữ-liệu-mới)
  - [Regularization (Chống Overfitting)](#regularization-chống-overfitting)
    - [L2 (Ridge) (Thêm hình phạt)](#l2-ridge-thêm-hình-phạt)
    - [L1 (Lasso) (Thêm hình phạt)](#l1-lasso-thêm-hình-phạt)
    - [Dropout (Tắt ngẫu nhiên một phần neuron)](#dropout-tắt-ngẫu-nhiên-một-phần-neuron)
    - [Early Stopping](#early-stopping)
- [Bias](#bias)
- [Variance](#variance)
- [Learning Curve](#learning-curve)
- [Vanishing Gradient \& Exploding Gradient](#vanishing-gradient--exploding-gradient)
- [Evaluate Regression (đánh giá mô hình hồi quy)](#evaluate-regression-đánh-giá-mô-hình-hồi-quy)
  - [Mean Absolute Error (MAE) (sai số tuyệt đối trung bình)](#mean-absolute-error-mae-sai-số-tuyệt-đối-trung-bình)
  - [Relative MAE (Sai số tuyệt đối trung bình tương đối)](#relative-mae-sai-số-tuyệt-đối-trung-bình-tương-đối)
  - [Mean Absolute Percentage Error (MAPE) (Trung bình sai số phần trăm tuyệt đối)](#mean-absolute-percentage-error-mape-trung-bình-sai-số-phần-trăm-tuyệt-đối)
  - [Mean Squared Error (MSE) (Bình phương sai số trung bình)](#mean-squared-error-mse-bình-phương-sai-số-trung-bình)
  - [Root Mean Squared Error (RMSE)](#root-mean-squared-error-rmse)
  - [R2 Score (r2)](#r2-score-r2)
- [Evaluate Classification (đánh giá mô hình phân loại)](#evaluate-classification-đánh-giá-mô-hình-phân-loại)
  - [Accuracy (Độ chính xác tổng thể)](#accuracy-độ-chính-xác-tổng-thể)
  - [Precision (Độ chính xác của dự đoán dương tính)](#precision-độ-chính-xác-của-dự-đoán-dương-tính)
  - [Recall (độ bao phủ)](#recall-độ-bao-phủ)
  - [F1-Score (Trung bình điều hòa giữa Precision và Recall)](#f1-score-trung-bình-điều-hòa-giữa-precision-và-recall)
  - [Binary Cross-Entropy (Log Loss) (hàm mất mát (loss function) phổ biến nhất cho bài toán phân loại nhị phân (0 hoặc 1))](#binary-cross-entropy-log-loss-hàm-mất-mát-loss-function-phổ-biến-nhất-cho-bài-toán-phân-loại-nhị-phân-0-hoặc-1)
    - [Demo về công thức BCE bằng math](#demo-về-công-thức-bce-bằng-math)
  - [Categorical Cross Entropy (dùng cho bài toán phân loại nhiều lớp (multi-class classification))](#categorical-cross-entropy-dùng-cho-bài-toán-phân-loại-nhiều-lớp-multi-class-classification)
  - [Sparse Categorical Cross-Entropy (SCCE) (hàm loss dùng cho bài toán phân loại nhiều lớp (multi-class classification))](#sparse-categorical-cross-entropy-scce-hàm-loss-dùng-cho-bài-toán-phân-loại-nhiều-lớp-multi-class-classification)
  - [ROC-AUC và PR-AUC](#roc-auc-và-pr-auc)
- [Optimizer (thuật toán tối ưu)](#optimizer-thuật-toán-tối-ưu)
  - [SGD (Stochastic Gradient Descent)](#sgd-stochastic-gradient-descent)
  - [Momentum (SGD + quán tính)](#momentum-sgd--quán-tính)
  - [RMSprop](#rmsprop)
  - [Adam (Momentum+RMSprop)](#adam-momentumrmsprop)
  - [AdamW (Adam nhưng sửa lỗi lớn nhất của Adam)](#adamw-adam-nhưng-sửa-lỗi-lớn-nhất-của-adam)
- [Learning rate (tối ưu learning rate)](#learning-rate-tối-ưu-learning-rate)
  - [Learning Rate Scheduler (cơ chế tự động điều chỉnh learning rate)](#learning-rate-scheduler-cơ-chế-tự-động-điều-chỉnh-learning-rate)
    - [Cosine Annealing (LR giảm từ từ theo đường cong cosine)](#cosine-annealing-lr-giảm-từ-từ-theo-đường-cong-cosine)
    - [ReduceLROnPlateau (giảm lr khi model bị kẹt)](#reducelronplateau-giảm-lr-khi-model-bị-kẹt)
    - [StepLR (Cứ N epoch giảm)](#steplr-cứ-n-epoch-giảm)
    - [OneCycleLR (Tăng rồi giảm)](#onecyclelr-tăng-rồi-giảm)
    - [Warmup + Cosine (Tăng nhẹ rồi giảm dần)](#warmup--cosine-tăng-nhẹ-rồi-giảm-dần)
---
# Underfitting (học quá kỹ dữ liệu huấn luyện, mất khả năng tổng quát với dữ liệu mới)
# Overfitting (học quá kỹ dữ liệu huấn luyện, mất khả năng tổng quát với dữ liệu mới)
```bash
Biểu hiện là accuracy trên tập huấn luyện rất cao còn trên tập test lại thấp.

Cách xử lý:
    + Thêm dữ liệu huấn luyện
    + Giảm độ phức tạp của mô hình
    + Regularization - phạt mô hình quá phức tạp
    + Early stopping cho mạng nơ ron
    + Dropout cho deep learning
    + Cross-validation (đánh giá mô hình nhiều lần với nhiều cách chia tập train/test khác nhau để tránh ăn may.
```
## Regularization (Chống Overfitting)
```bash
Là cách phạt mô hình nếu trọng số quá lớn.
    Mục tiêu: ngăn mô hình học thuộc lòng dữ liệu train

Dùng cả trong hồi quy và phân loại
```
### L2 (Ridge) (Thêm hình phạt)
```bash
Ý tưởng:
    Ép các trọng số nhỏ lại.

    Ví dụ:
        Trước:
            - w1 = 100
            - w2 = 50
            - w3 = 80
        Sau L2:
            - w1 = 10
            - w2 = 5
            - w3 = 8
        Nhưng hiếm khi về đúng 0.

Tác dụng
    - Giảm overfitting
    - Giữ lại hầu hết feature
    - Đây là loại được dùng nhiều nhất.
```
**Formula**
```bash
Loss = OriginalLoss + λ∑w**2

Tác dụng:
    - Không đưa weight về 0 hoàn toàn.
    - Làm weight nhỏ lại.
    - Phổ biến nhất trong Deep Learning
```
### L1 (Lasso) (Thêm hình phạt)
```bash
Ý tưởng:
    Ép nhiều trọng số về đúng 0.

Ví dụ:
    Trước:
        - w1 = 10
        - w2 = 0.2
        - w3 = 0.1
        - w4 = 8
    Sau L1:
        - w1 = 10
        - w2 = 0
        - w3 = 0
        - w4 = 8

Tác dụng
    - Ngoài chống overfitting còn: 👉 Tự chọn feature quan trọng.
    
    Ví dụ:
        100 feature
        L1 có thể loại bỏ 70 feature không cần thiết.
```
**Fomula**
```bash
Loss = OriginalLoss + λ∑∣w∣

Tác dụng:
    - Đẩy nhiều weight về 0.
    - Tự động chọn feature quan trọng
```
### Dropout (Tắt ngẫu nhiên một phần neuron)
**Ex**
```bash
Layer:
[O O O O O O]

Dropout 50%:
[O X O X X O]

Mục đích:
- Neuron không phụ thuộc lẫn nhau.
- Giảm overfitting mạnh.
```
### Early Stopping
**Ex**
```bash
Theo dõi Validation Loss:

Epoch 1: 0.8
Epoch 2: 0.6
Epoch 3: 0.4
Epoch 4: 0.35
Epoch 5: 0.37 ← tăng lên
Epoch 6: 0.40

Dừng ở Epoch 4 thay vì train tiếp.
```
# Bias
```bash
Underfitting = Bias cao
    Mô hình quá đơn giản → học chưa đủ.

Ví dụ:
    - Train Accuracy = 70%
    - Test Accuracy  = 68%
Cả train lẫn test đều thấp. 👉 Bias cao.
```
# Variance
```bash
Overfitting = Variance cao
    Mô hình quá phức tạp → học thuộc dữ liệu train.

Ví dụ:
    - Train Accuracy = 99%
    - Test Accuracy  = 75%
Train rất cao nhưng test thấp. 👉 Variance cao.
```
# Learning Curve
# Vanishing Gradient & Exploding Gradient 
```bash
- vanishing   : Gradient biến mất
- exploding   : Gradient bùng nổ
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
**Tại sao trong công thức mse có bình phương**
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
# Evaluate Classification (đánh giá mô hình phân loại)
## Accuracy (Độ chính xác tổng thể)
```bash
Trong tất cả dự đoán, mô hình đúng bao nhiêu phần trăm.

Nhược điểm
    Accuracy dễ gây hiểu lầm khi dữ liệu mất cân bằng.

    Ví dụ:
        - 99 email bình thường
        - 1 email spam
        
        Mô hình đoán tất cả là "không spam":
            Accuracy = 99%

        Nhưng thực tế không phát hiện được spam nào.
```
**Fomula**
```bash
Accuracy = (TP + TN)/(TP + TNN + FP + FN)
```
**Ex**
```bash

Accuracy= (80+90)/(80+90+10+20) = 170/200 = 85%
=> Mô hình dự đoán đúng 85% tổng số email.
```
## Precision (Độ chính xác của dự đoán dương tính)
```bash
Precision (độ chính xác) trả lời câu hỏi:
    + Trong những gì mô hình dự đoán là đúng (positive), thì bao nhiêu cái thực sự đúng?
    => Đo độ “chắc chắn” của mô hình khi dự đoán positive

Ý nghĩa
    Mô hình nói "Spam" 90 lần:
        - Đúng 80 lần
        - Sai 10 lần
    => Độ tin cậy của dự đoán Spam là 88.9%.

Khi nào quan trọng?
    Khi FP rất tệ.

    Ví dụ:
        - Chẩn đoán ung thư
        - Chặn tài khoản người dùng
        - Đánh dấu giao dịch gian lận
    => Bạn không muốn tố nhầm người vô tội.
```
**Fomula**
```bash
Precision = TP / (TP + FP)
```
**Ex**
```bash
Model nói 100 email là spam. Nhưng chỉ 80 cái thật sự là spam
    Precision = 80/100 = 0.8
        Nghĩa là: model không đoán bừa nhiều
```
## Recall (độ bao phủ)
```bash
Recall trả lời câu hỏi:
    + Trong tất cả những cái thực sự là positive, mô hình bắt được bao nhiêu?
    + Công thức: Recall = TP / (TP + FN)
    + Đo khả năng không bỏ sót

Ý nghĩa
    Có 100 email Spam thật:
        - Tìm được 80
        - Bỏ sót 20
    => Recall = 80%.

Khi nào quan trọng?
    Khi FN rất tệ.

    Ví dụ:
        - Phát hiện ung thư
        - Phát hiện cháy
        - Phát hiện gian lận
    => Bỏ sót một trường hợp nguy hiểm còn tệ hơn báo động nhầm.
```
**Ex: Recall**
```bash
- Có 100 email spam thật
- Model chỉ phát hiện được 80 → Recall = 80/100 = 0.8
→ Nghĩa là: model không bỏ sót nhiều
```
**Khi nào dùng cái nào Recall, Precision**
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
## F1-Score (Trung bình điều hòa giữa Precision và Recall)
**Fomula**
```bash
F1 = 2×(Precision*Recall)/(Precision+Recall)
```
## Binary Cross-Entropy (Log Loss) (hàm mất mát (loss function) phổ biến nhất cho bài toán phân loại nhị phân (0 hoặc 1))
**Fomula**
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
### Demo về công thức BCE bằng math
```python
import math

def bce(y, y_hat):
    return -(y*math.log(y_hat) + (1-y)*math.log(1-y_hat))

print(bce(1, 0.9))
print(bce(1, 0.1))
```
## Categorical Cross Entropy (dùng cho bài toán phân loại nhiều lớp (multi-class classification))
```bash
Là hàm mất mát (loss function) trong đó mỗi mẫu chỉ thuộc đúng 1 lớp.
    Ví dụ:
        Ảnh con vật:
            🐱 Mèo
            🐶 Chó
            🐦 Chim
        Một ảnh chỉ có thể là một trong ba lớp.

Dùng khi nào?
    - Có từ 3 lớp trở lên.
    - Mỗi mẫu chỉ thuộc 1 lớp duy nhất.
    - Output dùng Softmax.

    Ví dụ:
        - Nhận diện chữ số 0–9
        - Phân loại mèo/chó/chim
        - Phân loại cảm xúc: vui/buồn/tức giận
```
**Fomula**
```bash
Loss= −∑yilog⁡(pi)

- C: số lớp
- yi​: nhãn thật (one-hot)
- pi​: xác suất dự đoán
```
## Sparse Categorical Cross-Entropy (SCCE) (hàm loss dùng cho bài toán phân loại nhiều lớp (multi-class classification))
```bash
Dùng khi label được lưu dưới dạng số nguyên thay vì one-hot.

Ví dụ:
    Có 3 lớp: Cat, Dog, Bird
    
    Label là:
        - Cat  = 0
        - Dog  = 1
        - Bird = 2
```
**Fomula**
```bash
Loss = -log(P(lớp đúng))
```
## ROC-AUC và PR-AUC 
```bash
là hai cách đánh giá mô hình phân loại nhị phân, đặc biệt khi mô hình trả về xác suất thay vì chỉ trả lời Có/Không.

Trước tiên: tại sao cần ROC và PR?

Giả sử mô hình dự đoán:

A: 0.99
B: 0.90
C: 0.80
D: 0.60
E: 0.20

Nếu đặt ngưỡng (threshold) là 0.5:

>= 0.5 → Positive
< 0.5 → Negative

thì A, B, C, D là Positive.

Nhưng nếu đổi threshold thành 0.8:

>= 0.8 → Positive

thì chỉ còn A, B, C là Positive.

=> Precision và Recall sẽ thay đổi theo threshold.

ROC-AUC và PR-AUC đánh giá mô hình trên mọi threshold, không phụ thuộc vào việc bạn chọn 0.5 hay 0.8.

1. ROC Curve

ROC vẽ:

Trục X = FPR (False Positive Rate)
Trục Y = TPR (Recall)
FPR
FPR=
FP+TN
FP
	​


Ý nghĩa:

Trong số người vô tội, bắt nhầm bao nhiêu phần trăm?

TPR
TPR=Recall

Ý nghĩa:

Trong số tội phạm thật, bắt được bao nhiêu phần trăm?

Ví dụ cảnh sát

Có:

100 tội phạm
900 người vô tội

Mô hình:

Bắt được 90 tội phạm
Bắt nhầm 90 người vô tội

Ta có:

TPR = 90/100 = 90%
FPR = 90/900 = 10%

Điểm ROC sẽ là:

(0.1, 0.9)
ROC-AUC là gì?

AUC = Area Under Curve.

AUC = 1 → hoàn hảo
AUC = 0.5 → đoán ngẫu nhiên
AUC < 0.5 → tệ hơn random
Cách hiểu trực quan

ROC-AUC =

Xác suất mô hình xếp một Positive thật cao hơn một Negative thật.

Ví dụ:

Spam:      0.9
Không spam:0.3

→ đúng.

Nếu hầu hết Positive đều được xếp điểm cao hơn Negative:

ROC-AUC ≈ 1
2. PR Curve

PR = Precision-Recall.

Vẽ:

Trục X = Recall
Trục Y = Precision
Ví dụ

Có:

1000 email

990 email thường
10 email spam

Mô hình tìm được:

TP = 8
FP = 2
FN = 2

Ta có:

Precision = 8/(8+2)=80%
Recall    = 8/(8+2)=80%

Điểm trên PR Curve là:

(Recall=0.8, Precision=0.8)
PR-AUC là gì?

Diện tích dưới đường Precision-Recall.

Nó trả lời:

Khi cố gắng tăng Recall, Precision bị giảm bao nhiêu?

PR-AUC càng lớn càng tốt.

Khi nào dùng ROC-AUC?
Dữ liệu cân bằng

Ví dụ:

500 mèo
500 chó

hoặc

45% gian lận
55% không gian lận

ROC-AUC hoạt động rất tốt.

Khi nào dùng PR-AUC?
Dữ liệu mất cân bằng mạnh

Ví dụ:

9990 người bình thường
10 người bị bệnh

hoặc

99999 giao dịch bình thường
1 giao dịch gian lận

Lúc này PR-AUC đáng tin hơn.

Tại sao ROC có thể "đánh lừa" bạn?

Giả sử:

10000 người

9990 bình thường
10 bệnh

Mô hình:

TP = 8
FP = 100

Nhìn qua:

Recall = 80%

Rất ngon.

ROC:

FPR = 100 / 9990
    ≈ 1%

FPR rất nhỏ.

=> ROC-AUC có thể vẫn rất cao.

Nhưng thực tế:

Precision = 8 / (8+100)
          = 7.4%

Tức là:

Cứ báo có bệnh thì 92.6% là báo nhầm.

Đây là thảm họa.

PR-AUC sẽ phản ánh điều này ngay lập tức.

Mẹo nhớ cực nhanh
ROC-AUC

Quan tâm:

Mô hình có phân biệt được 2 lớp không?

Positive đứng trên Negative bao nhiêu?

Phù hợp khi dữ liệu tương đối cân bằng.

PR-AUC

Quan tâm:

Những gì tôi bắt được có đáng tin không?

Precision ↔ Recall

Phù hợp khi Positive rất hiếm.
```
# Optimizer (thuật toán tối ưu)
## SGD (Stochastic Gradient Descent)
```bash
Ý tưởng:
    - Sai ở đâu → sửa ở đó.
    - Mỗi bước chỉ đi theo hướng gradient hiện tại.

Ví dụ:
    Bạn đang leo núi trong sương mù để xuống thung lũng.SGD:- Nhìn dưới chân- Thấy dốc hướng nào thì đi hướng đó
    
    Ưu điểm
        - Đơn giản
        - Ít tốn RAM
        - Generalization thường tốt

    Nhược điểm
        - Học chậm
        - Dễ bị rung lắc
        - Có thể mắc kẹt ở local minimum
```
**Fomula**
```bash
W = W - learning_rate × gradient
```
## Momentum (SGD + quán tính)
**Ex**
```bash
- SGD = đi bộ
- Momentum = đẩy quả bóng
    Nếu nhiều bước liên tiếp cùng hướng:
        → đi nhanh hơn

    Nếu gặp chỗ lồi lõm nhỏ:
        → vẫn lăn qua được
    
    Ưu điểm
        - Nhanh hơn SGD
        - Ít rung hơn

    Nhược điểm
        - Vẫn phải tự chọn learning rate khá cẩn thận
```
## RMSprop
```bash
Vấn đề:
    - Một số trọng số cần update mạnh
    - Một số trọng số cần update nhẹ

RMSprop tự điều chỉnh learning rate cho từng trọng số.
    Ví dụ:
        - Weight A: gradient lớn → giảm tốc
        - Weight B:gradient nhỏ→ tăng tốc
    
    Ưu điểm
        - Hội tụ nhanh hơn SGD
        - Tốt cho dữ liệu phức tạp

    Nhược điểm
        - Có nhiều hyperparameter hơn
```
## Adam (Momentum+RMSprop)
```bash
Nó vừa:
    - nhớ hướng di chuyển trước đó
    - tự điều chỉnh learning rate
    - Nên thường:
        + Nhanh
        + Ổn định
        + Dễ dùng
=> Đây là optimizer phổ biến nhất hiện nay.

Ưu điểm
    - Train nhanh
    - Ít phải tuning
    - Hoạt động tốt trong đa số bài toán

Nhược điểm
    - Đôi khi generalization kém hơn SGD một chút
```
## AdamW (Adam nhưng sửa lỗi lớn nhất của Adam)
```bash
Weight Decay (L2 Regularization)
Adam gốc xử lý Weight Decay chưa chuẩn.
AdamW tách riêng:
Gradient UpdatevàWeight Decay
nên:


Regularization tốt hơn


Ít overfit hơn


Accuracy cuối thường cao hơn

thì phần lớn các mô hình Transformer/LLM hiện đại đều train bằng AdamW hoặc các biến thể của AdamW.
Quy tắc thực tế:
Mới học Deep Learning:→ AdamLàm project thật:→ AdamWNghiên cứu tối ưu accuracy cuối:→ SGD + Momentum hoặc AdamW
AdamW hiện là lựa chọn mặc định cho đa số mô hình production hiện đại.
```
**So sánh các kĩ thuật**
```bash
Optimizer   Accuracy    SGD             Momentum    RMSprop     Adam        AdamW
Tốc độ học  cuối        Chậm            Trung bình  Tốt         Rất tốt     Thường tốt nhất
Độ ổn định  Trung bình  Thường rất tốt  Tốt         NhanhTốt    Rất nhanh   Rất nhanh
```
# Learning rate (tối ưu learning rate)
```bash
Đây là một trong những khái niệm rất quan trọng khi train Deep Learning.

Hãy tưởng tượng Bạn đang đi xuống núi trong sương mù để tìm điểm thấp nhất.
    - Learning Rate (LR) = độ dài mỗi bước chân.
    - Loss Function = độ cao của ngọn núi.

    LR quá lớn
        Bước dài 10m    
              ↓
           X
              ↓
                 X
              ↓
           X
    => Bạn nhảy qua nhảy lại và có thể không bao giờ tới đáy

    LR quá nhỏ
        Bước dài 1cm
            X
             X
              X
               X
    => Tới đáy được nhưng mất rất nhiều thời gian

Vấn đề
    Khi mới train:
        - Loss = 10
            Ta muốn đi nhanh: lr = 0.001
            
        - Loss = 0.2: Nhưng khi đã gần tối ưu
            Nếu vẫn bước lớn: lr = 0.001 => thì model cứ dao động quanh điểm tối ưu.
                Giống như:

                      đáy
                       ▼

                   X
                       X
                  X
        => Không dừng chính xác được.
```
## Learning Rate Scheduler (cơ chế tự động điều chỉnh learning rate)
```bash
Ý tưởng: Ban đầu đi nhanh, gần đích thì đi chậm lại.
```
### Cosine Annealing (LR giảm từ từ theo đường cong cosine)
```bash
Đây là scheduler cực phổ biến cho:
    - GPT
    - BERT
    - LLaMA
    - ViT
```
**Ex**
```bash
Epoch 1 : LR = 0.001
Epoch 20: LR = 0.0008
Epoch 40: LR = 0.0004
Epoch 60: LR = 0.0001
Epoch 80: LR = 0.00001

Ban đầu => Bước dài
Cuối: => Bước rất ngắn
=> model fine-tune rất kỹ.
```
### ReduceLROnPlateau (giảm lr khi model bị kẹt)
**Ex**
```bash
Epoch 1  Loss=1.2
Epoch 2  Loss=0.9
Epoch 3  Loss=0.7
Epoch 4  Loss=0.5
Epoch 5  Loss=0.49
Epoch 6  Loss=0.49
Epoch 7  Loss=0.49
Epoch 8  Loss=0.49

=> Model bị "kẹt". Lúc này scheduler nói:
    "Giảm learning rate đi."
```
### StepLR (Cứ N epoch giảm)
### OneCycleLR (Tăng rồi giảm)
### Warmup + Cosine (Tăng nhẹ rồi giảm dần)
```bash
Trong production hiện nay Nếu bạn train:
    - LLM
    - Transformer
    - RAG Embedding Model
    - Fine-tune Gemini/Llama
thường thấy:
    Warmup   
    ↓
    Cosine Annealing

Ví dụ:
    0 → 5% số bước:
        LR tăng dần 
    5% → 100%:
        LR giảm theo Cosine
=> Đây gần như là cấu hình mặc định cho rất nhiều mô hình hiện đại của Google Research, Meta AI và Hugging Face Transformers.
```