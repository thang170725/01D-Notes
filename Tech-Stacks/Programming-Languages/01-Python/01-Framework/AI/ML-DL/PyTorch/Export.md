- [.onnx.export()](#onnxexport)
---
# .onnx.export()
```bash
- Chuyển model PyTorch → file .onnx để chạy ở ONNX Runtime, TensorRT, OpenVINO, C++…
```
**Ex: Linear model**
```python
import torch
import torch.nn as nn

class MyModel(nn.Module):
    def __init__(self):
        super().__init__()
        self.fc = nn.Linear(10, 3)

    def forward(self, x):
        return self.fc(x)

model = MyModel()
model.eval()   # RẤT QUAN TRỌNG, Tắt Dropout, BatchNorm

dummy_input = torch.randn(1, 10)

torch.onnx.export(
    model,                     # model PyTorch
    dummy_input,               # input mẫu
    "model.onnx",              # file output
    export_params=True,        # lưu weight
    opset_version=11,          # phổ biến & ổn định
    do_constant_folding=True,  # optimize
    input_names=["input"],     # tên input
    output_names=["output"]    # tên output
)

#  Xong. Có file model.onnx
```
**Ex2: CNN**
```python
class CNN(nn.Module):
    def __init__(self):
        super().__init__()
        self.conv = nn.Conv2d(3, 16, 3)
        self.pool = nn.AdaptiveAvgPool2d(1)
        self.fc = nn.Linear(16, 10)

    def forward(self, x):
        x = self.conv(x)
        x = self.pool(x)
        x = x.view(x.size(0), -1)
        return self.fc(x)

model = CNN().eval()
dummy_input = torch.randn(1, 3, 224, 224)

torch.onnx.export(
    model,
    dummy_input,
    "cnn.onnx",
    opset_version=11,
    input_names=["image"],
    output_names=["logits"]
)
```