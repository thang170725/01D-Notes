- [.LGBMRegressor() (Dùng cho regression)](#lgbmregressor-dùng-cho-regression)
- [LGBMClassifier()](#lgbmclassifier)
  - [.fit()](#fit)
  - [.predict()](#predict)
---
# .LGBMRegressor() (Dùng cho regression)
**Syn**
```bash
model = lgb.LGBMRegressor(
    objective="regression"
    n_estimators=100,
    learning_rate=0.1,
    max_depth=-1,
    num_leaves=31,
    subsample=0.8,
    colsample_bytree=0.8,
    random_state=42,
    verbosity=-1
)

- Input:
    + objective     : xác định loại bài toán
        - 'regression'  : dự đoán hồi quy
    + n_estimators  : Số cây 
        - mỗi cây = 1 "bước học"
        - càng nhiều -> model càng mạnh nhưng dễ overfitting
        - thường: 100 -> 1000      
    + learning_rate : Tốc độ học
        - nhỏ   : học chậm nhưng ổn định
        - lớn   : học nhanh nhưng dễ sai
    + max_depth     : Giới hạn độ sâu của cây
    + num_leaves    : Số lượng lá tối đa của mỗi cây (tree)
        - Càng lớn → model càng phức tạp, học được pattern chi tiết hơn
            + Nhưng dễ overfit
            💡 Quy tắc quan trọng: num_leaves <= 2^(max_depth) (dù LightGBM không bắt buộc max_depth, nhưng vẫn nên nhớ quan hệ này)
        - Khoảng nên thử:
            + Nhỏ: 15 – 31 → an toàn, ít overfit
            + Trung bình: 31 – 127 → phổ biến nhất
            + Lớn: 127 – 255+ → khi dữ liệu rất lớn
        👉 Thực tế:
            + Dataset nhỏ → giữ ~31
            + Dataset lớn → tăng dần
    + subsample: Tỷ lệ sample (row) dùng cho mỗi cây
        - < 1 → mỗi cây chỉ học trên một phần dữ liệu → giảm overfitting
        - = 1 → dùng toàn bộ dữ liệu
        - Khoảng nên thử: 0.6 – 1.0 👉 Thực tế: 0.7 – 0.9 là sweet spot
        - nếu overfit → giảm xuống (0.6–0.8)
    + colsample_bytree: Tỷ lệ feature dùng cho mỗi cây
        - giống Random Forest: mỗi cây chỉ nhìn một phần feature giúp:
            + giảm overfit
            + tăng diversity
        - Khoảng nên thử: 0.6 – 1.0 👉 Thực tế: 0.7 – 0.9 thường tốt
        - nhiều feature → nên giảm
    + random_state: Seed để kết quả reproducible
        - Không ảnh hưởng đến performance trực tiếp
        - Chỉ giúp:
            + debug dễ hơn
            + chạy lại ra cùng kết quả
        - Thực tế: random_state=42  # standard luôn 😄 👉 Bạn có thể đổi số khác, không quan trọng
    + n_jobs: Số core CPU dùng để train
        - -1 → dùng toàn bộ CPU
        - số dương → giới hạn số core
        - Thực tế:
            + Local machine → -1
            + Server shared → set cụ thể (vd: 4, 8)
    + verbosity: điều khiển mức độ log (thông báo) được in ra trong quá trình train. Nó không ảnh hưởng đến chất lượng mô hình chỉ ảnh hưởng đến lượng thông tin hiển thị trên terminal.
        - -1    : Không in bất kỳ warning/info nào (silent mode). Đây là giá trị được dùng nhiều nhất.
        - 0	    : Chỉ in các lỗi (Error).
        - 1	    : In warning.
        - >1	: In thêm nhiều thông tin debug và quá trình train.
```
# LGBMClassifier()
```bash
- Dùng cho bài toán classifier
- Có các hàm tương tự như LGBMRegressor:
    + [fit](#fit)
    + [predict](#predict)
```
```bash
clf=lgb.LGBMClassifier(
    n_estimators=200,
    num_leaves=31
)
```
## .fit()
```bash
model.fit(X_train,y_train)

- Input:
    + X_train -> features
    + y_train -> target
```
## .predict()
```bash
pred=model.predict(X_test)

- Output: numpy array predictions
```
