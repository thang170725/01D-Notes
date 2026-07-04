- [Image (Bản chất ảnh)](#image-bản-chất-ảnh)
  - [RGB (hệ màu phối của red – green – blue)](#rgb-hệ-màu-phối-của-red--green--blue)
  - [BGR (OpenCV mặc định dùng Blue - Green - Red)](#bgr-opencv-mặc-định-dùng-blue---green---red)
  - [Grayscale (Ảnh xám chỉ có 1 kênh màu)](#grayscale-ảnh-xám-chỉ-có-1-kênh-màu)
  - [HEX (giá trị thập lục phân)](#hex-giá-trị-thập-lục-phân)
  - [HSV là gì?](#hsv-là-gì)
- [Kernel (Weight)](#kernel-weight)
- [Feature map (output sau khi kernel quét qua ảnh)](#feature-map-output-sau-khi-kernel-quét-qua-ảnh)
- [FPS](#fps)
- [Circle (Hình tròn)](#circle-hình-tròn)
  - [Parametric](#parametric)
- [Euclidean distance](#euclidean-distance)
- [Cosine similarity](#cosine-similarity)
- [Loss Function](#loss-function)
  - [ArcFace](#arcface)
- [Color (Toán học về xử lý màu sắc trong ảnh)](#color-toán-học-về-xử-lý-màu-sắc-trong-ảnh)
  - [Gray Scale (ảnh xám)](#gray-scale-ảnh-xám)
- [Convolution](#convolution)
- [BatchNorm (Chuẩn hóa dữ liệu đưa output về phân phối “chuẩn hơn” → học nhanh, ổn định)](#batchnorm-chuẩn-hóa-dữ-liệu-đưa-output-về-phân-phối-chuẩn-hơn--học-nhanh-ổn-định)
  - [pooling](#pooling)
- [Rotation (Xoay)](#rotation-xoay)
  - [Affine](#affine)
- [𝑀](#𝑀)
- [𝛼](#𝛼)
- [𝛽](#𝛽)
- [\]](#)
- [Sharpen](#sharpen)
- [Blur](#blur)
  - [Gussian Blur](#gussian-blur)
- [Edge Detection](#edge-detection)
  - [Sobel Edge Detection](#sobel-edge-detection)
  - [Canny Edge Detection](#canny-edge-detection)
- [Data Augmentation (Giúp model học được nhiều tình huống hơn và giảm Overfitting)](#data-augmentation-giúp-model-học-được-nhiều-tình-huống-hơn-và-giảm-overfitting)
---
# Image (Bản chất ảnh)
**Ảnh trong máy tính được lưu như thế nào?**
```bash
Bản chất ảnh là một ma trận số (Numpy Array).

Ví dụ ảnh màu:
  img.shape = (H, W, C)
    - H (Height) = chiều cao
    - W (Width) = chiều rộng
    - C (Channel) = số kênh màu

Ví dụ:
  (720, 1280, 3)
    - 720 pixel cao
    - 1280 pixel rộng
    - 3 kênh màu
```
**Pixel là gì?**
```bash
Mỗi pixel chứa giá trị màu.

Ví dụ:
  img[0,0] = [255, 0, 0]
  => có nghĩa pixel góc trái là màu đỏ (trong RGB).

Thông thường mỗi kênh:
  - 0 → 255
  - 0 = không có màu đó
  - 255 = màu đó mạnh nhất
```
## RGB (hệ màu phối của red – green – blue)
```bash
Giá trị cao nhất là 255, thấp nhất là 0.
```
**Ex**
```bash
[255,0,0]   -> Đỏ
[0,255,0]   -> Xanh lá
[0,0,255]   -> Xanh dương
[255,255,255] -> Trắng
[0,0,0] -> Đen
=> Đây là chuẩn phổ biến nhất trong Deep Learning.
```
## BGR (OpenCV mặc định dùng Blue - Green - Red)
**Ex**
```bash
[255,0,0]
RGB → màu đỏ
BGR → màu xanh dương

Đây là lỗi rất hay gặp khi dùng OpenCV.
```
## Grayscale (Ảnh xám chỉ có 1 kênh màu)
```bash
Có:
  Shape: (H, W) thay vì (H, W, 3)

  Ví dụ:
    0   = đen
    255 = trắng
    128 = xám

Dùng khi:
  - OCR
  - Nhận diện chữ
  - Giảm kích thước dữ liệu
```
## HEX (giá trị thập lục phân)
## HSV là gì?

HSV =

Hue        (màu gì)
Saturation (độ đậm)
Value      (độ sáng)

Ví dụ:

Một màu đỏ có thể:

Hue = đỏ
Saturation = cao
Value = sáng

hoặc

Hue = đỏ
Saturation = thấp
Value = tối
Tại sao dùng HSV?

Tách riêng:

Màu sắc
↓
Độ sáng

nên dễ lọc màu hơn RGB.

Ví dụ:

Muốn tìm vật màu đỏ:

cv2.inRange(hsv, lower_red, upper_red)

dễ hơn rất nhiều so với RGB.s 
# Kernel (Weight)
**Kernel lấy ở đâu ra?**
```bash
Trường hợp 1 - xử lý ảnh truyền thống: Con người tự viết kernel
  1  0 -1
  1  0 -1
  1  0 -1
  hoặc
  -1 -1 -1
   0  0  0
   1  1  1
  => Những kernel này do con người thiết kế để phát hiện cạnh.

Trường hợp 2: CNN - Deep Learning: Con người không viết kernel nữa.
  Ban đầu máy tính tự tạo ngẫu nhiên

  Ví dụ:
    0.23  -0.51   0.18
    0.71   0.02  -0.66
    0.35  -0.14   0.49
    hoặc
    -0.82  0.15  0.44
    0.03 -0.29  0.67
    0.91  0.56 -0.11
    Đây là kernel ban đầu. 👉 Không ai biết nó có ý nghĩa gì cả. Nó chỉ là các số ngẫu nhiên
```
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
# Feature map (output sau khi kernel quét qua ảnh)
# FPS

Khi bạn làm bài toán CV (detect người, track object, camera AI…), hệ thống không xử lý “video” một lần, mà:

👉 tách video thành từng frame (ảnh tĩnh)
👉 xử lý từng frame
👉 ghép lại thành video

Video = chuỗi frame

Frame 1 → xử lý
Frame 2 → xử lý
Frame 3 → xử lý
...

👉 FPS = mỗi giây xử lý được bao nhiêu frame

🎯 Ví dụ dễ hiểu
FPS	Ý nghĩa
30 FPS	30 ảnh/giây (mượt bình thường)
60 FPS	rất mượt (game, real-time CV)
10 FPS	giật, chậm
1 FPS	gần như slideshow
⚡ FPS cao hay thấp có ý nghĩa gì?
🚀 FPS cao (tốt)
✔ xử lý nhanh
✔ phản hồi real-time tốt
✔ tracking mượt

👉 dùng trong:

camera AI
self-driving car
robot
video realtime detection

Ví dụ:

YOLO chạy 60 FPS → rất tốt
🐢 FPS thấp (xấu hoặc chậm)
✖ trễ (latency cao)
✖ không realtime
✖ dễ mất object khi tracking

Ví dụ:

2–5 FPS → gần như lag
detection chậm → camera bị “đứng hình”
📊 FPS trong Computer Vision phụ thuộc vào gì?
1. Model AI
YOLOv8 nano → nhanh
YOLOv8 large → chậm hơn
2. Hardware
CPU → chậm
GPU (RTX) → nhanh hơn nhiều lần
3. Input resolution
640x640 → nhanh
1920x1080 → chậm
4. Pipeline xử lý

Ví dụ:

decode video
→ preprocess
→ inference AI
→ postprocess
→ render

Càng nhiều bước → FPS càng giảm

🔥 FPS trong CV vs đời thực
Ứng dụng	FPS cần
Camera an ninh	10–15 FPS
Face recognition realtime	20–30 FPS
Self-driving	30–60 FPS
Gaming AI	60+ FPS
📌 FPS và latency liên quan gì?
FPS cao → latency thấp
FPS thấp → delay cao
FPS 30 → ~33ms/frame
FPS 10 → ~100ms/frame
FPS 1 → ~1000ms/frame
🧠 Tóm tắt cực dễ hiểu
FPS = tốc độ xử lý video trong CV

FPS cao → nhanh + mượt + realtime
FPS thấp → chậm + lag + trễ
⚠️ Một hiểu lầm phổ biến

❌ FPS cao = model tốt hơn
✔ Không đúng

👉 FPS chỉ nói về tốc độ, không nói về độ chính xác

Ví dụ:

Model	FPS	Accuracy
YOLO nano	80 FPS	thấp hơn
YOLO large	20 FPS	cao hơn
Nếu bạn muốn nâng level CV

Mình có thể giải thích thêm:

cách tăng FPS YOLO (quantization, TensorRT)
batching vs streaming
real-time pipeline architecture
OpenCV video processing tối ưu

Chỉ cần nói: “cách tăng FPS trong YOLO” 👍
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
# Convolution
**Tại sao mọi người lại làm tăng số chanel lên**
```bash

```
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
# BatchNorm (Chuẩn hóa dữ liệu đưa output về phân phối “chuẩn hơn” → học nhanh, ổn định)
```bash
Tại sao cần BatchNorm?
  1. Training nhanh hơn: giảm “internal covariate shift”
  2. Gradient ổn định: tránh exploding / vanishing
  3. Regularization nhẹ: giống noise → đỡ overfit
👉 BatchNorm làm 3 việc:
  + chuẩn hóa (mean = 0, var = 1)
  + scale lại (gamma)
  + shift lại (beta)
```
**Luồng hoạt động của BatchNorm**
<img src="../../../../../images/BatchNorm-Workflow.png">

**Ex: Code demo batchnorm**
[link demo cách hoạt động của batchNorm](./Practices.md#demo-cách-hoạt-động-của-batchnorm)
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
# Sharpen 
# Blur
```bash
- Ảnh = gồm:
  + Low-frequency → vùng mượt (trời, da, nền)
  + High-frequency → cạnh, chi tiết
- Vì vậy:
  + Blur (làm mờ)	Giữ low-frequency, loại high-frequency
  + Sharpen (làm nét)	Tăng high-frequency (cạnh)
  + Edge detection Chỉ giữ high-frequency
```
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
# Edge Detection
## Sobel Edge Detection 
**Ex**
```bash
10    10    10    200   200   200
Tối   Tối   Tối   Sáng  Sáng  Sáng

=> Giữa 10 và 200 có sự thay đổi rất mạnh → đó chính là cạnh.

Ý tưởng của Sobel:
  tính độ thay đổi cường độ sáng giữa các pixel lân cận.
  Ví dụ: Hiệu giữa hai vùng: 200 − 10 = 190 => rất lớn ⇒ Sobel kết luận: “Đây là cạnh.
```
## Canny Edge Detection 
```bash
Canny không chỉ hỏi “có thay đổi không?” 
  mà còn hỏi: 
    - Thay đổi có mạnh đủ không? 
    - Có phải nhiễu không?
    - Cạnh có liên tục không?
```
**Các bước của Canny**
```bash
1. Làm mờ ảnh (Gaussian Blur):
  Giảm nhiễu trước khi tìm cạnh.

2. Tính gradient
  Dùng Sobel để biết cạnh nằm ở đâu.

3. Làm mỏng cạnh
  Chỉ giữ đường cạnh mảnh nhất.

4. Ngưỡng kép (Double Threshold)
  Giữ cạnh mạnh, loại cạnh yếu hoặc nhiễu
```
# Data Augmentation (Giúp model học được nhiều tình huống hơn và giảm Overfitting)
Các kỹ thuật cơ bản
1. Flip (Lật ảnh)
Ví dụ:
🐱 → 🐱 (lật ngang)
Dùng khi:


Đối tượng có thể xuất hiện ở cả hai phía.


Classification, Object Detection thông thường.


Không nên dùng:


OCR (chữ sẽ bị ngược).


Biển báo, ký hiệu có hướng cố định.



2. Rotation (Xoay)
Ví dụ:
0° → 10° → -15°
Dùng khi:


Camera có thể nghiêng.


Ảnh thực tế không hoàn toàn thẳng.


Không nên:


Xoay 180° nếu ngoài thực tế đối tượng không bao giờ lộn ngược.



3. Color Jittering
Thay đổi:


Brightness


Contrast


Saturation


Hue


Ví dụ:


Chụp ban ngày


Chụp tối


Đèn vàng


Đèn trắng


Dùng khi:


Điều kiện ánh sáng thay đổi.



4. Random Crop
Cắt ngẫu nhiên một phần ảnh.
Ví dụ:
Ảnh gốc chứa con mèo toàn thân.
Crop chỉ còn:


Đầu mèo


Nửa thân mèo


Giúp model:


Tập trung đặc trưng quan trọng.


Không phụ thuộc vị trí chính xác của vật thể.



Kỹ thuật nâng cao chống Overfitting
5. MixUp
Trộn 2 ảnh lại với nhau.
Ví dụ:


70% ảnh mèo


30% ảnh chó


=> Label:


Cat = 0.7


Dog = 0.3


Model học mềm hơn, ít học thuộc dữ liệu.

6. CutMix
Lấy một vùng của ảnh A dán vào ảnh B.
Ví dụ:
Ảnh mèo
↓
Dán một phần ảnh chó vào.
Label:


Cat = 0.8


Dog = 0.2


Hiệu quả hơn MixUp cho:


Classification


Object Detection



Khi nào dùng gì?
Kỹ thuậtNên dùngFlipGần như luôn dùngRotationCamera có thể nghiêngColor JitterÁnh sáng thay đổiCropMuốn model robust với vị trí vật thểMixUpDataset nhỏ, dễ overfitCutMixDataset vừa/lớn, CNN hiện đại
Pipeline phổ biến trong production
Image ↓Random Flip ↓Random Rotation ↓Color Jitter ↓Random Crop ↓Normalize ↓Model
Nếu dataset nhỏ hoặc model bắt đầu overfit:
Flip + Rotation + Color Jitter + Crop + MixUp/CutMix
Đây là pipeline augmentation phổ biến cho các bài toán Computer Vision production hiện nay.