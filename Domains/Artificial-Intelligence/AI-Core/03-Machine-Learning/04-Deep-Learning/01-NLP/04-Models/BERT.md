- [Introduction](#introduction)
- [Practices](#practices)
  - [Demo Work flow BERT với Sentiment Classification (phân loại cảm xúc)](#demo-work-flow-bert-với-sentiment-classification-phân-loại-cảm-xúc)
- [Sentence Transformer (mô hình AI dùng để biến câu -\> vector số embedding)](#sentence-transformer-mô-hình-ai-dùng-để-biến-câu---vector-số-embedding)
- [BGE (dùng để chuyển văn bản thành các vector số)](#bge-dùng-để-chuyển-văn-bản-thành-các-vector-số)
- [train](#train)
- [xgb](#xgb)
- [E5](#e5)
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
# Sentence Transformer (mô hình AI dùng để biến câu -> vector số embedding)
```bash
Khác với BERT thông thường (trả về embedding của từng từ), Sentence Transformer được huấn luyện để tạo embedding cho cả câu, rất phù hợp cho:
  - Semantic Search (tìm kiếm theo ngữ nghĩa)
  - Chatbot
  - RAG (Retrieval-Augmented Generation)
  - Phát hiện câu trùng lặp
  - Phân cụm văn bản
  - Hệ thống gợi ý
```
# BGE (dùng để chuyển văn bản thành các vector số)
(BAAI General Embedding) là một mô hình tạo vector embedding do nhóm BAAI (Beijing Academy of Artificial Intelligence) phát triển. Nó được  sao cho những đoạn văn có ý nghĩa giống nhau sẽ có vector gần nhau trong không gian nhiều chiều.
Embedding là gì?

Giả sử có các câu:

"Tôi thích học AI."
"Tôi yêu trí tuệ nhân tạo."
"Hôm nay trời mưa."

Nếu dùng BGE để mã hóa:

"Tôi thích học AI."      -> [0.12, -0.45, 0.83, ...]
"Tôi yêu trí tuệ nhân tạo." -> [0.10, -0.47, 0.81, ...]
"Hôm nay trời mưa."      -> [-0.78, 0.51, -0.11, ...]

Hai câu đầu sẽ có vector rất gần nhau vì ý nghĩa tương tự, còn câu thứ ba sẽ ở rất xa.

BGE dùng để làm gì?
1. Semantic Search (Tìm kiếm theo ngữ nghĩa)

Đây là ứng dụng phổ biến nhất.

Ví dụ bạn có hàng nghìn tài liệu.

Người dùng hỏi:

"Làm sao train XGBoost?"

BGE sẽ biến:

câu hỏi
toàn bộ tài liệu

thành vector rồi tìm tài liệu có vector gần nhất.

Khác với tìm kiếm theo từ khóa:

Ví dụ:

Tài liệu:
"Hướng dẫn huấn luyện mô hình XGBoost"

Người hỏi:
"Cách train xgb"

Không có từ nào giống hệt nhau.

Keyword Search sẽ khó tìm.

Nhưng BGE hiểu rằng:

train
=
huấn luyện

xgb
=
XGBoost

nên vẫn tìm đúng.

2. RAG (Retrieval-Augmented Generation)

Đây là ứng dụng rất phổ biến khi xây chatbot AI.

Ví dụ:

Bạn có:

PDF
Word
Website
File txt

Muốn ChatGPT trả lời dựa trên dữ liệu đó.

Quy trình:

PDF
    ↓
chia nhỏ document

    ↓
BGE tạo embedding

    ↓
lưu vào Vector Database

    ↓
Người dùng hỏi

    ↓
BGE embedding câu hỏi

    ↓
tìm đoạn gần nhất

    ↓
LLM đọc đoạn đó

    ↓
trả lời

Nếu không có BGE, LLM sẽ không biết phải đọc đoạn nào trong hàng nghìn trang tài liệu.

3. Recommendation

Ví dụ Shopee.

Bạn xem:

Áo thun trắng

BGE sẽ tìm những sản phẩm có embedding gần:

Áo polo trắng

Áo cotton trắng

Áo basic trắng

Thay vì chỉ tìm đúng chữ.

4. Clustering

Có hàng triệu bình luận.

Muốn nhóm lại.

Ví dụ:

"Ship chậm"

"Giao hàng lâu"

"Vận chuyển quá chậm"

BGE sẽ tạo embedding gần nhau.

Sau đó thuật toán KMeans sẽ gom thành một nhóm.

5. Classification

Có thể dùng embedding làm đặc trưng (feature).

Ví dụ:

Email

↓

BGE

↓

Vector 1024 chiều

↓

Random Forest

↓

Spam / Không Spam
BGE hoạt động như thế nào?

Ví dụ câu:

Machine Learning rất thú vị

BGE sẽ đưa qua Transformer.

Sentence

↓

Tokenizer

↓

Transformer Encoder

↓

Embedding Layer

↓

Vector 1024 chiều

Ví dụ:

Machine Learning rất thú vị

↓

[0.35,
-0.19,
0.77,
...
0.28]

Mỗi số thể hiện một đặc trưng ngữ nghĩa mà mô hình đã học được.

BGE khác ChatGPT như thế nào?
BGE	ChatGPT
Tạo embedding	Sinh văn bản
Không trả lời câu hỏi	Có thể trả lời
Dùng để tìm kiếm	Dùng để hội thoại
Đầu ra là vector	Đầu ra là văn bản
Chạy rất nhanh	Chậm hơn do sinh từng token
Một số phiên bản BGE phổ biến
BGE-small: Nhanh, nhẹ, phù hợp máy cấu hình vừa phải.
BGE-base: Cân bằng giữa tốc độ và chất lượng.
BGE-large: Chính xác hơn nhưng tốn tài nguyên hơn.
BGE-M3: Hỗ trợ đa ngôn ngữ, nhiều chế độ truy hồi (dense, sparse, multi-vector), rất phù hợp cho các hệ thống tìm kiếm hiện đại.
Khi nào nên dùng BGE?

Bạn nên dùng BGE khi cần:

Tìm kiếm tài liệu theo ý nghĩa thay vì từ khóa.
Xây dựng chatbot hỏi đáp trên tài liệu (RAG).
Lưu trữ embedding trong các cơ sở dữ liệu vector như FAISS, ChromaDB, Milvus hoặc Pinecone.
Gợi ý nội dung hoặc sản phẩm tương tự.
Phân cụm hoặc phân loại văn bản dựa trên ngữ nghĩa.

Nếu bạn đang học AI/LLM, thì BGE thường xuất hiện trong pipeline:

Tài liệu
      ↓
Chia nhỏ (Chunking)
      ↓
BGE (Embedding)
      ↓
Vector Database
      ↓
Tìm kiếm (Retrieval)
      ↓
LLM (ChatGPT, Qwen, Llama...)
      ↓
Câu trả lời

Trong pipeline này, BGE không phải là mô hình trả lời câu hỏi. Vai trò của nó là biến văn bản và câu hỏi thành vector để tìm ra những đoạn tài liệu liên quan nhất, sau đó mới đưa các đoạn đó cho LLM tạo câu trả lời. Đây là nền tảng của hầu hết các hệ thống RAG hiện nay.
# E5 
là một họ mô hình embedding do Microsoft phát triển. Giống như BGE, E5  để máy tính có thể so sánh ý nghĩa của các đoạn văn bản.

Nói đơn giản:

BGE → mô hình embedding của BAAI.
E5 → mô hình embedding của Microsoft.

Cả hai đều được dùng cho các bài toán như tìm kiếm ngữ nghĩa, RAG, gợi ý nội dung và phân cụm văn bản.

E5 hoạt động như thế nào?

Ví dụ có ba câu:

"Tôi thích học AI."

"Tôi yêu trí tuệ nhân tạo."

"Hôm nay trời mưa."

Sau khi qua E5:

"Tôi thích học AI."
↓
[0.13, -0.22, ..., 0.41]

"Tôi yêu trí tuệ nhân tạo."
↓
[0.12, -0.24, ..., 0.39]

"Hôm nay trời mưa."
↓
[-0.81, 0.50, ..., -0.17]

Hai câu đầu sẽ có vector gần nhau vì mang ý nghĩa tương tự.

E5 dùng để làm gì?
1. Semantic Search

Ví dụ bạn có 100.000 tài liệu.

Người dùng hỏi:

How to train XGBoost?

E5 sẽ:

Câu hỏi
↓

Embedding

↓

Tìm vector gần nhất

↓

Tài liệu phù hợp

Không cần trùng từ khóa.

Ví dụ:

Question:
How to train XGBoost?

Document:
Guide for XGBoost model training

E5 vẫn hiểu hai câu này nói về cùng một chủ đề.

2. RAG

Đây là ứng dụng phổ biến nhất.

PDF

↓

Chunk

↓

E5

↓

Vector Database

↓

Question

↓

E5

↓

Nearest Chunks

↓

LLM

↓

Answer

E5 giúp tìm đúng đoạn tài liệu để LLM sử dụng khi trả lời.

3. Recommendation

Ví dụ:

Người xem

↓

Embedding

↓

Tìm embedding gần

↓

Gợi ý bài viết tương tự
4. Clustering

Có hàng triệu comment:

Ship chậm

Giao hàng lâu

Đợi cả tuần

Sau embedding:

Vector

↓

KMeans

↓

Nhóm "Vận chuyển"
5. Classification

Ví dụ:

Review

↓

Embedding

↓

Vector

↓

Classifier

↓

Positive / Negative

Embedding của E5 có thể làm đầu vào cho các mô hình học máy khác.

Điểm đặc biệt của E5

Khác với BGE, E5 được huấn luyện với tiền tố (prefix) để phân biệt loại văn bản.

Ví dụ:

query: How to train XGBoost?

passage: XGBoost is an ensemble learning algorithm...

Khi dùng E5, người ta thường thêm:

query: trước câu hỏi.
passage: trước tài liệu.

Ví dụ trong Python:

query = "query: How to train XGBoost?"

doc = "passage: XGBoost is a boosting algorithm..."

Điều này giúp E5 hiểu rõ vai trò của từng đoạn văn và thường cải thiện chất lượng tìm kiếm.

Các phiên bản E5

Một số phiên bản phổ biến:

e5-small: nhẹ, nhanh.
e5-base: cân bằng giữa tốc độ và chất lượng.
e5-large: chất lượng cao hơn nhưng cần nhiều tài nguyên.
multilingual-e5: hỗ trợ nhiều ngôn ngữ (bao gồm tiếng Việt) và thường được dùng trong các hệ thống đa ngôn ngữ.
So sánh E5 và BGE
Tiêu chí	E5	BGE
Nhà phát triển	Microsoft	BAAI
Loại mô hình	Embedding	Embedding
Cần prefix query:/passage:	Có (khuyến nghị)	Không bắt buộc
Hỗ trợ đa ngôn ngữ	Có (multilingual-e5)	Có (BGE-M3)
Ứng dụng	Search, RAG, Clustering, Recommendation	Search, RAG, Clustering, Recommendation
Khi nào nên dùng E5?

E5 là lựa chọn tốt khi bạn cần:

Xây dựng hệ thống tìm kiếm theo ngữ nghĩa.
Tạo chatbot RAG trên tài liệu.
Tìm kiếm đa ngôn ngữ.
Phân cụm hoặc phân loại văn bản.
Gợi ý tài liệu hoặc nội dung tương tự.

Nếu bạn đang học về LLM và RAG, thì E5 và BGE thường đóng cùng một vai trò: tạo embedding để truy xuất tài liệu, còn mô hình ngôn ngữ (như GPT, Qwen, Llama...) sẽ dùng các tài liệu đó để sinh ra câu trả lời. Việc chọn E5 hay BGE chủ yếu phụ thuộc vào yêu cầu về ngôn ngữ, hiệu năng và kết quả đánh giá trên bộ dữ liệu của bạn.