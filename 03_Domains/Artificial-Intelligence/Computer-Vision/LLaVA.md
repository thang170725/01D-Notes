```bash
- LLaVA (Large Language and Vision Assistant) là một mô hình đa phương thức (text + image), kết hợp LLM (như LLaMA) với encoder ảnh (CLIP) để hiểu ảnh và trả lời bằng ngôn ngữ tự nhiên.
- LLaVA dùng để làm gì?
    + Một vài use case phổ biến:
    + Hỏi–đáp về ảnh: “Trong ảnh có gì?”, “Người này đang làm gì?”
    + Phân tích biểu đồ / ảnh tài liệu: đọc bảng, biểu đồ, sơ đồ.
    + Suy luận từ ảnh: mô tả, so sánh, giải thích ngữ cảnh.
    + Xây chatbot đa phương thức: chat + upload ảnh.
    + Nghiên cứu Vision–Language: nền tảng để fine-tune, thử nghiệm.
- Yêu cầu hệ thống
    + Python ≥ 3.8
    + GPU NVIDIA (khuyến nghị)
    + 8GB VRAM chạy được bản nhỏ (7B, quantized)
    + CPU vẫn chạy được nhưng rất chậm
    + CUDA + PyTorch phù hợp GPU
```
# Installation
```bash
pip install transformers torch pillow accelerate
```