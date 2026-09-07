- [Sentence Transformers Introduction](#sentence-transformers-introduction)
- [Installation](#installation)
- [SentenceTransformer](#sentencetransformer)
  - [.encode() (chuyển text thành vector)](#encode-chuyển-text-thành-vector)
    - [.shape](#shape)
- [util](#util)
  - [cos\_sim() (hàm cosin để so sánh 2 vector)](#cos_sim-hàm-cosin-để-so-sánh-2-vector)
    - [.argmax()](#argmax)
---
# Sentence Transformers Introduction
[Kiến thức cơ bản về sentence transformers](../../../../../../../Domains/Artificial-Intelligence/AI-Core/03-Machine-Learning/04-Deep-Learning/01-NLP/04-Models/SBERT.md#sentence-bert-introduction-sbert-để-tạo-ra-vector-biểu-diễn-của-cả-câu-sentence-embedding)
# Installation
```bash
pip install sentence-transformers
```
# SentenceTransformer
## .encode() (chuyển text thành vector)
**Ex1: Mã hóa câu**
```python
from sentence_transformers import SentenceTransformer

model = SentenceTransformer("all-MiniLM-L6-v2")

sentence = "Tôi thích học Python"

embedding = model.encode(sentence)

print(type(embedding)) # <class 'numpy.ndarray'>
print(len(embedding)) # 384
print(embedding[:10]) # [-0.12  0.54 -0.78 ...]
```
### .shape
**Ex**
```python
Ví dụ 3: Nhiều câu
from sentence_transformers import SentenceTransformer

model = SentenceTransformer("all-MiniLM-L6-v2")

sentences = [
    "Tôi thích học Python",
    "Tôi rất yêu lập trình Python",
    "Hôm nay trời mưa",
    "Tôi đi siêu thị"
]

embeddings = model.encode(sentences)

print(embeddings.shape) # (4, 384). 4 câu Mỗi câu là một vector 384 chiều
```
# util
## cos_sim() (hàm cosin để so sánh 2 vector)
**Ex1: So sánh hai câu**
```python
from sentence_transformers import SentenceTransformer
from sentence_transformers.util import cos_sim

model = SentenceTransformer("all-MiniLM-L6-v2")

s1 = "Tôi thích học Python"
s2 = "Tôi rất yêu lập trình Python"

e1 = model.encode(s1, convert_to_tensor=True)
e2 = model.encode(s2, convert_to_tensor=True)

score = cos_sim(e1, e2)

print(score) # tensor([[0.93]]). Điểm càng gần 1 thì hai câu càng giống nhau.
```
**Ex2: Tìm câu giống nhất**
```python
from sentence_transformers import SentenceTransformer
from sentence_transformers.util import cos_sim

model = SentenceTransformer("all-MiniLM-L6-v2")

docs = [
    "Tôi thích học Python",
    "Hôm nay trời đẹp",
    "Con mèo đang ngủ",
    "Python là ngôn ngữ lập trình"
]

query = "Tôi muốn học lập trình Python"

doc_embeddings = model.encode(docs, convert_to_tensor=True)
query_embedding = model.encode(query, convert_to_tensor=True)

scores = cos_sim(query_embedding, doc_embeddings) # tensor([[0.89, 0.18, 0.10, 0.85]])
```
### .argmax()
