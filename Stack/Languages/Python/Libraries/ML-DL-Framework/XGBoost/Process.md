- [XGBClassifier](#xgbclassifier)
- [XGBRegressor](#xgbregressor)
---
# XGBClassifier
**Syn**
```bash
model = XGBClassifier(
    n_estimators=50,
    max_depth=3,
    learning_rate=0.1,
    eval_metric='mlogloss'
)

- max_depth	        : Cây sâu bao nhiêu (3 – 6)
- min_child_weight	: Lá có đủ dữ liệu mới tách	(1 – 10)
- subsample	        : % dữ liệu dùng mỗi cây	0.7 – 0.9
- colsample_bytree	: % feature mỗi cây	0.7 – 0.9
- learning_rate	    : Mỗi cây sửa sai bao nhiêu
- n_estimators	    : Số cây

# learning_rate = 0.05 ~ 0.1
# n_estimators = 200 ~ 500
# max_depth = 3 ~ 5
# subsample = 0.8
# colsample_bytree = 0.8
# -> 80% bài toán dùng ổn luôn
```
**Ex**
```bash
from xgboost import XGBClassifier
from sklearn.datasets import load_iris
from sklearn.model_selection import train_test_split
from sklearn.metrics import accuracy_score

# 1. Load dữ liệu
X, y = load_iris(return_X_y=True)

# 2. Chia dữ liệu
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
)

# 3. Model
model = XGBClassifier(
    n_estimators=50,
    max_depth=3,
    learning_rate=0.1,
    eval_metric='mlogloss'
)

# 4. Train
model.fit(X_train, y_train)

# 5. Predict
y_pred = model.predict(X_test)

# 6. Accuracy
acc = accuracy_score(y_test, y_pred)
print("Accuracy:", acc)
```
# XGBRegressor
```bash
from xgboost import XGBRegressor

model = XGBRegressor(
    n_estimators=100,
    learning_rate=0.1,
    max_depth=6,
    subsample=1.0,
    colsample_bytree=1.0,
    objective="reg:squarederror",
    random_state=42
)

- n_estimators	    : Số cây boosting
- learning_rate	    : Tốc độ học (eta)
- max_depth	        : Độ sâu tối đa của cây
- subsample	        : Tỉ lệ sample cho mỗi cây
- colsample_bytree	: Tỉ lệ feature cho mỗi cây
- objective	        : Hàm loss (reg:squarederror thường dùng)
- gamma	            : Mức giảm loss tối thiểu để chia node
- reg_alpha	        : L1 regularization
- reg_lambda	    : L2 regularization
```