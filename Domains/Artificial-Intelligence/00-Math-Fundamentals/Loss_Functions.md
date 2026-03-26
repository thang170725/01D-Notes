- [Mean Squared Error (MSE)](#mean-squared-error-mse)
- [Binary Cross-Entropy (Log Loss)](#binary-cross-entropy-log-loss)
  - [Demo về công thức BCE bằng math](#demo-về-công-thức-bce-bằng-math)
---
# Mean Squared Error (MSE)
```bash
Công thức tính loss function thương dùng cho Regression (Linear, v.v).
```
**Formula**
```bash
MSE = 1/n . [(y1_true - y1_pred)^2 + (y2_true - y2_pred)^2 + … ]

- Output: càng gần 0 càng tốt
```
# Binary Cross-Entropy (Log Loss)
```bash
Dùng cho phân loại nhị phân.
```
**Syn**
```bash
1. Công thức cho 1 mẫu: BCE(y_true, y_pred) = −[y_true.log(y_pred) + (1-y_true).log(1−y_pred)]
2. Công thức cho batch (N mẫu): BCE = −(1/n) . [yi_true . log(yi_pred) + (1-yi_true) . log(1−yi_pred)]
3. dL/dw = (y-pred – y_true).x
4. dL/db = (y_pred - y_true)
```
## Demo về công thức BCE bằng math
```python
import math

def bce(y, y_hat):
    return -(y*math.log(y_hat) + (1-y)*math.log(1-y_hat))

print(bce(1, 0.9))
print(bce(1, 0.1))
```