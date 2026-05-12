- [Loss\_Function](#loss_function)
- [Cost\_Function](#cost_function)
  - [Demo về công thức BCE bằng math](#demo-về-công-thức-bce-bằng-math)
---
# Loss_Function
```bash
Tính cho 1 sample (1 dòng).
```
# Cost_Function
```bash
Tính trên toàn bộ dataset
```
## Demo về công thức BCE bằng math
```python
import math

def bce(y, y_hat):
    return -(y*math.log(y_hat) + (1-y)*math.log(1-y_hat))

print(bce(1, 0.9))
print(bce(1, 0.1))
```