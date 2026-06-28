# Introduction
```bash
- Là một mô hình học có giám sát
- Đầu ra dự đoán là liên tục và có độ dốc không đổi. Nó được sử dụng để dự đoán các giá trị trong một phạm vi liên tục (doanh số, giá cả) thay vì cố gắng phân loại chúng thành các danh mục nhóm (chó, mèo).
```
**Thuật toán Linear Regression**
```bash
Bạn có dataset đã được scale sẵn (Z-score), gồm:
| x₁ | x₂ | x₃ | y  |
| -- | -- | -- | -- |
| 1  | 0  | -1 | 2  |
| 0  | 1  | 1  | 3  |
| -1 | -1 | 0  | -1 |

Yêu cầu:
1. Viết mô hình: 𝑦 = 𝑤1.𝑥1 + 𝑤2.𝑥2 + 𝑤3.𝑥3 + 𝑏 
2. Dùng dạng ma trận: 𝑦 = w𝑋 + 𝑏
3. Tìm: 𝑤1,𝑤2,𝑤3, w1
```
```bash
---- Loop 1 ------
Step 1: Tính y
    - Tự chọn w1 = 0.1, w2 = 0.2, w3 = 0.15, b = 0
    - y1 = 𝑤1.𝑥1 + 𝑤2.𝑥2 + 𝑤3.𝑥3 + 𝑏 = 0.1x1 + 0.2x0 + 0.15x2 = 0.4
    - y2 = 0.5
    - y3 = 0.2
    - ... (nếu data co nhiều dòng)
Step 2: Tính loss (MSE)
    MSE = (1/n) [(y1_true - y2_pred)**2 + ...] = 3.4
Step 3: BackProp (đạo hàm)
    dL/dw = -(2/n).(Y_true - (W.X + b)).X = [1.2, 3.0, 2]
    dL/db = -(2/n).(Y_true - (W.X + b)) = 1
Step 3: Update (cập nhật trọng số)
    - Tự chọn learning rate = 0.002
    W = W - (dL/dw).lr = [1, 2.8, 1]
    b = b - (dL/db).lr = 1

---- Loop 2 -----
...
```
**Đạo hàm loss MSE**
```bash
MSE = (1/n) [(y1_true - y2_pred)**2 + ...] = (1/n)*(Y-(WX+b))**2)
MSE' = (-2/n)*(Y-(W.X+b))*X
```