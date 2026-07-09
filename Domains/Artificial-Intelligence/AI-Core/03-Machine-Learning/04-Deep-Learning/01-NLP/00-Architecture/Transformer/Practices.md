# Demo Piple Transformer Simple
```python
import torch
import pandas as pd
from collections import Counter
import math

class TransformerV1:
    def __init__(self):
        self.df = None # dataframe chứa văn bản
        self.all_tokens = [] # danh sách toàn bộ token sau khi tách
        self.vocab = dict() # từ điển vocab: token -> id
        self.embedding_layer = None # lớp embedding
        self.pad_token = '<PAD>' # ký hiệu padding token

    def export_dataset(self):
        # dataset demo
        data = {
            'text': ['hà nội', 'hải phòng', 'ninh bình', 'hà ninh', 'bình định', 'hải dương']
        }

        self.df = pd.DataFrame(data)

    def embedding_first(self, text: str):
        # tách câu thành vector chứa các token
        return text.strip().split()

    # xây dựng từ điển vocab từ Dataframe văn bản
    def build_vocab_from_dataframe(self):
        for sentence in self.df['text']:
            tokens = self.embedding_first(sentence)
            self.all_tokens.extend(tokens)

        # đếm tần suất từng token
        token_counter = Counter(self.all_tokens)

        # gán id cho token: bắt đầu từ 1, để 0 dành cho <PAD>
        self.vocab = {self.pad_token: 0}
        for idx, (token, _) in  enumerate(token_counter.items(), start=1):
            self.vocab[token] = idx

        return self.vocab, len(self.vocab)
    
    def build_embedding_layer(self, embedding_dim=4, vocab_size=None):
        if vocab_size == None:
            vocab_size = len(self.vocab)

        self.embedding_layer = torch.nn.Embedding(num_embeddings=vocab_size, embedding_dim=embedding_dim)
        return self.embedding_layer
    
    def vectorize(self, text, max_len=None):
        # chuyển câu thành tensor embedding, thêm padding nếu cần

        tokens = self.embedding_first(text)
        token_ids = [self.vocab[token] for token in tokens]

        if max_len is not None:
            #thêm padding nếu chuỗi ngắn gọn hơn max_len
            while len(token_ids) < max_len:
                token_ids.append(self.vocab[self.pad_token])
            # Hoặc cắt bớt nếu dài hơn
            token_ids = token_ids[:max_len]

        input_tensor = torch.tensor(token_ids)
        embedding_vector = self.embedding_layer(input_tensor)
        return embedding_vector

    def positional_encoding(self, seq_len, d_model):
        pe = torch.zeros(seq_len, d_model)
        for pos in range(seq_len):
            for i in range(0, d_model, 2):
                pe[pos, i] = math.sin(pos / (10000 ** ((2 * i)/d_model)))
                if i + 1 < d_model:
                    pe[pos, i + 1] = math.cos(pos / (10000 ** ((2 * (i+1))/d_model)))
        return pe

class MultiHeadSelfAttention(torch.nn.Module):
    def __init__(self, d_model, num_heads):
        super().__init__()
        assert d_model % num_heads == 0, "d_model phải chia hết cho num_heads"

        self.d_model = d_model
        self.num_heads = num_heads
        self.d_k = d_model // num_heads

        # Linear projection cho Q, K, V
        self.W_q = torch.nn.Linear(d_model, d_model)
        self.W_k = torch.nn.Linear(d_model, d_model)
        self.W_v = torch.nn.Linear(d_model, d_model)

        # Linear output
        self.W_o = torch.nn.Linear(d_model, d_model)

    def forward(self, x):
        """
        x: Tensor [seq_len, d_model]
        """
        seq_len = x.size(0)

        # Step 1: Linear projections
        Q = self.W_q(x)  # [seq_len, d_model]
        K = self.W_k(x)
        V = self.W_v(x)

        # Step 2: Split thành multi-head
        # [seq_len, num_heads, d_k]
        Q = Q.view(seq_len, self.num_heads, self.d_k)
        K = K.view(seq_len, self.num_heads, self.d_k)
        V = V.view(seq_len, self.num_heads, self.d_k)

        # Step 3: Tính attention cho từng head
        # softmax((Q @ Kᵀ) / √d_k) @ V
        scores = torch.einsum('ihd,jhd->ijh', Q, K)  # [seq_len, seq_len, num_heads]
        scores /= math.sqrt(self.d_k)
        attn_weights = torch.nn.functional.softmax(scores, dim=1)

        out = torch.einsum('ijh,jhd->ihd', attn_weights, V)  # [seq_len, num_heads, d_k]

        # Step 4: Nối các head lại
        out = out.reshape(seq_len, self.d_model)  # [seq_len, d_model]

        # Step 5: Output linear layer
        output = self.W_o(out)  # [seq_len, d_model]

        return output

import torch.nn as nn

class AddNorm(nn.Module):
    def __init__(self, d_model, dropout=0.1):
        """
        d_model: kích thước vector đầu vào
        dropout: tỷ lệ dropout áp dụng lên sublayer output trước khi cộng residual
        """
        super().__init__()
        self.norm = nn.LayerNorm(d_model)
        self.dropout = nn.Dropout(dropout)

    def forward(self, x, sublayer_output):
        """
        x: Tensor gốc trước sublayer (residual)
        sublayer_output: Tensor đầu ra của sublayer (attention/ffn)
        """
        return self.norm(x + self.dropout(sublayer_output))

class PositionwiseFeedForward(nn.Module):
    def __init__(self, d_model, d_ff):
        """
        d_model: kích thước đầu vào và đầu ra
        d_ff: kích thước ẩn (thường d_ff = 4 * d_model)
        """
        super(PositionwiseFeedForward, self).__init__()
        self.linear1 = nn.Linear(d_model, d_ff)
        self.relu = nn.ReLU()
        self.linear2 = nn.Linear(d_ff, d_model)

    def forward(self, x):
        return self.linear2(self.relu(self.linear1(x)))

# DECODER
import torch
import torch.nn as nn
import math

class MaskedMultiHeadSelfAttention(nn.Module):
    def __init__(self, d_model, num_heads):
        super().__init__()
        assert d_model % num_heads == 0, "d_model phải chia hết cho num_heads"

        self.d_model = d_model
        self.num_heads = num_heads
        self.d_k = d_model // num_heads

        self.W_q = nn.Linear(d_model, d_model)
        self.W_k = nn.Linear(d_model, d_model)
        self.W_v = nn.Linear(d_model, d_model)
        self.W_o = nn.Linear(d_model, d_model)

    def forward(self, x):
        """
        x: Tensor [seq_len, d_model]
        """
        seq_len = x.size(0)

        # Projection
        Q = self.W_q(x)  # [seq_len, d_model]
        K = self.W_k(x)
        V = self.W_v(x)

        # Reshape để chia head
        Q = Q.view(seq_len, self.num_heads, self.d_k)
        K = K.view(seq_len, self.num_heads, self.d_k)
        V = V.view(seq_len, self.num_heads, self.d_k)

        # Tính attention scores
        scores = torch.einsum('ihd,jhd->ijh', Q, K)  # [seq_len, seq_len, num_heads]
        scores = scores / math.sqrt(self.d_k)

        # Tạo mask tam giác dưới [seq_len, seq_len]
        mask = torch.tril(torch.ones(seq_len, seq_len)) == 0  # True ở những vị trí cần che đi

        # Áp dụng mask: gán -inf cho các vị trí không được thấy
        scores = scores.masked_fill(mask.unsqueeze(-1), float('-inf'))

        # Softmax attention weights
        attn_weights = torch.softmax(scores, dim=1)  # softmax theo chiều j (key)

        # Attention output
        out = torch.einsum('ijh,jhd->ihd', attn_weights, V)  # [seq_len, num_heads, d_k]

        # Gộp các head lại
        out = out.reshape(seq_len, self.d_model)  # [seq_len, d_model]

        # Linear output
        output = self.W_o(out)  # [seq_len, d_model]

        return output

class EncoderDecoderAttention(nn.Module):
    def __init__(self, d_model, num_heads):
        super().__init__()
        assert d_model % num_heads == 0

        self.num_heads = num_heads
        self.d_k = d_model // num_heads

        self.W_q = nn.Linear(d_model, d_model)
        self.W_k = nn.Linear(d_model, d_model)
        self.W_v = nn.Linear(d_model, d_model)
        self.W_o = nn.Linear(d_model, d_model)

    def forward(self, query, key, value):
        """
        query: decoder input       [tgt_seq_len, d_model]
        key, value: encoder output [src_seq_len, d_model]
        """
        tgt_len = query.size(0)
        src_len = key.size(0)

        Q = self.W_q(query).view(tgt_len, self.num_heads, self.d_k)
        K = self.W_k(key).view(src_len, self.num_heads, self.d_k)
        V = self.W_v(value).view(src_len, self.num_heads, self.d_k)

        scores = torch.einsum('ihd,jhd->ijh', Q, K) / math.sqrt(self.d_k)  # [tgt_len, src_len, heads]
        attn_weights = torch.softmax(scores, dim=1)
        out = torch.einsum('ijh,jhd->ihd', attn_weights, V)  # [tgt_len, num_heads, d_k]
        out = out.reshape(tgt_len, self.num_heads * self.d_k)
        return self.W_o(out)
    
import torch
import torch.nn as nn

class DecoderOutputLayer(nn.Module):
    def __init__(self, d_model, vocab_size):
        super().__init__()
        self.linear = nn.Linear(d_model, vocab_size)
        self.softmax = nn.Softmax(dim=-1)  # chuẩn hóa theo chiều vocab

    def forward(self, x):
        """
        x: tensor đầu vào từ decoder, shape: [seq_len, d_model] hoặc [batch, seq_len, d_model]
        """
        logits = self.linear(x)        # shape: [seq_len, vocab_size] hoặc [batch, seq_len, vocab_size]
        probs = self.softmax(logits)   # xác suất trên toàn bộ vocab
        return probs

if __name__ == "__main__":
    model = TransformerV1()
    model.export_dataset()
    vocab, vocab_size = model.build_vocab_from_dataframe()

    print("Vocab:", vocab)

    embedding_layer = model.build_embedding_layer(embedding_dim=4)
    print("Initial embedding weights:\n", embedding_layer.weight)

    # Câu test
    sentence = "hà nội"
    max_len = 4  # độ dài cố định cho mọi input

    vectors = model.vectorize(sentence, max_len=max_len)
    print("Embedding vectors:\n", vectors)

    pos_enc = model.positional_encoding(seq_len=vectors.size(0), d_model=vectors.size(1))
    vectors += pos_enc
    print("Embedding + Positional Encoding:\n", vectors)
```