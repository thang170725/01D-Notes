- [Pipeline](#pipeline)
---
# Pipeline
```bash
Chuỗi các bước xử lý dữ liệu + model
```
**Syn**
```bash
from sklearn.pipeline import Pipeline

pipe = Pipeline(steps=[
    ("tên_bước_1", transformer),
    ("tên_bước_2", model)
])
```
**Ex: Chuẩn hóa dữ liệu +  Logistic Regression**
```python
from sklearn.pipeline import Pipeline
from sklearn.preprocessing import StandardScaler
from sklearn.linear_model import LogisticRegression
from sklearn.model_selection import train_test_split
from sklearn.datasets import load_iris

# Load data
X, y = load_iris(return_X_y=True)

# Train / test split
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
)

# Tạo pipeline
pipe = Pipeline([
    ("scaler", StandardScaler()),
    ("model", LogisticRegression())
])

# Train
pipe.fit(X_train, y_train)

# Predict
y_pred = pipe.predict(X_test)

# Score
print("Accuracy:", pipe.score(X_test, y_test))

# Không cần gọi scaler.fit_transform() thủ công Pipeline tự xử lý thứ tự chuẩn.
```