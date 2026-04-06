- [ChatOllama](#chatollama)
- [PromptTemplate (Nhóm thiết lập khuôn mẫu)](#prompttemplate-nhóm-thiết-lập-khuôn-mẫu)
  - [.from\_template()](#from_template)
  - [.format()](#format)
- [| (nối pipeline)](#-nối-pipeline)
- [.invoke()](#invoke)
- [RunnablePassthrough](#runnablepassthrough)
- [RunnableParallel](#runnableparallel)
- [RunnableLambda](#runnablelambda)
- [streaming](#streaming)
- [PydanticOutputParser()](#pydanticoutputparser)
- [.bind()](#bind)
- [RunnableWithMessageHistory](#runnablewithmessagehistory)
- [Agent tạo nhanh](#agent-tạo-nhanh)
---
# ChatOllama
```bash
- khởi tạo một đối tượng LLM (Large Language Model).
- cần tải và import thư viện:
    + pip install langchain_community | pip install langchain_ollama
    + from langchain_community.chat_models import ChatOllama
    + from langchain_ollama import ChatOllama
    + langchain_community (cách cũ): Là nơi chứa các integration “gom chung” (Ollama, HuggingFace, v.v.)
        - Đang bị deprecate dần
        - Update chậm hơn
        - Code đôi khi không tối ưu
    + langchain_ollama (cách mới): Là package tách riêng chính thức cho Ollama
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
# PromptTemplate (Nhóm thiết lập khuôn mẫu)
```bash
- PromptTemplate là một template (khuôn mẫu) để tạo prompt động cho LLM
- Nó giống:
    + f-string trong Python
    + nhưng có cấu trúc + quản lý tốt hơn
- Dùng để làm gì?
    1. Truyền biến vào prompt. Thay vì viết cứng: "Hãy trả lời câu hỏi: AI là gì?". Bạn làm: "Hãy trả lời câu hỏi: {question}"
    2. Tái sử dụng prompt: Viết 1 lần. Dùng nhiều lần với dữ liệu khác nhau
    3. Build hệ thống LLM (RAG, chatbot, agent). Ví dụ:
        + {context} → dữ liệu từ vector DB
        + {question} → câu hỏi user
    4. Kết hợp với pipeline (|): prompt | llm
```
**Syn**
```bash
prompt = PromptTemplate(
    input_variables=["topic"],
    template="Giải thích {topic} trong 1 câu ngắn gọn"
)

- input_variables   : danh sách biến được phép truyền vào
```
**Ex**
```python
from langchain_community.chat_models import ChatOllama
from langchain_core.prompts import PromptTemplate

llm = ChatOllama(model="llama3", temperature=0)

prompt = PromptTemplate(
    input_variables=["topic"],
    template="Giải thích {topic} trong 1 câu ngắn gọn"
)

response = llm.invoke(prompt.format(topic="LangChain"))
print(response.content)
```
**Ex: Gợi ý nấu ăn**
```python
prompt = PromptTemplate(
    input_variables=["ingredients"],
    template="""
Bạn là trợ lý nấu ăn.
Nguyên liệu có sẵn: {ingredients}
Hãy gợi ý 1 món ăn phù hợp.
"""
)

llm.invoke(
    prompt.format(
        ingredients="trứng, cà chua, hành"
    )
)
```
**Ex3: PromptTemplate + dic**
```python
prompt.invoke({
    "ingredients": "trứng, cà chua"
})
```
**Ex: gợi ý tên món ăn**
```python
from langchain_community.chat_models import ChatOllama
from langchain_core.prompts import PromptTemplate

llm = ChatOllama(
    model="llama3",
    temperature=0
)

prompt = PromptTemplate(
    input_variables=["ingredients"],
    template="""
Bạn là backend AI cho ứng dụng Smart-Recipe.

Nhiệm vụ:
- CHỈ trả về TÊN MỘT MÓN ĂN DUY NHẤT
- KHÔNG mô tả
- KHÔNG liệt kê nguyên liệu
- KHÔNG hướng dẫn nấu
- KHÔNG thêm giải thích

Ràng buộc BẮT BUỘC:
- Chỉ đề xuất món ăn có thể chế biến từ TẤT CẢ nguyên liệu đã cho
- KHÔNG được bỏ qua nguyên liệu chính

Nguyên liệu chính: {ingredients}

Trả lời đúng 1 dòng, chỉ chứa tên món.
"""
)

response = llm.invoke(
    prompt.format(
        ingredients="thịt heo, hành tây, cà chua, mực"
    )
)

print(response.content)
```
## .from_template()
```bash
- Dùng để tạo một PromptTemplate từ chuỗi template
```
**Syn**
```bash
PromptTemplate.from_template(template_string)

- Input:
    + template_string: chuỗi có chứa biến {}
```
**Ex**
```python
from langchain.prompts import PromptTemplate

prompt = PromptTemplate.from_template(
    "Hãy trả lời câu hỏi: {question}"
)

# prompt = một object template. CHƯA có giá trị thật
# from_template = khai báo khuôn mẫu
```
## .format()
```bash
- Dùng để điền dữ liệu vào template → tạo prompt hoàn chỉnh
```
**Syn**
```bash
prompt.format(variable_name=value)

- Input:
    + variable_name: tên biến trong prompt
```
**Ex**
```python
result = prompt.format(
    question="AI là gì?"
)

print(result) # Hãy trả lời câu hỏi: AI là gì?
```
# | (nối pipeline)
```bash
Để nối pipeline.
```
**Ex**
```bash
chain = prompt | model | StrOutputParser()
chain.invoke({"topic": "AI"})
```
# .invoke()
```bash
- Đây là lệnh gửi prompt cho AI.
- invoke() là API chuẩn của LangChain
    + Input: string / message / prompt object
    + Output: AIMessage
```
**Syn**
```bash
result = runnable.invoke(input, config=None)

- Input:
    + input: dữ liệu đầu vào (có thể là str, dict, list, messages…)
    + config: optional (timeout, callbacks, metadata…)
```
**Ex: nhận list**
```python
from langchain_openai import ChatOpenAI
from langchain_core.messages import HumanMessage

llm = ChatOpenAI()

response = llm.invoke([
    HumanMessage(content="Hello")
])

#  Input: List[BaseMessage]
#  Output: AIMessage
```
**Ex2: Nhận string**
```bash
from langchain_openai import OpenAI

llm = OpenAI()

response = llm.invoke("Write a poem about AI")

# Input: str
# Output: str
```
**Ex3: Nhận dict**
```python
from langchain_core.prompts import PromptTemplate

prompt = PromptTemplate.from_template("Hello {name}")

result = prompt.invoke({"name": "Thang"})

# Input: dict
# Output: PromptValue
```
**Ex4**
```python
chain = prompt | llm

result = chain.invoke({"name": "Thang"})

#  Input: dict (theo variables của prompt)
```
**Ex**
```python
chain.invoke(
    {"topic": "AI"},
    config={"tags": ["demo"]}
)
```
**Ex**
```python
from langchain_ollama import ChatOllama
from langchain_core.prompts import PromptTemplate

# ========== LLM ==========
llm = ChatOllama(
    model="mistral",
    temperature=0
)

prompt = PromptTemplate(
    input_variables=["ingredients"],
    template="""
Bạn là trợ lý nấu ăn.
Nguyên liệu có sẵn: {ingredients}
Hãy gợi ý 1 món ăn phù hợp.
"""
)

response = llm.invoke(
    prompt.format(
        ingredients="thịt lợn, cà chua, hành, trứng"
    )
)

print(response.content)
```
# RunnablePassthrough
```bash
- Rất hay dùng trong RAG
- Nó truyền thẳng input xuống bước sau
```
**Syn**
```bash
from langchain_core.runnables import RunnablePassthrough

chain = {
    "context": retriever,
    "question": RunnablePassthrough()
} | prompt | model
```
# RunnableParallel
```bash
- Chạy song song
```
**Syn**
```bash
from langchain_core.runnables import RunnableParallel

chain = RunnableParallel(
    vi=prompt_vi | model,
    en=prompt_en | model
)

chain.invoke({"topic": "AI"})

# {
#   "vi": "...",
#   "en": "..."
# }
```
# RunnableLambda
```bash
Cho phép chèn hàm python vào pipeline
```
**Syn**
```bash
from langchain_core.runnables import RunnableLambda

def upper(text):
    return text.upper()

chain = prompt | model | RunnableLambda(upper)
```
# streaming
```bash
- Quan trong khi làm chatbot realtime
```
**Ex**
```python
for chunk in chain.stream({"topic": "AI"}):
    print(chunk, end="")
```
# PydanticOutputParser()
```bash
dùng khi muốn output chuẩn JSON
```
**Ex**
```bash
from pydantic import BaseModel
from langchain_core.output_parsers import PydanticOutputParser

class Answer(BaseModel):
    explanation: str
    example: str

parser = PydanticOutputParser(pydantic_object=Answer)

chain = prompt | model | parser
```
# .bind()
```python
model = ChatOpenAI().bind(
    temperature=0.2,
    max_tokens=200
)

# chain = prompt | model.bind(temperature=0)
```
# RunnableWithMessageHistory
```bash
Dùng khi làm chatbot có session.
```
**Syn**
```bash
from langchain_core.runnables.history import RunnableWithMessageHistory
```
# Agent tạo nhanh
```bash
from langchain.agents import create_openai_tools_agent
from langchain.agents import AgentExecutor
```
SystemMessage là gì?
👉 Mục đích
Dùng để thiết lập “luật chơi” / ngữ cảnh chung cho model.
Định nghĩa: vai trò, phong cách, quy tắc trả lời.
🧾 Ví dụ
from langchain_core.messages import SystemMessage

system_msg = SystemMessage(
    content="You are a helpful assistant that explains code clearly."
)
📌 Khi nào dùng?
Muốn model:
trả lời theo phong cách cụ thể (giáo viên, chuyên gia…)
hạn chế/tuân thủ quy tắc
định hướng toàn bộ cuộc hội thoại
👤 2. HumanMessage là gì?
👉 Mục đích
Đại diện cho input của người dùng (user prompt).
🧾 Ví dụ
from langchain_core.messages import HumanMessage

human_msg = HumanMessage(
    content="Explain what a Python decorator is."
)
🤖 3. Cách dùng chung với Chat Model
🧾 Ví dụ đầy đủ
from langchain_core.messages import SystemMessage, HumanMessage
from langchain_openai import ChatOpenAI

llm = ChatOpenAI(model="gpt-4o-mini")

messages = [
    SystemMessage(content="You are a strict Python teacher."),
    HumanMessage(content="Explain list comprehension.")
]

response = llm.invoke(messages)

print(response.content)
🔄 4. Luồng hoạt động

Model sẽ đọc theo thứ tự:

SystemMessage → hiểu vai trò
HumanMessage → hiểu câu hỏi
(có thể có thêm AIMessage nếu multi-turn)

👉 Sau đó sinh ra câu trả lời.

⚖️ 5. So sánh nhanh
Loại message	Vai trò	Dùng khi nào
SystemMessage	Setup global behavior	Luôn nên có
HumanMessage	Input user	Bắt buộc
AIMessage	Output model	Multi-turn chat
⚡ 6. Ví dụ nâng cao (multi-turn)
from langchain_core.messages import SystemMessage, HumanMessage, AIMessage

messages = [
    SystemMessage(content="You are a coding assistant."),
    HumanMessage(content="What is recursion?"),
    AIMessage(content="Recursion is when a function calls itself."),
    HumanMessage(content="Give me an example in Python.")
]
🚀 7. Best practices
✅ Luôn đặt SystemMessage ở đầu
✅ Viết rõ ràng, cụ thể (prompt engineering)
❌ Không nhồi quá nhiều rules → model dễ bị nhiễu
✅ Giữ HumanMessage ngắn gọn, đúng trọng tâm
🔚 Tóm lại
SystemMessage = thiết lập cách model suy nghĩ
HumanMessage = câu hỏi của người dùng
Kết hợp lại → tạo thành context hội thoại chuẩn cho LLM

Nếu bạn muốn, mình có thể giải thích thêm:

PromptTemplate vs Messages
ChatPromptTemplate (rất quan trọng trong LangChain)
hoặc debug lỗi khi dùng LangChain 👀