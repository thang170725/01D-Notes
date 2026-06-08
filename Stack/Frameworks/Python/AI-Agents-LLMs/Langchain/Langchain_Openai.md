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