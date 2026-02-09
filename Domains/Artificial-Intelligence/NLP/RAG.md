# RAG (Retrieval-Augmented Generation)
```bash
- “Tìm tài liệu trước → rồi mới trả lời”
- Thay vì:
    + AI trả lời dựa hoàn toàn vào trí nhớ
    + Thì RAG: AI đi tìm tài liệu liên quan, đọc nó, rồi trả lời dựa trên tài liệu đó
```
**Thành phần**
```bash
Người dùng hỏi
     ↓
[1] Chia tài liệu
     ↓
[2] Biến thành vector
     ↓
[3] Tìm đoạn liên quan
     ↓
[4] AI trả lời

- Chia tài liệu (Chunking): Tài liệu dài không đưa thẳng cho AI được. Phải chia nhỏ thành các đoạn:
    + 300 – 1000 chữ
    + Ví dụ:File PDF 100 trang→ chia thành 300 đoạn nhỏ
```