- [Introduction](#introduction)
---
# Introduction
```bash
- K-Means là một trong những thuật toán clustering (phân cụm) nổi tiếng nhất.
    + Khác với Linear Regression hay Classification:
        - Không có nhãn (label)
        - Không biết trước dữ liệu thuộc nhóm nào

Nhiệm vụ của K-Means là:
    "Tự động chia dữ liệu thành K nhóm sao cho các điểm trong cùng nhóm giống nhau nhất có thể."

Ý tưởng cốt lõi
    Giả sử chọn: K=2
        tức muốn chia thành 2 cụm.
    K-Means sẽ:
        1. Chọn 2 tâm cụm (centroid) ban đầu
        2. Gán mỗi điểm vào tâm gần nhất
        3. Tính lại tâm cụm
        4. Lặp lại đến khi không thay đổi nữa
```
**Ex**
```bash
Giả sử bạn có dữ liệu khách hàng:
| Khách hàng | Thu nhập |
| ---------- | -------- |
| A          | 10       |
| B          | 12       |
| C          | 15       |
| D          | 100      |
| E          | 105      |
| F          | 110      |

Nhìn bằng mắt:
    10 12 15          100 105 110
Rõ ràng có 2 nhóm:
    - Nhóm thu nhập thấp
    - Nhóm thu nhập cao
K-Means sẽ tự tìm ra điều này.
```
**Ex: Ví dụ chi tiết**
```bash
Dữ liệu:
    10, 12, 15, 100, 105, 110
Muốn: K=2
```
```bash
Bước 1: Chọn centroid ngẫu nhiên
    Giả sử:
        C1 = 12
        C2 = 105
Bước 2: Gán điểm vào centroid gần nhất
    Tính khoảng cách.
        Điểm 10
            Đến C1: ∣10−12∣=2
            Đến C2: ∣10−105∣=95
            → thuộc cụm 1
        Điểm 15
            Đến C1: ∣15−12∣=3
            Đến C2: ∣15−105∣=90
            → cụm 1
        Điểm 100
            Đến C1: ∣100−12∣=88
            Đến C2: ∣100−105∣=5
            → cụm 2

    Kết quả:
        Cluster 1:
        10 12 15

        Cluster 2:
        100 105 110
Bước 3: Tính centroid mới
    Centroid = trung bình các điểm trong cụm.
        Cluster 1: 10 12 15
            Trung bình:(10+12+15)/3 = 12.33
        Cluster 2: 100 105 110
            Trung bình: (100+105+110)/3 = 105
    Centroid mới:
        C1 = 12.33
        C2 = 105
Bước 4: Gán lại
    Tính lại khoảng cách.
    Kết quả không đổi: 
        10 12 15
            vẫn thuộc Cluster 1
        100 105 110
            vẫn thuộc Cluster 2

Thuật toán dừng.
```