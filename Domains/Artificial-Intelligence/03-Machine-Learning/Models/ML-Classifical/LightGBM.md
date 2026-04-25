- [Introduction](#introduction)
  - [GOSS (Graduent-based One-Side Sampling)](#goss-graduent-based-one-side-sampling)
- [Practices](#practices)
  - [Demo Pipeline của LightGBM bằng ý tưởng](#demo-pipeline-của-lightgbm-bằng-ý-tưởng)
---
# Introduction 
- LightGBM (Light Gradient Boosting Machine) là một model machine learning. Cụ thể hơn nó là dạng ensemble model (kết hợp nhiều mô hình nhỏ)
- Nó cùng “họ” XGBoost, CatBoost và được huấn luyện theo các **[boosting](./Base.md#Boosting)**

**Lịch sử ra đời**
```bash
- Do Microsoft phát triển bắt đầu khoảng từ năm 2016
- Paper chính công bố năm 2017 tại NeurIPS
```
**Paper nên đọc**
```bash
1. “LightGBM: A Highly Efficient Gradient Boosting Decision Tree” (2017)
```
**LightGBM ra đời để giải quyết vấn đề gì?**
```bash
- Trước LightGBM đã có:
    + Gradient Boosting (cổ điển)
    + XGBoost (rất nổi tiếng)
- Nhưng vấn đề:
    ❌ Train chậm
    ❌ Dataset lớn là “toang”
    ❌ Feature nhiều → cực kỳ tốn tài nguyên
→ LightGBM được tạo ra để:
    🚀 train nhanh hơn
    💾 ít tốn RAM hơn
    📊 scale được dữ liệu lớn
```
**So sánh Decision Tree, Random Forest, LightGBM**
```bash
| Loại     | Ví dụ         | Ý tưởng                             |
| -------- | ------------- | ----------------------------------- |
| Tree đơn | Decision Tree | 1 cây duy nhất                      |
| Ensemble | Random Forest | nhiều cây, train độc lập            |
| Boosting | **LightGBM**  | nhiều cây, train tuần tự để sửa lỗi |
```
**LightGBM khác XGBoost ở điểm nào?**
```bash
1. Cách xây cây
    - XGBoost: grow theo level-wise (từng tầng một)
    - LightGBM: grow theo leaf-wise (chọn leaf có gain lớn nhất để tách tiếp)
        + Leaf-wise thường:
            - Giảm loss nhanh hơn
            - Có thể chính xác hơn
            - Nhưng dễ overfit nếu dataset nhỏ
2. Tốc độ
    - LightGBM: Dùng histogram-based algorithm. Thường train nhanh hơn XGBoost. Tốn ít memory hơn
```
**Ý tưởng cốt lõi của model LightGBM**
```bash
Giả sử:
    - Model đầu tiên dự đoán sai nhiều
    - Model thứ 2 học lỗi của model 1
    - Model thứ 3 học tiếp lỗi
    => Cứ thế cộng dồn lại → model mạnh dần => Đây gọi là Gradient Boosting
```
## GOSS (Graduent-based One-Side Sampling)
```bash
👉 GOSS = cách lấy mẫu dữ liệu thông minh trong LightGBM
- Thay vì dùng toàn bộ data, nó:
    + Giữ lại những điểm có gradient lớn (quan trọng)
    + Lấy ngẫu nhiên một phần gradient nhỏ (ít quan trọng)
➡️ Giảm data nhưng vẫn giữ thông tin chính
- Gradient = “mức độ sai”
    + |gradient| lớn → model đang dự đoán rất sai → rất quan trọng
    + |gradient| nhỏ → model dự đoán gần đúng → ít quan trọng
    👉 Ý tưởng: Không cần học lại những điểm đã gần đúng
```
**Ex**
```bash
Giả sử bạn có 8 sample:
| ID | y   | y_pred | gradient = y - y_pred |
| -- | --- | ------ | --------------------- |
| 1  | 100 | 130    | -30                   |
| 2  | 120 | 130    | -10                   |
| 3  | 150 | 130    | +20                   |
| 4  | 170 | 130    | +40                   |
| 5  | 140 | 130    | +10                   |
| 6  | 135 | 130    | +5                    |
| 7  | 128 | 130    | -2                    |
| 8  | 132 | 130    | +2                    |
```
```bash
⚡ Bước 1: Chọn top gradient lớn
    - Giả sử: Giữ top 50% gradient lớn nhất 👉 Sắp xếp theo |gradient|:
        | ID | gradient | |gradient| |
        |----|----------|------------|
        | 4  | +40      | 40         |
        | 1  | -30      | 30         |
        | 3  | +20      | 20         |
        | 2  | -10      | 10         |
        | ...| ...      | ...        |
        👉 Lấy 4 điểm lớn nhất: ID: 4, 1, 3, 2
🎲 Bước 2: Sample phần còn lại
    - Phần còn lại: ID: 5, 6, 7, 8 👉 Lấy ngẫu nhiên 50%: ID: 5, 7
    - 📦 Dataset sau GOSS Final data: 4, 1, 3, 2, 5, 7
    👉 Tức là:
        + Không dùng toàn bộ data
        + Nhưng vẫn giữ:
        + tất cả điểm quan trọng
        + một ít điểm “ít quan trọng”
    - ⚠️ Vấn đề: bị lệch phân phối
        + Nếu bạn dừng ở đây → sai ❌ Vì:
            - Bạn giữ nhiều điểm gradient lớn
            - Ít điểm gradient nhỏ
            ➡️ Dataset bị bias
Bước 3: Re-weight (cực quan trọng)
    - LightGBM sẽ tăng trọng số cho phần sample nhỏ
    👉 Ví dụ bạn giữ:
        + 100% gradient lớn
        + 50% gradient nhỏ
        ➡️ thì: các điểm gradient nhỏ sẽ được nhân weight ≈ 2
🌳 Bước 4: Dùng data này để build tree
    - LightGBM sẽ:
        + tính histogram
        + split
        + grow tree
    👉 Nhưng chỉ trên subset data đã chọn
```
**Dataset**
```bash
1. https://archive.ics.uci.edu/dataset/321/electricityloaddiagrams20112014
```
# Practices
## Demo Pipeline của LightGBM bằng ý tưởng
```bash
Bài toán dự đoán giá nhà (regression)

Dataset đơn giản:
| ID | Diện tích (m²) | Số phòng | Giá thật (y) |
| -- | -------------- | -------- | ------------ |
| 1  | 50             | 2        | 100          |
| 2  | 60             | 2        | 120          |
| 3  | 70             | 3        | 150          |
| 4  | 80             | 3        | 170          |
```
```bash
Bước 0: Khởi tạo model (LightGBM bắt đầu bằng 1 dự đoán ban đầu)
    - y_pred0 = (100+120+150+170)/4=135
    - Tất cả sample ban đầu: y_pred = [135, 135, 135, 135]
Bước 1: Tính gradient (residual)
    - Với regression (loss = MSE): gradient = y - y_pred
    - Ta có:
        | ID | y   | y_pred | gradient |
        | -- | --- | ------ | -------- |
        | 1  | 100 | 135    | -35      |
        | 2  | 120 | 135    | -15      |
        | 3  | 150 | 135    | +15      |
        | 4  | 170 | 135    | +35      |
        + âm → dự đoán quá cao
        + dương → dự đoán quá thấp
Bước 2: GOSS (LightGBM đặc biệt)
    - Giả sử: 
        + giữ top gradient lớn: 35, -35
        + sample thêm 1 điểm nhỏ: -15
    ➡️ Data dùng để train tree: ID: 1, 2, 4
    💡 Đây là cách LightGBM giảm data nhưng vẫn giữ thông tin quan trọng.
Bước 3: Build tree (Histogram-based) → "Diện tích <= bao nhiêu thì chia tốt nhất"
    Dataset (nhắc lại):
        | ID | Diện tích | gradient |
        | -- | --------- | -------- |
        | 1  | 50        | -35      |
        | 2  | 60        | -15      |
        | 3  | 70        | +15      |
        | 4  | 80        | +35      |
    ⚡ 3.1 Binning feature
        - Thay vì giữ giá trị thật: 50, 60, 70, 80. LightGBM chia thành bin:   
            | Bin | Range |
            | --- | ----- |
            | B1  | <=60  |
            | B2  | >60   |
            + LightGBM dùng quantile-based binning để chia bin
                - Hiểu đơn giản
                    + Nó cố gắng chia sao cho: mỗi bin có số lượng data gần bằng nhau
                    + 📊 Ví dụ: Giả sử feature “diện tích”: [50, 60, 70, 80, 90, 100]. Bạn muốn chia 3 bin:
                        👉 LightGBM sẽ sort: [50, 60, 70, 80, 90, 100]
                        👉 chia đều:
                            Bin	Range
                            B1	50–60
                            B2	70–80
                            B3	90–100
                        💡 Đây gọi là quantile binning
                ⚠️ Nhưng thực tế còn tinh vi hơn
                    + LightGBM không làm naive như trên, nó dùng:
                        - approximate quantile (rất nhanh)
                    👉 vì:
                        dataset có thể hàng triệu dòng
                        không thể sort full mỗi lần
                🔥 Một twist quan trọng 👉 LightGBM KHÔNG chỉ dựa vào feature. Nó còn tối ưu cho: gradient distribution ➡️ nghĩa là: bin nào có gradient “khác biệt” sẽ được giữ rõ hơn
        - Mapping:
            | ID | Diện tích | Bin |
            | -- | --------- | --- |
            | 1  | 50        | B1  |
            | 2  | 60        | B1  |
            | 3  | 70        | B2  |
            | 4  | 80        | B2  |
        💡 Ý nghĩa:
            - Giảm số lượng giá trị cần xét
            - Tăng tốc cực mạnh
    3.2 Gom gradient theo bin
        | Bin | Samples | Tổng gradient     |
        | --- | ------- | ----------------- |
        | B1  | ID 1,2  | -35 + (-15) = -50 |
        | B2  | ID 3,4  | +15 + 35 = +50    |
        - (LightGBM thật còn có Hessian H). Với MSE: Hessian ≈ 1 cho mỗi điểm 👉 nên:
            | Bin | H (số mẫu) |
            | --- | ---------- |
            | B1  | 2          |
            | B2  | 2          |
    3.3 Tìm điểm để split tốt nhất
        - Vì có 2 bin → chỉ có 1 cách split: Split tại: <=60
        - Công thức Gain (đơn giản hóa): Gain = GL**2/HL + GR**2/HR
            + GL: tổng gradient bên trái
            + HL: tổng hessian bên trái
        - Thay số vào
            + Left (B1): GL = −50, HL = 2
            + Right (B2): GR = 50, HR = 2
        - Tính: Gain=(−50)^2/2+(50)^2/2 = 2500/2+2500/2 =1250+1250=2500
            👉 Nếu:
                + bên trái toàn gradient âm
                + bên phải toàn gradient dương
            ➡️ nghĩa là: model đang sai theo 2 hướng hoàn toàn khác nhau 👉 Split này RẤT TỐT (Gain càng lớn càng tốt)
Bước 4: Leaf-wise growth
    - LightGBM chọn leaf có gain lớn nhất để split tiếp
    - Ở đây đơn giản:
        Root
         ├── Leaf 1 (<=60)
         └── Leaf 2 (>60)
Bước 5: Tính output cho mỗi leaf
    - Công thức: leaf_value = (∑gradient)/(số mẫu)
        + Leaf 1 (ID 1,2): (−35−15)/2=−25
        + Leaf 2 (ID 4): 35/1=35
Bước 6: Update prediction
    - Giả sử learning rate = 0.1
    - Update:
        ID	y_pred_cũ	leaf	update	y_pred_mới
        1	135	        Leaf1	-2.5	132.5
        2	135	        Leaf1	-2.5	132.5
        3	135	        Leaf2	+3.5	138.5
        4	135	        Leaf2	+3.5	138.5
    - Công thức: ynew = yold + η⋅leaf_value
Bước 7: Lặp lại
    - LightGBM sẽ:
        + Tính gradient mới
        + Build cây mới
        + Update tiếp

➡️ Sau nhiều vòng → model hội tụ
```