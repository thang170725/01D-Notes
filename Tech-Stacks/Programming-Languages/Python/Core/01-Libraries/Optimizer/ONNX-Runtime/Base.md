- [Introduction](#introduction)
- [Installation](#installation)
---
# Onnxruntime Introduction (engine chạy suy luận (inference) cho mô hình machine learning)
```bash
- ONNX Runtime là một thư viện (library) – cụ thể là.
- Không phải framework huấn luyện như PyTorch/TensorFlow.
- ONNX Runtime dùng để:
    + Chạy model AI đã train sẵn (inference)
    + Tăng tốc model (CPU, GPU, TensorRT, OpenVINO…)
    + Deploy model ra production
- ONNX là format chuẩn để lưu model AI: Train bằng PyTorch → export sang ONNX → chạy bằng ONNX Runtime
- Ứng dụng thực tế: ONNX Runtime được dùng rất nhiều trong production:
    + Backend AI: API nhận ảnh → chạy model → trả kết quả
    + Computer Vision: Face recognition (InsightFace dùng ONNX Runtime bên dưới)
    + Object detection: OCR
    + Mobile / Edge: Chạy model trên: Android, iOS, IoT devices
    + Web / Browser: ONNX Runtime Web (chạy bằng WebAssembly)
- Vai trò trong hệ sinh thái AI. Bạn có thể hình dung:
    + PyTorch / TensorFlow	Train model
    + ONNX	Format model
    + ONNX Runtime	Chạy model
    => Tức là: Train → Export → Inference
```
# Installation
```bash
pip install onnxruntime 
```