- [Create (Nhóm khởi tạo)](#create-nhóm-khởi-tạo)
  - [ChatGoogleGenerativeAI](#chatgooglegenerativeai)
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