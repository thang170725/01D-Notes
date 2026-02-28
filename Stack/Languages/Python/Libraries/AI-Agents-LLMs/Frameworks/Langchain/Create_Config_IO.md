- [ChatOllama](#chatollama)
- [PromptTemplate](#prompttemplate)
  - [gợi ý tên món ăn](#gợi-ý-tên-món-ăn)
- [|](#)
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
khởi tạo một đối tượng LLM (Large Language Model)
```
**Syn**
```bash
from langchain_community.chat_models import ChatOllama # from langchain_ollama import ChatOllama

llm = ChatOllama(
    model="llama3",
    temperature=0
)

- model         : tên của model llm
- temperature   : độ ngẫu nhiên của AI
```
# PromptTemplate
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
## gợi ý tên món ăn
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
# |
```bash
Để nối pipeline.
```
**Ex**
```bash
chain = prompt | model | StrOutputParser()
chain.invoke({"topic": "AI"})
```
## .invoke()
```bash
- Đây là lệnh gửi prompt cho AI.
- invoke() là API chuẩn của LangChain
    + Input: string / message / prompt object
    + Output: AIMessage
```
**Syn**
```bash
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