- [Installation](#installation)
- [Create (Nhóm khởi tạo)](#create-nhóm-khởi-tạo)
  - [ChatOllama() (khởi tạo một đối tượng LLM)](#chatollama-khởi-tạo-một-đối-tượng-llm)
---
# Installation
```bash
1. pip install langchain_community
2. pip install langchain_ollama
```
Được. Nếu bạn muốn dùng langchain_ollama, cách đơn giản nhất là chạy Qwen/Qwen2.5-1.5B-Instruct qua Ollama trước, sau đó LangChain gọi model bằng ChatOllama.

1. Cài thư viện
pip install langchain-ollama
2. Đảm bảo model đã có trong Ollama

Nếu Ollama có model Qwen tương ứng:

ollama pull qwen2.5:1.5b

Sau đó test trực tiếp:

ollama run qwen2.5:1.5b
3. Test bằng LangChain

Tạo test_qwen.py:

from langchain_ollama import ChatOllama

llm = ChatOllama(
    model="qwen2.5:1.5b",
    temperature=0,
)

response = llm.invoke("Giải thích RNN là gì trong 3 câu.")

print(response.content)

Chạy:

python test_qwen.py

Nếu thành công, flow của bạn sẽ là:

Python
   ↓
LangChain
   ↓
langchain_ollama
   ↓
Ollama
   ↓
Qwen2.5 1.5B
Nếu bạn muốn test đúng kiểu Chat

ChatOllama nhận message nên có thể viết:

from langchain_ollama import ChatOllama
from langchain_core.messages import HumanMessage

llm = ChatOllama(
    model="qwen2.5:1.5b",
    temperature=0,
)

messages = [
    HumanMessage(content="Bạn là trợ lý AI. Hãy giải thích Seq2Seq là gì.")
]

response = llm.invoke(messages)

print(response.content)

Lưu ý: Qwen/Qwen2.5-1.5B-Instruct trên Hugging Face và qwen2.5:1.5b trong Ollama không phải là hai cách gọi trực tiếp cho cùng một registry model. Nếu bạn bắt buộc muốn chạy chính xác file model Hugging Face Qwen/Qwen2.5-1.5B-Instruct qua Ollama, cần kiểm tra/đóng gói model đó vào format mà Ollama hỗ trợ trước.
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