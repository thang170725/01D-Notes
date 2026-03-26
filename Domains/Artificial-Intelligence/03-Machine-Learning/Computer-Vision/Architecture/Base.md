- [Architecture](#architecture)
  - [CNN (Convolutional Neural network)](#cnn-convolutional-neural-network)
  - [ResNet](#resnet)
  - [RetinaNet](#retinanet)
---
# Architecture
## CNN (Convolutional Neural network)
```bash
- Được thiết kế để xử lý dữ liệu có cấu trúc dạng lưới, ví dụ như hình ảnh.
- Cấu trúc 3 tầng:
    + Convolutional: CNN sử dụng một bộ lọc nhỏ (filter hoặc kernel) trượt trên ảnh đầu vào để lấy ra những đặc trưng nhỏ như cạnh, góc, hay các mẫu đơn giản. Bộ lọc này sẽ quét khắp ảnh. Phát hiện các đặc điểm quan trọng tại nhiều vị trí. Mỗi kernel học một đặc trưng khác nhau
    + Pooling: Giúp giảm kích thước dữ liệu sau khi tích chấp, làm cho mạng nhẹ hơn, giảm tính toán, đồng thời giữ lại đặc trưng quan trọng. Ví dụ, max pooling chọn giá trị lớn nhất trong một vùng nhỏ.
    + Fully connected: Sau các lớp convolutional và pooling, dữ liệu đặc trưng được dàn phẳng và dựa vào các lớp MLP để phân loại hay dự đoán.
```
**Pipeline**
```bash
Original Image (HxWxC) (Ex: 224x224x3)
      ↓
Preprocess Image (height x width)
      ↓
┌──────────────────────────────────────────────────────────────────────────────────────────────────┐
│ CNN                                                                                              │
│  ├─ Convolution Layer (trích xuất đặc trưng bằng kernel) (H'xW'xF)                               │
│  ├─ Activation Function (ReLU)                                                                   │ x N layer
│  ├─ BatchNorm                                                                                    │
│  └─ Pooling                                                                                      │
└──────────────────────────────────────────────────────────────────────────────────────────────────┘
      ↓
Flatten (Chuyển sang vector) (VD: 7x7x512 -> 25088 chiều)
      ↓
Fully Connected Layer (Giống MLP truyền thống)
      ↓
Softmax 
      ↓
Loss Function
      ↓
Backpropagation (lan truyền ngược)
```
## ResNet
```bash
- ResNet (Residual Network) là một kiến trúc CNN sâu dùng để:
  + Trích xuất đặc trưng mạnh từ ảnh và giải quyết bài toán thị giác máy tính phức tạp.
  + Nó nổi tiếng vì đưa ra skip connection (residual connection) giúp huấn luyện được mạng rất sâu (50, 101, 152 layer…) mà không bị vanishing gradient.
- Ứng dụng:
  + Image Classification
  + Object Detection
  + Image Segmentation (phân vùng ảnh)
  + Face Recognition 
  + Medical AI
  + Autonomous Driving
```
**Pipeline**
```bash
Original Image (H × W × C)
(Ex: 224 × 224 × 3)
      ↓
Preprocess Image
- Resize
- Normalize
- (Optional) Data Augmentation
      ↓
┌──────────────────────────────────────────────────────────────────────────────┐
│ ResNet Backbone                                                             │
│                                                                              │
│  ├─ Initial Convolution                                                     │
│  │     7×7 Conv, 64 filters, stride=2                                       │
│  │     Output: 112×112×64                                                    │
│  │     ↓                                                                     │
│  │     BatchNorm                                                             │
│  │     ↓                                                                     │
│  │     ReLU                                                                  │
│  │     ↓                                                                     │
│  │     3×3 MaxPool, stride=2                                                 │
│  │     Output: 56×56×64                                                      │
│  │                                                                           │
│  ├─ Residual Block Stage 1 (×3 blocks)                                      │
│  │     Output: 56×56×256                                                     │
│  │                                                                           │
│  ├─ Residual Block Stage 2 (×4 blocks)                                      │
│  │     Output: 28×28×512                                                     │
│  │                                                                           │
│  ├─ Residual Block Stage 3 (×6 blocks)                                      │
│  │     Output: 14×14×1024                                                    │
│  │                                                                           │
│  ├─ Residual Block Stage 4 (×3 blocks)                                      │
│  │     Output: 7×7×2048                                                      │
│  │                                                                           │
│  └─ Global Average Pooling                                                   │
│        7×7×2048 → 1×1×2048                                                   │
└──────────────────────────────────────────────────────────────────────────────┘
      ↓
Flatten
1×1×2048 → 2048 chiều
      ↓
Fully Connected Layer
2048 → Number of Classes (Ex: 1000)
      ↓
Softmax
      ↓
Loss Function (Cross Entropy)
      ↓
Backpropagation (Training Only)
```
## RetinaNet
```bash
- Là một kiến trúc dùng để phát hiện và phân loại nhiều vật thể trong ảnh (object detection)
- Nó dự đoán Bounding box, class của vật thể
- Ứng dụng:
  + Xe tự lái (phát hiện người, xe, biển báo)
  + Camera an ninh
  + Retail (đếm sản phẩm)
  + Phát hiện tổn thương trong ảnh y tế
  + Drone surveillance
- Điểm nổi bật: sử dụng Focal Loss để xử lý mất cân bằng class (nhiều background hơn object).
```
**Pipeline RetinaNet**
```bash
Original Image (H × W × C)
(Ex: 800 × 800 × 3)
      ↓
Preprocess Image
- Resize
- Normalize
      ↓
┌──────────────────────────────────────────────────────────────────────────────┐
│ Backbone Network (Feature Extractor)                                       │
│  ├─ ResNet (Conv + Residual Blocks)                                         │
│  └─ Output multi-scale feature maps (C3, C4, C5)                            │
└──────────────────────────────────────────────────────────────────────────────┘
      ↓
┌──────────────────────────────────────────────────────────────────────────────┐
│ Feature Pyramid Network (FPN)                                               │
│  ├─ Tạo feature đa tỉ lệ (P3, P4, P5, P6, P7)                               │
│  └─ Kết hợp feature nông + sâu                                              │
└──────────────────────────────────────────────────────────────────────────────┘
      ↓
┌──────────────────────────────────────────────────────────────────────────────┐
│ Detection Heads (song song)                                                 │
│                                                                              │
│  ├─ Classification Subnet                                                   │
│  │     → Dự đoán class cho mỗi anchor                                       │
│                                                                              │
│  └─ Box Regression Subnet                                                   │
│        → Dự đoán bounding box offsets                                        │
└──────────────────────────────────────────────────────────────────────────────┘
      ↓
Anchor Boxes (tại mỗi pixel của mỗi scale)
      ↓
Predicted Boxes + Class Scores
      ↓
Non-Maximum Suppression (NMS)
      ↓
Final Detected Objects
      ↓
Loss Function
- Focal Loss (classification)
- Smooth L1 Loss (box regression)
      ↓
Backpropagation (Training Only)
```
Inception
    • Là một kiến trúc mạng nơ-ron tích chập (CNN), nó kết hợp nhiều kernel khác nhau chạy song song và sau đó gộp kết quả lại, nhằm giúp mô hình vừa học được chi tiết nhỏ, vừa nhìn được tổng thể.
    • Cách hoạt động:
        ◦ Tạo nhiều nhánh song song.
        ◦ Mooic nhánh xử lý cùng một input - tức sao chép ảnh gốc cho nhiều nhánh.
        ◦ Mỗi nhánh áp dụng một loại xử lý khác nhau, ví dụ:
            ▪ Nhánh 1: Convolution 1x1
            ▪ Nhánh 2: Convolution 1x1 → 3x3
            ▪ Nhánh 3: Convolution 1x1 → 5x5
            ▪ Nhánh 4: MaxPooling 3x3 → Convolution 1x1
        ◦ Gộp kết quả từ tất cả các nhanh theo chiều channel.
MobileNet - Mạng nhẹ cho di động
    • Mô hình VGG hay ResNet rất mạnh nhwung quá nặng, không chạy nổi trên điện thoại hoặc thiết bị trên IoT.
    • Mô hình sử dụng kỹ thuật Depthwise Separable Convolution, thay vì dùng Convolution thường.
        ◦ Depthwise Separable tách ra làm 2 bước → Nhệ hơn 8-9 lần so với Conv chuẩn mà vẫn giữ được độ chính xác.
            ▪ Depthwise Convolution - Xử lý từng kênh riêng biệt (nhẹ hơn rất nhiều).
            ▪ Pointwise Convolution - Dùng Conv 1x1 để kết hợp các kênh lại.
EfficientNet - Mạng cân bằng cả tốc độ và độ chính xác
    • Dùng MobileNet thì nhẹ nhwung độ chính xác hơi kém so với ResNet. Dùng ResNet thì chính xác nhưng chậm.
    • EfficientNet dùng kỹ thuật Compound Scaling để cân bằng giữa độ sâu, độ rộng, và độ phân giải đầu vào.
    • Cấu trúc:
        ◦ Dùng khối MBConv (Mobile Inverted Bottleneck) giống MobileNetV2.
        ◦ Thêm SE Block (Squeeze-and-Excitation) để học kênh nào quan trọng.
        ◦ Dùng Swish hoạc SiLU activation thay cho ReLU để tăng độ mượt.
SSD - Single Shot Detector
    • Phát hiện vật thể trong 1 lần quét ảnh (sigle shot).
    • Nhanh, nhẹ, dùng tốt cho real-time (ảnh từ wwebcam, robot, …)
Faster R-CNN
    • Phát hiện vật thể chính xác cao nhưng chậm hơn YOLO.
    • Gồm 2 bước: Xác định vùng → nhận diện vật thể.
    • Dùng khi cần độ chính xác cao, ít quan trọng tốc độ.
U-Net
    • Phân đoạn ảnh y tế (VD: Tách khối u khỏi ảnh chụp CT).
    • Inout là ảnh, output là mặt nạ (mask) có cùng kích thước.
    • Cực kỳ hiệu quả với ảnh nhỏ, ít dữ liệu.
Mask R-CNN
    • Phát hiện + phân đoạn vật thể (VD: viền rõ từng người, từng con mèo, …).
    • Nâng cấp từ Fastẻ R-CNN + thêm mặt nạ phân đoạn.
    • Output: Bounding box + Class + Mask.
DeepLab (V3, V3+)
    • Phân đoạn ảnh toàn cục (sematic segmentation).
    • Biết từng pixel là cái gì (VD: pixel này là người, kia là đường, …).
    • Rất mạnh trong phân đoạn cảnh quan, bản đồ, ảnh vệ tinh.
OpenPose
    • Dự đoán vị trí khớp cơ thể người (pose estimation).
    • Trích ra được: Đầu, vai, tay, chân, … từ ảnh/video.
MediaPipe
    • Thư viện của Google, hỗ trợ real-time:
    • Nhận diện tay, pose, tracking, …
    • Rất nhẹ và chạy được trên điện thoại
HRNet - High Resolution Network
    • Dự đoán khớp người, phân đoạn ảnh với độ chi tiết cao.
    • Giữ ảnh độ phân giải lớn suốt mạng → chính xác hơn OpenPose.
VGG-Face
Facenet
OpenFace
DeepFace
ArcFace
Dlib
Sface