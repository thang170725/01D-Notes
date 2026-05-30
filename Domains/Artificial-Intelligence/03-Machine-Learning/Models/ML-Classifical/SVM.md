- [Introduction](#introduction)
---
# Introduction
```bash
- SVM là thuật toán học có giám sát (supervised learning) trong Machine Learning.
- Thường dùng cho:
    + Phân loại (classification) (phổ biến nhất)
    + Hồi quy (regression) thường dùng biến thể SVR
- Ý tưởng chính của SVM:
    + Hãy tưởng tượng bạn có dữ liệu gồm 2 nhóm:
        - Chấm đỏ
        - Chấm xanh
    + SVM sẽ cố tìm một “đường ranh giới” để tách 2 nhóm này ra tốt nhất.
    + Ví dụ:
        Đỏ  Đỏ  Đỏ | Xanh Xanh
        Đỏ  Đỏ  Đỏ | Xanh Xanh
        - Dấu | là đường phân chia.
    + Nhưng SVM không chỉ tìm “một đường bất kỳ”. Nó tìm đường có khoảng cách xa nhất tới các điểm gần nhất của hai lớp → giúp mô hình tổng quát hóa tốt hơn.
    + Các điểm nằm sát biên nhất được gọi là: Support Vectors => Đó là lý do tên gọi là “Support Vector Machine”.
```
**Ex: Ví dụ phân loại 2 lớp**
```bash
Giả sử ta có dữ liệu:
| Điểm | x1 | x2 | Nhãn |
| ---- | -- | -- | ---- |
| A    | 1  | 1  | -1   |
| B    | 2  | 2  | -1   |
| C    | 4  | 4  | +1   |
| D    | 5  | 5  | +1   |
Ta muốn dùng SVM để phân loại:
    - -1 = lớp đỏ
    - +1 = lớp xanh
```
```bash
Step 1: Biểu diễn dữ liệu
    - Trên mặt phẳng:
        (-1)  A(1,1)   B(2,2)

    (+1)                  C(4,4)   D(5,5)
    => Có thể thấy 2 nhóm tách khá rõ
Step 2: Tìm hyperplane
    - SVM sẽ tìm đường phân chia: w**T.x + b = 0
    - Trong bài toán 2 chiều: w1.x1 + w2.x2 + b = 0
    - Giả sử sau khi học được: x1 + x2 − 6 = 0
    => Đường này chính là ranh giới phân loại.
Bước 3: Kiểm tra phân loại
    - Ta thay từng điểm vào:
        + Điểm A(1,1): 1 + 1 − 6 = −4. Âm → lớp -1
        + Điểm D(5,5): 5 + 5 − 6 = 4. Dương → lớp +1
Bước 4: Margin
    - SVM không chỉ tìm đường phân chia đúng. Nó tìm đường có khoảng cách lớn nhất tới hai lớp.
    - Margin được tính bằng: Margin = 2/∥w∥
	​   + ∥w∥ = sqrt(w1**2 + w2**2)
	​   + Nếu: w = (1,1) thì: ∥w∥ = 2
	​       - Margin: 2/sqrt(2) = sqrt(2). SVM sẽ cố làm margin lớn nhất.
Bước 5: Support Vectors
    - Các điểm gần biên nhất gọi là: Support Vectors
    - Trong ví dụ này thường là:
        + B(2,2)
        + C(4,4)
    - Vì chúng nằm sát đường phân chia nhất. Điều thú vị là: Chỉ vài điểm support vector quyết định mô hình.
Step6: Hàm tối ưu của SVM
    - SVM giải bài toán tối ưu: min 1/2.∥w∥**2
        + với điều kiện: yi.(w**T.xi + b) ≥ 1
    - Ý nghĩa:
        + Phân loại đúng tất cả điểm
        + Đồng thời làm margin lớn nhất
```