- [.content](#content)
---
# .content
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