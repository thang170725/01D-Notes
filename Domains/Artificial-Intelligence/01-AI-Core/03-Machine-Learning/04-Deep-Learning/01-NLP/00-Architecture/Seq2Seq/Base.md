- [Seq2Seq Introduction (mô hình nhận một chuỗi đầu vào và tạo ra một chuỗi khác đầu ra)](#seq2seq-introduction-mô-hình-nhận-một-chuỗi-đầu-vào-và-tạo-ra-một-chuỗi-khác-đầu-ra)
- [----- 1. Simple Seq2Seq model -----](#------1-simple-seq2seq-model------)
- [----- 2. Mini example -----](#------2-mini-example------)
---
# Seq2Seq Introduction (mô hình nhận một chuỗi đầu vào và tạo ra một chuỗi khác đầu ra)
```bash
Ứng dụng:
    - dịch câu → từ tiếng Việt sang tiếng Anh
    - tóm tắt văn bản
    - chatbot trả lời tin nhắn
    - biến dãy số → dãy số khác

Cấu trúc chuẩn gồm:
    - Encoder: đọc chuỗi đầu vào, nén thông tin thành vector ngữ cảnh.
    - Decoder: dùng vector đó để tạo chuỗi đầu ra từng bước một.
```
Bài tập
Biến chuỗi ký tự viết thường bằng chuỗi ký tự viết hoa
import torch
import torch.nn as nn

# ----- 1. Simple Seq2Seq model -----
class Encoder(nn.Module):
    def __init__(self, vocab, hidden):
        super().__init__()
        self.embed = nn.Embedding(vocab, hidden)
        self.rnn = nn.GRU(hidden, hidden)

    def forward(self, x):
        emb = self.embed(x)
        output, h = self.rnn(emb)
        return h  # context


class Decoder(nn.Module):
    def __init__(self, vocab, hidden):
        super().__init__()
        self.embed = nn.Embedding(vocab, hidden)
        self.rnn = nn.GRU(hidden, hidden)
        self.fc = nn.Linear(hidden, vocab)

    def forward(self, x, h):
        emb = self.embed(x)
        output, h = self.rnn(emb, h)
        return self.fc(output), h


class Seq2Seq(nn.Module):
    def __init__(self, enc, dec):
        super().__init__()
        self.enc = enc
        self.dec = dec

    def forward(self, src, trg):
        h = self.enc(src)
        outputs = []
        dec_in = trg[0].unsqueeze(0)   # start token
        for _ in range(1, trg.size(0)):
            out, h = self.dec(dec_in, h)
            outputs.append(out)
            dec_in = out.argmax(-1)   # greedy decode
        return torch.stack(outputs)

# ----- 2. Mini example -----
vocab = 30
hidden = 32
enc = Encoder(vocab, hidden)
dec = Decoder(vocab, hidden)
model = Seq2Seq(enc, dec)

src = torch.tensor([[1, 5, 8]])   # "a,b,c"
trg = torch.tensor([[2, 6, 9]])   # expected uppercase

out = model(src, trg)
print(out.shape)   # (seq_len-1, batch, vocab)