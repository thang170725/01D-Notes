# Introduction
```bash
- Ridge Regression là phiên bản của Linear Regression có thêm một cơ chế phạt (regularization) để tránh mô hình học thuộc dữ liệu (overfitting).
    1. Linear Regression bình thường
        y_pred = w1x1 + w2x2+ ⋯ + wnxn + b -> Mục tiêu là tìm www sao cho lỗi nhỏ nhất.
        Loss thường dùng là MSE = 1/N . ∑(y_truei − y_predi)**2

        Vấn đề của Linear Regression
            - Giả sử dữ liệu có nhiễu
            - Hai feature gần như giống nhau.
            - Linear Regression có thể học:
                + w1=1000w_1=1000w1​=1000
                + w2=−998w_2=-998w2​=−998
            Dự đoán vẫn đúng. Nhưng trọng số rất lớn. Mô hình trở nên không ổn định.
            
        2. Ý tưởng của Ridge. Không chỉ tối thiểu lỗi dự đoán, mà còn phải giữ trọng số nhỏ.
            - Thêm một khoản phạt: w1**2 + w2**2 + ⋯ + wn**2
            - Loss mới:
                J = 1/N . ∑(y_truei−y_predi)**2 + λ.∑wj**2
                    Trong đó:
                        + phần đầu = lỗi dự đoán
                        + phần sau = hình phạt trọng số lớn
                        + Vai trò của λ (lambda) # quyết định mức độ phạt.
                            λ = 0
                                J = MSE => Chính là Linear Regression.
                            λ nhỏ
                                λ=0.01 => Phạt nhẹ.
                            λ lớn
                                λ=100 => Phạt rất mạnh. Các trọng số bị kéo về gần 0.
```