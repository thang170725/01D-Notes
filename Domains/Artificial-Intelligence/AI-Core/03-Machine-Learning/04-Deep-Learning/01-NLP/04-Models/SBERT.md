- [Sentence-BERT Introduction (SBERT để tạo ra vector biểu diễn của cả câu (sentence embedding))](#sentence-bert-introduction-sbert-để-tạo-ra-vector-biểu-diễn-của-cả-câu-sentence-embedding)
---
# Sentence-BERT Introduction (SBERT để tạo ra vector biểu diễn của cả câu (sentence embedding))
[thư viện để sử dụng SBERT](../../../../../../../Tech-Stacks/Languages/Python/Libraries/NLP-Audio-Speech/NLP-Core/Transformers-Libs/Sentence_Transformers.md)
**Tại sao cần Sentence-BERT?**
```bash
Giả sử có hai câu:
    - "Tôi thích học Python."
    - "Tôi rất yêu lập trình Python."

Nếu dùng BERT gốc, để tính độ giống nhau giữa hai câu phải đưa cả hai câu vào cùng một lần suy luận (cross-encoder), rất chậm khi có nhiều câu.

SBERT chỉ cần:
    - Mã hóa từng câu thành vector.
    - So sánh hai vector bằng Cosine Similarity.
=> Điều này nhanh hơn rất nhiều.

Minh họa
"Tôi thích học Python"
        │
        ▼
      SBERT
        │
        ▼
[0.25, -0.61, 0.82, ...]

"Tôi rất yêu lập trình Python"
        │
        ▼
      SBERT
        │
        ▼
[0.28, -0.58, 0.80, ...]

Sau đó tính:
    Cosine Similarity(vector1, vector2)
        Ví dụ: 0.95 → Hai câu rất giống nhau.
```