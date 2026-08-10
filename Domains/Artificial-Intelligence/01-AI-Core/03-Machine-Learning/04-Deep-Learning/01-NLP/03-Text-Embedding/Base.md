- [Embedding Introduction (vector ngữ nghĩa được học từ dữ liệu)](#embedding-introduction-vector-ngữ-nghĩa-được-học-từ-dữ-liệu)
- [Word2Vec (nhận token id của vocab -\> vector số embedding)](#word2vec-nhận-token-id-của-vocab---vector-số-embedding)
  - [CBOW (Continuous Bag of Words)](#cbow-continuous-bag-of-words)
  - [Skip-Gram](#skip-gram)
- [Glove (Global Vectors)](#glove-global-vectors)
- [FastText](#fasttext)
  - [N-gram](#n-gram)
- [nomic-embed-text](#nomic-embed-text)
- [OpenAI Embedding](#openai-embedding)
  - [Ask](#ask)
    - [OpenAI Embedding khác Hugging Face thế nào?](#openai-embedding-khác-hugging-face-thế-nào)
- [Practices](#practices)
  - [Demo Transformer Embedding](#demo-transformer-embedding)
---
# Embedding Introduction (vector ngữ nghĩa được học từ dữ liệu)
# Word2Vec (nhận token id của vocab -> vector số embedding)
```bash
Ý tưởng:
    Những từ xuất hiện trong ngữ cảnh giống nhau sẽ có vector gần nhau

Ví dụ:
    - Vua gần Hoàng hậu
    - Hà Nội gần TP.HCM

    Word2Vec học được:
        King - Man + Woman ≈ Queen

Dùng để:
    - Biểu diễn từ thành vector
    - Tìm từ đồng nghĩa
    - Làm input cho model NLP
```
## CBOW (Continuous Bag of Words)
```bash
Nhiệm vụ:
    Đoán từ ở giữa từ các từ xung quanh.

Ví dụ:
    Tôi ăn ___ vào buổi sáng

    Từ context:
        Tôi ăn ... vào buổi sáng
    Model đoán:
        phở

Dùng để train Word2Vec
```
## Skip-Gram 
```bash
Ngược với CBOW.

Nhiệm vụ:
    Dùng từ trung tâm để đoán các từ xung quanh.

Ví dụ:
    Tôi ăn phở vào buổi sáng

    Input:
        phở
    Output:
        ăn
        vào
        buổi
        sáng

Dùng để train Word2Vec.
```
# Glove (Global Vectors)
```bash
- Word2Vec:
    Nhìn từng câu
- GloVe:
    Nhìn toàn bộ thống kê corpus

Ví dụ đếm:
    King xuất hiện với Queen bao nhiêu lần

    Từ đó học embedding.

Dùng để:
    - Sinh word embedding
    - Từng rất phổ biến trước BERT
```
# FastText 
```bash
Do Meta AI phát triển.

Ý tưởng:
    Một từ được tạo từ nhiều n-gram ký tự.

Ví dụ:
    học
        Tách:
            <h
            họ
            ọc
            c>

Embedding từ: = tổng embedding các n-gram

Ưu điểm:
    - Hiểu từ hiếm
    - Hiểu từ chưa từng gặp (OOV)

Ví dụ:
    chatgptxyz

    Word2Vec:
        Không biết
    FastText:
        Đoán được nhờ các n-gram
```
## N-gram
```bash
Là chuỗi gồm N token liên tiếp.

Ví dụ:
    Câu: Tôi thích học NLP

Unigram (1-gram):
    Tôi
    thích
    học
    NLP

Bigram (2-gram):
    Tôi thích
    thích học
    học NLP

Trigram (3-gram):
    Tôi thích học
    thích học NLP

Dùng để:
    - Language Model cổ điển
    - FastText
    - Gợi ý từ tiếp theo
```
# nomic-embed-text
# OpenAI Embedding
```bash
OpenAI hiện cung cấp các embedding model như text-embedding-3-small và text-embedding-3-large.
```
## Ask
### OpenAI Embedding khác Hugging Face thế nào?
```bash
Hãy hình dung:

                 EMBEDDING
                     │
        ┌────────────┴────────────┐
        │                         │
     OpenAI                  Hugging Face
        │                         │
 text-embedding-3        BGE / E5 / GTE / ...
        │                         │
       API                    Local model
        │                         │
    Internet                GPU / CPU của bạn

Cả hai đều làm cùng một nhiệm vụ: Text → Vector Nhưng cách sử dụng khác nhau.
    OpenAI Embedding
        Ví dụ bạn dùng: text-embedding-3-small

        Kiến trúc ứng dụng:
            Your Python application
                    │
                    │ HTTPS API
                    ↓
            OpenAI Embedding API
                    │
                    ↓
            Embedding Model
                    │
                    ↓
            Vector
                    │
                    ↓
            Your application

        Bạn không tải model về máy.

        Bạn gửi:
            text = "Docker là gì?"

            OpenAI xử lý và trả về:
                [
                    0.012,
                    -0.034,
                    0.127,
                    ...
                ]

    Hugging Face Embedding
        Ở đây:
            model
              ↓
            được download về máy
              ↓
            CPU/GPU của bạn
              ↓
            text → vector

        Hugging Face cũng hỗ trợ inference qua API thay vì chạy local; tài liệu hiện tại cho phép gọi feature extraction qua InferenceClient.
```
Đúng, 5 nhóm bạn nêu — BAAI BGE, E5, Jina, GTE, Voyage — đều là những dòng embedding rất đáng biết nếu bạn đang xây Semantic Search / Hybrid Search / RAG cho AI Agent.

Điểm quan trọng là không có model nào "mạnh nhất mọi mặt". Mỗi dòng có triết lý hơi khác nhau.

1. Nhìn nhanh trước
Model	Điểm mạnh chính	Multilingual	Local	Phù hợp
BAAI BGE	Retrieval tổng quát, chất lượng tốt	⭐⭐⭐⭐	✅	RAG, semantic search
E5	Query ↔ document retrieval	⭐⭐⭐⭐⭐	✅	Search/RAG
Jina	Context dài, multilingual	⭐⭐⭐⭐⭐	✅/API	Tài liệu dài, RAG
GTE	General text embedding, hiệu năng tốt	⭐⭐⭐⭐	✅	RAG/search
Voyage	Chất lượng retrieval rất cao, API	⭐⭐⭐⭐⭐	❌*	Production RAG

* Voyage chủ yếu được dùng qua API thay vì tự chạy model như BGE/E5/GTE.

Nếu bạn đang tự build Personal AI Agent chạy local, mình sẽ ưu tiên:

BGE / E5 / Jina / GTE

Còn nếu chấp nhận cloud API:

Voyage

là một lựa chọn rất đáng cân nhắc.

2. BAAI BGE

BGE = Beijing Academy of Artificial Intelligence General Embedding.

Đây là một trong những dòng embedding open-source nổi tiếng nhất.

Ví dụ:

BAAI/bge-small-en-v1.5
BAAI/bge-base-en-v1.5
BAAI/bge-large-en-v1.5
BAAI/bge-m3

Trong đó BGE-M3 đặc biệt đáng chú ý nếu bạn làm multilingual RAG.

BGE mạnh ở đâu?
Semantic Search
      ↓
Document Retrieval
      ↓
RAG

Ví dụ:

Query:
"Tôi muốn biết cách train YOLO"

Document:
"Training a YOLO model requires preparing
the dataset and configuring the training parameters."

Dù không trùng hoàn toàn từ khóa, BGE có thể đưa document này lên cao vì ngữ nghĩa gần nhau.

BGE-M3

Nếu dữ liệu của bạn có:

Tiếng Việt
Tiếng Anh
Code
PDF
Documentation

thì BGE-M3 khá hấp dẫn.

3. E5

E5 là dòng embedding của Microsoft.

Một số model nổi tiếng:

intfloat/e5-base-v2
intfloat/e5-large-v2

intfloat/multilingual-e5-small
intfloat/multilingual-e5-base
intfloat/multilingual-e5-large

E5 rất nổi tiếng trong bài toán:

query ↔ passage retrieval

Ví dụ:

query:
"GPU nào chạy được model 30B?"

passage:
"Models with approximately 30 billion
parameters require substantial GPU memory..."

E5 được thiết kế khá rõ cho dạng quan hệ này.

Một đặc điểm cần nhớ

E5 thường sử dụng prefix:

query: ...

cho câu hỏi và:

passage: ...

cho tài liệu.

Ví dụ:

query = "query: GPU nào chạy được model 30B?"

document = "passage: Model 30B yêu cầu..."

Sau đó embedding.

Khi nào chọn E5?

Nếu hệ thống của bạn chủ yếu là:

User Query
      ↓
Search Documents
      ↓
RAG

thì E5 là lựa chọn rất hợp lý.

4. Jina

Jina AI có nhiều embedding model, đáng chú ý nhất là dòng:

Jina Embeddings

Điểm nổi bật của Jina là context dài và khả năng xử lý tài liệu dài.

Ví dụ:

PDF
│
├── 100 pages
├── technical documentation
├── manuals
└── research papers

Đây là tình huống Jina khá hấp dẫn.

Thay vì chỉ xử lý các chunk rất nhỏ:

500 tokens

các model context dài cho phép bạn có nhiều không gian hơn cho document.

Jina phù hợp với:
Technical documentation
PDF
Research papers
Long documents
Multilingual RAG

Nếu Personal Agent của bạn sau này phải đọc:

Documentation
PDF
Source code
Project specification
Meeting notes

thì Jina rất đáng thử.

5. GTE

GTE là dòng embedding của Alibaba/NLP ecosystem.

Một số model:

thenlper/gte-base
thenlper/gte-large

và các model GTE mới hơn trong hệ Qwen/GTE ecosystem.

GTE hướng tới general text embedding, tức không chỉ một task cụ thể.

Ví dụ:

Semantic Search
Classification
Clustering
Retrieval
RAG

Điểm mạnh của GTE là:

một lựa chọn local khá cân bằng giữa chất lượng và chi phí inference.

Nếu bạn muốn chạy embedding trên workstation của mình thay vì gọi API thì GTE đáng xem.

6. Voyage

Voyage khác một chút.

Thay vì tư duy:

Hugging Face
    ↓
download model
    ↓
GPU local

Voyage thường được dùng theo kiểu:

Your Agent
     ↓
HTTPS
     ↓
Voyage API
     ↓
Embedding
     ↓
Vector DB

Nó tập trung rất mạnh vào retrieval quality cho production.

Có các model dành cho:

general retrieval
multilingual retrieval
code retrieval
reranking

Đặc biệt nếu bạn làm:

Code RAG

thì các model embedding chuyên cho code rất đáng chú ý.

Ví dụ Agent của bạn hỏi:

"Hàm nào trong project chịu trách nhiệm load YOLO model?"

thì code embedding model có thể phù hợp hơn một embedding model text tổng quát.

7. Đây là điểm cực kỳ quan trọng: embedding model phải phù hợp dữ liệu

Không nên nghĩ:

"Model nào benchmark cao nhất thì dùng model đó."

Ví dụ Agent của bạn có:

                DATA
                  │
        ┌─────────┼──────────┐
        ↓         ↓          ↓
       PDF       TEXT       CODE
        │         │          │
        ↓         ↓          ↓
     Embedding  Embedding  Code Embedding

Nếu bạn hỏi:

"Hàm nào xử lý YOLO training?"

thì embedding dành cho code retrieval có thể tốt hơn embedding text tổng quát.

Nếu hỏi:

"Chính sách hoàn tiền là gì?"

thì text embedding là phù hợp.

8. Một điểm khác nhau rất quan trọng: model local vs API
BGE / E5 / GTE / một số Jina

Bạn có thể:

Hugging Face
     ↓
download
     ↓
local machine
     ↓
GPU/CPU

Ví dụ:

from sentence_transformers import SentenceTransformer

model = SentenceTransformer("BAAI/bge-m3")

embeddings = model.encode([
    "Tôi muốn hoàn tiền",
    "Khách hàng có thể yêu cầu refund"
])

Sau đó:

embeddings
      ↓
Vector DB
Voyage

Thường:

Your Agent
     ↓
HTTPS
     ↓
Voyage
     ↓
embedding

Không cần:

GPU
VRAM
model loading
quantization

Nhưng:

API cost
+
Internet dependency
+
data leaves your infrastructure
9. Nếu bạn xây Personal AI Agent của mình

Mình sẽ chia thành 3 loại dữ liệu:

                    PERSONAL DATA
                         │
             ┌───────────┼───────────┐
             ↓           ↓           ↓
            TEXT         PDF         CODE
             │           │           │
             ↓           ↓           ↓
           BGE/E5      Jina/BGE    Code Embedding

Sau đó:

                       Vector DB
                           │
                           ↓
                     Hybrid Search
                           │
             ┌─────────────┴─────────────┐
             ↓                           ↓
       Keyword Search              Semantic Search
             │                           │
             └─────────────┬─────────────┘
                           ↓
                         RRF
                           ↓
                       Reranker
                           ↓
                          LLM

Đây là kiến trúc rất phù hợp với Agent mà chúng ta đang nói từ đầu.

10. Nếu chỉ muốn chọn 1 model để bắt đầu

Mình sẽ chọn theo tình huống:

🇻🇳 Việt + Anh + tài liệu cá nhân

BGE-M3

⭐ multilingual
⭐ local
⭐ RAG
⭐ semantic search
⭐ phù hợp workstation
🌎 Multilingual retrieval

multilingual-E5

⭐ query/document retrieval
⭐ multilingual
⭐ local
📚 PDF / tài liệu dài

Jina Embeddings

⭐ long context
⭐ documents
⭐ RAG
💻 Code + technical project

Xem Jina/Voyage code-oriented embeddings hoặc các embedding model chuyên code.

☁️ Muốn chất lượng tốt và không muốn vận hành embedding server

Voyage API

Agent
 ↓
HTTPS
 ↓
Voyage
11. Và đừng nhầm Embedding Model với Reranker

Trong hệ thống RAG tốt, hai thứ này khác nhau:

Embedding Model
     ↓
"Trong 10.000 documents,
20 documents nào có vẻ liên quan?"

Sau đó:

Reranker
     ↓
"Trong 20 documents này,
5 documents nào thực sự trả lời được câu hỏi?"

Cho nên pipeline hoàn chỉnh có thể là:

Query
  ↓
Embedding
  ↓
Vector Search
  ↓
Top 50
  ↓
Keyword Search
  ↓
Hybrid/RRF
  ↓
Top 20
  ↓
Reranker
  ↓
Top 5
  ↓
LLM
  ↓
Answer

Đây mới là kiến trúc bạn nên hướng tới, thay vì chỉ đơn giản text → embedding → vector DB → LLM.

Nếu bạn muốn tự build trên PC như kiến trúc chúng ta vừa bàn, BGE-M3 + PostgreSQL/pgvector + BM25/full-text search + RRF + một reranker là một stack khởi đầu rất hợp lý.
# Practices
## Demo Transformer Embedding
```python
from typing import List, Dict, Tuple
from collections import Counter
import random as rnd
import torch
import math

class TransformerEmbedding:
    def __init__(self, vocab_size: int = 1000, d_model: int = 64, max_len: int = 32):
        self.vocab_size = vocab_size
        self.d_model = d_model
        self.max_len = max_len
        
        # Khởi tạo embedding matrix [vocab_size × d_model]
        # Đây là bảng tra cứu embedding của *toàn bộ từ vựng*
        self.embedding_matrix = torch.randn(vocab_size, d_model) * 0.01

    # =================================================================================
    # 1. Split sentence → tokens
    # =================================================================================
    def _split(self, sentence: str) -> List[str]:
        """
        Input:  "hello world NLP"
        Output: ["hello", "world", "NLP"]
        """
        return sentence.split()

    # =================================================================================
    # 2. Build vocabulary
    # =================================================================================
    def _counts_and_most(self, tokens: List[str], vocab_size: int) -> Dict[str, int]:
        """
        Input: tokens = ["hello","hello","world"], vocab_size=5
        Output: {"hello":0, "world":1, "<unk>":2}
        """
        counter = Counter(tokens)
        most = counter.most_common(vocab_size - 1)

        vocab = {tok: idx for idx, (tok, _) in enumerate(most)}
        vocab["<unk>"] = len(vocab)
        return vocab

    # =================================================================================
    # 3. Convert tokens → token_ids
    # =================================================================================
    def _token_id(self, text: str, vocab: Dict[str, int]) -> List[int]:
        """
        Input: "hello NLP"
        Output: [0, 2] nếu "hello":0 và "NLP":2 là <unk>
        """
        tokens = self._split(text)
        unk_id = vocab["<unk>"]
        return [vocab.get(tok, unk_id) for tok in tokens]

    # =================================================================================
    # 4. Padding sequences to max_len
    # =================================================================================
    def _padding_sequence(self, seqs: List[List[int]], max_len: int = 4) -> List[List[int]]:
        """
        Input: [[1,2,3], [4]]
        Output: [[1,2,3,0], [4,0,0,0]]
        """
        out = []
        for seq in seqs:
            if len(seq) < max_len:
                padded = seq + [0] * (max_len - len(seq))
            else:
                padded = seq[:max_len]
            out.append(padded)
        return out

    # =================================================================================
    # 5. Create attention mask
    # =================================================================================
    def _attention_mask(self, padded_seq: List[int]) -> List[int]:
        """
        Input: [1,2,0,0]
        Output: [1,1,0,0]
        """
        return [1 if x != 0 else 0 for x in padded_seq]

    # =================================================================================
    # 6. Random embedding matrix (chỉ dùng khi demo)
    # =================================================================================
    def _random_embedding(self, vocab_size: int, d_model: int) -> List[List[float]]:
        """
        Tạo embedding ngẫu nhiên để demo.
        """
        out = []
        for _ in range(vocab_size):
            r = [rnd.uniform(-0.1, 0.1) for _ in range(d_model)]
            out.append(r)
        return out

    # =================================================================================
    # 7. Lookup embedding for 1 token_id
    # =================================================================================
    def _lookup_embedding_for_one(self, token_id: int, embedding_matrix) -> List[float]:
        """
        Input: token_id=5
        Output: vectơ 1×d_model
        """
        return embedding_matrix[token_id]

    # =================================================================================
    # 8. Lookup embedding for a list of token_ids
    # =================================================================================
    def _lookup_embedding(self, token_ids: List[int], embedding_matrix) -> torch.Tensor:
        """
        Input: [2,5,9]
        Output: tensor (3 × d_model)
        """
        return torch.tensor([embedding_matrix[t] for t in token_ids], dtype=torch.float32)

    # =================================================================================
    # 9. Embed whole batch → vectorized (không for)
    # =================================================================================
    def _embedding_batch(self, batch: List[List[int]], embedding_matrix: torch.Tensor) -> torch.Tensor:
        """
        Input: [[1,2],[3,4]]
        Output: (batch_size=2, seq_len=2, d_model)
        """
        batch_tensor = torch.tensor(batch)            # (B, L)
        return embedding_matrix[batch_tensor]         # PyTorch tự broadcast → (B, L, D)

    # =================================================================================
    # 10. Positional Encoding (sin/cos)
    # =================================================================================
    def _positional_encoding(self, seq_len: int, d_model: int) -> torch.Tensor:
        """
        Output: (seq_len × d_model) matrix
        """
        position = torch.arange(seq_len).unsqueeze(1)  # (L,1)
        div_term = torch.exp(torch.arange(0, d_model, 2) * (-math.log(10000.0) / d_model))

        pe = torch.zeros(seq_len, d_model)
        pe[:, 0::2] = torch.sin(position * div_term)
        pe[:, 1::2] = torch.cos(position * div_term)
        return pe

    # =================================================================================
    # 11. Full Transformer Embedding = token embedding + positional encoding
    # =================================================================================
    def transformer_embedding(self, batch_token_ids: List[List[int]]) -> torch.Tensor:
        """
        Input: batch token IDs
        Output: (B, L, d_model) embedding sử dụng trong Transformer Encoder
        """

        # Step 1: padding
        padded = self._padding_sequence(batch_token_ids, self.max_len)  # (B, L)

        # Step 2: embed batch
        batch_emb = self._embedding_batch(padded, self.embedding_matrix)   # (B, L, D)

        # Step 3: positional encoding
        pe = self._positional_encoding(self.max_len, self.d_model)         # (L, D)

        # Step 4: add PE vào embedding (broadcast)
        final = batch_emb + pe                                             # (B, L, D)

        return final                   # embedding chính xác như trong Transformer


# ===============================================================================
# Demo chạy thử
# ===============================================================================
if __name__ == "__main__":
    te = TransformerEmbedding(vocab_size=10, d_model=8, max_len=4)

    # Demo batch token_ids
    batch = [
        [1, 2],
        [3, 4, 5]
    ]

    final_emb = te.transformer_embedding(batch)

    print("Transformer Embedding Output Shape:", final_emb.shape)
    print(final_emb)
```