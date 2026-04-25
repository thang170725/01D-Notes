- [.LGBMRegressor()](#lgbmregressor)
  - [.fit()](#fit)
  - [.predict()](#predict)
- [LGBMClassifier()](#lgbmclassifier)
---
# .LGBMRegressor()
```bash
Dùng cho regression
```
**Syn**
```bash
model = lgb.LGBMRegressor(
    n_estimators=100,
    learning_rate=0.1,
    max_depth=-1,
    num_leaves=31
)

- Input:
    + n_estimators  : Số cây booosting
    + learning_rate : Tốc độ học
    + max_depth     : Giới hạn độ sâu của cây
    + num_leaves    : số lá tối đa mỗi cây
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