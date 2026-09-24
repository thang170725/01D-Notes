- [Create (Nhóm khởi tạo)](#create-nhóm-khởi-tạo)
  - [ChatGoogleGenerativeAI](#chatgooglegenerativeai)
    - [.bind\_tools()](#bind_tools)
---
# Create (Nhóm khởi tạo)
## ChatGoogleGenerativeAI
```python
from langchain_google_genai import ChatGoogleGenerativeAI

llm = ChatGoogleGenerativeAI(
    model="gemini-1.5-flash",  # hoặc gemini-pro
    temperature=0
)

response = llm.invoke("Giải thích AI là gì?")
print(response.content)

#  3. Dùng trong chain
from langchain_core.prompts import ChatPromptTemplate

prompt = ChatPromptTemplate.from_template("Hãy trả lời: {question}")

chain = prompt | llm

res = chain.invoke({"question": "Python là gì?"})
print(res.content)
```
### .bind_tools()
**Ex**
```python
from langchain.tools import tool

@tool
def calculator(expression: str) -> str:
    """Tính toán biểu thức toán học"""

    return str(eval(expression))

from langchain_google_genai import ChatGoogleGenerativeAI

llm = ChatGoogleGenerativeAI(
    model="gemini-2.5-flash",
    google_api_key="YOUR_API_KEY",
    temperature=0
)

llm_with_tools = llm.bind_tools([calculator])