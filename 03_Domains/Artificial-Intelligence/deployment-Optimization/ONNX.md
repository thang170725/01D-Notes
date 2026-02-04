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