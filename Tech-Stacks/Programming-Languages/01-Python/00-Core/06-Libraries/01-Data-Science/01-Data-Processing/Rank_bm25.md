- [Rank\_bm25 Introduction (thư viện này thường dùng với các kỹ thuật xoay quanh thuật toán bm25)](#rank_bm25-introduction-thư-viện-này-thường-dùng-với-các-kỹ-thuật-xoay-quanh-thuật-toán-bm25)
- [Installation](#installation)
- [BM250kapi](#bm250kapi)
  - [.get\_scores()](#get_scores)
  - [.get\_top\_n() (lấy tài liệu tốt nhất)](#get_top_n-lấy-tài-liệu-tốt-nhất)
- [Practices](#practices)
  - [Tìm kiếm tài liệu đơn giản bằng BM250kapi và get\_scrores](#tìm-kiếm-tài-liệu-đơn-giản-bằng-bm250kapi-và-get_scrores)
---
# Rank_bm25 Introduction (thư viện này thường dùng với các kỹ thuật xoay quanh thuật toán bm25)
- Link: [Kiến thức cơ bản](../../../../../../Domains/Artificial-Intelligence/AI-Core/03-Machine-Learning/04-Deep-Learning/01-NLP/00-NLP-Algorithm.md#bm25-best-matching-25---thuật-toán-xếp-hạng-văn-bản-để-tìm-tài-liệu-nào-liên-quan-nhất-đến-từ-khóa-người-dùng-tìm-kiếm)
# Installation
```bash
pip install rank-bm25
```
# BM250kapi
## .get_scores()
## .get_top_n() (lấy tài liệu tốt nhất)
```bash
best = bm25.get_top_n(tokenized_query, docs, n=2)

- Input:
    + tokenized_query (str) : câu người dùng nhập vào dạng str để tìm tài liệu
    + docs (list)           : tài liệu 
    + n (int)               : lấy mấy tài liệu phù hợp nhất
```
# Practices
## Tìm kiếm tài liệu đơn giản bằng BM250kapi và get_scrores
**Ex**
```python
from rank_bm25 import BM25Okapi

docs = [
    "Python is a programming language",
    "Python is used for machine learning",
    "OCR extracts text from images",
    "Machine learning uses Python",
    "Java is also a programming language"
]

# Tokenize (tách từ)
tokenized_docs = [doc.lower().split() for doc in docs]

# Xây dựng BM25
bm25 = BM25Okapi(tokenized_docs)

# Người dùng tìm kiếm
query = "python machine learning"

tokenized_query = query.lower().split()

scores = bm25.get_scores(tokenized_query)

print(scores) [1.25, 4.82, 0.00, 4.35, 0.68]
```