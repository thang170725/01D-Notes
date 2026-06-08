- [ChatGoogleGenerativeAI](#chatgooglegenerativeai)
- [.invoke()](#invoke)
  - [.content](#content)
- [with\_structured\_output() (ép model trả về kết quả theo một cấu trúc cố định (schema) thay vì trả về text tự do)](#with_structured_output-ép-model-trả-về-kết-quả-theo-một-cấu-trúc-cố-định-schema-thay-vì-trả-về-text-tự-do)
---
# ChatGoogleGenerativeAI 
```bash
ChatGoogleGenerativeAI là class trong package langchain-google-genai, dùng để kết nối LangChain với các model Gemini của Google.
```
**Syn**
```bash
llm = ChatGoogleGenerativeAI(
    model="models/gemini-2.5-flash",
    google_api_key=api_key,
    temperature=0,
    request_timeout=60
)
```
# .invoke()
```bash
response = llm.invoke()

- Output: thường trả về một đối tượng
```
## .content
**Ex**
```python
from langchain_google_genai import ChatGoogleGenerativeAI

llm = ChatGoogleGenerativeAI(
    model="gemini-2.5-flash",
    temperature=0
)
# Lúc này biến llm đại diện cho một model Gemini mà bạn có thể gọi:

response = llm.invoke("Thủ đô Việt Nam là gì?")

print(response.content) # Kết quả: Hà Nội là thủ đô của Việt Nam.
```
# with_structured_output() (ép model trả về kết quả theo một cấu trúc cố định (schema) thay vì trả về text tự do)
```bash
- Nó rất hữu ích khi bạn muốn:
    + Nhận JSON đúng format
    + Parse dữ liệu an toàn
    + Tránh lỗi model trả lời lung tung
    + Dùng cho API backend / automation
```
**Ex**
```python
from pydantic import BaseModel

class Person(BaseModel):
    name: str
    age: int

structured_llm = llm.with_structured_output(Person)

result = structured_llm.invoke("Nam 25 tuổi")
print(result)

# Kết quả luôn là object:
# Person(name='Nam', age=25)
```