- [.invoke()](#invoke)
---
# .invoke()
```bash
- Đây là lệnh gửi prompt cho AI.
- invoke() là API chuẩn của LangChain
    + Input: string / message / prompt object
    + Output: AIMessage
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