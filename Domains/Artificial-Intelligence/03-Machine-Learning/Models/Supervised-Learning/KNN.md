- [Introduction](#introduction)
- [KNN Classification (Phân loại)](#knn-classification-phân-loại)
- [KNN Regression (Hồi quy)](#knn-regression-hồi-quy)
---
# Introduction
```bash
KNN (K-Nearest Neighbors) là thuật toán học máy suppervised learning cực kỳ đơn giản dùng được cho cả phân lớp và hồi quy

Ưu điểm
  ✅ Dễ hiểu
  ✅ Dễ cài đặt
  ✅ Không cần huấn luyện phức tạp
  ✅ Hoạt động tốt với dữ liệu nhỏ
Nhược điểm
  ❌ Chậm khi dữ liệu lớn. Vì mỗi lần dự đoán phải so sánh với toàn bộ dữ liệu train.
  ❌ Tốn RAM, Vì phải lưu toàn bộ dữ liệu.
  ❌ Nhạy với outlier
  ❌ Nhạy với scale dữ liệu

Điều quan trọng nhất cần nhớ
  - KNN thực chất chỉ làm 3 việc:
      1. Xem điểm mới nằm ở đâu trong không gian dữ liệu.
      2. Tìm K điểm gần nó nhất.
      3. Dùng các hàng xóm đó để bỏ phiếu (classification) hoặc lấy trung bình (regression).

"Nắm vững cơ chế phân tách không gian của KNN" nghĩa là hiểu rằng:
  KNN không học một công thức toán học tổng quát. Nó chia không gian thành các vùng dựa trên vị trí của các điểm dữ liệu. Một điểm mới sẽ được gán nhãn theo những hàng xóm gần nhất nằm trong vùng xung quanh nó.
Đó là lý do KNN thường được gọi là thuật toán "học theo láng giềng" hơn là thuật toán học ra một hàm dự đoán rõ ràng.

Cơ chế phân tách không gian của KNN chính là:
  - Lưu toàn bộ dữ liệu huấn luyện.
  - Khi có điểm mới, tìm K điểm gần nhất.
  - Xem đa số hàng xóm thuộc lớp nào.
  - Gán điểm mới vào lớp đó.
```
**Hệ số K trong KNN**
```bash
K = số lượng hàng xóm được xem xét.

Ví dụ: 
  - K=1 -> Chỉ nhìn người gần nhất.
    + Ưu điểm: Nhạy
    + Nhược điểm: Dễ bị nhiễu.

  - K=100. Nhìn quá nhiều người.
    + Ưu điểm: Ổn định
    + Nhược điểm: Mất chi tiết địa phương.

Ví dụ: Bạn muốn biết giá căn nhà ở Ba Vì.
  - Nếu hỏi: 3 căn gần nhất → hợp lý.
  - Nếu hỏi: 500 căn trên toàn Hà Nội => kết quả bị pha loãng.
```
**Khoảng cách được tính như nào?**
```bash
Phổ biến nhất là khoảng cách Euclid.
Hai điểm: (x1,y1) và (x2,y2)
Khoảng cách: d = sqrt((x2-x1)**2+(y2-y1)**2)
```
**Phân tách không gian" của KNN là gì?**
```bash
Dữ liệu:
  - Chó ở bên phải
  - Mèo ở bên trái
  M M M MM M M-----------      C C C      C C C

KNN không học công thức kiểu:
  - Nếu x > 10 thì là chó như cây quyết định.
  - Nó chỉ nhớ toàn bộ dữ liệu.
  - Khi có điểm mới:
    + Nhìn xung quanh
    + Xem khu vực đó đa số là gì

Cơ chế phân tách không gian. Không gian dữ liệu được chia thành nhiều vùng.
Ví dụ:
  MMMMMMM|CCCCCCCMMMMMMM|CCCCCCCMMMMMMM|CCCCCCC
  
  Đường ở giữa là ranh giới quyết định. 
  Nếu điểm nằm:
    - Bên trái → Mèo
    - Bên phải → Chó

KNN tạo ranh giới bằng các điểm dữ liệu. Không có công thức rõ ràng. Nó giống như: "Khu dân cư này đa số là mèo thì ai mới đến đây cũng được xem là mèo."
```
**Tại sao KNN có thể tạo ranh giới rất ngoằn ngoèo?**
```bash
Ví dụ:
M M M    CM M M
Con chó nằm giữa đám mèo.
KNN sẽ tạo một "ốc đảo chó".
MMMMMMMMMMMCCCMMMMMMMMMMM
Đó là lý do KNN có thể học các hình dạng cực kỳ phức tạp.
```
# KNN Classification (Phân loại)
```bash
Mục tiêu: Dự đoán một nhãn.

Ví dụ:
  - Chó hay mèo?
  - Spam hay không spam?
  - Bệnh hay không bệnh?
```
**Ex**
```bash
Ví dụ phân loại chó mèo.

Train:
| Cân nặng | Loài |
| -------- | ---- |
| 4kg      | Mèo  |
| 5kg      | Mèo  |
| 20kg     | Chó  |
| 25kg     | Chó  |

Con mới: 6kg
K=3 (3 hàng xóm gần nhất)
| Điểm     |
| -------- |
| 5kg Mèo  |
| 4kg Mèo  |
| 20kg Chó |

Kết quả:
  - Mèo: 2 phiếu
  - Chó: 1 phiếu
⇒ Dự đoán Mèo
```
# KNN Regression (Hồi quy)
**Ex**
```bash
| Diện tích | Giá    |
| --------- | ------ |
| 50m²      | 2 tỷ   |
| 55m²      | 2.1 tỷ |
| 60m²      | 2.3 tỷ |
| 200m²     | 10 tỷ  |

Có căn nhà mới: 58m²
Ta tìm những căn gần nhất:
    - 55m² → 2.1 tỷ
    - 60m² → 2.3 tỷ
    => dự đoán khoảng: 2.2 tỷ

Thay vì bỏ phiếu, ta lấy trung bình.
```