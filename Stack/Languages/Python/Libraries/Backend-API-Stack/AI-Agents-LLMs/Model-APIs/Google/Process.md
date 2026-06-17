- [genai](#genai)
  - [.Client()](#client)
    - [.models](#models)
      - [.embed\_content() (biến văn bản thành vector)](#embed_content-biến-văn-bản-thành-vector)
      - [.list()](#list)
        - [.name](#name)
---
# genai
## .Client()
**Syn**
```bash
from google import genai

client = genai.Client(api_key="YOUR_API_KEY")
```
```python
from google import genai

client = genai.Client(api_key="YOUR_API_KEY")

response = client.models.generate_content(
    model="gemini-2.5-flash",
    contents="Xin chào"
)

print(response.text)
```
### .models
#### .embed_content() (biến văn bản thành vector)
```bash
Nó là một trong những hàm quan trọng nhất khi xây dựng:
    - RAG (Retrieval-Augmented Generation)
    - Semantic Search
    - Chat với tài liệu PDF
    - Hệ thống hỏi đáp trên dữ liệu riêng
    - Recommendation dựa trên ngữ nghĩa
```
**Syn**
```bash
response = client.models.embed_content(
    model=...,
    contents=...,
    config=...
)

- Input:
    + model: Model embedding                 
    + contents: Văn bản cần chuyển thành vector 
    + config: Cấu hình embedding              
- Output:
    + response: Kết quả chứa vector             
```
**Ex**
```python
from google import genai

client = genai.Client(api_key=API_KEY)

response = client.models.embed_content(
    model="text-embedding-004",
    contents="Tôi thích học AI"
)

print(response.embeddings[0].values[:5])
# [
#     -0.012,
#     0.345,
#     0.129,
#     -0.908,
#     0.442
# ]
```
#### .list() 
##### .name
```python
for model in client.models.list():
    print(model.name)
```