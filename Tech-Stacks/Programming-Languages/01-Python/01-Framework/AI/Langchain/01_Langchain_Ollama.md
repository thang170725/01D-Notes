- [Langchain Ollama Introduction (gói tích hợp giữa LangChain và Ollama, dùng để cho ứng dụng LangChain gọi các model AI chạy thông qua Ollama)](#langchain-ollama-introduction-gói-tích-hợp-giữa-langchain-và-ollama-dùng-để-cho-ứng-dụng-langchain-gọi-các-model-ai-chạy-thông-qua-ollama)
- [Installation](#installation)
- [ollama pull ... (tải model từ hugging face)](#ollama-pull--tải-model-từ-hugging-face)
- [ollama run ... (chạy llm trực tiếp ằng terminal)](#ollama-run--chạy-llm-trực-tiếp-ằng-terminal)
- [Create (Nhóm khởi tạo)](#create-nhóm-khởi-tạo)
  - [ChatOllama() (khởi tạo một đối tượng LLM)](#chatollama-khởi-tạo-một-đối-tượng-llm)
    - [.bind\_tools() (abstract từ langchain\_core dùng để cho phép LLM sử dụng tool nào)](#bind_tools-abstract-từ-langchain_core-dùng-để-cho-phép-llm-sử-dụng-tool-nào)
      - [.ainvoke()](#ainvoke)
---
# Langchain Ollama Introduction (gói tích hợp giữa LangChain và Ollama, dùng để cho ứng dụng LangChain gọi các model AI chạy thông qua Ollama)
```bash
Nói ngắn gọn:
    - Ollama = runtime/server chạy LLM
    - langchain_ollama = adapter để LangChain giao tiếp với Ollama
```
# Installation
```bash
1. pip install langchain_community
2. pip install langchain_ollama
```
# ollama pull ... (tải model từ hugging face)
**Syn**
```bash
ollama pull qwen2.5:1.5b
```
# ollama run ... (chạy llm trực tiếp ằng terminal)
**Syn**
```bash
ollama run qwen2.5:1.5b
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
- Output: <class 'langchain_ollama.chat_models.ChatOllama'>
```
### .bind_tools() (abstract từ langchain_core dùng để cho phép LLM sử dụng tool nào)
**Syn**
```bash
runnable = llm.bind_tools(
    tools,
    *,
    tool_choice=None,
    **kwargs
)

- Output: Nó trả về một Runnable đã được bind tool
```
**bind_tools() thực sự truyền gì cho LLM?**
```bash
@tool
def search_recipe(query: str) -> str:
    """Search recipes based on user's query."""
    ...

LangChain có thể chuyển nó thành dạng schema kiểu:
{
  "type": "function",
  "function": {
    "name": "search_recipe",
    "description": "Search recipes based on user's query.",
    "parameters": {
      "type": "object",
      "properties": {
        "query": {
          "type": "string"
        }
      },
      "required": ["query"]
    }
  }
}

Tức LLM được biết:
    - Có một tool tên: search_recipe
    - Nó dùng để: Search recipes...
    - Nó nhận: query: string
    - Nhưng LLM chưa chạy function Python.
```

**Ex: Dùng bind_tools với langchain_ollama**
```python
from langchain_ollama import ChatOllama

@tool
def get_user_info() -> str:
    """Get current user's profile."""
    return "..."

@tool
def search_recipe(query: str) -> str:
    """Search recipes."""
    return "..."

llm = ChatOllama(
    model="qwen3.5:4b",
    temperature=0
)

llm_with_tools = llm.bind_tools([
    get_user_info,
    search_recipe,
])
# Nó tạo ra một model mới đã được gắn thông tin về các tool.
# Nó chưa chạy get_user_info().
# Cụ thể, LangChain lấy từ mỗi tool:
# name
# description
# input schema
# rồi đưa thông tin đó vào request gửi cho model.
```
#### .ainvoke()
**Syn**
```bash
ai_msg = await runnable.ainvoke(messages)

- Output: <class 'langchain_core.messages.ai.AIMessage'>
```
Đây mới là phần quan trọng đối với Agent của bạn.

ai_msg = await runnable.ainvoke(messages)

có thể cho:

print(ai_msg)

đại loại:

AIMessage(
    content='',
    tool_calls=[
        {
            'name': 'search_customer',
            'args': {'customer_id': 123},
            'id': '...'
        }
    ]
)

Tức là:

bind_tools()
    ↓
RunnableBinding          ← OUTPUT của bind_tools()
    ↓
ainvoke()
    ↓
AIMessage                ← OUTPUT của model
    ↓
tool_calls               ← nếu model muốn gọi tool
Vì vậy ghi chú của bạn có thể viết chính xác thành:
Input:
    tools
    tool_choice=None
    **kwargs

Output:
    Runnable đã được bind với tools
    (thường là một RunnableBinding bao quanh ChatOllama)

Và đừng ghi:

Output: AIMessage

cho bind_tools().

AIMessage là output của:

runnable.invoke(...)

hoặc:

await runnable.ainvoke(...)

chứ không phải output của bind_tools().