- [Overfitting \& Underfitting](#overfitting--underfitting)
- [Vanishing Gradient \& Exploding Gradient](#vanishing-gradient--exploding-gradient)
- [Precision \& Recall](#precision--recall)
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