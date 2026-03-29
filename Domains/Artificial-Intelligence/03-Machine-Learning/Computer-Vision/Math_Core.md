- [Blur](#blur)
  - [Gussian Blur](#gussian-blur)
- [Circle (thuật toán \& công thức đường tròn, hình tròn)](#circle-thuật-toán--công-thức-đường-tròn-hình-tròn)
  - [Parametric](#parametric)
- [Euclidean distance](#euclidean-distance)
- [Cosine similarity](#cosine-similarity)
- [Loss Function](#loss-function)
  - [ArcFace](#arcface)
---
# Blur
## Gussian Blur
**Cách hoạt động**
```bash
Giả sử chúng ta muốn tính giá trị của pixel tại vị trí (1,1), giá trị 60 trong ví dụ. Chúng ta sẽ đặt môt kernel 3x3 lên ma trận ảnh sao cho trung tâm của kernel đó trùng với pixel(1,1).
Các pixel xung quanh pixel (1,1) trong ma trận ảnh gốc sẽ là:
```
```bash
Bây giờ, chúng ta sẽ thực hiện phép tích chập:
Giá trị pixel mới tại (1,1) sẽ là: 
= (10×0.0625)+(20×0.125)+(30×0.0625)+ (50×0.125)+(60×0.25)+(70×0.125)+ (90×0.0625)+(100×0.125)+(110×0.0625)
= 0.625+2.5+1.875+ 6.25+15+8.75+ 5.625+12.5+6.875
= 65
Vậy, giá trị pixel mới tại vị trí (1,1) trong ma trận kết quả sẽ là 65.
```
# Circle (thuật toán & công thức đường tròn, hình tròn)
## Parametric
```bash
Dùng để biểu diễn điểm chạy trên đường tròn theo góc
```
**Formula**
```bash
x=rcos(θ),y=rsin(θ)

- Input:
  + r = bán kính
  + θ (angle) = góc quay (tính bằng radian)
- Output:
  + (x, y) = tọa độ điểm trên đường tròn
```
# Euclidean distance
```bash
- Đo khoảng cách thật giữa 2 điểm trong không gian
- nhỏ -> gần nhau, lớn -> xa nhau
```
**Formula**
```bash
d(A,B) = sqrt((A1​−B1​)**2 + (A2​−B2​)**2 +...+ (An​−Bn​)**2)
```
**Ex**
```bash
A = [1, 1]
B = [2, 2]
C = [1, -1]

d(A, B) = √((1-2)² + (1-2)²) = √(1+1) = √2 ≈ 1.41
d(A, C) = √((1-1)² + (1-(-1))²) = √(0+4) = 2

→ A gần B hơn C (Euclidean) ✅
```
# Cosine similarity
```bash
- Chỉ quan tâm hướng vector, bỏ qua độ dài
  + 1 -> gần nhau hoàn toàn
  + 0 -> hoàn toàn khác hướng
  + -1 -> ngược hướng
```
**Formula**
```bash
cosine(A,B) = (A.B)/(∣∣A∣∣⋅∣∣B∣∣) ​= (A1.B1 ​+ ... + An.Bn​)/(sqrt(​A1**2 + ...).sqrt(​B1**2 ​+ ...))
```
**Ex**
```bash
A = [1, 1]
B = [2, 2]
C = [1, -1]

A · B = 1*2 + 1*2 = 4
||A|| = √(1²+1²) = √2 ≈ 1.41
||B|| = √(2²+2²) = √8 ≈ 2.83
cosine(A, B) = 4 / (1.41*2.83) ≈ 1 (gần giống hoàn toàn)
A · C = 1*1 + 1*(-1) = 0
||C|| = √(1²+(-1)²) = √2 ≈ 1.41
cosine(A, C) = 0 / (1.41*1.41) = 0 (khác hoàn toàn)
```
# Loss Function
## ArcFace
```bash
- ArcFace = một loại loss fuction đặc biệt cho face recognition
- Nó không phải model riêng
- Nó thay thế loss function khi train model
- Mục tiêu: tạo embedding chất lượng hơn, các cụm vector tách rõ hơn
```
**Tại sao cần ArcFace?**
```bash
- Softmax hay Triplet Loss: 
  + vector các người chưa tách đều → dễ nhầm
  + Triplet Loss cần chọn bộ triplet “khó” → training chậm
- ArcFace: thêm margin góc (angular margin) → ép vector của mỗi người phải cách nhau ít nhất m độ trên hình cầu cosine
  + Kết quả: embedding rõ ràng, khó nhầm, nhận diện tốt hơn cả người chưa từng thấy
```