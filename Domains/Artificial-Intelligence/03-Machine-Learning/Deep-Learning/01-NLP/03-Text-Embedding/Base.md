- [Word2Vec](#word2vec)
  - [CBOW (Continuous Bag of Words)](#cbow-continuous-bag-of-words)
  - [Skip-Gram](#skip-gram)
- [Glove (Global Vectors)](#glove-global-vectors)
- [FastText](#fasttext)
  - [N-gram](#n-gram)
- [nomic-embed-text](#nomic-embed-text)
- [Practices](#practices)
  - [Demo Transformer Embedding](#demo-transformer-embedding)
---
# Word2Vec
```bash
Là kỹ thuật biến từ thành vector số (embedding).

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