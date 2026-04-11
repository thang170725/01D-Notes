- [Decision Tree](#decision-tree)
- [Random Forest](#random-forest)
- [XGBoost](#xgboost)
- [LightGBM](#lightgbm)
- [CatBoost](#catboost)
---
# Decision Tree
```bash
- Decision Tree (ví dụ: CART) là một cây duy nhất chia dữ liệu theo rule.
- Ưu điểm
    + Rất dễ hiểu và dễ giải thích
    + Trực quan (có thể vẽ cây)
    + Chạy nhanh
Phù hợp khi:
    + Dataset nhỏ
    + Cần explainability cao (y tế, tài chính, luật)
    + Prototype nhanh
    + Nhược điểm
    + Dễ overfit
    + Độ chính xác thường thấp hơn ensemble methods
    + Nhạy với nhiễu
```
# Random Forest
```bash
Random Forest là bagging ensemble:
    + Train nhiều cây độc lập song song
    + Mỗi cây dùng bootstrap sample
    + Random subset features mỗi split
    + Kết quả = average / majority vote
    → Mục tiêu: giảm variance
Random Forest tốt cho:
    1. Dataset nhỏ – vừa
    2. Data noisy: RF trung bình hóa → ổn định hơn
    3. Muốn model ổn định, ít tuning
        RF: Chỉ cần chỉnh n_estimators. Ít nhạy hyperparameter
    4. Cần train nhanh & song song
        RF tận dụng multi-core rất tốt.
```
# XGBoost
```bash
- Ý tưởng cốt lõi là "sai -> học thêm cây mới để sửa sai"
- Có thể phân loại và dự đoán
- XGBoost mạnh vì:
    + chạy nhanh
    + Xử lý dữ liệu lớn tốt
    + Tự xử lý missing value
    + phổ biến trong production
- XGBoost tốt cho:
    1. Dataset lớn, phức tạp. Boosting bắt nonlinear pattern tốt hơn.
    2. Muốn squeeze từng % accuracy. Competition / production high-stakes.
    3. Feature engineering chưa hoàn hảo. Boosting có thể học interaction tốt hơn.
    4. Tabular data structured. Trong 80% bài toán tabular → XGBoost thường thắng RF.
```
# LightGBM
LightGBM (Light Gradient Boosting Machine) là một thư viện gradient boosting dựa trên decision tree, do Microsoft phát triển.

Nó cùng “họ” với:

XGBoost

CatBoost

⚙️ LightGBM khác XGBoost ở điểm nào?
1️⃣ Cách xây cây

XGBoost: grow theo level-wise (từng tầng một)

LightGBM: grow theo leaf-wise (chọn leaf có gain lớn nhất để tách tiếp)

👉 Leaf-wise thường:

Giảm loss nhanh hơn

Có thể chính xác hơn

Nhưng dễ overfit nếu dataset nhỏ

2️⃣ Tốc độ

LightGBM:

Dùng histogram-based algorithm

Thường train nhanh hơn XGBoost

Tốn ít memory hơn

❓ LightGBM có mạnh hơn XGBoost trong đa số trường hợp?

Câu trả lời trung thực:

👉 Không có cái nào luôn thắng.

Thực tế:

Dataset lớn (100k+ rows): LightGBM thường nhanh và có thể tốt hơn

Dataset nhỏ – vừa (vài nghìn → vài chục nghìn): XGBoost thường ổn định hơn

Nhiều categorical feature: CatBoost có thể thắng cả hai
# CatBoost
CatBoost là gì?

CatBoost là thư viện gradient boosting do Yandex phát triển, đặc biệt mạnh khi:

Có nhiều categorical feature

Không muốn encoding thủ công

Dataset không quá lớn

🎯 CatBoost khác XGBoost & LightGBM ở đâu?

Nó giải quyết 2 vấn đề lớn của boosting:

1️⃣ Xử lý categorical thông minh

Trong:

XGBoost

LightGBM

Bạn thường phải:

One-hot encoding

Target encoding

Hoặc label encoding

CatBoost:

Encode nội bộ bằng kỹ thuật ordered target encoding

Giảm leakage

Ít overfit hơn

👉 Nếu dataset bạn có nhiều cột dạng category → CatBoost rất đáng thử.

2️⃣ Ít overfit hơn trong dataset nhỏ – vừa

Với 10k sample:

LightGBM (leaf-wise) có thể hơi aggressive

XGBoost ổn định

CatBoost thường khá “smooth”

📊 So sánh nhanh cho dataset 10k tabular
	XGBoost	LightGBM	CatBoost
Ổn định	✅	⚠️	✅
Tốc độ	Trung bình	Nhanh	Trung bình
Categorical	Cần encode	Cần encode	⭐ Tốt nhất
Dễ tuning	Trung bình	Khó hơn	Dễ
Overfit	Trung bình	Dễ hơn	Thấp