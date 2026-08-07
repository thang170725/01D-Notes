- [Batch Size](#batch-size)
- [TensorRT (công cụ của NVIDIA để tăng tốc model AI khi chạy trên GPU)](#tensorrt-công-cụ-của-nvidia-để-tăng-tốc-model-ai-khi-chạy-trên-gpu)
  - [TensorRT Engine](#tensorrt-engine)
- [ONNX (định dạng model trung gian, dùng để “nói chuyện” giữa các framework)](#onnx-định-dạng-model-trung-gian-dùng-để-nói-chuyện-giữa-các-framework)
  - [Ask (các câu hỏi về ONNX)](#ask-các-câu-hỏi-về-onnx)
    - [ONNX có phải công ty không?](#onnx-có-phải-công-ty-không)
    - [ONNX chỉ dành cho AI?](#onnx-chỉ-dành-cho-ai)
    - [Tại sao ONNX lại nổi tiếng?](#tại-sao-onnx-lại-nổi-tiếng)
    - [ONNX có thật sụ nhanh hơn các định dạng khác như pkl, pt không?](#onnx-có-thật-sụ-nhanh-hơn-các-định-dạng-khác-như-pkl-pt-không)
- [Installation](#installation)
  - [Demo export .onnx](#demo-export-onnx)
---
# Batch Size 
**Ex**
```bash
Giả sử có:
    1000 ảnh mèo

Batch Size = 1
    GPU xem: 
        Ảnh 1 => Cập nhật model
        Ảnh 2 => Cập nhật model
        Ảnh 3 => Cập nhật model

Batch Size = 32
    GPU xem:
        32 ảnh cùng lúc → tính loss trung bình → update 1 lần

Batch Size = 128
    GPU xem: 128 ảnh cùng lúc
```
**Batch Size ảnh hưởng VRAM thế nào?**
```bash
Ví dụ:
    Batch = 8VRAM = 4GB
    Tăng:
    Batch = 16VRAM = 8GB
    Tăng tiếp:
    Batch = 32VRAM = 16GB
    Gần như:
    Batch Size ↑VRAM ↑
```
**Batch Size ảnh hưởng Gradient thế nào?**
```bash
Đây là ý quan trọng nhất.

Batch nhỏ
    Ví dụ:
        Ảnh 1: mèo trắng
            Model nghĩ: Ồ, mèo thường màu trắng

        Ảnh tiếp: Mèo đen
            Model: Không đúng rồi

        Gradient sẽ:
            - Lúc trái
            - Lúc phải

Batch lớn
    Cho model xem: 64 ảnh cùng lúc
    Nó thấy:
        - Mèo trắng
        - Mèo đen
        - Mèo vàng
        - Mèo xám
        - ...
    
    Gradient trở nên:
        - ổn định hơn
        - Đi đúng hướng hơn.
```
**Batch quá lớn cũng không tốt**
```bash
Nhiều người nghĩ:
    - Batch càng lớn càng ngon
    - Không hẳn.

Ví dụ:
    Batch = 8192
    Gradient quá "mượt".
    Model dễ:
        - học chậm
        - generalization kém (tức là train đẹp nhưng test dở)
```
**Tốc độ train**
```bash
Ví dụ:
    Batch = 1
        1000 ảnh→ 1000 lần update

    Batch = 100
        1000 ảnh→ chỉ 10 lần update (GPU tận dụng tốt hơn)

    Thường: Batch lớn=Train nhanh hơn (nếu GPU đủ VRAM)
```
# TensorRT (công cụ của NVIDIA để tăng tốc model AI khi chạy trên GPU)
```bash
Hiểu đơn giản: Bạn train model bằng PyTorch / TensorFlow. Khi đem model đi chạy thật → TensorRT giúp:
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
## TensorRT Engine
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
Không. Đây là một hiểu nhầm rất phổ biến.

TensorRT không phải là công cụ để export sang ONNX. Ngược lại, trong đa số trường hợp TensorRT sử dụng ONNX làm đầu vào.

Quan hệ của chúng như sau:

PyTorch (.pt)
       │
       │ Export
       ▼
ONNX (.onnx)
       │
       │ TensorRT build/optimize
       ▼
TensorRT Engine (.engine)
       │
       ▼
Inference trên GPU NVIDIA
Vai trò của từng thành phần
1. PyTorch (.pt)

Đây là model khi bạn train xong.

Ví dụ:

model = YOLO("best.pt")

File:

best.pt

Chứa:

Kiến trúc model
Trọng số
Chỉ chạy được với PyTorch
2. ONNX

ONNX là định dạng trung gian (intermediate format).

Nó giống như một "ngôn ngữ chung" để nhiều framework có thể hiểu.

Ví dụ:

PyTorch
      \
TensorFlow ---> ONNX
      /
Paddle

Nhờ vậy bạn có thể chạy model bằng nhiều runtime khác nhau.

3. TensorRT

TensorRT là một Inference Engine do NVIDIA phát triển.

Nó nhận model (thường là ONNX), sau đó:

tối ưu graph
fusion các layer
chọn kernel CUDA nhanh nhất
chuyển FP32 → FP16 hoặc INT8 (nếu muốn)
sinh ra file .engine

Ví dụ:

best.onnx
      │
      ▼
TensorRT
      │
      ▼
best.engine
Tại sao không export thẳng sang TensorRT?

Thực tế là có thể.

Ví dụ YOLO:

model.export(format="engine")

Nhưng bên trong YOLO thường làm gần như sau:

best.pt
    │
    ▼
best.onnx
    │
    ▼
TensorRT
    │
    ▼
best.engine

Tức là ONNX vẫn thường là bước trung gian, chỉ là YOLO tự động thực hiện giúp bạn.

So sánh
Định dạng/Công cụ	Vai trò
.pt	Model PyTorch
.onnx	Định dạng trung gian
TensorRT	Công cụ tối ưu và chạy model
.engine	Model đã được TensorRT tối ưu
Ví dụ với project YOLO của bạn

Hiện tại bạn đang có:

best.pt

Nếu muốn chạy nhanh hơn trên GPU NVIDIA:

best.pt
     │
     ▼
best.onnx
     │
     ▼
TensorRT
     │
     ▼
best.engine

Sau đó khi predict:

detector = TensorRT("best.engine")

Tốc độ có thể nhanh hơn PyTorch đáng kể (tùy GPU và model).

Còn nếu chỉ dùng CPU?

Đây là điểm rất quan trọng đối với bạn.

Trước đây bạn có nói máy của bạn chỉ có CPU Intel i3, không có GPU NVIDIA.

Trong trường hợp đó:

❌ TensorRT không giúp ích, vì nó chỉ hoạt động trên GPU NVIDIA.
✅ ONNX Runtime mới là lựa chọn phù hợp nếu muốn tối ưu tốc độ trên CPU.

Với máy của bạn, luồng tối ưu sẽ là:

best.pt
     │
     ▼
best.onnx
     │
     ▼
ONNX Runtime (CPU)

đây là hướng có khả năng mang lại cải thiện tốc độ hơn so với chạy trực tiếp bằng PyTorch trên CPU.
# ONNX (định dạng model trung gian, dùng để “nói chuyện” giữa các framework)
[Thư viện sử dụng ONNX](../../../../Tech-Stacks/Programming-Languages/Python/Core/01-Libraries/AI-Libraries/01-AI-Optimizer/ONNX-Runtime/Base.md)

**ONNX là gì?**
```bash
ONNX là format chuẩn để lưu model AI: Train bằng PyTorch → export sang ONNX → chạy bằng ONNX Runtime
```
**ONNX Runtime dùng để làm gì?**
```bash
- Chạy model AI đã train sẵn (inference)
- Tăng tốc model (CPU, GPU, TensorRT, OpenVINO…)
- Deploy model ra production
```
**Ứng dụng thực tế: ONNX Runtime được dùng rất nhiều trong production**
```bash
- Backend AI: API nhận ảnh → chạy model → trả kết quả
- Computer Vision: Face recognition (InsightFace dùng ONNX Runtime bên dưới)
- Object detection: OCR
- Mobile / Edge: Chạy model trên: Android, iOS, IoT devices
- Web / Browser: ONNX Runtime Web (chạy bằng WebAssembly)
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
## Ask (các câu hỏi về ONNX)
### ONNX có phải công ty không?
```bash
Không, ONNX không phải là một công ty. ONNX là một chuẩn (standard) mở để biểu diễn mô hình machine learning.

Tên đầy đủ của ONNX là Open Neural Network Exchange.

Ban đầu, ONNX được phát triển bởi hai công ty lớn:
    - Microsoft
    - Meta (lúc đó còn là Facebook)

Sau đó ONNX trở thành một dự án mã nguồn mở, được nhiều công ty cùng đóng góp như Microsoft, Meta, NVIDIA, Intel, AMD,...
```
### ONNX chỉ dành cho AI?
```bash
Đúng, gần như vậy.

ONNX được thiết kế cho Machine Learning, đặc biệt là:
    - Computer Vision
    - NLP
    - Speech Recognition
    - Recommendation
    - Time Series
    - Deep Learning nói chung

Nó mô tả các phép toán như:
    - Convolution
    - Linear
    - Attention
    - LSTM
    - BatchNorm
    - ReLU
    - Softmax
    - ...
-> Đây đều là các toán tử phục vụ mô hình AI.
```
### Tại sao ONNX lại nổi tiếng?
```bash
Vì nó giúp tách riêng quá trình huấn luyện và quá trình chạy suy luận (inference).

Ví dụ:
    - Train bằng PyTorch trên GPU NVIDIA.
    - Xuất thành model.onnx.
    - Chạy trên:
    - CPU Intel
    - GPU AMD
    - GPU NVIDIA
    - Windows
    - Linux
    - Android
    - iPhone
    - Edge device
```
### ONNX có thật sụ nhanh hơn các định dạng khác như pkl, pt không?
```bash
Câu trả lời ngắn là: Thường là có, nhưng không phải vì .onnx thần kỳ hơn .pt hay .pkl, mà vì engine chạy ONNX (ONNX Runtime) được tối ưu mạnh cho inference.

Để hiểu rõ, cần phân biệt định dạng lưu và engine thực thi.
    Định dạng	Dùng với	                Engine chạy
    .pkl	    scikit-learn	            Python + scikit-learn
    .pt	        PyTorch	                    PyTorch
    .onnx	    Mọi framework hỗ trợ ONNX	ONNX Runtime, TensorRT, OpenVINO...

1. Với YOLO (.pt)
    PyTorch sẽ phải:
        - load tensor
        - autograd (dù inference đã tắt)
        - dispatcher
        - rất nhiều lớp abstraction

    Nếu dùng onnx thì ONNX Runtime sẽ:
        - fuse Conv + BatchNorm
        - tối ưu graph
        - dùng SIMD
        - dùng thread tốt hơn
        - ít overhead Python hơn
    => Thường nhanh hơn 10–50% trên CPU.

2. Với scikit-learn (.pkl)
    Lợi ích nếu export sang onnx:
        - không cần cài sklearn
        - deploy C++, C#, Java dễ hơn
        - đôi khi nhanh hơn
    
    Nhưng: pkl ≈ onnx -> Chênh lệch chỉ khoảng vài phần trăm đến vài chục phần trăm tùy model.

3. Với Deep Learning # Đây mới là nơi ONNX phát huy sức mạnh.
    Ví dụ:
        PyTorch
        ↓
        Conv
        ↓
        BatchNorm
        ↓
        ReLU
        -> PyTorch thực hiện 3 kernel.
    
    ONNX Runtime có thể gộp thành: Conv+BN+ReLU -> chỉ còn 1 kernel. GPU và CPU đều hưởng lợi.
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
GIL (Global Interpreter Lock)
    • GIL (Global Interpreter Lock) là một cơ chế khóa trong CPython (trình thông dịch Python phổ biến nhất). Tại mọi thời điểm, chỉ có 1 thread được phép thực thi Python bytecode, dù máy có nhiều CPU core.
    • Ví dụ:
        ◦ Thread: 1 người cầm chìa khóa (GIL), nhiều người xếp hàng
        ◦ Process: mỗi người có chìa khóa riêng chạy độc lập