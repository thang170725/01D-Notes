- [Circle (Hình tròn)](#circle-hình-tròn)
  - [Parametric](#parametric)
- [Euclidean distance](#euclidean-distance)
- [Cosine similarity](#cosine-similarity)
- [Loss Function](#loss-function)
  - [ArcFace](#arcface)
- [Color (Toán học về xử lý màu sắc trong ảnh)](#color-toán-học-về-xử-lý-màu-sắc-trong-ảnh)
  - [Gray Scale (ảnh xám)](#gray-scale-ảnh-xám)
- [CNN (Toán học trong CNN)](#cnn-toán-học-trong-cnn)
  - [Convolution](#convolution)
  - [BatchNorm](#batchnorm)
  - [pooling](#pooling)
- [Rotation (Xoay)](#rotation-xoay)
  - [Affine](#affine)
- [𝑀](#𝑀)
- [𝛼](#𝛼)
- [𝛽](#𝛽)
- [\]](#)
- [Sharpen \& Blur](#sharpen--blur)
  - [Kernel](#kernel)
  - [Blur](#blur)
    - [Gussian Blur](#gussian-blur)
---
# Circle (Hình tròn)
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
# Color (Toán học về xử lý màu sắc trong ảnh)
## Gray Scale (ảnh xám)
```bash
- Mỗi pixel ảnh có dạng (R, G, B) -> Ảnh xám chỉ cần 1 giá trị cho mỗi pixel
```
**Formula**
```bash
Gray = 0.299 * R + 0.587 * G + 0.114 * B

- Mắt người nhạy với xanh lá (G) nhất. Sau đó là đỏ (R). Ít nhạy với xanh dương (B)
```
# CNN (Toán học trong CNN)
## Convolution
**Ex: Code thuần Conv2d ảnh 100x100**
```python
import numpy as np

def conv2d(image, kernel, padding=1, stride=1):
  '''
    image: ma trận 2D (H x W)
    kernel: ma trận 2D (K x K)
  '''
  H, W = image.shape           # chiều cao & rộng ảnh
  K = kernel.shape[0]          # giả sử kernel vuông (3x3)
  print(f"(H,W)=({H,W})", f"K={K}")

  # === 1. Padding (Thêm viền 0 xung quanh ảnh) === 
  # Ví dụ padding=1: (100x100) -> (102x102)
  padded = np.pad(
      image,
      ((padding, padding), (padding, padding)),
      mode='constant'          # điền 0
  )
  print("Shape Image Pad: ", padded.shape)

  # === 2. Tính kích thước output và tạo ma trận output ===
  # Công thức: (H + 2P - K) / S + 1
  out_h = (H + 2 * padding - K) // stride + 1
  out_w = (W + 2 * padding - K) // stride + 1
  print(f"Shape output: (H,W)=({out_h, out_w})")

  output = np.zeros((out_h, out_w)) # Tạo ma trận output (ban đầu toàn 0)

  # === 3. Sliding window + convolution ===
  # Duyệt từng vị trí trên output
  for i in range(out_h):
      for j in range(out_w):
        # === 3.1 Xác định vùng window trên ảnh đã padding ===
        # i*stride    : vị trí bắt đầu theo chiều cao
        # i*stride + K: vị trí kết thúc (lấy K phần tử)
        row_start = i * stride
        row_end   = row_start + K

        col_start = j * stride
        col_end   = col_start + K

        window = padded[row_start:row_end, col_start:col_end] # Lấy window KxK từ ảnh
    
        # === 3.2 Nhân element-wise và cộng lại ===
        # window * kernel: nhân từng phần tử
        # np.sum(...): cộng tất cả lại thành 1 số
        output[i, j] = np.sum(window * kernel)

  return output

# --------------------------------------------------
# 🔥 DEMO
# --------------------------------------------------
# === 1. Tạo ảnh grayscale 100x100 (giá trị 0-255) ===
np.random.seed(42)
image = np.random.randint(0, 256, (100, 100))
print("Image grayscale original: ", image)

# === 2. Tạo Kernel 3x3 (ví dụ: phát hiện cạnh dọc)
kernel = np.array([
    [ 1,  0, -1],
    [ 1,  0, -1],
    [ 1,  0, -1]
])

# === 3. Chạy convolution ===
result = conv2d(image, kernel, padding=1, stride=1)
print("Output Image Con2d: ", result)
print("Output shape:", result.shape)

# Image grayscale original:  [[102 179  92 ...   3  53 220]
# [190 145 217 ... 123 204 178]
# [ 62  95 230 ...  86 228 223]
# ...
# [ 86  37 118 ... 215 228  56]
# [129  95 120 ... 151 188  53]
# [ 61 128  48 ... 245 221 116]]
# (H,W)=((100, 100)) K=3
# Shape Image Pad:  (102, 102)
# Shape output: (H,W)=((100, 100))
# Output Image Con2d:  [[-324.  -17.  267. ... -111. -272.  257.]
# [-419. -185.  122. ... -286. -409.  485.]
# [-368. -117.  -40. ... -306. -299.  551.]
# ...
# [-188.  -48. -495. ... -171.  299.  512.]
# [-260.  -10. -222. ... -228.  386.  637.]
# [-223.   22.  -52. ... -144.  227.  409.]]
# Output shape: (100, 100)
```
## BatchNorm
```bash
- BatchNorm là một trong những “vũ khí” quan trọng trong CNN — nếu hiểu đúng thì bạn nắm được cách ổn định training luôn 👍
- Ý tưởng chính
  👉 Chuẩn hóa dữ liệu ngay trong mạng theo từng mini-batch:
  + đưa output về phân phối “chuẩn hơn” → học nhanh, ổn định 
- Tại sao cần BatchNorm?
  1. Training nhanh hơn: giảm “internal covariate shift”
  2. Gradient ổn định: tránh exploding / vanishing
  3. Regularization nhẹ: giống noise → đỡ overfit
👉 BatchNorm làm 3 việc:
  + chuẩn hóa (mean = 0, var = 1)
  + scale lại (gamma)
  + shift lại (beta)
```
**Luồng hoạt động của BatchNorm**
```bash
- Giả sử output của một lớp convolution trong CNN có shape: (batch, height, width, channels)=(16, 1000, 1000, 32)
- Tức là:
  + batch size = 16
  + ảnh feature map = 1000×1000
  + có 32 channels
```
```bash
Ta xét channel số 7
1. Tensor đầu vào:
  - Giả sử vài giá trị đầu của channel 7 là:
    Batch 1:
    [[2, 4, 3, ...],
     [5, 6, 7, ...],
     ...]

    Batch 2:
    [[1, 2, 3, ...],
     ...]

    ...
  - Tổng cộng: 16000000 giá trị
  - Tổng toàn bộ giá trị của channel 7 là: ∑xi = 80000000 (x1 + x2 + ...)
2. Tính mean:
  - Công thức: μB​ = (1/m)​∑xi (m=16000000) = 80000000/16000000 = 5
3. Tính variance
  - Giả sử: ∑(xi​−μB​)**2 = 144,000,000
  - variance: σB**2 = 144,000,000/16,000,000 = 9
4. Chuẩn hóa từng phần tử:
  - x_outi = (xi - μB)/sqrt(σB**2 + ϵ)
  - giả sử: ϵ = 0.00001 => x_outi = 3
5. Scale & Shift
  - BatchNorm có tham số học được:
    + γ
    + β
  - giả sử:
    + γ = 1.5
    + β = 0.
  - Output cuối: yi = γ.x_outi + β

- Sau khi xử lý
  + Input shape: (16, 1000, 1000, 32)
  + Output shape vẫn là: (16, 1000, 1000, 32)
- BatchNorm:
  + KHÔNG đổi kích thước tensor
  + chỉ đổi phân phối dữ liệu
```
**Ex: Code demo batchnorm)**
```python
import numpy as np

def batchnorm(x, eps=1e-5):
    # x: (N, H, W, C)
    
    # mean theo channel
    mean = np.mean(x, axis=(0,1,2), keepdims=True)
    
    # variance theo channel
    var = np.var(x, axis=(0,1,2), keepdims=True)
    
    # normalize
    x_hat = (x - mean) / np.sqrt(var + eps)
    
    # gamma, beta (giả sử =1,0)
    gamma = np.ones_like(mean)
    beta = np.zeros_like(mean)
    
    out = gamma * x_hat + beta
    
    return out
```
## pooling 
```bash
- Pooling là bước giảm kích thước (downsampling) trong CNN — cực kỳ giống sliding window bạn đã học 👍
- Ý tưởng chính
  👉 Trượt một cửa sổ (window) trên ảnh
  → nhưng không nhân kernel như conv
  → chỉ lấy 1 giá trị đại diện
- Các loại phổ biến:
  1. Max Pooling (dùng nhiều nhất): output = max(window) 👉 lấy giá trị lớn nhất
  2. Average Pooling: output = mean(window) 👉 lấy trung bình
- Tại sao dùng pooling?
  1. Giảm kích thước: nhanh hơn, ít memory
  2. Giữ feature quan trọng: maxpool → giữ điểm nổi bật
  3. Tăng robustness: ít nhạy với dịch chuyển nhỏ
- Lưu ý
  + pooling không có tham số học
  + chỉ là phép toán cố định
```
**Cách hoạt động**
```bash
- Giống conv:
  + kernel size (ví dụ 2×2)
  + stride (thường = kernel size)
- Ví dụ:
  Input:
    1 3 2 4
    5 6 1 2
    7 8 3 1
    2 4 6 5
    MaxPool 2×2, stride = 2
  - Các window:
    [1 3      [2 4
     5 6]      1 2]

    [7 8      [3 1
     2 4]      6 5]
  - Output:
    6 4
    8 6
- Công thức size
  + Giống conv:
    - H_out = (H - K) / S + 1
    - W_out = (W - K) / S + 1
  (thường không padding)
```
**Ex: Code demo (numpy)**
```python
import numpy as np

def maxpool2d(image, k=2, stride=2):
    H, W = image.shape
    
    out_h = (H - k) // stride + 1
    out_w = (W - k) // stride + 1
    
    output = np.zeros((out_h, out_w))
    
    for i in range(out_h):
        for j in range(out_w):
            window = image[i*stride:i*stride+k,
                           j*stride:j*stride+k]
            
            output[i, j] = np.max(window)
    
    return 
```
# Rotation (Xoay)
## Affine
Nó trả về một ma trận:

𝑀
=
[
𝛼
	
𝛽
	
(
1
−
𝛼
)
⋅
𝑐
𝑥
−
𝛽
⋅
𝑐
𝑦


−
𝛽
	
𝛼
	
𝛽
⋅
𝑐
𝑥
+
(
1
−
𝛼
)
⋅
𝑐
𝑦
]
M=[
α
−β
	​

β
α
	​

(1−α)⋅cx−β⋅cy
β⋅cx+(1−α)⋅cy
	​

]

Trong đó:

(
𝑐
𝑥
,
𝑐
𝑦
)
(cx,cy): tâm xoay (center)
𝜃
θ: góc xoay (đơn vị độ)
𝑠
𝑐
𝑎
𝑙
𝑒
scale: hệ số scale
𝛼
=
𝑠
𝑐
𝑎
𝑙
𝑒
⋅
cos
⁡
(
𝜃
)
α=scale⋅cos(θ)
𝛽
=
𝑠
𝑐
𝑎
𝑙
𝑒
⋅
sin
⁡
(
𝜃
)
β=scale⋅sin(θ)
📌 Ý nghĩa

Ma trận này dùng để biến đổi một điểm 
(
𝑥
,
𝑦
)
(x,y) thành 
(
𝑥
′
,
𝑦
′
)
(x
′
,y
′
):

[
𝑥
′


𝑦
′
]
=
𝑀
⋅
[
𝑥


𝑦


1
]
[
x
′
y
′
	​

]=M⋅
	​

x
y
1
	​

	​


👉 Tức là:

Xoay quanh center
Có thể scale
Không cần dùng ma trận 3×3 (vì đây là affine)
# Sharpen & Blur
```bash
- Ảnh = gồm:
  + Low-frequency → vùng mượt (trời, da, nền)
  + High-frequency → cạnh, chi tiết
- Vì vậy:
  + Blur (làm mờ)	Giữ low-frequency, loại high-frequency
  + Sharpen (làm nét)	Tăng high-frequency (cạnh)
  + Edge detection	Chỉ giữ high-frequency
```
## Kernel
**Cách nhận biết kernel khi nào dùng để sharpen, blur, ...**
```bash
1. Kernel làm mờ (blur). Ví dụ:
  [1 1 1
   1 1 1
   1 1 1] / 9
  - Đặc điểm: Tất cả giá trị dương, Gần như giống nhau. Tổng ≈ 1
  - Ý nghĩa: Lấy trung bình lân cận → ảnh mượt hơn → blur
2. Kernel làm nét (sharpen). Ví dụ:
  [ 0 -1  0
   -1  5 -1
    0 -1  0]
  - Đặc điểm: Trung tâm lớn hơn 1. Xung quanh có giá trị âm. Tổng ≈ 1
  - Ý nghĩa: Lấy pixel gốc. Trừ đi vùng xung quanh → làm nổi bật khác biệt → sắc nét hơn
3. Kernel phát hiện cạnh (edge). Ví dụ:
  [-1 -1 -1
   -1  8 -1
   -1 -1 -1]
  - Đặc điểm: Tổng ≈ 0. Nhiều số âm + số dương lớn
  - Ý nghĩa: Vùng phẳng → triệt tiêu (≈0). Vùng có cạnh → giữ lại mạnh → edge detection
```
**Quy tắc “nhìn phát biết luôn”**
```bash
Rule 1: Tổng kernel
  - ≈ 1	giữ độ sáng → blur hoặc sharpen
  - ≈ 0	chỉ giữ cạnh (edge)
Rule 2: Dấu của phần tử
  - toàn dương	blur
  - center lớn + xung quanh âm	sharpen
  - nhiều âm + tổng 0	edge
Rule 3: So sánh center vs neighbors
Center ≈ neighbors → blur
Center >> neighbors → sharpen
Center đối nghịch neighbors → edge
```
## Blur
### Gussian Blur
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
