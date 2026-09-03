- [Introduction](#introduction)
- [Pipeline CNN](#pipeline-cnn)
- [DCNN Introduction (Deep Convolutional Neural Network về bản chất không phải một loại phép convolution khác CNN)](#dcnn-introduction-deep-convolutional-neural-network-về-bản-chất-không-phải-một-loại-phép-convolution-khác-cnn)
---
# Introduction
```bash
CNN (Convolutional Neural network) được thiết kế để xử lý dữ liệu có cấu trúc dạng lưới, ví dụ như hình ảnh.

Cấu trúc 3 tầng:
    - Convolutional: CNN sử dụng một bộ lọc nhỏ (filter hoặc kernel) trượt trên ảnh đầu vào để lấy ra những đặc trưng nhỏ như cạnh, góc, hay các mẫu đơn giản. Bộ lọc này sẽ quét khắp ảnh. Phát hiện các đặc điểm quan trọng tại nhiều vị trí. Mỗi kernel học một đặc trưng khác nhau
    - Pooling: Giúp giảm kích thước dữ liệu sau khi tích chấp, làm cho mạng nhẹ hơn, giảm tính toán, đồng thời giữ lại đặc trưng quan trọng. Ví dụ, max pooling chọn giá trị lớn nhất trong một vùng nhỏ.
    + Fully connected: Sau các lớp convolutional và pooling, dữ liệu đặc trưng được dàn phẳng và dựa vào các lớp MLP để phân loại hay dự đoán.
```
# Pipeline CNN
**Tài liệu tham khảo**  
[Kiến thức về BathNorm](../00-Math-Core/Math_Core.md#batchnorm-chuẩn-hóa-dữ-liệu-về-phân-phối-chuẩn-hơn-giúp-học-nhanh-ổn-định)
```bash
Original Image (HxWxC)
└── Input: 224x224x3 (ảnh 3 kênh màu rgb) 
      ↓
Preprocess Image (224x224x1)
├── Process: grayscale chuyển từ ảnh 3 channels -> ảnh 1 channel
└── Output: 224x224
      ↓
┌──────────────────────────────────────────────────────────────────────────────────────────────────┐
│ CNN                                                                                              │
│  ├─ Convolution Layer (trích xuất đặc trưng bằng kernel)                                         │
|  |   ├── giả sử dụng kernel=3x3, stride=1, padding=0 (32 filters)                                |
|  |   ├── H_out = (H + 2P - K) / S + 1 = 222, W_out = 222                                         |
|  |   -> Output=222x222x32                                                                        |
|  |                                                                                               |
│  ├─ BatchNorm                                                                                    │
│  ├─ Activation Function (ReLU)                                                                   │ x N layer
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
# DCNN Introduction (Deep Convolutional Neural Network về bản chất không phải một loại phép convolution khác CNN)
```bash
Nó chủ yếu có nghĩa là:
      CNN có nhiều tầng convolution hơn → mạng sâu hơn → học được đặc trưng từ đơn giản đến phức tạp hơn.

1. CNN "bình thường"
      Ví dụ một CNN đơn giản: Image 224×224×1 -> Conv -> ReLU -> Pooling -> Conv -> ReLU -> Pooling -> Flatten -> FC -> Output
            -> Có thể chỉ có 2–3 convolution blocks.

2. DCNN
      Deep CNN có thể như: Image -> Conv Block 1 -> Conv Block 2 -> Conv Block 3 -> Conv Block 4 -> Conv Block 5 -> ... -> FC / Head -> Output
      
      Ví dụ VGG-16:
            Input
             ↓
            Conv
            Conv
            Pool
             ↓
            Conv
            Conv
            Pool
             ↓
            Conv
            Conv
            Conv
            Pool
             ↓
            Conv
            Conv
            Conv
            Pool
             ↓
            Conv
            Conv
            Conv
            Pool
             ↓
            FC
             ↓
            Classification
      -> Đây được gọi là Deep CNN.
```