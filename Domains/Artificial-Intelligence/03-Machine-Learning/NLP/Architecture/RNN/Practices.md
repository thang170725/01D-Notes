# Mô hình RNN
class RNNModel(nn.Module):
    def __init__(self):
        super(RNNModel, self).__init__()
        self.embedding = nn.Embedding(vocab_size, embedding_dim)
        self.rnn = nn.RNN(embedding_dim, hidden_dim, batch_first=True)
        self.fc = nn.Linear(hidden_dim, vocab_size)

    def forward(self, x):
        x = self.embedding(x)  # [batch, seq, embed_dim]
        out, _ = self.rnn(x)   # [batch, seq, hidden_dim]
        out = self.fc(out)     # [batch, seq, vocab_size]
        return out

model = RNNModel()
criterion = nn.CrossEntropyLoss()
optimizer = optim.Adam(model.parameters(), lr=0.01)

# Huấn luyện
for epoch in range(100):
    optimizer.zero_grad()
    output = model(input_seq)
    loss = criterion(output.view(-1, vocab_size), target_seq.view(-1))
    loss.backward()
    optimizer.step()
    if epoch % 10 == 0:
        print(f"Epoch {epoch}, Loss: {loss.item():.4f}")

# Dự đoán tiếp theo
with torch.no_grad():
    out = model(input_seq)
    predicted_idx = torch.argmax(out, dim=2).squeeze().tolist()
    predicted_chars = ''.join([idx2char[idx] for idx in predicted_idx])
    print("Dự đoán:", predicted_chars)

import torchimport torch.nn as nn
import torch.optim as optim

# Dữ liệu: mapping từ chữ cái sang số
chars = sorted(list(set("hello")))
char2idx = {ch: idx for idx, ch in enumerate(chars)}
idx2char = {idx: ch for ch, idx in char2idx.items()}

# Dữ liệu huấn luyện
seq = "hell"
target = "ello"

# Biến đổi thành tensor
input_seq = torch.tensor([char2idx[ch] for ch in seq])  # [h, e, l, l]
target_seq = torch.tensor([char2idx[ch] for ch in target])  # [e, l, l, o]

# Đưa về định dạng batch_size x seq_len
input_seq = input_seq.unsqueeze(0)
target_seq = target_seq.unsqueeze(0)

# Tham số mô hình
vocab_size = len(chars)
embedding_dim = 10
hidden_dim = 20

# Mô hình RNN
class RNNModel(nn.Module):
    def __init__(self):
        super(RNNModel, self).__init__()
        self.embedding = nn.Embedding(vocab_size, embedding_dim)
        self.rnn = nn.RNN(embedding_dim, hidden_dim, batch_first=True)
        self.fc = nn.Linear(hidden_dim, vocab_size)

    def forward(self, x):
        x = self.embedding(x)  # [batch, seq, embed_dim]
        out, _ = self.rnn(x)   # [batch, seq, hidden_dim]
        out = self.fc(out)     # [batch, seq, vocab_size]
        return out

model = RNNModel()
criterion = nn.CrossEntropyLoss()
optimizer = optim.Adam(model.parameters(), lr=0.01)

# Huấn luyện
for epoch in range(100):
    optimizer.zero_grad()
    output = model(input_seq)
    loss = criterion(output.view(-1, vocab_size), target_seq.view(-1))
    loss.backward()
    optimizer.step()
    if epoch % 10 == 0:
        print(f"Epoch {epoch}, Loss: {loss.item():.4f}")

# Dự đoán tiếp theo
with torch.no_grad():
    out = model(input_seq)
    predicted_idx = torch.argmax(out, dim=2).squeeze().tolist()
    predicted_chars = ''.join([idx2char[idx] for idx in predicted_idx])
    print("Dự đoán:", predicted_chars)
# Demo RNN
```python
import torch
import torch.nn as nn

class SimpleRNN:
    def __init__(self, input_dim=4, hidden_dim=3, output_dim=3):
        self.Wxh = nn.Parameter(torch.randn(input_dim, hidden_dim))
        self.Whh = nn.Parameter(torch.randn(hidden_dim, hidden_dim))
        self.bh  = nn.Parameter(torch.zeros(hidden_dim))

        self.Why = nn.Parameter(torch.randn(hidden_dim, output_dim))
        self.by  = nn.Parameter(torch.zeros(output_dim))

        self.parameters = [self.Wxh, self.Whh, self.bh, self.Why, self.by]
        self.loss_fn = nn.CrossEntropyLoss()

    def forward(self, X):
        h_t = torch.zeros(1, self.Whh.shape[0])  # batch=1
        for x_t in X:
            x_t = x_t.unsqueeze(0)
            h_t = torch.tanh(x_t @ self.Wxh + h_t @ self.Whh + self.bh)
        logits = h_t @ self.Why + self.by
        return logits  # shape: (1, output_dim)

    def train_step(self, X, y, lr=0.1):
        logits = self.forward(X)             # (1, output_dim)
        loss = self.loss_fn(logits, y)       # y: (batch_size,)
        loss.backward()

        with torch.no_grad():
            for p in self.parameters:
                p -= lr * p.grad
                p.grad.zero_()
        return loss.item()

# ================= DEMO =================
embedding = nn.Embedding(num_embeddings=10, embedding_dim=4)
inputs = torch.tensor([1,2,3])
X = embedding(inputs)  # shape: (seq_len, emb_dim)

y = torch.tensor([2])  # target class, not embedding

rnn = SimpleRNN(input_dim=4, hidden_dim=3, output_dim=3)

for epoch in range(100):
    X = embedding(inputs)  # tạo lại mỗi epoch
    loss = rnn.train_step(X, y)
    if epoch % 20 == 0:
        print(epoch, loss)
```