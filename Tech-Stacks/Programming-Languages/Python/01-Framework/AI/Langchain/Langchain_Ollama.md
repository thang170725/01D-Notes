- [Langchain Ollama Introduction](#langchain-ollama-introduction)
- [Installation](#installation)
- [ollama pull ... (tải model từ hugging face)](#ollama-pull--tải-model-từ-hugging-face)
- [ollama run ... (chạy llm trực tiếp ằng terminal)](#ollama-run--chạy-llm-trực-tiếp-ằng-terminal)
- [Create (Nhóm khởi tạo)](#create-nhóm-khởi-tạo)
  - [ChatOllama() (khởi tạo một đối tượng LLM)](#chatollama-khởi-tạo-một-đối-tượng-llm)
    - [.bind\_tools()](#bind_tools)
---
# Langchain Ollama Introduction 
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
```
### .bind_tools()
**Syn**
```bash
llm.bind_tools(
    tools,
    *,
    tool_choice=None,
    **kwargs
)

- Output: Nó trả về một Runnable đã được bind tool
```
**Ex**
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


llm_with_tools
    ↓
Runnable

API hiện tại ghi return type là:

Runnable[LanguageModelInput, AIMessage]

Nói đơn giản:

llm

là model bình thường.

Còn:

llm_with_tools

là model đã được cấu hình để tool calling.

5. Khi nào mới thực sự gọi model?

Phải:

response = llm_with_tools.invoke(
    "Tôi muốn xem thông tin tài khoản của tôi"
)

Lúc này mới có:

User
 │
 │ "Tôi muốn xem thông tin tài khoản"
 ↓
llm_with_tools
 │
 │ model suy luận
 ↓
AIMessage

Nếu model quyết định gọi tool:

response.tool_calls

có thể nhận:

[
    {
        "name": "get_user_info",
        "args": {},
        "id": "call_xxx",
        "type": "tool_call"
    }
]

Đây là behavior được mô tả trong docs của ChatOllama.

6. Đây là chỗ nhiều người nhầm nhất

Bạn có:

llm_with_tools = llm.bind_tools(tools)

Không có nghĩa:

bind_tools
   ↓
chạy tool

Mà là:

bind_tools
   ↓
đăng ký / mô tả tools cho model
   ↓
model biết những tool nào nó có thể yêu cầu

Sau đó:

invoke()
   ↓
LLM quyết định
   ↓
có cần tool không?

Nếu có:

AIMessage
   ↓
tool_calls
   ↓
ToolExecutor / ToolNode
   ↓
thực thi Python function
7. tool_choice là gì?

Signature:

llm.bind_tools(
    tools,
    tool_choice=None
)

Theo API hiện tại, tool_choice có thể nhận các dạng như:

None
"auto"
"any"
True / False
dict

nhưng đối với ChatOllama, tool_choice hiện được docs ghi là bị bỏ qua vì Ollama không hỗ trợ parameter này theo cách đó.

Ví dụ với một số integration khác người ta có thể làm:

llm.bind_tools(
    tools,
    tool_choice="any"
)

ý tưởng là:

"Model phải sử dụng tool."

Nhưng với ChatOllama hiện tại, đừng dựa vào tool_choice để ép Ollama gọi một tool cụ thể, vì parameter này được ghi rõ là ignored.

8. **kwargs là gì?

Phần:

**kwargs

cho phép truyền thêm tham số xuống self.bind(...).

Ví dụ về mặt cơ chế:

llm.bind_tools(
    tools,
    some_parameter=...
)

thì các keyword argument bổ sung sẽ được chuyển tiếp.

Nhưng khi dùng ChatOllama, bạn thường không cần quan tâm **kwargs ở bước đầu học tool calling.

9. Liên hệ với @tool bạn hỏi lúc trước

Bạn có:

@tool(
    "get_user_info",
    args_schema=GetUserInfoInput
)
def get_user_info() -> str:
    """
    Lấy thông tin người dùng.
    """
    ...

Sau đó:

llm_with_tools = llm.bind_tools([
    get_user_info
])

Có thể hình dung toàn bộ quá trình:

                  @tool
                    │
                    ▼
          ┌───────────────────┐
          │ get_user_info     │
          │                   │
          │ name              │
          │ description       │
          │ args_schema       │
          │ function          │
          └─────────┬─────────┘
                    │
                    │ bind_tools()
                    ▼
          ┌───────────────────┐
          │    ChatOllama     │
          │ + tool schema     │
          └─────────┬─────────┘
                    │
                    │ invoke()
                    ▼
                 LLM
                    │
             ┌──────┴──────┐
             │             │
          trả lời        gọi tool
          trực tiếp         │
                            ▼
                       tool_calls
10. Còn ToolExecutor nằm ở đâu?

Đây mới là kiến trúc đầy đủ:

User
 │
 │ "Cho tôi xem thông tin tài khoản"
 ↓
ChatOllama
 + bind_tools([get_user_info])
 │
 │ model quyết định
 ↓
AIMessage
 │
 └── tool_calls
       │
       │ name = get_user_info
       │ args = {}
       ↓
ToolExecutor / ToolNode
       │
       ↓
get_user_info(...)
       │
       ↓
Repository
       │
       ↓
MySQL
       │
       ↓
ToolMessage
       │
       ↓
ChatOllama
       │
       ↓
Final answer

Đây chính là lý do đoạn code trước của bạn có:

raise NotImplementedError("Executed via ToolExecutor")

Nếu project của bạn thiết kế theo architecture này thì get_user_info được khai báo cho LLM, còn Executor mới là thằng thực thi logic thật.

11. Một ví dụ hoàn chỉnh tối giản
from langchain_core.tools import tool
from langchain_ollama import ChatOllama


@tool
def add(a: int, b: int) -> int:
    """Add two integers."""
    return a + b


llm = ChatOllama(
    model="qwen3.5:4b",
    temperature=0,
)

llm_with_tools = llm.bind_tools([add])

response = llm_with_tools.invoke(
    "What is 10 + 20?"
)

print(response)
print(response.tool_calls)

Model có thể trả:

response.tool_calls
[
    {
        "name": "add",
        "args": {
            "a": 10,
            "b": 20
        },
        "id": "call_xxx",
        "type": "tool_call"
    }
]

Chú ý: ở thời điểm này add(10, 20) có thể chưa được Python thực thi. AIMessage.tool_calls chỉ là model nói:

"Tôi muốn gọi tool add với a=10, b=20."

Sau đó executor mới lấy name + args để thực thi tool.

Đây là điểm cốt lõi của tool calling: bind_tools() đưa khả năng/tool schema vào model; invoke() nhận quyết định tool-call từ model; executor mới thực sự chạy function.