- [Introduction](#introduction)
- [Pracices](#pracices)
  - [Pipeline xác định danh tính](#pipeline-xác-định-danh-tính)
---
# Introduction
```bash
- Cốt lõi của bài toán không phải là “nhận diện khuôn mặt”, mà là:
    + Biến một khuôn mặt thành một vector số sao cho:
        - Cùng người → vector gần nhau
        - Khác người → vector xa nhau
    => Đây gọi là embedding (biểu diễn đặc trưng).
```
**Pipeline cốt lõi (tất cả model đều theo)**
```bash
Dù là model gì (FaceNet, ArcFace, VGGFace…), pipeline luôn là:
(1) Face Detection: Tìm vị trí khuôn mặt trong ảnh
(2) Face Alignment: Căn chỉnh mặt (mắt, mũi thẳng hàng)
(3) Feature Extraction (QUAN TRỌNG NHẤT) → CNN/Transformer biến ảnh → vector (ví dụ 128-d, 512-d)
(4) So sánh vector: Dùng cosine similarity hoặc Euclidean distance (Xem trong Math_Core)
```
# Pracices
## Pipeline xác định danh tính
```bash
Input: ảnh khuôn mặt
Output: người A / B / Unknown
```
```bash
1. Chuẩn bị dataset (định dạng ảnh .jpg, ...)
    + Ảnh người A: 100 ảnh 
    + Ảnh người B: 100 
2. Cho từng ảnh vào model -> embedding
    + model có thể là CNN, ResNet, MobileNet, Vision Transformer, ...
```