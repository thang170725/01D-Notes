- [Elastic Net Regression Introduction (là một biến thể của hồi quy tuyến tính có thêm regularization. Nó kết hợp hai loại regularization)](#elastic-net-regression-introduction-là-một-biến-thể-của-hồi-quy-tuyến-tính-có-thêm-regularization-nó-kết-hợp-hai-loại-regularization)
- [Ask](#ask)
  - [Tại sao không dùng Lasso luôn?](#tại-sao-không-dùng-lasso-luôn)
---
# Elastic Net Regression Introduction (là một biến thể của hồi quy tuyến tính có thêm regularization. Nó kết hợp hai loại regularization)
[Regularization là gì?](../../../../04-Evaluate-Optimize/Accuracy_Optimization.md#regularization-chống-overfitting)

```bash
Elastic Net = Lasso + Ridge
             Elastic Net
                 │
      ┌──────────┴──────────┐
      ↓                     ↓
    L1/Lasso              L2/Ridge
      │                     │
chọn feature          ổn định model
coefficient = 0       giảm coefficient

- alpha = 1 → gần như Lasso
- alpha = 0 → Ridge
- 0 < alpha < 1 → Elastic Net
```
Khi nào nên dùng Elastic Net?

Một rule khá thực tế:

Dùng Linear Regression khi
ít feature
+
feature không quá tương quan
+
ít nguy cơ overfitting
Dùng Ridge khi
nhiều feature
+
feature tương quan
+
muốn giữ tất cả feature

Ví dụ:

1000 features
→ hầu hết đều có một chút thông tin
→ không muốn loại bỏ feature

Ridge thường phù hợp.

Dùng Lasso khi
rất nhiều feature
+
nghi ngờ nhiều feature không quan trọng
+
muốn feature selection

Ví dụ:

10,000 features
        ↓
Lasso
        ↓
9,000 coefficient = 0
1,000 coefficient ≠ 0
Dùng Elastic Net khi

Đây là trường hợp rất đáng nhớ:

nhiều feature
+
có feature tương quan với nhau
+
muốn feature selection

Ví dụ:

10,000 features
        ↓
nhiều nhóm feature tương quan
        ↓
Elastic Net
        ↓
shrink coefficient
+
có thể loại bỏ feature
+
xử lý correlation tốt hơn Lasso
1. Ví dụ thực tế

Giả sử bạn làm bài toán dự đoán giá nhà và có 5,000 feature:

x1  diện tích
x2  số phòng
x3  diện tích phòng khách
x4  diện tích phòng ngủ
...
x5000 ...

Có rất nhiều feature tương quan:

x1 ←→ x3
x1 ←→ x4
x3 ←→ x4

Bạn không muốn model:

coefficient của tất cả 5000 feature đều lớn

vì dễ overfit.

Bạn có thể dùng:

from sklearn.linear_model import ElasticNet
from sklearn.preprocessing import StandardScaler
from sklearn.pipeline import make_pipeline

model = make_pipeline(
    StandardScaler(),
    ElasticNet(alpha=0.1, l1_ratio=0.5)
)

model.fit(X_train, y_train)

Elastic Net sẽ vừa:

shrink coefficient
loại bỏ một số feature
xử lý tốt hơn trường hợp các feature tương quan
7. Một điểm rất quan trọng: phải scale feature

Với Elastic Net, thường nên:

StandardScaler
      ↓
ElasticNet

Ví dụ:

age:        20 ~ 80
salary:     5,000 ~ 100,000,000
population: 1 ~ 10,000,000

Nếu không scale, penalty có thể tác động không công bằng giữa các feature.

Do đó thường dùng:

Pipeline([
    ("scaler", StandardScaler()),
    ("model", ElasticNet())
])
8. alpha và l1_ratio hiểu thế nào?

Đây cũng là phần rất quan trọng.

alpha

Điều khiển mức độ regularization.

alpha nhỏ
    ↓
ít regularization
    ↓
gần Linear Regression

Ngược lại:

alpha lớn
    ↓
regularization mạnh
    ↓
coefficient bị shrink mạnh
l1_ratio

Điều khiển:

L1 ←────────────→ L2

Ví dụ:

l1_ratio = 1.0
→ Lasso

l1_ratio = 0.0
→ Ridge

l1_ratio = 0.5
→ 50% L1 + 50% L2

Thường không nên tự đoán alpha và l1_ratio, mà tune bằng cross-validation.

Ví dụ:

from sklearn.linear_model import ElasticNetCV

model = ElasticNetCV(
    alphas=[0.001, 0.01, 0.1, 1],
    l1_ratio=[0.1, 0.5, 0.7, 0.9, 1.0],
    cv=5
)

Model sẽ tìm combination tốt hơn dựa trên cross-validation.

9. Cách nhớ cực nhanh

Bạn có thể nhớ bảng này:

Model	L1	L2	Feature selection	Correlated features
Linear Regression	❌	❌	❌	Không tốt lắm
Ridge	❌	✅	❌	✅
Lasso	✅	❌	✅	Có thể không ổn định
Elastic Net	✅	✅	✅	✅
Một câu để nhớ:

Ridge giữ feature nhưng làm chúng nhỏ đi.
Lasso có thể vứt feature đi.
Elastic Net vừa có thể vứt feature đi, vừa ổn định hơn Lasso khi feature tương quan.

Nếu bạn đang học ML theo hướng hiểu bản chất, thì Elastic Net rất đáng học sau Linear Regression → Ridge/Lasso, vì từ nó bạn sẽ thấy rõ regularization thực sự đang giải quyết vấn đề gì, chứ không chỉ nhớ công thức.
# Ask
## Tại sao không dùng Lasso luôn?
```bash
Giả sử dataset có:
    - x1 = chiều cao
    - x2 = cân nặng
    - x3 = BMI
    - x4 = tuổi
    - x5 = thu nhập

Có thể:
    - x1 và x2 tương quan rất mạnh
    - x2 và x3 tương quan rất mạnh

Lasso đôi khi có xu hướng chọn một feature và loại feature tương quan còn lại:
    - height → 0.0
    - weight → 2.7
    - BMI    → 0.0

Trong khi Elastic Net có thể giữ nhiều feature liên quan:
    - height → 0.8
    - weight → 1.1
    - BMI    → 0.6
```