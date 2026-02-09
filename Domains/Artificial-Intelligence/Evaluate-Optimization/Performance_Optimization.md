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
# ONNX
```bash
- ONNX = định dạng model trung gian, dùng để “nói chuyện” giữa các framework.
- ONNX KHÔNG:
    + train model
    + chạy nhanh hơn
    + ONNX chỉ là file mô tả graph model
    -> ONNX = “PDF” của thế giới AI model
```
**Vì sao cần ONNX?**
```bash
- PyTorch, TensorFlow, Keras… mỗi thằng 1 kiểu
- TensorRT không muốn học hết. Nó chỉ nói 1 ngôn ngữ chung: ONNX
```
**Ex**
```bash
PyTorch model (.pt)
   ↓ export
ONNX model (.onnx)
   ↓
TensorRT đọc & tối ưu
```
# Installation
```bash
1. pip install onnx onnxscript
```
## Demo export .onnx
```python
import torch
import torch.nn as nn

class SimpleNet(nn.Module):
    def __init__(self):
        super().__init__()
        self.fc = nn.Linear(10, 5)

    def forward(self, x):
        return self.fc(x)

model = SimpleNet().eval()

dummy_input = torch.randn(1, 10)

torch.onnx.export(
    model,
    dummy_input,
    "simplenet.onnx",
    input_names=["input"],
    output_names=["output"],
    opset_version=13
)
```
# TensorRT Engine
```bash
- Engine = model đã được TensorRT “compile” riêng cho GPU của bạn.
- So sánh cho dễ hiểu:
    + PyTorch           : model, code Python
    + ONNX	            : file, trung gian
    + TensorRT Engine   : file .engine giống file .exe
- Engine:
    + chỉ chạy trên đúng GPU + CUDA version
    + rất nhanh
    + không portable
- Vì sao Engine nhanh?
    + TensorRT làm 4 việc chính:
    + Fuse layer (gộp nhiều layer)
    + Chọn kernel GPU tốt nhất
    + Giảm precision (FP32 → FP16 / INT8)
    + Tối ưu memory
```
GIL (Global Interpreter Lock)
    • GIL (Global Interpreter Lock) là một cơ chế khóa trong CPython (trình thông dịch Python phổ biến nhất). Tại mọi thời điểm, chỉ có 1 thread được phép thực thi Python bytecode, dù máy có nhiều CPU core.
    • Ví dụ:
        ◦ Thread: 1 người cầm chìa khóa (GIL), nhiều người xếp hàng
        ◦ Process: mỗi người có chìa khóa riêng chạy độc lập
