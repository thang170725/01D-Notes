- [LinearRegression()](#linearregression)
- [LogisticRegression](#logisticregression)
- [Naive bayes](#naive-bayes)
---
# LinearRegression()
```python
from sklearn.linear_model import LinearRegression

model = LinearRegression()
model.fit(X_train, y_train)

y_pred = model.predict(X_test)
```
# LogisticRegression
```python
from sklearn.linear_model import LogisticRegression
import numpy as np

dataSet = np.array(
    [[-10, 0],
     [-5, 0],
     [-7, 0],
     [0, 0],
     [-2, 0],
     [5, 1],
     [7, 1],
     [6, 1],
     [10, 1],
     [15, 1],
     [9, 1]
     ]
)
X = dataSet[:, 0].reshape(-1, 1)
y = dataSet[:, 1]

logr = LogisticRegression()
logr.fit(X, y)
print(logr.predict(np.array([1]).reshape(-1,1)))
preprocessing
```
# Naive bayes
```bash
Naive Bayes Là một mô hình phân loại dựa trên định lý Bayes và giả định độc lập có điều kiện giữa các đặc trưng.
```
**Ex**
```python
import numpy as np

# X: mỗi hàng là 1 email, mỗi cột là đặc trưng: "free", "win", "click"
X_train = np.array([
    [1, 1, 1],  # spam
    [1, 1, 0],  # spam
    [1, 0, 1],  # spam
    [0, 1, 1],  # spam
    [1, 0, 0],  # spam
    [0, 0, 1],  # spam
    [0, 1, 0],  # not spam
    [0, 0, 0],  # not spam
    [0, 0, 1],  # not spam
    [0, 1, 1],  # not spam
])

# Nhãn: 1 = spam, 0 = not spam
y_train = np.array([1, 1, 1, 1, 1, 1, 0, 0, 0, 0])

def train_naive_bayes(X, y):
    n_samples, n_features = X.shape
    classes = np.unique(y)
    n_classes = len(classes)

    priors = np.zeros(n_classes)
    likelihoods = np.zeros((n_classes, n_features))
    for cls in classes:
        X_cls = X[y == cls]
        priors[cls] = X_cls.shape[0] / n_samples
        likelihoods[cls] = (X_cls.sum(axis=0) + 1) / (X_cls.shape[0] + 2)  # Laplace smoothing

    return priors, likelihoods

def predict_naive_bayes(X_test, priors, likelihoods):
    log_probs = []
    for cls in range(len(priors)):
        log_prior = np.log(priors[cls])
        log_likelihood = X_test * np.log(likelihoods[cls]) + (1 - X_test) * np.log(1 - likelihoods[cls])
        log_probs.append(log_prior + log_likelihood.sum(axis=1))
    return np.argmax(np.stack(log_probs, axis=1), axis=1)

# Huấn luyện
priors, likelihoods = train_naive_bayes(X_train, y_train)

# Dự đoán trên tập huấn luyện
y_pred = predict_naive_bayes(X_train, priors, likelihoods)

# Độ chính xác
accuracy = np.mean(y_pred == y_train)
print("Accuracy:", accuracy)

# Ví dụ: Email mới có "free" và "click", không có "win"
X_new = np.array([[1, 0, 1]])
y_new_pred = predict_naive_bayes(X_new, priors, likelihoods)
print("Dự đoán: Spam" if y_new_pred[0] == 1 else "Dự đoán: Không Spam")
```
