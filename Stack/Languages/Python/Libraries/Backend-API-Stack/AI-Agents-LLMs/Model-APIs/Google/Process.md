- [genai (làm việc với mô hình AI của Google)](#genai-làm-việc-với-mô-hình-ai-của-google)
  - [.Client() (class dùng để tạo đối tượng kết nối tới dịch vụ Gemini)](#client-class-dùng-để-tạo-đối-tượng-kết-nối-tới-dịch-vụ-gemini)
    - [.models](#models)
      - [.embed\_content() (biến văn bản thành vector)](#embed_content-biến-văn-bản-thành-vector)
        - [.embeddings](#embeddings)
          - [.values](#values)
      - [.list()](#list)
        - [.name](#name)
  - [types](#types)
    - [.EmbedContentConfig()](#embedcontentconfig)
---
# genai (làm việc với mô hình AI của Google)
```bash
Nó chứa các class và hàm để làm việc với mô hình AI của Google như:
    - Tạo văn bản
    - Phân tích hình ảnh
    - Sinh ảnh
    - Chat nhiều lượt
    - Embedding
    - Gọi tool/function
```
## .Client() (class dùng để tạo đối tượng kết nối tới dịch vụ Gemini)
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
    model="gemini-embedding-2",
    contents=text,
    config=types.EmbedContentConfig(
        task_type="RETRIEVAL_DOCUMENT"  # Ép kiểu enum chuẩn viết hoa
    )
)

- Input:
    + model: Model embedding                 
    + contents: Văn bản cần chuyển thành vector 
    + config: Cấu hình embedding              
- Output:
    + response: Kết quả là một object          
```
##### .embeddings
###### .values
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
## types
```bash
là module chứa các kiểu dữ liệu (classes, enums, config objects) mà SDK Gemini định nghĩa sẵn
```
types.GenerateContentConfig
### .EmbedContentConfig()
**Syn**
```bash
types.EmbedContentConfig(
    task_type="RETRIEVAL_DOCUMENT"
)

- task_type:
    + RETRIEVAL_DOCUMENT    : Embedding tài liệu để lưu vector DB
    + RETRIEVAL_QUERY	    : Embedding câu hỏi của người dùng
    + SEMANTIC_SIMILARITY	: So sánh độ giống nhau
    + CLASSIFICATION	    : Phân loại văn bản
    + CLUSTERING	        : Gom nhóm văn bản
```
types.SafetySetting
types.Part
types.Content
...