Overfitting & Underfitting
Overfitting xảy ra khi mô hình học quá kỹ dữ liệu huấn luyện -> mất khả năng tổng quát với dữ liệu mới. Biểu hiện là accuracy trên tập huấn luyện rất cao còn trên tập test lại thấp.
Cách xử lý:
    • Thêm dữ liệu huấn luyện
    • Giảm độ phức tạp của mô hình
    • Regularization - phạt mô hình quá phức tạp
    • Early stopping cho mạng nơ ron
    • Dropout cho deep learning
    • Cross-validation (đánh giá mô hình nhiều lần với nhiều cách chia tập train/test khác nhau để tránh ăn may.
Underfitting xảy ra khi mô hình quá đơn giản hoặc thiếu dữ liệu, không thể học ra quy luật dẫn đến hiệu suất kém.

Vanishing Gradient (Gradient biến mất) & Exploding Gradient (Gradient bùng nổ)

Vanishing
Exploding