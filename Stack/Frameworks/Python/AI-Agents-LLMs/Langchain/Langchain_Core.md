- [Introduction](#introduction)
- [langchain\_core.messages](#langchain_coremessages)
  - [SystemMessage](#systemmessage)
  - [HumanMessage()](#humanmessage)
- [PydanticOutputParser()](#pydanticoutputparser)
- [RunnableWithMessageHistory](#runnablewithmessagehistory)
- [RunnableLambda](#runnablelambda)
- [RunnableParallel](#runnableparallel)
- [PromptTemplate (Nhóm thiết lập khuôn mẫu)](#prompttemplate-nhóm-thiết-lập-khuôn-mẫu)
  - [.from\_template()](#from_template)
---
# Introduction
```bash
- Nếu bạn thấy LangChain “khó đọc” vì nó chia theo pipeline, thì langchain_core chính là nơi định nghĩa các primitive (khối cơ bản) để pipeline đó hoạt động.
- Nói ngắn gọn: langchain_core không phải để build app trực tiếp, mà là để định nghĩa chuẩn chung cho các thành phần như model, prompt, output, chain.
```
# langchain_core.messages
## SystemMessage
```bash
- Dùng để thiết lập “luật chơi” / ngữ cảnh chung cho model.
- Định nghĩa: vai trò, phong cách, quy tắc trả lời.
- Dùng khi muốn model:
    + trả lời theo phong cách cụ thể (giáo viên, chuyên gia…)
    + hạn chế/tuân thủ quy tắc
    + định hướng toàn bộ cuộc hội thoại
```
**Ex**
```python
from langchain_core.messages import SystemMessage

system_msg = SystemMessage(
    content="You are a helpful assistant that explains code clearly."
)
```
## HumanMessage()
```bash
- Đại diện cho input của người dùng (user prompt).
```
**Ex**
```python
from langchain_core.messages import HumanMessage

human_msg = HumanMessage(
    content="Explain what a Python decorator is."
)
```
**Ex2: Cách dùng chung với Chat Model**
```python
from langchain_core.messages import SystemMessage, HumanMessage
from langchain_openai import ChatOpenAI

llm = ChatOpenAI(model="gpt-4o-mini")

messages = [
    SystemMessage(content="You are a strict Python teacher."),
    HumanMessage(content="Explain list comprehension.")
]

response = llm.invoke(messages)

print(response.content)

# Model sẽ đọc theo thứ tự: (có thể có thêm AIMessage nếu multi-turn)
# SystemMessage → hiểu vai trò
# HumanMessage → hiểu câu hỏi
# Sau đó sinh ra câu trả lời.
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
# RunnableWithMessageHistory
```bash
Dùng khi làm chatbot có session.
```
**Syn**
```bash
from langchain_core.runnables.history import RunnableWithMessageHistory
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