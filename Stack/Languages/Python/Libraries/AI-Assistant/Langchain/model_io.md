- [ChatOllama](#chatollama)
  - [.content](#content)
- [PromptTemplate](#prompttemplate)
  - [gợi ý tên món ăn](#gợi-ý-tên-món-ăn)
---
# ChatOllama
```bash
khởi tạo một đối tượng LLM (Large Language Model)
```
**Syn**
```bash
llm = ChatOllama(
    model="llama3",
    temperature=0
)

- temperature   : độ ngẫu nhiên của AI
```
## .content
**Ex**
```python
from langchain_community.chat_models import ChatOllama

llm = ChatOllama(
    model="llama3",
    temperature=0
)

response = llm.invoke("Giải thích LangChain trong 1 câu")
print(response.content)
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