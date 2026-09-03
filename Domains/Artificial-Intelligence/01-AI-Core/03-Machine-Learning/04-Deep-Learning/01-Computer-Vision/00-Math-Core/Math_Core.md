- [Image (Bản chất ảnh)](#image-bản-chất-ảnh)
  - [RGB (hệ màu phối của red – green – blue)](#rgb-hệ-màu-phối-của-red--green--blue)
  - [BGR (OpenCV mặc định dùng Blue - Green - Red)](#bgr-opencv-mặc-định-dùng-blue---green---red)
  - [Grayscale (Ảnh xám chỉ có 1 kênh màu)](#grayscale-ảnh-xám-chỉ-có-1-kênh-màu)
  - [HEX (giá trị thập lục phân)](#hex-giá-trị-thập-lục-phân)
  - [HSV (Hue Saturation value)](#hsv-hue-saturation-value)
  - [LAB (CIELAB)](#lab-cielab)
  - [YCbCr](#ycbcr)
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
- [BatchNorm (Chuẩn hóa dữ liệu về phân phối “chuẩn hơn” giúp học nhanh, ổn định)](#batchnorm-chuẩn-hóa-dữ-liệu-về-phân-phối-chuẩn-hơn-giúp-học-nhanh-ổn-định)
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
  - [Sobel Edge Detection (dùng để tìm cạnh)](#sobel-edge-detection-dùng-để-tìm-cạnh)
  - [Canny Edge Detection](#canny-edge-detection)
- [Data Augmentation (Giúp model học được nhiều tình huống hơn và giảm Overfitting)](#data-augmentation-giúp-model-học-được-nhiều-tình-huống-hơn-và-giảm-overfitting)
- [Aspect Ratio](#aspect-ratio)
- [Erosion \& Dilation](#erosion--dilation)
- [Erosion](#erosion)
- [Dilation](#dilation)
- [Opening](#opening)
- [Closing](#closing)
- [Opening \& Closing](#opening--closing)
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
## HSV (Hue Saturation value)
```bash
Hue (H) = quyết định màu gốc (đỏ, vàng, xanh lá, xanh dương,...).
Saturation (S) = độ bão hòa (màu có đậm/rực hay nhạt gần xám).
Value (V) = độ sáng (sáng hay tối).

Hue	  Saturation	Value	  Màu
0°	  100%	      100%	  🔴 Đỏ
60°	  100%	      100%	  🟡 Vàng
120°	100%	      100%	  🟢 Xanh lá
180°	100%	      100%	  🟦 Cyan
240°	100%	      100%	  🔵 Xanh dương
300°	100%	      100%	  🟣 Tím
Nếu bạn đặt:
```
**Ex**
```bash
HSV(0°, 100%, 100%) → 🔴 đỏ thuần.
HSV(5°, 90%, 100%) → đỏ cam.
HSV(350°, 80%, 100%) → đỏ hồng.
```
## LAB (CIELAB)
```bash
Ứng dụng:
  - YCbCr được dùng trong gần như mọi chuẩn video:
    + JPEG
    + MPEG
    + H.264
    + H.265
    + AV1
    + Camera
    + TV
    + YouTube
=> Lý do là nén rất hiệu quả.
```
```bash
LAB mô tả màu bằng 3 thành phần:
  - L (Lightness): Độ sáng
  - a: Trục xanh lá ↔ đỏ
  - b: Trục xanh dương ↔ vàng

Có thể hình dung như thế này:
            +b
          (Vàng)
             ↑
             │
-a ←─────────┼────────→ +a
(Xanh lá)    │        (Đỏ)
             │
             ↓
         -b (Xanh dương)

Trong đó:
  - L = 0 → đen hoàn toàn
  - L = 100 → trắng hoàn toàn
```
**Ex**
```bash
Màu đỏ:
  - L = 55  # L vừa phải
  - a = +80 # a rất dương ⇒ rất đỏ
  - b = +60 # b hơi dương ⇒ hơi ngả vàng
→ Đỏ cam.

Màu xanh lá:
  - L = 70
  - a = -70 # a âm ⇒ xanh lá
  - b = +50 # b dương ⇒ hơi vàng
→ Xanh lá tươi.

Màu xanh dương:
  - L = 40
  - a = +10
  - b = -80 # b âm mạnh ⇒ xanh dương.
```
**Vì sao LAB hay dùng?**
```bash
Điểm mạnh nhất: Khoảng cách giữa hai màu gần giống với cảm nhận của mắt người.

Ví dụ:
  Màu A
  ↓
  dịch 5 đơn vị
  ↓
  Màu B
Khoảng cách 5 trong LAB gần như luôn có nghĩa là "khác nhau một chút". Trong RGB thì không như vậy.

Cho nên:
  - Photoshop
  - Color correction
  - AI xử lý ảnh
  - In ấn
=> rất thích dùng LAB.
```
## YCbCr
```bash
Nó tách thành:
  - Y = Độ sáng (Luminance)
  - Cb = Độ xanh dương
  - Cr = Độ đỏ
```
**Ex**
```bash
Một pixel đỏ:
  - Y = 80    # Y khá sáng
  - Cb = 90   
  - Cr = 240  # # Cr rất cao ⇒ đỏ mạnh

Pixel xanh dương:
  - Y = 60
  - Cb = 220 # Cb cao ⇒ xanh dương.
  - Cr = 100

Pixel xám:
  - Y = 120
  - Cb = 128 # Cb và Cr gần trung tính.
  - Cr = 128
→ Chỉ còn độ sáng.
```
**Tại sao lại tách như vậy?**
```bash
Mắt người nhạy với độ sáng hơn là màu sắc.

Ví dụ: ████████
  Nếu làm mờ màu nhưng giữ nguyên độ sáng,
    ta vẫn nhìn thấy vật thể khá rõ.

  Do đó người ta giữ:
    - Y ở độ phân giải đầy đủ.
    - Cb, Cr thì giảm xuống.
```
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
# BatchNorm (Chuẩn hóa dữ liệu về phân phối “chuẩn hơn” giúp học nhanh, ổn định)
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
## Sobel Edge Detection (dùng để tìm cạnh)
**Cách sử dụng sobel**
[cv2.Sobel](../../../../../../../Tech-Stacks/Programming-Languages/Python/00-Core/06-Libraries/01-AI-Libraries/00-ML/02-DL/00-CV/Preprocessing/OpenCV/Process_IMG.md#sobel)
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

# Aspect Ratio

Nó là:

$$ Aspect\ Ratio = \frac{Width}{Height} $$

Ví dụ ảnh:

Width  = 1920
Height = 1080

thì:

$$ AR = \frac{1920}{1080}=1.777... $$

→ thường gọi là 16:9.

7. Ví dụ các aspect ratio
200 × 200

→

1:1

Hình vuông.

400 × 200

→

2:1

Rộng gấp đôi chiều cao.

200 × 400

→

1:2

Cao gấp đôi chiều rộng.

8. Aspect Ratio cực kỳ quan trọng trong OCR

Đây là phần liên quan trực tiếp đến thứ bạn đang học.

Giả sử OCR detect được một text box:

┌─────────────────────────────────────────┐
│              HELLO WORLD                │
└─────────────────────────────────────────┘

Ví dụ:

width  = 300
height = 50

Aspect Ratio:

$$ 300/50 = 6 $$

Tức:

AR = 6:1

Đây là một bounding box rất rộng và thấp.

9. Tại sao OCR quan tâm Aspect Ratio?

Bởi vì text có hình dạng rất khác nhau.

Ví dụ:

HELLO WORLD

có thể:

300 × 50

→ AR = 6

Trong khi:

A

có thể:

40 × 50

→ AR = 0.8

Nếu bạn ép tất cả về:

224 × 224

thì:

HELLO WORLD
300 × 50

bị resize thành:

224 × 224

thì chữ sẽ bị bóp méo.

Ví dụ trực giác:

Original:

HELLO WORLD
────────────────────────

sau resize méo:

HELLO WORLD
────────

Các ký tự bị thay đổi tỷ lệ.

10. Đây là lý do OCR recognition thường quan tâm width

Đặc biệt khi bạn học CRNN.

Thay vì:

Text image
300 × 50
      ↓
224 × 224

có thể giữ tỷ lệ:

300 × 50
      ↓
240 × 40

hoặc chuẩn hóa height:

300 × 50
      ↓
Height = 32
Width  = 192

Sau đó CNN biến nó thành feature map:

192 × 32
    ↓
...
    ↓
feature sequence

Rồi đưa sequence đó cho:

BiLSTM
 ↓
CTC
 ↓
text

Đây là một trong những lý do OCR recognition khác image classification.

11. Aspect Ratio còn dùng trong Object Detection

Ví dụ bounding boxes:

Box A
100 × 100
AR = 1

Box B
200 × 100
AR = 2

Box C
100 × 300
AR = 0.33

Trong object detection, aspect ratio được dùng để:

thiết kế anchor boxes trong các detector kiểu anchor-based;
phân tích hình dạng object;
resize/crop dữ liệu;
đánh giá và xử lý bounding box.

Ví dụ nếu dataset chủ yếu có:

AR ≈ 2
AR ≈ 4
AR ≈ 8

thì việc thiết kế anchor có những aspect ratio tương ứng có thể giúp detector phù hợp hơn.

12. Hai khái niệm này đặt cạnh nhau
	KL Divergence	Aspect Ratio
Nó là gì?	Độ khác nhau giữa 2 phân phối	Tỷ lệ Width/Height
Đối tượng	Probability distribution	Image / bounding box
Công thức	\(\sum P\log(P/Q)\)	\(W/H\)
Dùng trong	ML, VAE, distillation, RL	CV, OCR, detection
Ví dụ	P=[.7,.2,.1] vs Q=[.6,.3,.1]	300×50 → AR=6
Liên quan OCR?	Có nhưng không phải cốt lõi ban đầu	Rất quan trọng
13. Đặt vào roadmap học OCR của bạn

Hai khái niệm này sẽ xuất hiện ở hai tầng khác nhau:

                    OCR
                     │
          ┌──────────┴──────────┐
          │                     │
      Detection             Recognition
          │                     │
          │                 CNN / CRNN
          │                     │
   Bounding Box                  │
          │                     │
   Aspect Ratio                  │
          │                     │
          └──────────────┐      │
                         │      │
                         ↓      ↓
                     Probability
                         │
                         ↓
                  CTC / Loss
                         │
                         ↓
                 KL / Cross Entropy

Aspect Ratio bạn sẽ gặp rất thường xuyên khi xử lý text box / crop / resize.

KL Divergence thì không phải thứ bạn cần ưu tiên ngay để hiểu CNN → CRNN. Với roadmap hiện tại của bạn, mình sẽ ưu tiên:

1. Convolution
2. Feature map
3. Receptive field
4. Padding / stride
5. Pooling
6. CNN feature extraction
7. Sequence modeling
8. RNN / LSTM / BiLSTM
9. CTC
10. Cross Entropy / KL Divergence

Đặc biệt, CTC là thứ bạn nên học trước KL Divergence nếu mục tiêu trước mắt là hiểu sâu OCR/CRNN.

# Erosion & Dilation 
là hai phép toán cơ bản của morphological image processing (xử lý hình thái ảnh), thường dùng trên ảnh nhị phân hoặc grayscale để làm sạch, nối, tách các vùng ảnh.

Nếu bạn đang học OCR/OpenCV thì hai phép này rất đáng hiểu vì chúng xuất hiện khá nhiều trong preprocessing.

1. Ý tưởng đơn giản nhất

Hãy tưởng tượng ảnh có:

1 = pixel trắng / vật thể
0 = pixel đen / background

Ví dụ:

0000000
0011100
0011100
0011100
0000000

Đây là một hình vuông trắng.

Erosion = "ăn mòn"

Nó làm vật thể trắng nhỏ lại.

0000000
0001000
0001000
0001000
0000000
Dilation = "giãn ra"

Nó làm vật thể trắng lớn ra.

0111110
0111110
0111110
0111110
0111110

Tất nhiên kết quả thực tế phụ thuộc vào kernel/structuring element.

2. Kernel đóng vai trò gì?

Ví dụ kernel:

111
111
111

Ta lấy kernel này đặt lên từng vị trí của ảnh.

Có thể hiểu kernel như một cái "khuôn" dùng để kiểm tra vùng xung quanh mỗi pixel.

3. Erosion

Với ảnh binary, cách hiểu đơn giản:

Erosion giữ lại pixel trắng nếu vùng kernel xung quanh nó gần như đều trắng.

Ví dụ:

Image:

00000
01110
01110
01110
00000

Kernel:

111
111
111

Pixel ở giữa:

111
111
111

→ toàn bộ trắng → giữ lại.

Nhưng pixel gần biên:

000
011
011

→ không đủ trắng → bị loại.

Kết quả:

00000
00000
00100
00000
00000

Vì vậy:

Erosion → object nhỏ lại.

4. Dilation

Dilation gần như ngược lại.

Nếu kernel chạm vào một vùng trắng, nó có xu hướng biến vùng đó thành trắng.

Ví dụ:

00000
00100
00000
00000
00000

Kernel:

111
111
111

Dilation:

00000
01110
01110
01110
00000

Một pixel trắng được lan rộng ra vùng xung quanh.

Vì vậy:

Dilation → object lớn ra.

5. Một ví dụ rất trực quan

Giả sử chữ A:

  1
 1 1
11111
1   1
1   1
Erosion

Làm nét chữ mỏng hơn:

  1
     
 111
1   1

Các pixel ở biên bị "ăn".

Dilation

Làm nét chữ dày hơn:

 111
11111
11111
11111
11 11

Các pixel được lan ra xung quanh.

6. Dùng để làm gì?

Đây mới là phần quan trọng.

Erosion thường dùng để
① Loại bỏ noise nhỏ

Ví dụ ảnh scan:

................
....####........
....####....#...
....####........
..........#.....

Hai dấu # nhỏ có thể là noise.

Erosion có thể làm những vùng nhỏ biến mất.

................
....####........
....####........
....####........
................
② Làm mỏng object

Nếu chữ/nét quá dày:

██████
██████
██████

Erosion có thể làm nó mỏng hơn.

③ Tách các object gần nhau

Ví dụ:

████████████
████████████

Hai object gần nhau có thể bị dính.

Erosion có thể làm chúng nhỏ lại và tách ra.

7. Dilation thường dùng để
① Làm dày nét

Ví dụ OCR:

--A--

Nét chữ bị quá mảnh hoặc đứt:

A  B  C

Dilation có thể làm nét dày hơn.

② Nối các vùng bị đứt

Ví dụ:

███  ███

Có một khoảng cách nhỏ.

Dilation:

████████

Có thể nối chúng lại.

③ Lấp các khoảng trống nhỏ

Ví dụ:

████ ████
████ ████

Dilation có thể làm vùng trắng mở rộng và lấp gap.

8. Opening và Closing

Đây là chỗ Erosion/Dilation bắt đầu rất hữu ích trong thực tế.

Opening
Opening = Erosion → Dilation

Dùng khi muốn:

Loại noise nhỏ nhưng giữ hình dạng object lớn.

Ví dụ:

Object + noise

→ Erosion:

Object nhỏ lại + noise biến mất

→ Dilation:

Object trở lại gần kích thước ban đầu
Opening thường dùng:
remove small noise
remove small objects
tách các vùng nhỏ
preprocessing trước OCR
9. Closing
Closing = Dilation → Erosion

Ngược lại:

Lấp lỗ nhỏ và nối các vùng gần nhau.

Ví dụ:

████ ████
████ ████

→ Dilation:

██████████
██████████

→ Erosion:

████████
████████

Khoảng trống nhỏ được đóng lại.

Closing thường dùng:
nối nét chữ bị đứt
lấp hole nhỏ
nối các vùng gần nhau
làm bounding region liên tục hơn
10. Trong OCR thì dùng thế nào?

Đây là phần liên quan trực tiếp đến thứ bạn đang học.

Giả sử OCR nhận được ảnh:

Original scan

T h i s

Nhưng ảnh scan có noise:

T .h i.s
. . . . .

Có thể dùng:

Grayscale
    ↓
Threshold
    ↓
Binary image
    ↓
Morphological operation
    ↓
OCR

Ví dụ:

Noise nhỏ
Binary
   ↓
Opening
   ↓
Clean image
   ↓
OCR
Chữ bị đứt nét
Binary
   ↓
Closing
   ↓
Connected characters
   ↓
OCR
11. OpenCV code
import cv2

image = cv2.imread("image.png", cv2.IMREAD_GRAYSCALE)

kernel = cv2.getStructuringElement(
    cv2.MORPH_RECT,
    (3, 3)
)

# Erosion
eroded = cv2.erode(image, kernel)

# Dilation
dilated = cv2.dilate(image, kernel)

# Opening
opening = cv2.morphologyEx(
    image,
    cv2.MORPH_OPEN,
    kernel
)

# Closing
closing = cv2.morphologyEx(
    image,
    cv2.MORPH_CLOSE,
    kernel
)
12. Kernel càng lớn thì sao?

Đây là một insight rất quan trọng.

kernel = 3x3

→ tác động nhẹ.

kernel = 5x5

→ tác động mạnh hơn.

kernel = 9x9

→ tác động rất mạnh.

Ví dụ dilation:

3x3 kernel
    ↓
██████

Object lớn hơn một chút.

Nhưng:

9x9 kernel
    ↓
████████████████

Object có thể phình rất nhiều.

Kernel size và shape quyết định morphology tác động lên ảnh như thế nào.

13. Nhớ bằng một bảng
Operation	Tác động	Thường dùng
Erosion	Object nhỏ lại	Remove noise, làm mỏng
Dilation	Object lớn ra	Nối vùng, làm dày
Opening	Erosion → Dilation	Remove noise nhỏ
Closing	Dilation → Erosion	Lấp gap/hole, nối vùng

Có thể nhớ cực ngắn:

EROSION   = SHRINK
DILATION  = GROW

OPENING   = REMOVE SMALL NOISE
CLOSING   = CLOSE SMALL GAPS
Liên hệ với pipeline OCR của bạn

Nếu pipeline hiện tại là:

Image
 ↓
Grayscale
 ↓
Threshold
 ↓
CNN

thì morphology thường nằm trước CNN, như một bước preprocessing:

Image
 ↓
Grayscale
 ↓
Threshold
 ↓
Erosion / Dilation
 ↓
Opening / Closing
 ↓
CNN
 ↓
Feature extraction
 ↓
Recognition

Nhưng không phải cứ OCR là phải dùng Erosion/Dilation. Nếu ảnh đã sạch thì morphology thậm chí có thể làm mất chi tiết chữ. Đây là preprocessing phụ thuộc vào chất lượng và đặc tính dữ liệu.

# Opening & Closing
Đúng chỗ này rất đáng hiểu kỹ, vì Opening và Closing không phải là hai phép hoàn toàn mới. Chúng chỉ là cách kết hợp Erosion và Dilation theo một thứ tự nhất định.

1. Opening là gì?

Opening = Erosion → Dilation

Input
  ↓
Erosion
  ↓
Dilation
  ↓
Output

Ý tưởng:

Opening dùng để loại bỏ những vùng trắng nhỏ/noise nhỏ, trong khi cố gắng giữ lại object lớn.

Ví dụ

Giả sử ảnh binary:

000000000
001110000
001110010
001110000
000100000
000000000

Ta có:

Object lớn ở bên trái
Một noise nhỏ 1 ở bên phải
       noise
          ↓
001110010
       ↑
   object
Bước 1: Erosion

Erosion làm mọi object nhỏ lại.

Noise quá nhỏ → biến mất.

000000000
000100000
000100000
000100000
000000000
000000000
Bước 2: Dilation

Sau đó dilation làm object lớn trở lại gần kích thước ban đầu.

Noise đã biến mất thì không tự xuất hiện lại.

Vì vậy:

Opening
= Erosion + Dilation
= Remove small objects/noise
2. Tại sao không chỉ dùng Erosion?

Đây là điểm quan trọng.

Nếu chỉ:

Erosion

thì noise biến mất, nhưng object chính cũng bị co lại.

Ví dụ:

Original

██████
██████
██████
██████

Erosion:

████
████

Object bị nhỏ đi.

Opening:

Erosion
   ↓
████
████
   ↓
Dilation
   ↓
██████
██████

Object được phục hồi gần kích thước ban đầu.

→ Noise nhỏ bị loại, object lớn được giữ tương đối nguyên.

3. Khi nào dùng Opening?

Hãy nghĩ:

"Tôi muốn REMOVE thứ nhỏ."

Ví dụ:

Ảnh scan có noise
████████
████████
   ·
       ·

Các dấu · nhỏ là noise.

Dùng:

Opening

→ loại bỏ noise.

OCR

Ví dụ chữ:

H E L L O

nhưng scan có các chấm nhỏ:

H·E L·L O

Opening có thể giúp loại các thành phần nhỏ không mong muốn nếu kernel được chọn phù hợp.

Pipeline:

Image
 ↓
Grayscale
 ↓
Threshold
 ↓
Opening
 ↓
OCR
4. Closing là gì?

Closing = Dilation → Erosion

Ngược lại với Opening.

Input
  ↓
Dilation
  ↓
Erosion
  ↓
Output

Ý tưởng:

Closing dùng để lấp các khoảng trống nhỏ và nối các vùng trắng gần nhau.

Ví dụ

Giả sử chữ/nét bị đứt:

████  ████

Có một khoảng trống nhỏ ở giữa.

Bước 1: Dilation

Dilation làm object phình ra:

████████████

Hai phần có thể chạm nhau.

Bước 2: Erosion

Sau đó erosion làm object co lại:

██████████

Khoảng gap nhỏ đã được đóng lại.

Đó là lý do gọi là:

Closing = đóng các khoảng trống nhỏ.

5. Khi nào dùng Closing?

Hãy nghĩ:

"Tôi muốn CONNECT hoặc FILL thứ nhỏ."

Trường hợp 1: Nét bị đứt
████  ████

→ Closing:

██████████
Trường hợp 2: Có hole nhỏ
████████
███  ███
████████

→ Closing có thể lấp hole:

████████
████████
████████
Trường hợp 3: Hai vùng gần nhau
█████ █████

Nếu khoảng cách đủ nhỏ so với kernel:

Closing
   ↓
███████████

Hai vùng được nối thành một vùng.

6. So sánh Opening và Closing

Đây là cách mình khuyên bạn nhớ:

	Opening	Closing
Công thức	Erosion → Dilation	Dilation → Erosion
Mục đích	Remove	Connect / Fill
Loại bỏ noise nhỏ	✅	❌
Loại bỏ object nhỏ	✅	❌
Nối vùng gần nhau	❌	✅
Lấp gap nhỏ	❌	✅
Lấp hole nhỏ	❌	✅
Làm sạch ảnh	✅	Có thể
OCR	Noise	Nét chữ bị đứt
7. Một cách nhớ cực dễ

Hãy nhớ 2 từ:

OPENING  → REMOVE
CLOSING  → CONNECT

Hoặc:

Opening:
Erosion → Dilation
      ↓
  bỏ vật nhỏ


Closing:
Dilation → Erosion
      ↓
  nối/lấp khoảng nhỏ
8. Tại sao phải Erosion trước Opening?

Đây là câu hỏi rất hay nếu bạn muốn hiểu bản chất thay vì học thuộc.

Opening:

Erosion → Dilation

Erosion trước để:

giết những object quá nhỏ.

Sau đó Dilation:

phục hồi object lớn.

Object nhỏ đã bị xóa ở bước Erosion thì Dilation không thể "hồi sinh" nó.

9. Tại sao Closing phải Dilation trước?

Closing:

Dilation → Erosion

Dilation trước để:

làm các vùng gần nhau chạm vào nhau và lấp gap nhỏ.

Sau đó Erosion:

co object trở lại gần kích thước ban đầu.

10. Liên hệ trực tiếp với OCR

Đây là cách bạn nên suy nghĩ khi gặp một ảnh OCR:

Case A — ảnh có nhiều chấm noise
Text + noise

H . E . L . L O .

Bạn muốn:

REMOVE

→ thử Opening.

Case B — chữ bị đứt nét
H E L  L O
      ↑
    nét đứt

Bạn muốn:

CONNECT

→ thử Closing.

Case C — ảnh đã sạch
HELLO

→ không cần morphology.

Đây là điểm quan trọng:

Không phải OCR nào cũng nên dùng Opening/Closing.

Nếu kernel quá lớn, bạn có thể:

Opening → làm mất nét chữ
Closing → làm các chữ dính vào nhau

Vì vậy phải chọn kernel size/shape dựa trên kích thước noise, độ dày nét và khoảng cách giữa các vùng.

Nếu muốn hiểu sâu hơn

Bạn nên học tiếp theo thứ tự này:

Erosion
   ↓
Dilation
   ↓
Opening = Erosion → Dilation
   ↓
Closing = Dilation → Erosion
   ↓
Kernel / Structuring Element
   ↓
Tại sao kernel 3×3, 5×5 lại cho kết quả khác nhau?
   ↓
Morphology trong OCR

Phần kernel/structuring element mới là phần rất đáng học tiếp, vì khi hiểu nó bạn sẽ tự suy ra được tại sao Opening loại được noise nào, Closing nối được gap nào, thay vì chỉ nhớ OPEN = erosion + dilation.
1. Scharr

Scharr = tính gradient của ảnh, tương tự Sobel nhưng thường cho gradient theo hướng x/y chính xác hơn với kernel nhỏ.

Ví dụ:

Image
  ↓
Scharr X
  ↓
Gradient theo chiều ngang

Image
  ↓
Scharr Y
  ↓
Gradient theo chiều dọc

Nó tìm nơi pixel thay đổi mạnh.

Ví dụ cạnh:

████████│░░░░░░░░
████████│░░░░░░░░
████████│░░░░░░░░
         ↑
        edge

Scharr sẽ cho phản ứng mạnh ở vị trí edge.

Dùng khi nào?
Edge detection
Tìm gradient
Phân tích texture
Preprocessing CV
Khi muốn gradient tốt hơn Sobel 3×3
2. Laplacian

Laplacian sử dụng đạo hàm bậc hai.

Nếu Scharr/Sobel hỏi:

"Ảnh thay đổi nhanh đến mức nào?"

thì Laplacian gần với:

"Gradient đang thay đổi nhanh đến mức nào?"

Ví dụ:

Image
 ↓
Gradient
 ↓
Laplacian
 ↓
Edge / sharp change
Dùng:
Edge detection
Detect vùng thay đổi mạnh
Sharpening
Blur detection

Ví dụ một ảnh bị blur:

Sharp image
→ gradient mạnh
→ Laplacian variance lớn

Blur image
→ gradient yếu
→ Laplacian variance nhỏ

Nên người ta đôi khi dùng:

cv2.Laplacian(image, cv2.CV_64F).var()

để đánh giá ảnh có bị blur hay không.

3. Binary

Binary image = ảnh chỉ có 2 giá trị, thường:

0 = black
255 = white

Ví dụ:

Grayscale:

120 130 250
20  40  230

threshold:

< 128 → 0
>= 128 → 255

thành:

0   255 255
0   0   255
Dùng khi nào?

Khi bạn muốn tách:

foreground
vs
background

Rất phổ biến trong OCR.

4. Adaptive Threshold

Threshold nhưng ngưỡng không cố định cho toàn ảnh.

Global threshold:

if pixel > 128:
    white
else:
    black

Adaptive:

threshold(x, y)

được tính dựa trên vùng lân cận.

Ví dụ ảnh:

████████████
██████░░░░░░
██████░░░░░░

Một bên sáng, một bên tối.

Threshold cố định có thể thất bại.

Adaptive threshold:

mỗi vùng có threshold riêng.

Dùng khi:
Lighting không đều
Document scan bị bóng
OCR
Camera chụp giấy
Background thay đổi độ sáng
5. Otsu

Otsu cũng là thresholding nhưng:

Tự động tìm threshold tốt nhất cho toàn ảnh.

Ví dụ bạn không biết:

threshold = ?

Otsu tìm nó dựa trên histogram.

Histogram

       █
       █
   █   █
   █   █       ███
___█___█_______███____
       ↑
    threshold
Dùng khi:

Ảnh có foreground/background tương đối rõ ràng.

Ví dụ:

_, binary = cv2.threshold(
    gray,
    0,
    255,
    cv2.THRESH_BINARY + cv2.THRESH_OTSU
)
Nhớ:
Binary   = kết quả / kiểu threshold
Otsu     = cách tự chọn threshold
Adaptive = threshold thay đổi theo local region
6. findContours

Sau khi có binary image:

000000
011110
010010
011110
000000

findContours tìm đường biên của object.

Image
 ↓
Binary
 ↓
findContours
 ↓
Contour 1
Contour 2
...
Dùng:
tìm object
tìm boundary
tìm chữ
tìm blob
đo diện tích
bounding box

Ví dụ:

contours, hierarchy = cv2.findContours(...)
7. convexHull

Cho một contour:

      *
   *     *
 *         *
    *  *

Convex hull tìm bao lồi nhỏ nhất chứa toàn bộ điểm.

Tưởng tượng:

dùng một sợi dây cao su quấn quanh object.

    __________
   /          \
  /    ****    \
 /  **    **    \
 \______________/
Dùng:
shape analysis
hand detection
object geometry
convexity defects
so sánh hình dạng
8. Moments

Image moments cho bạn thông tin hình học của object.

Ví dụ từ contour có thể tính:

area
centroid
center of mass
orientation-related quantities

Centroid:

Cx = M10 / M00
Cy = M01 / M00

Ví dụ object:

  ███
 █████
  ███
   ↑
 centroid
Dùng:
tìm tâm object
tracking object
shape analysis
tính center của contour
9. WarpAffine

Affine transformation giữ các quan hệ song song.

Bao gồm:

translation
rotation
scaling
shear

Ví dụ:

Original

┌──────┐
│      │
│      │
└──────┘

      ↓ WarpAffine

   ┌──────┐
  /      /
 /______/
Dùng:
rotate
resize
shift
align image
data augmentation

Affine transformation dùng ma trận:

[x']
[y']
[1]

với ma trận 2×3.

10. Perspective

Perspective transformation xử lý biến dạng do góc nhìn.

Ví dụ chụp tờ giấy:

Camera

    ________
   /       /
  /_______/

Bạn muốn biến thành:

┌────────────┐
│            │
│   TEXT     │
│            │
└────────────┘

Đây thường gọi là:

Perspective transform / perspective warp

Dùng:
document scanning
OCR
biển số xe
rectify image
bird-eye view
11. FFT

FFT = Fast Fourier Transform.

Nó chuyển ảnh từ:

Spatial Domain

sang:

Frequency Domain

Thay vì nhìn:

pixel ở đâu?

ta nhìn:

ảnh chứa những tần số nào?

Ví dụ:

Image
 ↓
FFT
 ↓
Frequency representation
Dùng:
frequency analysis
filtering
remove periodic noise
blur/sharpen
signal processing
12. Frequency Domain

Đây không phải một thuật toán cụ thể.

Nó là cách biểu diễn dữ liệu theo tần số.

Spatial domain:

pixel(x, y)

Frequency domain:

frequency(u, v)

Ví dụ:

Spatial:

████████
░░░░░░░░
████████
░░░░░░░░

→ có pattern lặp lại

Frequency domain sẽ thể hiện mạnh các frequency tương ứng với pattern đó.

13. Low-pass

Low-pass filter:

giữ low frequency, loại high frequency.

High frequency thường liên quan đến:

edge
noise
chi tiết nhỏ

Low frequency liên quan đến:

vùng lớn
thay đổi chậm
illumination

Vì vậy:

Low-pass
   ↓
Smooth / Blur
Dùng:
denoise
smoothing
remove high-frequency noise
preprocessing

Ví dụ Gaussian blur về bản chất có thể nhìn dưới góc frequency domain như một low-pass filter.

14. High-pass

Ngược lại:

giữ high frequency.

High-pass
   ↓
Edge / Fine detail
Dùng:
edge enhancement
sharpening
texture detection
detail extraction

Có thể nhớ:

Low-pass  → Smooth
High-pass → Detail / Edge
15. Harris

Harris Corner Detector tìm corner.

Một corner là nơi intensity thay đổi mạnh theo nhiều hướng.

Ví dụ:

████
████
██░░
██░░
 ↑
corner

Một edge chỉ thay đổi mạnh theo một hướng.

Corner thay đổi mạnh theo nhiều hướng.

Dùng:
feature detection
tracking
image registration
geometric analysis
16. Shi-Tomasi

Shi-Tomasi cũng tìm corner.

Nó là một cải tiến/biến thể dựa trên ý tưởng của Harris.

Điểm quan trọng:

Harris:
corner response

Shi-Tomasi:
"Good Features to Track"

Shi-Tomasi thường rất phù hợp khi cần chọn các điểm tốt để tracking.

Dùng:
feature tracking
Lucas-Kanade
motion estimation
17. SIFT

SIFT = Scale-Invariant Feature Transform.

Nó không chỉ tìm corner.

Nó tìm:

keypoints + descriptor

Ví dụ:

Image A
   ↓
SIFT
   ↓
keypoints
   +
descriptors

Descriptor mô tả vùng xung quanh keypoint.

Điểm mạnh:

scale invariant
rotation invariant
khá robust với viewpoint/illumination thay đổi
Dùng:
image matching
object recognition
image registration
panorama
18. SURF

SURF cũng là feature detector + descriptor.

Mục tiêu tương tự SIFT nhưng thiết kế để nhanh hơn bằng các kỹ thuật xấp xỉ.

SIFT
vs
SURF

SURF từng rất phổ biến nhưng vấn đề licensing/patent khiến OpenCV hiện đại không phải lựa chọn mặc định như ORB.

Dùng:
feature matching
image registration
object recognition
19. ORB

ORB = Oriented FAST and Rotated BRIEF.

Nó kết hợp:

FAST → keypoint detection
BRIEF → descriptor

và bổ sung orientation.

Điểm rất quan trọng:

ORB nhanh hơn SIFT rất nhiều trong nhiều trường hợp và descriptor dạng binary.

Dùng:
real-time matching
robotics
SLAM
object matching
mobile/computer vision
20. BFMatcher

BF = Brute Force Matcher.

Bạn có:

Image A
SIFT/ORB
 ↓
Descriptors A

Image B
SIFT/ORB
 ↓
Descriptors B

BFMatcher thử so sánh descriptor của A với descriptor của B.

Ví dụ:

descriptor A1
   ↓
A2
A3
A4
...

Tìm cái gần nhất.

Dùng:
matching keypoints
object matching
image registration
21. FLANN

FLANN = Fast Library for Approximate Nearest Neighbors.

Thay vì brute-force mọi descriptor:

A1 ↔ B1
A1 ↔ B2
A1 ↔ B3
...

nó xây cấu trúc dữ liệu để tìm nearest neighbor nhanh hơn.

Dùng:

Khi:

số lượng descriptors lớn

và bạn muốn matching nhanh.

22. Homography

Homography mô tả quan hệ projective giữa hai mặt phẳng.

Ví dụ:

Image A                 Image B

┌────────┐              /────────/
│        │      →      /        /
│  TEXT  │            /  TEXT  /
└────────┘            /────────/

Nếu hai ảnh nhìn cùng một mặt phẳng nhưng từ hai góc khác nhau, homography có thể map điểm này sang điểm kia.

Công thức:

p' = H p

trong homogeneous coordinates.

Dùng:
panorama
document rectification
image registration
perspective correction
planar object tracking
23. Perspective

Bạn có Perspective ở #10 và #22.

Thực chất chúng liên quan rất chặt:

Perspective Transform
       ↓
Homography
       ↓
3×3 matrix H

Ví dụ:

4 điểm source
      ↓
4 điểm destination
      ↓
findHomography
      ↓
H
      ↓
warpPerspective
24. Lucas-Kanade

Lucas-Kanade dùng để tracking motion của points giữa các frame.

Video:

Frame t

    ●

Frame t+1:

       ●
       ↑
     motion

Lucas-Kanade tìm:

(x, y)
   ↓
(x + dx, y + dy)
Dùng:
optical flow
point tracking
motion estimation

Thường kết hợp:

Shi-Tomasi
   ↓
Good points
   ↓
Lucas-Kanade
   ↓
Track points

Đây là một pipeline rất kinh điển.

25. Farneback

Farneback cũng là optical flow.

Nhưng khác Lucas-Kanade:

Lucas-Kanade

Theo dõi một tập điểm:

●  ●  ●
 ↓  ↓  ↓
●  ●  ●
Farneback

Ước lượng dense optical flow:

→ → → → →
→ → → → →
→ → → → →
→ → → → →

Gần như mỗi pixel có motion vector.

Dùng:
motion estimation
video analysis
action analysis
moving object detection
26. KCF

KCF = Kernelized Correlation Filters.

Đây là object tracker.

Bạn cho bounding box ban đầu:

Frame 1

┌────────┐
│ object │
└────────┘

KCF theo object:

Frame 2

    ┌────────┐
    │ object │
    └────────┘
Ưu:
nhanh
phù hợp real-time
Nhược:
dễ fail khi object thay đổi mạnh
occlusion
scale change lớn
27. CSRT

CSRT cũng là object tracker.

So với KCF:

KCF  → nhanh hơn
CSRT → thường robust/chính xác hơn

CSRT xử lý spatial information tốt hơn.

Dùng:

Khi:

accuracy > speed

Ví dụ tracking object trong video mà object thay đổi kích thước/appearance.

28. Stereo Matching

Stereo vision:

Left Camera       Right Camera

    📷                📷
     \                /
      \              /
       \            /
          Object

Hai camera nhìn cùng scene.

Ta tìm:

pixel bên trái
       ↕
pixel bên phải

Độ lệch này gọi là disparity.

disparity
    ↓
depth
Dùng:
3D reconstruction
robot
autonomous driving
depth estimation
29. Depth

Depth = khoảng cách từ camera đến object.

Ví dụ:

Camera

│
│  1m
│
● Object A

│
│  5m
│
● Object B

Depth map:

near → bright
far  → dark

tùy cách visualization.

Dùng:
3D vision
robotics
AR/VR
obstacle detection
autonomous driving
30. Intrinsic

Intrinsic = thông số bên trong camera.

Ví dụ:

fx
fy
cx
cy

Camera matrix:

K =
[ fx  0  cx ]
[ 0  fy  cy ]
[ 0   0   1 ]

Nó mô tả:

Camera biến điểm 3D thành pixel như thế nào, xét các thông số quang học/hình học bên trong.

31. Extrinsic

Extrinsic = vị trí và orientation của camera trong world.

Thường:

R = Rotation
t = Translation

Camera:

World
  ↓
R, t
  ↓
Camera coordinate system

Nó trả lời:

Camera đang ở đâu và đang nhìn theo hướng nào?

32. Calibration

Calibration là quá trình ước lượng intrinsic + distortion, và tùy bài toán có thể ước lượng extrinsic.

Ví dụ dùng chessboard:

┌─┬─┬─┬─┬─┐
├─┼─┼─┼─┼─┤
├─┼─┼─┼─┼─┤
└─┴─┴─┴─┴─┘

Chụp chessboard ở nhiều góc.

OpenCV tìm:

Camera Matrix
+
Distortion Coefficients

Sau đó:

distorted image
       ↓
undistort
       ↓
correct image
Dùng:
camera calibration
stereo vision
3D reconstruction
robotics
measurement
33. Autograd

Đây chuyển sang Deep Learning.

Autograd = automatic differentiation.

Bạn có:

x
 ↓
y = f(x)
 ↓
loss

Autograd tự tính:

∂loss/∂x

Trong PyTorch:

x = torch.tensor(2.0, requires_grad=True)

y = x ** 2

y.backward()

print(x.grad)

Kết quả:

dy/dx = 2x = 4

Đây chính là nền tảng của:

Forward
 ↓
Loss
 ↓
Backpropagation
 ↓
Gradient
 ↓
Optimizer
 ↓
Update weights

Liên hệ trực tiếp với CNN mà bạn đang học.

34. AMP

AMP = Automatic Mixed Precision.

Thay vì tất cả phép tính đều:

FP32

ta dùng kết hợp:

FP16 / BF16
+
FP32

Ví dụ:

Forward
 ↓
FP16/BF16
 ↓
faster + less memory
 ↓
some operations FP32
Mục đích:
giảm VRAM
tăng tốc training
cho phép batch size lớn hơn

Ví dụ PyTorch hiện đại thường dùng:

with torch.autocast(device_type="cuda"):
    output = model(x)
    loss = criterion(output, target)

AMP rất hữu ích khi train model lớn trên GPU.

35. DDP

DDP = Distributed Data Parallel.

Bạn có:

GPU 0
GPU 1
GPU 2
GPU 3

thay vì:

Model
 ↓
GPU 0

DDP chạy:

          Model
       /    |    \
     GPU0 GPU1 GPU2 GPU3
       \    |    /
       Gradient Sync
             ↓
       Update weights

Mỗi GPU có một bản copy model và xử lý một phần batch.

Ví dụ:

Batch = 256

GPU0 → 64
GPU1 → 64
GPU2 → 64
GPU3 → 64

Sau đó gradient được synchronize.

Dùng khi:
1 GPU không đủ

hoặc:

muốn training nhanh hơn với nhiều GPU
Quan trọng: đừng học 32 cái này theo kiểu thuộc lòng

Nếu mục tiêu của bạn là thực sự mạnh về Computer Vision, mình sẽ ưu tiên theo thứ tự này:

Level 1 — Image fundamentals
Grayscale
 ↓
Binary
 ↓
Threshold
 ↓
Otsu
 ↓
Adaptive Threshold
 ↓
Erosion
 ↓
Dilation
 ↓
Opening
 ↓
Closing

Bạn sẽ hiểu preprocessing.

Level 2 — Edge + shape
Sobel
Scharr
Laplacian
 ↓
findContours
 ↓
Moments
 ↓
ConvexHull

Bạn sẽ hiểu:

Làm sao máy nhìn thấy edge và hình dạng?

Level 3 — Geometry
Affine
 ↓
WarpAffine

Perspective
 ↓
Homography
 ↓
WarpPerspective

Đây cực kỳ quan trọng cho OCR/document.

Level 4 — Frequency
FFT
 ↓
Frequency Domain
 ↓
Low-pass
 ↓
High-pass

Hiểu sâu hơn về:

ảnh thực chất chứa những frequency nào?

Level 5 — Features
Harris
 ↓
Shi-Tomasi
 ↓
SIFT
 ↓
ORB
 ↓
BFMatcher / FLANN

Lúc này bạn bắt đầu hiểu:

Làm sao tìm một điểm đặc trưng và nhận ra điểm tương ứng trong ảnh khác?

Level 6 — Motion
Lucas-Kanade
 ↓
Farneback
 ↓
KCF
 ↓
CSRT

Hiểu:

Làm sao biết object/pixel di chuyển như thế nào giữa các frame?

Level 7 — 3D
Camera
 ↓
Intrinsic
Extrinsic
 ↓
Calibration
 ↓
Stereo Matching
 ↓
Disparity
 ↓
Depth
 ↓
3D

Đây là nền tảng Computer Vision 3D.

Level 8 — Deep Learning engineering
Autograd
 ↓
Backpropagation
 ↓
AMP
 ↓
DDP

Đây là phần kết nối với PyTorch training.

Và có một "map" rất đáng nhớ

Toàn bộ danh sách của bạn thực chất đang trả lời 7 câu hỏi khác nhau:

1. Ảnh thay đổi ở đâu?
   → Scharr, Laplacian

2. Pixel nào thuộc object?
   → Binary, Otsu, Adaptive

3. Object có hình dạng gì?
   → Contour, Hull, Moments

4. Ảnh bị biến dạng/góc nhìn thế nào?
   → Affine, Perspective, Homography

5. Ảnh chứa những pattern/frequency nào?
   → FFT, Frequency Domain, Low/High-pass

6. Hai ảnh/frame có điểm/object nào giống nhau hoặc di chuyển?
   → Harris, Shi-Tomasi, SIFT, ORB
   → BFMatcher, FLANN
   → Lucas-Kanade, Farneback, KCF, CSRT

7. Làm sao suy ra thế giới 3D và train model hiệu quả?
   → Stereo, Depth, Intrinsic, Extrinsic, Calibration
   → Autograd, AMP, DDP

Nếu bạn đang học để đi sâu vào OCR, thì trong cả danh sách này, mình sẽ ưu tiên đặc biệt:

Binary
→ Otsu / Adaptive
→ Erosion / Dilation / Opening / Closing
→ Scharr / Laplacian
→ Contour / Moments
→ Affine / Perspective / Homography
→ FFT cơ bản
→ CNN
→ RNN / BiLSTM
→ CTC
→ Transformer

Còn Harris → SIFT → ORB → BFMatcher → FLANN → optical flow → stereo là một nhánh rất quan trọng của classical Computer Vision, nhưng không cần chen vào giữa quá trình học CRNN/OCR recognition.