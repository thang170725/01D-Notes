- [VGG (2014 - CNN sâu hơn)](#vgg-2014---cnn-sâu-hơn)
---
# VGG (2014 - CNN sâu hơn)
```bash
Ý tưởng:
    Trước VGG, CNN thường khá nông (5–8 lớp).

    Nhóm nghiên cứu đặt câu hỏi:
        Nếu cứ tăng số lớp lên thì sao?

        Họ tạo ra mạng rất sâu:
            - VGG-16: 16 lớp học được
            - VGG-19: 19 lớp học được

Điểm đặc biệt
    Thay vì dùng nhiều kernel kích thước khác nhau như trước, VGG chỉ dùng:
        3×3 Convolution Lặp đi lặp lại rất nhiều lần.

    Ví dụ
        Input
         ↓
        3×3 Conv
         ↓
        3×3 Conv
         ↓
        MaxPool
         ↓
        3×3 Conv
         ↓
        3×3 Conv
         ↓
        MaxPool

    Toàn bộ kiến trúc gần như chỉ là:
        Conv 3×3
        ↓
        ReLU
        ↓
        MaxPool
```
**Tại sao dùng nhiều Conv 3×3?**
```bash
Ví dụ:
    Một Conv 7×7 ≈ Ba Conv 3×3 liên tiếp

Ưu điểm:
    - ít tham số hơn
    - nhiều tầng phi tuyến hơn
    - học được đặc trưng tốt hơn
Nhược điểm:
    - Rất nặng.

Ví dụ:
    VGG16 ≈ 138 triệu tham số.
=> Huấn luyện rất tốn GPU.
```