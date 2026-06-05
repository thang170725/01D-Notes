- [Installation](#installation)
- [Create (Nhóm khởi tạo)](#create-nhóm-khởi-tạo)
  - [ChatOllama() (khởi tạo một đối tượng LLM)](#chatollama-khởi-tạo-một-đối-tượng-llm)
---
# Installation
```bash
1. pip install langchain_community
2. pip install langchain_ollama
```
# Create (Nhóm khởi tạo)
## ChatOllama() (khởi tạo một đối tượng LLM)
```bash
2 thư viện có thể dùng:
    - langchain_community (cách cũ): Là nơi chứa các integration “gom chung” (Ollama, HuggingFace, v.v.)
        - Đang bị deprecate dần
        - Update chậm hơn
        - Code đôi khi không tối ưu
    - langchain_ollama (cách mới): Là package tách riêng chính thức cho Ollama
        - Được maintain riêng → cập nhật nhanh hơn
        - Tương thích tốt với API mới của Ollama
```
**Syn**
```bash
from langchain_ollama import ChatOllama

llm = ChatOllama(
    model="llama3",
    temperature=0,
    client_kwargs={
        "timeout": 30
    }

)

- Input:
    + model         : tên của model llm, phải đúng tên model bạn đã pull bằng Ollama
    + temperature   : độ sáng tạo của AI
        - 0: ít sáng tạo
        - 0.7: cân bằng
        - 1+: sáng tạo hơn
    + base_url: 
        - Mặc định: Ollama chạy ở port 11434
        - Nếu bạn chạy Docker / server khác → bắt buộc set
    + num_predict: giới hạn số token output
        - Tránh output quá dài hoặc tốn tài nguyên
    + repeat_penalty: giảm lặp từ
```