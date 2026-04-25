- [Introduction](#introduction)
- [Practices](#practices)
  - [Demo Work flow BERT với Sentiment Classification (phân loại cảm xúc)](#demo-work-flow-bert-với-sentiment-classification-phân-loại-cảm-xúc)
---
# Introduction
```bash
BERT (Bidirectional Encoder Representations from Transformers) là một mô hình ngôn ngữ do Google phát triển (2018), dùng để hiểu ngữ cảnh của câu theo cả hai chiều (trái → phải và phải → trái) và được xây dựng chỉ dùng phần encoder của transformer.
- BERT không tạo văn bản mới (như GPT), mà hiểu và biểu diễn ngữ nghĩa câu chữ. Nó được dùng như "bộ não ngôn ngữ" trong các bài toán hiểu ngôn ngữ tự nhiên (NLU).
- Nhiệm cụ của BERT:
    + BERT chỉ là một bộ biểu diễn ngữ nghĩa. BERT mã hóa câu hoặc từ thành vector chứa ngữ cảnh 2 chiều. 
    + Ví dụ với hai câu: "Tôi ăn no rồi", "Tôi đã no bụng" → BERT sẽ biến mỗi câu thành một vector 768 chiều (nếu dùng bert-base), và vì nghĩa tương tự → 2 vector gần nhau trong không gian embedding.
```
**Architecture**
```bash
Input Text (VD: "I love AI")
      ↓
Add Special Tokens
      ├─ [CLS] (đại diện toàn câu)
      └─ [SEP] (ngăn cách câu)
      ↓
Tokenization (WordPiece)
      ↓
Token IDs
      ↓
Embedding Layer
      ├─ Token Embedding
      ├─ Segment Embedding (câu A / câu B)
      └─ Positional Encoding
      ↓
(Tổng 3 embedding lại)
      ↓
┌──────────────────────────────────────────────────────────────────────────────┐
│ BERT Encoder Stack (L layers, vd: 12 hoặc 24)                                │
│                                                                              │
│  ├─ Multi-Head Self-Attention (Bidirectional)                                │
│  │     ├─ Q, K, V từ toàn bộ câu                                              │
│  │     └─ Attention giữa mọi token (trái + phải)                             │
│  │                                                                           │
│  ├─ Add & LayerNorm                                                         │
│  │                                                                           │
│  ├─ Feed Forward Network (FFN)                                               │
│  │     ├─ Linear (d → 4d)                                                    │
│  │     ├─ Activation (GELU)                                                  │
│  │     └─ Linear (4d → d)                                                    │
│  │                                                                           │
│  └─ Add & LayerNorm                                                         │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘
      ↓
Output: Vector cho từng token
      ↓
┌──────────────────────────────────────────────┐
│ Tùy theo task                               │
│                                              │
│  ├─ Classification → dùng vector [CLS]        │
│  ├─ NER → dùng từng token                    │
│  ├─ QA → span start/end                      │
│  └─ Similarity → pooling (mean / CLS)        │
└──────────────────────────────────────────────┘
      ↓
Loss Function
      ↓
Backpropagation
```
# Practices
## Demo Work flow BERT với Sentiment Classification (phân loại cảm xúc)
```bash
Bài toán: Xác định câu sau là tích cực hay tiêu cực

Input:
"The movie is not good"
```
```bash
Bước 1: Thêm special tokens
    [CLS] The movie is not good [SEP]
    [CLS] → đại diện toàn câu (dùng để phân loại)
    [SEP] → kết thúc câu
Bước 2: Tokenization (WordPiece)
    Giả sử: ["[CLS]", "the", "movie", "is", "not", "good", "[SEP]"]
Bước 3: Convert sang ID (giả định)
    [101, 1996, 3185, 2003, 2025, 2204, 102]
Bước 4: Embedding
    - Mỗi token → vector (ví dụ 768 chiều)
        "not"  → [0.2, -0.1, ..., 0.5]
        "good" → [0.6,  0.3, ..., -0.2]
    - Sau đó cộng thêm:
        + positional embedding
        + segment embedding
Bước 5: Đi qua các layer Encoder (12 layers)
    - Đây là chỗ quan trọng nhất
    - Self-Attention xảy ra
        Token "good" sẽ nhìn:
            good ← not (rất quan trọng)
            good ← movie
            good ← is
    - Giả sử attention weights: Token Attention tới "good"
        not	0.7 🔥
        movie	0.1
        is	0.1
        the	0.1
    - Insight:
        BERT hiểu rằng:
            "not good" ≠ "good"
        → vì "good" bị ảnh hưởng mạnh bởi "not"
Bước 6: Vector [CLS] (tóm tắt toàn câu)
    - Sau 12 layers: [CLS] → [0.3, -1.2, ..., 2.1]   (vector 768 chiều). Vector này đã encode:
        + "movie"
        + "good"
        + và quan trọng: "not good" = tiêu cực
Bước 7: Classification Layer
    - [CLS] → Linear → Softmax
    - Output (giả định):
        + Positive: 0.12
        + Negative: 0.88
    => KẾT QUẢ CUỐI CÙNG. Prediction: NEGATIVE

# Tại sao BERT đúng?
# Nếu không có attention:
# "good" → positive ❌
# Nhưng với BERT:
# "not" ảnh hưởng mạnh → đảo nghĩa → negative ✅
```