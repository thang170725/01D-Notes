- [ResNet (2015 - "Đừng bắt mạng học từ đầu")](#resnet-2015---đừng-bắt-mạng-học-từ-đầu)
  - [ResNet](#resnet)
---
# ResNet (2015 - "Đừng bắt mạng học từ đầu")
```bash
- ResNet (Residual Network) là một kiến trúc CNN sâu dùng để:
  + Trích xuất đặc trưng mạnh từ ảnh và giải quyết bài toán thị giác máy tính phức tạp.
  + Nó nổi tiếng vì đưa ra skip connection (residual connection) giúp huấn luyện được mạng rất sâu (50, 101, 152 layer…) mà không bị vanishing gradient.

Ứng dụng:
  + Image Classification
  + Object Detection
  + Image Segmentation (phân vùng ảnh)
  + Face Recognition 
  + Medical AI
  + Autonomous Driving
```
```bash
Sau VGG, mọi người nghĩ:
    "Tăng số layer nữa chắc càng tốt."
    
    Họ làm CNN:
        - 30 lớp
        - 50 lớp
        - 100 lớp

    Kết quả:
        Accuracy lại giảm.

        Không phải overfitting.
            Mà là: Gradient rất khó truyền về đầu mạng.

Ý tưởng của ResNet
    Thay vì học: Output = H(x)

    ResNet học: Output = F(x) + x
        - x: được nối tắt (skip connection).

    Ví dụ
        Input
           │
           ├──────────────┐
           │              │
        Conv              │
         ↓                │
        Conv              │
         ↓                │
         + <──────────────┘
         ↓
        Output
            
            Nếu hai Conv học rất kém.
                Thì Output = Input => Mạng vẫn hoạt động. Không làm hỏng thông tin.

Lợi ích. Có thể xây:
    - ResNet18
    - ResNet34
    - ResNet50
    - ResNet101
    - ResNet152
    - Thậm chí hơn 1000 layer. Điều mà VGG gần như không làm được.

Hãy tưởng tượng
    Không có ResNet:
        A
        ↓

        B
        ↓

        C
        ↓

        D
    => Muốn đi từ A tới D phải đi hết.

    ResNet:
        A
        ↓

        B
        ↓

        C
        ↓

        D

        ╲──────────────╱

    => Có đường tắt. Thông tin truyền dễ hơn.
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
│ ResNet Backbone                                                              │
│                                                                              │
│  ├─ Initial Convolution                                                      │
│  │     7×7 Conv, 64 filters, stride=2                                        │
│  │     Output: 112×112×64                                                    │
│  │     ↓                                                                     │
│  │     BatchNorm                                                             │
│  │     ↓                                                                     │
│  │     ReLU                                                                  │
│  │     ↓                                                                     │
│  │     3×3 MaxPool, stride=2                                                 │
│  │     Output: 56×56×64                                                      │
│  │                                                                           │
│  ├─ Residual Block Stage 1 (×3 blocks)                                       │
│  │     Output: 56×56×256                                                     │
│  │                                                                           │
│  ├─ Residual Block Stage 2 (×4 blocks)                                       │
│  │     Output: 28×28×512                                                     │
│  │                                                                           │
│  ├─ Residual Block Stage 3 (×6 blocks)                                       │
│  │     Output: 14×14×1024                                                    │
│  │                                                                           │
│  ├─ Residual Block Stage 4 (×3 blocks)                                       │
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