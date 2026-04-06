- [Introduction](#introduction)
- [Installation](#installation)
---
# Introduction
```bash
- Ollama là một công cụ phần mềm giúp bạn chạy các mô hình AI (LLM – Large Language Model) trực tiếp trên máy tính cá nhân, thay vì phải dùng qua cloud như ChatGPT.
- Hiểu đơn giản:
    + Ollama giống như một “trình quản lý + môi trường chạy AI” trên máy bạn.
    + Bạn cài Ollama. Tải model về (ví dụ: Llama 3, Mistral…)
    + Sau đó chat AI offline hoặc local
- Nó làm được gì?
    + Chạy chatbot AI ngay trên máy (giống ChatGPT nhưng local)
    + Viết code, giải thích tài liệu, hỏi đáp
    + Tùy chỉnh model (fine-tune, system prompt…)
    + Tích hợp với app khác qua API local
- Ưu điểm
    + Riêng tư: dữ liệu không gửi lên server
    + Nhanh (không phụ thuộc mạng)
    + Dễ dùng (cài 1 lệnh là chạy)
    + Hỗ trợ nhiều model open-source
- Nhược điểm
    + Cần máy đủ mạnh (RAM, GPU càng tốt)
    + Model local thường kém mạnh hơn GPT-4/5
    + Phải tải model (có thể vài GB)
```
# Installation
```bash
**Installation**
```bash
1. ollama --version     # kiểm tra model
2. ollama pull mistral  # tải model
3. ollama run mistral   # chạy model
```