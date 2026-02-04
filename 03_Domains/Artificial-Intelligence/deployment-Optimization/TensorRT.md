- [TensorRT](#tensorrt)
---
# TensorRT
```bash
- TensorRT = công cụ của NVIDIA để tăng tốc model AI khi chạy (inference) trên GPU.
- Hiểu đơn giản: Bạn train model bằng PyTorch / TensorFlow. Khi đem model đi chạy thật → TensorRT giúp:
    + Chạy nhanh hơn
    + Dùng ít bộ nhớ hơn
    + Tối ưu cho GPU NVIDIA
    + TensorRT KHÔNG dùng để train, chỉ dùng để chạy model đã train.
- PyTorch model → (convert) → TensorRT engine → chạy rất nhanh trên GPU
-> TensorRT = tối ưu & tăng tốc model AI khi inference trên GPU NVIDIA
```
**Khi nào cần TensorRT?**
```bash
- Model đã train xong
- Cần chạy nhanh (real-time, production)
- Chạy trên GPU NVIDIA
```
**Ex**
```bash
- Xe tự lái (YOLO detect 30–60 FPS)
- Camera AI (face, object detection)
- Robot
- Server inference (tiết kiệm GPU → giảm tiền)
```
**Khi KHÔNG cần TensorRT:**
```bash
- Đang học ML cơ bản
- Chỉ train & test nhỏ
- Không có GPU NVIDIA
```
**TensorRT hoạt động như thế nào? (pipeline cực gọn)**
```bash
- TensorRT không nhận trực tiếp file .pt hay .ckpt. Nó cần model ở dạng trung gian.

Pipeline chuẩn (90% ai cũng dùng):
PyTorch / TensorFlow
        ↓
       ONNX
        ↓
   TensorRT Engine
        ↓
     Inference siêu nhanh

- ONNX = định dạng trung gian chung
- TensorRT:
- fuse layer
- tối ưu kernel GPU
- giảm precision (FP16 / INT8)
- Kết quả: engine (.engine) chạy rất nhanh
-> Nhớ hình này là đủ: .pt → .onnx → .engine
```
**Muốn học TensorRT cần chuẩn bị gì?**
```bash
1. GPU NVIDIA (bắt buộc)
2. Phần mềm (đúng thứ tự): Bạn KHÔNG cần nhớ chi tiết, chỉ nhớ quan hệ:
GPU
 └─ Driver NVIDIA
     └─ CUDA
         └─ TensorRT
-> Driver ↔ CUDA ↔ TensorRT phải tương thích
```