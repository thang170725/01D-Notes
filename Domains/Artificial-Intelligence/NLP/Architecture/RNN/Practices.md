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