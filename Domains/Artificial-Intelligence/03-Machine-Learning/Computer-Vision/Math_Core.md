- [Blur](#blur)
  - [Gussian Blur](#gussian-blur)
- [Circle (thuật toán \& công thức đường tròn, hình tròn)](#circle-thuật-toán--công-thức-đường-tròn-hình-tròn)
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
- [𝜇](#𝜇)
- [2](#2)
- [2](#2-1)
- [𝑖](#𝑖)
- [𝑖](#𝑖-1)
  - [thuật toán pooling như nào](#thuật-toán-pooling-như-nào)
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
    # image: ma trận 2D (H x W)
    # kernel: ma trận 2D (K x K)

    H, W = image.shape           # chiều cao & rộng ảnh
    K = kernel.shape[0]          # giả sử kernel vuông (3x3)

    # --------------------------------------------------
    # 1. Padding
    # --------------------------------------------------
    # Thêm viền 0 xung quanh ảnh
    # Ví dụ padding=1: (100x100) -> (102x102)
    padded = np.pad(
        image,
        ((padding, padding), (padding, padding)),
        mode='constant'          # điền 0
    )

    # --------------------------------------------------
    # 2. Tính kích thước output
    # --------------------------------------------------
    # Công thức:
    # (H + 2P - K) / S + 1
    out_h = (H + 2 * padding - K) // stride + 1
    out_w = (W + 2 * padding - K) // stride + 1

    # Tạo ma trận output (ban đầu toàn 0)
    output = np.zeros((out_h, out_w))

    # --------------------------------------------------
    # 3. Sliding window + convolution
    # --------------------------------------------------
    # Duyệt từng vị trí trên output
    for i in range(out_h):
        for j in range(out_w):

            # --------------------------------------------------
            # 3.1 Xác định vùng window trên ảnh đã padding
            # --------------------------------------------------
            # i*stride: vị trí bắt đầu theo chiều cao
            # i*stride + K: vị trí kết thúc (lấy K phần tử)
            row_start = i * stride
            row_end   = row_start + K

            col_start = j * stride
            col_end   = col_start + K

            # Lấy window KxK từ ảnh
            window = padded[row_start:row_end, col_start:col_end]

            # --------------------------------------------------
            # 3.2 Nhân element-wise và cộng lại
            # --------------------------------------------------
            # window * kernel: nhân từng phần tử
            # np.sum(...): cộng tất cả lại thành 1 số
            output[i, j] = np.sum(window * kernel)

    return output


# --------------------------------------------------
# 🔥 DEMO
# --------------------------------------------------

# Tạo ảnh grayscale 100x100 (giá trị 0-255)
image = np.random.randint(0, 256, (100, 100))

# Kernel 3x3 (ví dụ: phát hiện cạnh dọc)
kernel = np.array([
    [ 1,  0, -1],
    [ 1,  0, -1],
    [ 1,  0, -1]
])

# Chạy convolution
result = conv2d(image, kernel, padding=1, stride=1)

print("Input shape :", image.shape)
print("Output shape:", result.shape)
```
## BatchNorm
thuật toán BatchNorm trong CNN như nào

BatchNorm là một trong những “vũ khí” quan trọng trong CNN — nếu hiểu đúng thì bạn nắm được cách ổn định training luôn 👍

🧠 1. Ý tưởng chính

👉 Chuẩn hóa dữ liệu ngay trong mạng theo từng mini-batch:

đưa output về phân phối “chuẩn hơn” → học nhanh, ổn định hơn

📐 2. Công thức

Cho 1 batch giá trị 
𝑥
x:

Bước 1: tính mean & variance
𝜇
=
1
𝑚
∑
𝑥
𝑖
μ=
m
1
	​

∑x
i
	​

𝜎
2
=
1
𝑚
∑
(
𝑥
𝑖
−
𝜇
)
2
σ
2
=
m
1
	​

∑(x
i
	​

−μ)
2
Bước 2: chuẩn hóa
𝑥
^
𝑖
=
𝑥
𝑖
−
𝜇
𝜎
2
+
𝜖
x
^
i
	​

=
σ
2
+ϵ
	​

x
i
	​

−μ
	​

Bước 3: scale & shift (learnable)
𝑦
𝑖
=
𝛾
𝑥
^
𝑖
+
𝛽
y
i
	​

=γ
x
^
i
	​

+β
📦 3. Áp dụng trong CNN (quan trọng)

👉 Với tensor:

(N, H, W, C)

BatchNorm sẽ:

tính mean & var theo từng channel
trên toàn bộ:
N × H × W
🔥 Nghĩa là:

👉 mỗi channel có:

1 mean
1 variance
1 gamma
1 beta
🔍 4. Flow trong CNN
Conv → BatchNorm → ReLU
💻 5. Code đơn giản (numpy)
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
⚡ 6. Tại sao cần BatchNorm?
✅ 1. Training nhanh hơn
giảm “internal covariate shift”
✅ 2. Gradient ổn định
tránh exploding / vanishing
✅ 3. Regularization nhẹ
giống noise → đỡ overfit
❗ 7. Khác nhau train vs inference
🔥 Train:
dùng mean/var của batch
🔥 Test:
dùng running mean/var (đã tích lũy)
🚀 Tóm gọn

👉 BatchNorm làm 3 việc:

chuẩn hóa (mean = 0, var = 1)
scale lại (gamma)
shift lại (beta)
💡 Mental model

“Mỗi channel được chuẩn hóa riêng để phân phối ổn định hơn”

Nếu bạn muốn, mình có thể:

giải thích tại sao BN đặt trước hay sau ReLU
hoặc so sánh BatchNorm vs LayerNorm vs GroupNorm (rất hay hỏi)
## thuật toán pooling như nào

Pooling là bước giảm kích thước (downsampling) trong CNN — cực kỳ giống sliding window bạn đã học 👍

🧠 1. Ý tưởng chính

👉 Trượt một cửa sổ (window) trên ảnh
→ nhưng không nhân kernel như conv
→ chỉ lấy 1 giá trị đại diện

🔥 2. Các loại phổ biến
✅ 1. Max Pooling (dùng nhiều nhất)
output = max(window)

👉 lấy giá trị lớn nhất

✅ 2. Average Pooling
output = mean(window)

👉 lấy trung bình

📦 3. Cách hoạt động

Giống conv:

kernel size (ví dụ 2×2)
stride (thường = kernel size)
📌 Ví dụ

Input:

1 3 2 4
5 6 1 2
7 8 3 1
2 4 6 5
MaxPool 2×2, stride = 2
Các window:
[1 3      [2 4
 5 6]      1 2]

[7 8      [3 1
 2 4]      6 5]
Output:
6 4
8 6
📐 4. Công thức size

Giống conv:

H_out = (H - K) / S + 1
W_out = (W - K) / S + 1

(thường không padding)

💻 5. Code demo (numpy)
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
    
    return output
🧠 6. Với CNN (multi-channel)

👉 mỗi channel xử lý độc lập

Input:  (H, W, C)
Output: (H_out, W_out, C)

👉 số channel không đổi

⚡ 7. Tại sao dùng pooling?
✅ 1. Giảm kích thước
nhanh hơn
ít memory
✅ 2. Giữ feature quan trọng
maxpool → giữ điểm nổi bật
✅ 3. Tăng robustness
ít nhạy với dịch chuyển nhỏ
❗ 8. Lưu ý
pooling không có tham số học
chỉ là phép toán cố định
🚀 Tóm gọn

👉 Pooling =

sliding window + lấy max/mean

💡 Mental model
Conv: “học feature”
Pooling: “nén feature”

Nếu bạn muốn, mình có thể:

so sánh pooling vs stride=2 conv (câu phỏng vấn hay)
hoặc giải thích global average pooling (dùng trong ResNet) 🔥