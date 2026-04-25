- [Introduction](#introduction)
- [langchain\_core.messages](#langchain_coremessages)
  - [SystemMessage](#systemmessage)
  - [HumanMessage()](#humanmessage)
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