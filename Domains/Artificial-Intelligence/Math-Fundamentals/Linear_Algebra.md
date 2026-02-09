- [eigenvector \& eigenvalue](#eigenvector--eigenvalue)
  - [demo eigenvalue](#demo-eigenvalue)
---
# eigenvector & eigenvalue
```bash
- eigenvector   : Hướng đặc biệt không bị đổi hướng khi qua ma trận
- eiganvalue    : mức độ phóng to thu nhỏ theo hướng đó.
    + eigenvalue > 1: nổ (độ dài tăng vô hạn)
    + eigenvalue < 1: triệt (về 0)
    + eigenvalue = 1: giữ biên / dạo động / nghiên về một hướng
```
**Dùng để làm gì**
```bash
1. tìm ra cái “quan trọng nhất / ổn định nhất” trong một hệ phức tạp.
```
## demo eigenvalue & eigenvector
```python
import numpy as np

A = np.array([[0.9, 0.4],
              [0, 0.9]])

# Tính eigen
eigenvalues, eigenvectors = np.linalg.eig(A)

print("Eigenvalues:", eigenvalues)
print("Eigenvectors:\n", eigenvectors)

# Kiểm tra Av = λv với eigen đầu tiên
v = eigenvectors[:, 0]
lam = eigenvalues[0]

print("A @ v =", A @ v)
print("λ * v =", lam * v)

# Eigenvalues: [0.9 0.9] - Ma trận có 1 eigenvalue = 0.9 với bội đại số = 2. |λ|=0.9 < 1 -> không nổ -> A**n -> 0
# Eigenvectors:
#  [[ 1.00000000e+00 -1.00000000e+00]
#  [ 0.00000000e+00  4.99600361e-16]]
# A @ v = [0.9 0. ]
# λ * v = [0.9 0. ]
```