# Introduction
```bash
- CNN (Convolutional Neural network) được thiết kế để xử lý dữ liệu có cấu trúc dạng lưới, ví dụ như hình ảnh.
- Cấu trúc 3 tầng:
    + Convolutional: CNN sử dụng một bộ lọc nhỏ (filter hoặc kernel) trượt trên ảnh đầu vào để lấy ra những đặc trưng nhỏ như cạnh, góc, hay các mẫu đơn giản. Bộ lọc này sẽ quét khắp ảnh. Phát hiện các đặc điểm quan trọng tại nhiều vị trí. Mỗi kernel học một đặc trưng khác nhau
    + Pooling: Giúp giảm kích thước dữ liệu sau khi tích chấp, làm cho mạng nhẹ hơn, giảm tính toán, đồng thời giữ lại đặc trưng quan trọng. Ví dụ, max pooling chọn giá trị lớn nhất trong một vùng nhỏ.
    + Fully connected: Sau các lớp convolutional và pooling, dữ liệu đặc trưng được dàn phẳng và dựa vào các lớp MLP để phân loại hay dự đoán.
```
# Pipeline
```bash
Original Image (HxWxC) (Ex: 224x224x3)
      ↓
Preprocess Image (height x width)
      ↓
┌──────────────────────────────────────────────────────────────────────────────────────────────────┐
│ CNN                                                                                              │
│  ├─ Convolution Layer (trích xuất đặc trưng bằng kernel) (H'xW'xF)                               │
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