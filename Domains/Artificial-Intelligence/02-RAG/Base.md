- [Introduction](#introduction)
  - [Pipeline chuẩn (production mindset)](#pipeline-chuẩn-production-mindset)
  - [Phân loại RAG](#phân-loại-rag)
---
# Introduction
```bash
- Vấn đề của AI thông thường. Các mô hình như ChatGPT chỉ biết những gì đã được huấn luyện trước đó.
    + Ví dụ: Em hỏi: “Quy định nội bộ công ty ABC về nghỉ phép là gì?” AI không biết, vì tài liệu đó không có trong dữ liệu huấn luyện. => Đây là lúc RAG xuất hiện.
- RAG = Retrieval-Augmented Generation. Dịch dễ hiểu: “Tìm tài liệu trước → rồi mới trả lời”
- Thay vì:
    + AI trả lời dựa hoàn toàn vào trí nhớ
    + Thì RAG: AI đi tìm tài liệu liên quan, đọc nó, rồi trả lời dựa trên tài liệu đó
```
**Pipeline**
```bash
User hỏi → tìm tài liệu → nhét vào prompt → LLM trả lời
```
**3 khối trong RAG**
```bash
1. Retriever (trái tim của RAG)
    - Nhiệm vụ: Tìm tài liệu liên quan nhất
    - Có 3 loại (từ paper):
        1. Sparse retrieval:
            - BM25 (kiểu Google search)
            - dựa vào keyword
            - mạnh: chính xác literal
            - yếu: không hiểu nghĩa
        2. Dense retrieval (vector)
            - embedding + cosine similarity
            - mạnh: hiểu semantic
            - yếu: đôi khi “đoán sai”
        3. Hybrid (pro dùng cái này)
            - kết hợp BM25 + vector => đây là best practice trong industry  
2. Chunking (cái mà paper ít nói nhưng cực quan trọng)
    - Bạn KHÔNG đưa cả document vào. bạn phải chia nhỏ (chunk)
    - Quy tắc: 200–500 tokens, có overlap (10–20%)
    - Vì:
        + nhỏ quá → mất context
        + to quá → search kém
    => Đây là thứ quyết định 80% chất lượng RAG 
3. Embedding
    - Chuyển text → vector
    - Lưu ý quan trọng:
        + embedding model ≠ LLM
        + embedding quyết định retrieval quality
4. Generator (LLM)
    - chỉ làm 1 việc: viết lại câu trả lời dựa trên context
    - Nếu RAG sai: 80% lỗi ở retriever, KHÔNG phải LLM
```
## Pipeline chuẩn (production mindset)
```bash
Pipeline chuẩn từ paper → thực tế:
- Offline:
    1. Load document
    2. Chunk
    3. Embed
    4. Lưu vào vector DB
- Online:
    1. User hỏi
    2. Embed query
    3. Retrieve top-k chunks
    4. Inject vào prompt
    5. LLM trả lời
```
## Phân loại RAG
```bash
Cách 1: Phân loại theo retrieval (cách tìm tài liệu)
    1. Sparse retrieval
    2. Dense retrieval
    3. Hybrid retrieval
Cách 2: Phân loại theo kiến trúc RAG (pipeline)
    1. Naive RAG
    2. Advanced RAG
    3. Modular / Agentic RAG
```