Seq2Seq (Sequence-to-Sequence)
    • Là mô hình nhận một chuỗi đầu vào và tạo ra một chuỗi khác đầu ra.
    • Kiểu như:
        ◦ dịch câu → từ tiếng Việt sang tiếng Anh
        ◦ tóm tắt văn bản
        ◦ chatbot trả lời tin nhắn
        ◦ biến dãy số → dãy số khác

    • Cấu trúc chuẩn gồm:
        ◦ Encoder: đọc chuỗi đầu vào, nén thông tin thành vector ngữ cảnh.
        ◦ Decoder: dùng vector đó để tạo chuỗi đầu ra từng bước một.
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

Ví dụ:
F(x) = x2
Tại x = 2, đạo hàm bằng 4
Ý nghĩa: Nếu bạn tăng x lên một chút, thì fx tăng khoảng 4 lần so với thay đổi đó. Nói cách khác đạo hàm là cách đo độ dốc của một đường cong tại một điểm.
Ví dụ:
Vị trị s(t) của xe tại thời điểm t thì đạo hàm của nó chính là vận tốc.
Nếu bạn biết vị trí thay đổi theo thời gian như thế nào, thì đạo hàm cho bạn biết xe đang chạy nhanh hay chậm, đang tăng tốc hay giảm tốc.
Công thức:



Xử lý dữ liệu
Chuẩn hóa dữ liệu
Chuẩn hóa về [0,1]
Công thức:
Result = (x-min(x) / (max(x) - min(x))
Cho mảng arr = np.array([5, 10, 15, 20, 25]). Hãy chuẩn hóa các giá trị này về đoạn [0, 1] chỉ bằng numpy.
import numpy as np

arr = np.array([5, 10, 15, 20, 25], dtype=float)
res = (arr - arr.min()) / (arr.max() - arr.min())

print(res) # [0.   0.25 0.5  0.75 1.  ]


Vector hóa văn bản
One-Hot
Tạo ra một cột cho mỗi giá trị và đánh 1 tại vị trí đúng, 0 ở vị trí khác
Loss Function (Hàm mất mát) & cost function (Hàm chi phí)


Categorical Cross-Entropy
Dùng cho phân loại nhiều nhãn
Công thức:
L = -(yi.log(y_predi) + … + )
Lỗi thường gặp & Giải pháp & Đánh giá mô hình
Accuracy
Accuracy (độ chính xác) được dùng để đánh giá độ đúng của mô hình phân loại. Nó cho biết mô hình dự đoán đúng bao nhiêu phần trăm so với toàn bộ dữ liệu.
    • Dùng cho: phân loại nhị phân, đa lớp (classification).
    • Không dùng tốt khi dữ liệu mất cân bằng (VD: 95 mẫu âm, 5 mẫu dương → đoán tất cả là âm sẽ đạt 95% accuracy nhưng vô dụng).
Công thức:
Accuracy = Số dự đoán đúng / Tổng số dự đoán
Hoặc với confusion matrix:
Accuracy=TP+TN+FP+FNTP+TN​ 
Trong đó:
    • TP: dự đoán đúng lớp dương
    • TN: dự đoán đúng lớp âm
    • FP: dự đoán sai (dự đoán dương nhưng thực tế âm)
    • FN: dự đoán sai (dự đoán âm nhưng thực tế dương)
Cú pháp:
y_true = [1, 0, 1, 1, 0]
y_pred = [1, 0, 0, 1, 1]

accuracy = sum(t == p for t, p in zip(y_true, y_pred)) / len(y_true)
print("Accuracy =", accuracy)

F1
Overfitting & Underfitting
Overfitting xảy ra khi mô hình học quá kỹ dữ liệu huấn luyện -> mất khả năng tổng quát với dữ liệu mới. Biểu hiện là accuracy trên tập huấn luyện rất cao còn trên tập test lại thấp.
Cách xử lý:
    • Thêm dữ liệu huấn luyện
    • Giảm độ phức tạp của mô hình
    • Regularization - phạt mô hình quá phức tạp
    • Early stopping cho mạng nơ ron
    • Dropout cho deep learning
    • Cross-validation (đánh giá mô hình nhiều lần với nhiều cách chia tập train/test khác nhau để tránh ăn may.
Underfitting xảy ra khi mô hình quá đơn giản hoặc thiếu dữ liệu, không thể học ra quy luật dẫn đến hiệu suất kém.

Vanishing Gradient (Gradient biến mất) & Exploding Gradient (Gradient bùng nổ)

Vanishing
Exploding

Khi huấn luyên bằng backpropagation, đạo hàm (gradient) giảm rất nhỏ qua từng lớp. Dẫn đến các lớp đầu (gần input) gần như không học được gì → Mạng hội tụ rất chậm hoặc không học được gì. Đặc biệt nghiêm trọng trong RNN do lan truyền qua nhiều bước thời gian (time steps). loss giảm chậm. 
Đạo hàm (gradient) qua từng lớp bị nhân lên quá lớn. => Dẫn đến việc cập nhật trọng số quá mạnh, mô hình không ổn định, có thể NaN.học
loss tăng vọt, nổ NaN, model không ổn định
Giải pháp
Dùng ReLu thay cho sigmoid/tanh
dùng batch Normalization
Dùng kiến trúc LSTM/GRU thay cho RNN thường
Khởi động trọng số dúng cách.
Gradient clipping: giới hạn giá trị gradient.
chọn learning rate vừa phải
khởi tạo trọng số cẩn thận
L1 & L2 regularization
Là một kỹ thuật thêm một hình phạt vào hàm mất mát để làm mô hình đơn giản hơn, tránh học quá kỹ dữ liệu huấn luyện (overfitting)
L1
L2
Giống như ép các trọng số về đúng không, chỉ giữ lại đặc trưng thật sự quan trọng.
Dùng khi muốn chọn lọc đặc trưng tự động (ví dụ mô hình có quá nhiều đặc trưng).
Giảm nhẹ tất cả trọng số, giúp mô hình ổn định hơn, tránh quá nhạy.
Dùng khi muốn giảm độ phức tạp chung của mô hình mà vẫn giữ lại toàn bộ đặc trưng.
Precision & recall
Precision
recall
Là độ chính xác của positive
precision = TP / (TP + FP) => trong số các dự đoán là positive (tích cực) có bao nhiêu cái đúng thật.
precision cao nghĩa là ít cảnh báo sai. Dùng khi chi phí của dự đoán sai là cao.
Nếu tăng Precision => dễ giảm recall (mô hình dè dặt hơn khi dự đoán positive)
Recall = TP / (TP + FN) => trong số các trường hợp thật sự là positive, mô hình bắt được bao nhiêu
Recall cao nghĩa là ít bị bỏ sót
Dùng khi cần bắt hết các trường hợp dương tính
Nếu tăng Recall => dễ gaimr Precision (mô hình mạnh tay dự đoán Positive nhưng dễ sai hơn)
Ví dụ: Hệ thống kiểm tra ung thư
Nếu precision cao tức hạn chế cảnh báo nhầm tới người khỏe mạnh còn recall cao sẽ hạn chế bỏ sót bệnh nhân thật sự. 
Nên sử dụng F1-Score (2x(PrecisionxRecall)/(Precision+Recall) => thích hợp khi cần cân bằng giữa Precision và recall
Xử lý token sau khi tách
Stopwords removal
    • Ý tưởng: danh sách các từ “không mang nhiều ý nghĩa” như “và”, “là”, “the”, “a” — thường loại bỏ trước khi xử lý để giảm noise và kích thước feature.
    • Tiền xử lý — giảm kích thước bộ từ và tăng chất lượng feature cho TF/Count.
    • Lưu ý: với một số tác vụ (ví dụ sentiment, questions), stopwords có thể mang thông tin (ví dụ “not” cực kỳ quan trọng) → cẩn thận khi loại.
Stemming
    • Ý tưởng: Cắt đuôi từ để đưa về dạng gốc thô bằng cách dùng rule cứng (heuristics). Không quan tâm ngữ pháp. Không đảm bảo trả về từ có nghĩa.
    • Cách làm: cắt suffix kiểu “ing”, “ed”, “ly”, “s”, …
    • Dùng để làm gì: giảm số lượng dạng của từ, đơn giản hoá văn bản để dùng cho TF-IDF, bag-of-words, search,…
Lemmatization
    • Ý tưởng: đưa từ về dạng nguyên mẫu có nghĩa (lemma) dựa trên từ điển + phân tích ngữ pháp. Dùng mô hình ngôn ngữ / từ điển. Trả về từ hợp lệ của ngôn ngữ. Hiểu ngữ cảnh của từ trong câu.
    • xử lý NLP có yêu cầu ngữ nghĩa tốt hơn information extraction, question answering, machine translation

sentence segmentation
Embedding & Vector Representation
CBOW
Skip-gram
Glove
Transformer embedding
Luồng hoạt động:
raw text → token → token_id → padding → attention mask → embedding lookup → positional encoding → final transformer embedding

Positional Encoding
    • Với câu “tôi ăn cơm” Token embedding của Transformer không biết 3 từ này đang ở vị trí 1–2–3 hay 3–2–1, vì attention không có tính tuần tự như RNN. Ta phải cộng thêm 1 vectơ đại diện cho “vị trí số mấy trong câu” → Đó là positional encoding.
    • Ví dụ:
        1. Token IDs: 
           [1, 2, 3, 4]
        2. Lookup embedding → mỗi token thành vector 3 chiều
           token embeddings = [
               [1, 2, 3],      # token 1
               [4, 5, 6],      # token 2
               [7, 8, 9],      # token 3
               [10,11,12]      # token 4
           ]
           → Đây là Embedding → học được ý nghĩa của từ.
        3. Positional Encoding (PE):
           PE = [
               [0,    0,    0   ],   # vị trí 0
               [1,    1,    1   ],   # vị trí 1
               [2,    2,    2   ],   # vị trí 2
               [3,    3,    3   ],   # vị trí 3
           ]
        4. Cộng embedding + positional encoding theo từng vị trí
           [
               [1,  2,  3 ],
               [5,  6,  7 ],
               [9, 10, 11 ],
               [13,14, 15 ]
           ]

Công thức:
Với vị trí pos và chiều vector I
    • PE(pos, 2i) = sin(pos/10000**(2i/d))
    • PE(pos, 2i+1) = cos(pos/10000**(2i/d)
Tức là token ở vị trí 0,1,2,3,… sẽ có vector chứa sin/cos có tần số khác nhau. Mỗi chiều dùng tần số khác nhau → mô hình phân biệt được vị trí.
Công thức nâng cao chunt Hugging Face:
    • a**b = e**(b.ln(a)) → 10000**(2i/d) = e**(ln(10000) . (2i/d))
Ví dụ:
Giả sử embedding size = 4 (d = 4)
Vị trí token = 2
Ta tính:
Với i = 0:
    • chiều 0 (even): PE(2,0)=sin⁡(2 / (10000**(0/4))=sin⁡(2)=0.9093
    • chiều 1 (odd): PE(2,1)=cos⁡(2 / (10000**(0/4))=cos⁡(2)=−0.4161
Với i = 1:
    • chiều 2 (even): PE(2,2)=sin⁡(2/100001/4)≈sin⁡(2/10)=sin⁡(0.2)=0.1987
    • chiều 3 (odd): PE(2,3)=cos⁡(2/100001/4)=cos⁡(0.2)=0.9801
Positional embedding cho vị trí 2: [ 0.9093,  -0.4161,  0.1987,  0.9801 ]
Cú pháp:
import torch
import math

def positional_encoding(seq_len, d_model):
    PE = torch.zeros(seq_len, d_model)
    
    for pos in range(seq_len):
        for i in range(d_model):
            angle = pos / (10000 ** (2 * (i // 2) / d_model))
            if i % 2 == 0:
                PE[pos, i] = math.sin(angle)
            else:
                PE[pos, i] = math.cos(angle)

    return PE


pe = positional_encoding(seq_len=5, d_model=8)
print(pe)
tensor([
 [0.0000, 1.0000, 0.0000, 1.0000, ...],  # pos=0
 [0.8415, 0.5403, 0.0100, 1.0000, ...],  # pos=1
 [0.9093,-0.4161, 0.0200, 0.9998, ...],  # pos=2
 ...
])
def positional_encoding_fast(seq_len, d_model):
    position = torch.arange(seq_len).unsqueeze(1)
    div_term = torch.exp(torch.arange(0, d_model, 2) * (-math.log(10000.0) / d_model))

    PE = torch.zeros(seq_len, d_model)
    PE[:, 0::2] = torch.sin(position * div_term)
    PE[:, 1::2] = torch.cos(position * div_term)
    return PE

PhoBERT
RNN (Recurrent Neural Network)
    • Là một loại mạng neural dùng để xử lý dữ liệu tuần tự (sequential data). RNN hoạt động dựa trên ý tưởng: thông tin ở bước t−1 sẽ được kết hợp với đầu vào ở bước t để tạo ra trạng thái mới.
    • Thay vì xử lý từng input một cách độc lập như MLP (Multilayer Perceptron), RNN giữ lại trạng thái (state) từ bước trước đó và sử dụng nó để xử lý input hiện tại. Điều này rất phù hợp với: Chuỗi văn bản, Dữ liệu thời gian (time series), Chuỗi tín hiệu âm thanh, video…
    • Có một khái niệm quan trong là hidden state (trí nhớ tạm thời của RNN tại thời điểm đó).
    • Ý tưởng: Mỗi bước thơi gian lấy input + trạng thái cũ → tạo trạng thái mới
    • Vấn đề: 
        ◦ RNN quên rất nhanh.
        ◦ Không nhớ được thông tin xa.
        ◦ Bị vanishing gradient khi chuỗi dài.
        ◦ Bạn đọc câu: "Tôi ăn cơm lúc 7h sáng, và đến chiều thì tôi đói." RNN có thể không nhớ phần trước (7h sáng) vì quá xa → mất ngữ cảnh → RNN phù hợp với chuỗi ngắn, hoặc tác vụ đơn giản.
BPTT (Backpropagation Through Time)
    • Đây là kỹ thuật tính gradient cho RNN. Vì RNN có trạng thái ẩn h_t phụ thuộc vào tất cả các h_(t-1), h_(t-2), …, nên backprop bình thường không đủ, ta phải "trải graph ra theo thời gian" và tính gradient qua từng step.
    • Về cơ bản: BPTT là backpropagation chuẩn, nhưng áp dụng lên graph được unfold theo time steps.
    • Công thức: dL/dW = sum((dL/dh_t) . (dh_t/dW))
Cú pháp:
# Forward RNN qua seq_len steps
h = torch.zeros(batch, hidden_dim)
for t in range(seq_len):
    h = torch.tanh(X[:, t, :] @ Wxh + h @ Whh + bh)

# Loss dựa trên h cuối
loss = cross_entropy(h @ Why + by, y)

# BPTT
loss.backward()  # PyTorch tự lan truyền qua tất cả h_t
Bài tập
Demo RNN bằng torch
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

LSTM (Long Short-Term Memory)
    • Để giải quyết việc mất trí nhớ của RNN, LSTM tách biệt hoàn toàn hai khái niệm: Hidden State (trạng thái ẩn) và Cell State (trạng thái ô - đóng vai trò như một đường băng chuyền thông tin xuyên suốt). Thêm cấu trúc “cổng” (gate) và có cell state giúp duy trì thông tin dài hạn.
    • Cơ chế 3 Cổng (Gates): Hãy tưởng tượng Cell State là một băng tải chạy dọc từ đầu đến cuối chuỗi. Các cổng sẽ quyết định cái gì được đặt lên hoặc nhấc ra khỏi băng tải đó:
        ◦ Forget Gate (Cổng quên): "Chúng ta nên bỏ bớt cái gì cũ không?"
            ▪ Nó nhận đầu vào xt​ và ht−1​, đi qua hàm Sigmoid (cho ra giá trị từ 0 đến 1).
            ▪ Nếu là 0: Xóa bỏ hoàn toàn thông tin cũ. Nếu là 1: Giữ lại toàn bộ.
        ◦ Input Gate (Cổng vào): "Có thông tin mới nào đáng giá để lưu lại không?"
            ▪ Gồm 2 phần: Một hàm Sigmoid quyết định cập nhật cái gì và một hàm tanh tạo ra một vector giá trị mới tiềm năng để đưa vào Cell State.
        ◦ Output Gate (Cổng ra): "Từ những gì đang có, chúng ta nên xuất bản cái gì ra ngoài?"
            ▪ Nó quyết định giá trị nào trong Cell State sẽ được dùng để tạo ra Hidden State (ht​) cho bước tiếp theo. LSTM có 3 cổng: Forget - Input – Output
    • Ưu điểm: Nhớ được thông tin xa hơn, Giảm vanishing gradient, Ổn định hơn khi xử lý văn bản dài
GRU (Gated Recurrent Unit)
    • GRU (Gated Recurrent Unit) là một phiên bản "tối giản" của LSTM. Nó ra đời sau (vào năm 2014) với mục tiêu làm cho mạng nơ-ron hồi tiếp chạy nhanh hơn và tốn ít bộ nhớ hơn nhưng vẫn giữ được khả năng "nhớ lâu" của LSTM.
    • 3 sự thay đổi lớn so với LSTM:
        1. Hợp nhất hai trạng thái thành một: Trong khi LSTM tách biệt Cell State (Ct​ - trí nhớ dài hạn) và Hidden State (ht​ - trí nhớ ngắn hạn), thì GRU gộp chúng lại làm một. GRU chỉ dùng duy nhất Hidden State (ht​) để truyền tải thông tin xuyên suốt qua các bước thời gian. Điều này giúp cấu trúc của nó gọn nhẹ hơn hẳn.
        2. Cơ chế 2 Cổng (Gates) thay vì 3: GRU không dùng "Cổng quên" riêng biệt và "Cổng vào" riêng biệt. Thay vào đó, nó dùng: Update Gate (Cổng cập nhật): Đây là sự kết hợp giữa Cổng quên và Cổng vào của LSTM. Nó quyết định xem bao nhiêu phần trăm thông tin cũ từ quá khứ cần giữ lại, và bao nhiêu phần trăm thông tin mới sẽ được nạp vào. Ví dụ: Nếu giá trị cổng là 0.7, nó có thể hiểu là giữ 70% cũ và nạp thêm 30% mới.
    • Reset Gate (Cổng đặt lại): Cổng này quyết định xem nên "quên" bao nhiêu thông tin từ trạng thái ẩn trước đó để tính toán thông tin mới (candidate state). Nó giúp mô hình loại bỏ những thông tin không còn liên quan đến ngữ cảnh hiện tại.
Transformer
Positional encoding
Giúp mô hình biết vị trí từ trong câu, vì cơ chế Attention không tự biết thứ tự
Công thức:
    • PEpos,2i = sin(pos/10000^(2i/dmodel))
    • PEpos,2i+1 = cos(pos/10000(2i/dmodel))
        ◦ pos: vị trí từ trong câu
        ◦ i: chỉ số chiều embedding
        ◦ d_model: chiều embedding (thường 512, 768…)
Bài tập
Demo về positional encoding
import torch
import torch.nn.functional as F
import matplotlib.pyplot as plt
import math

# Câu demo: 5 từ
words = ["Tôi", "yêu", "học", "máy", "."]
seq_len = len(words)
d_model = 8  # embedding nhỏ để minh họa

# Token embedding giả (random)
torch.manual_seed(0)
token_embeddings = torch.rand(seq_len, d_model)

# Hàm Positional Encoding
def positional_encoding(max_len, d_model):
    pe = torch.zeros(max_len, d_model)
    for pos in range(max_len):
        for i in range(0, d_model, 2):
            pe[pos, i] = math.sin(pos / (10000 ** ((2*i)/d_model)))
            if i+1 < d_model:
                pe[pos, i+1] = math.cos(pos / (10000 ** ((2*i)/d_model)))
    return pe

pe = positional_encoding(seq_len, d_model)

# Cộng token embedding + PE
x = token_embeddings + pe
print("Embedding + Positional Encoding:\n", x)
Self-Attention
    • Attention (đặc biệt là Self-Attention) chính là "linh hồn" giúp Transformer hiểu được ngữ cảnh mà không cần xử lý tuần tự từng từ như RNN hay LSTM.
    • Nếu RNN/LSTM giống như việc bạn đọc một cuốn sách từ trái sang phải và cố gắng nhớ những gì đã qua, thì Attention giống như việc bạn nhìn vào một từ và ngay lập tức "liếc" sang tất cả các từ khác trong câu để hiểu nghĩa của nó.
1. Tại sao Attention lại "thắng" RNN/LSTM?

Trong RNN/LSTM, thông tin phải đi qua một "nút thắt cổ chai" (vector trạng thái ẩn). Nếu câu quá dài, thông tin từ đầu câu sẽ bị mờ nhạt dần khi đến cuối câu.

Attention giải quyết bằng cách: Cho phép mỗi từ (token) kết nối trực tiếp với tất cả các từ khác, bất kể khoảng cách.

    Ví dụ: Trong câu "Con mèo nằm trên thảm vì nó mệt".

        Cơ chế Attention sẽ giúp từ "nó" kết nối mạnh nhất với từ "con mèo".

        Mô hình hiểu ngay ngữ cảnh: "nó" ở đây là "con mèo" chứ không phải "cái thảm".

2. "Bộ ba nguyên tử": Query, Key, Value (Q, K, V)

Để tính toán xem "nên chú ý vào đâu", Attention sử dụng một hệ thống giống như việc tìm kiếm thông tin trong thư viện:

    Query (Q - Truy vấn): "Tôi là từ hiện tại, tôi đang tìm kiếm mối liên quan gì?"

    Key (K - Khóa): "Tôi là các từ khác trong câu, tôi có đặc điểm này, liệu có khớp với bạn không?"

    Value (V - Giá trị): "Nếu tôi và bạn liên quan đến nhau, đây là thông tin nội dung mà tôi sẽ đóng góp cho bạn."

Quy trình tính toán:

    Lấy Query nhân với Key của tất cả các từ khác để ra một con số (điểm số tương quan).

    Dùng hàm Softmax để biến các con số đó thành tỷ lệ phần trăm (ví dụ: chú ý vào chính nó 70%, chú ý vào từ 'mèo' 20%, các từ khác 10%).

    Nhân tỷ lệ này với các Value tương ứng để tạo ra vector đại diện mới mang đầy đủ ngữ cảnh.
Điểm yếu của Attention (để trả lời sâu hơn)

Dù mạnh mẽ, Attention có một nhược điểm chí mạng: Độ phức tạp tính toán.

    Vì mỗi từ phải "nhìn" tất cả các từ khác, nên nếu câu có n từ, số phép tính sẽ là n2 (bình phương).

    Đây là lý do tại sao các mô hình như ChatGPT có giới hạn về "Context Window" (độ dài văn bản đầu vào) – vì nếu input quá dài, lượng RAM và năng lượng tính toán sẽ tăng vọt theo cấp số nhân.
Multi-head Attention
    • Multi-Head Attention = nhiều self-attention “head” chạy song song
    • Mỗi head học một khía cạnh khác nhau của ngữ cảnh
    • Output cuối cùng = concat tất cả head → linear layer
Công thức:
Attention(Q, K, V) = softmax(Q.k^T/sqrt(dk)).V
Bài tập
Demo Multi-head Attention
import torch
import torch.nn.functional as F

# Câu demo: 4 từ
words = ["Tôi", "yêu", "AI", "."]
seq_len = len(words)
d_model = 8  # embedding nhỏ để minh họa
num_heads = 2  # 2 head

# Token embedding giả
torch.manual_seed(0)
x = torch.rand(seq_len, d_model)

# Chia embedding cho mỗi head
d_k = d_model // num_heads

# Tạo Q,K,V weights cho mỗi head
W_Q = torch.rand(num_heads, d_model, d_k)
W_K = torch.rand(num_heads, d_model, d_k)
W_V = torch.rand(num_heads, d_model, d_k)

heads = []
for h in range(num_heads):
    Q = x @ W_Q[h]  # (seq_len, d_k)
    K = x @ W_K[h]
    V = x @ W_V[h]
    
    # Attention score
    scores = Q @ K.T / (d_k ** 0.5)
    attn = F.softmax(scores, dim=-1)
    
    # Weighted sum
    head_out = attn @ V
    heads.append(head_out)

# Concat các head
multi_head_out = torch.cat(heads, dim=-1)
print("Multi-Head Attention output shape:", multi_head_out.shape)
print("Multi-Head Attention output:\n", multi_head_out)

BERT (Bidirectional Encoder Representations from Transformers)
    • Là một mô hình ngôn ngữ do Google phát triển (2018), dùng để hiểu ngữ cảnh của câu theo cả hai chiều (trái → phải và phải → trái) và được xây dựng chỉ dùng phần encoder của transformer.
    • BERT không tạo văn bản mới (như GPT), mà hiểu và biểu diễn ngữ nghĩa câu chữ. Nó được dùng như "bộ não ngôn ngữ" trong các bài toán hiểu ngôn ngữ tự nhiên (NLU).
Nhiệm cụ của BERT:
    • BERT chỉ là một bộ biểu diễn ngữ nghĩa. BERT mã hóa câu hoặc từ thành vector chứa ngữ cảnh 2 chiều. 
    • Ví dụ với hai câu: "Tôi ăn no rồi", "Tôi đã no bụng" → BERT sẽ biến mỗi câu thành một vector 768 chiều (nếu dùng bert-base), và vì nghĩa tương tự → 2 vector gần nhau trong không gian embedding.
Pipeline hoạt động của BERT:
Inputs → input Embedding + Positional Encoding → Multi-head Attention → Add & Norm → Feed Forward → Add & Norm → Linear → Softmax → Output
GPT (Generative Pre-trained Transformer)
    • Là mô hình của OpenAI dùng decoder của Transformer để: Sinh văn bản (generate), chứ không phải hiểu như BERT.
    • GPT được huấn luyện để:
        ◦ Dự đoán token tiếp theo trong chuỗi
        ◦ Học cách viết mượt, logic, tự nhiên
        ◦ Hoàn thành câu, sinh câu trả lời, dịch, viết code,…
        ◦ Bạn có thể xem GPT như bộ não viết/generate, trong khi BERT là bộ não phân tích/understand.
Dùng để làm gì:
    • Sinh văn bản: viết bài, viết code, tóm tắt
    • Chatbot hội thoại: ChatGPT chính là GPT + RLHF
    • Hoàn thành câu / dự đoán token tiếp theo: Cho nửa câu, GPT viết tiếp
    • Dịch, rewrite, paraphrase
    • Sinh câu trả lời hỏi đáp (free-form)
Pipline của GPT:
    • Input: "Tôi đang đói nên tôi muốn"
    • GPT làm:
        1. Tokenize câu
        2. Áp vào Transformer Decoder
        3. Dự đoán token tiếp theo: "ăn"
        4. Ghép vào chuỗi → tiếp tục dự đoán token tiếp theo nữa
        5. Dừng khi gặp token kết thúc
Bài tập
Demo Fine-Tune Chatbot Hỏi-Đáp bằng transformer
from transformers import AutoTokenizer, AutoModelForCausalLM, Trainer, TrainingArguments
from datasets import load_dataset

model_name = "Qwen/Qwen2.5-7B-Instruct"
tokenizer = AutoTokenizer.from_pretrained(model_name)
model = AutoModelForCausalLM.from_pretrained(model_name)

# Load dữ liệu
dataset = load_dataset("csv", data_files={"train": "data.csv"})

# Tokenize
def preprocess(example):
    text = f"### User: {example['input']}\n### Assistant: {example['response']}"
    tokens = tokenizer(text, truncation=True, padding="max_length", max_length=512)
    tokens["labels"] = tokens["input_ids"].copy()  # labels = input_ids cho LM
    return tokens

tokenized_dataset = dataset["train"].map(preprocess, batched=False)

# Training
training_args = TrainingArguments(
    output_dir="./chatbot_model",
    per_device_train_batch_size=2,
    num_train_epochs=1,
    save_steps=100,
    logging_steps=10,
    fp16=True  # nếu GPU hỗ trợ
)

trainer = Trainer(
    model=model,
    args=training_args,
    train_dataset=tokenized_dataset
)

trainer.train()
4. AI
Math (Toán học)
Đạo hàm
Đạo hàm là “tốc độ thay đổi” của một đại lượng.
    • Tối ưu hóa: Tìm điểm nhỏ nhất, lớn nhất trong hàm (mất mát trong ML).
    • Kinh tế: Tối đa hóa lợi nhuận, tối thiểu hóa chi phí.
    • Vật lý: Mối liên hệ giữa vị trí - vận tốc - gia tốc.
    • ML/DL: Sử dụng tính toán hàm mất mát (gradient descent).Nếu không có đạo hàm → máy không biết “học” thế nào để tốt hơn.
    • Game: Mô phỏng chuyển động, ánh sáng, âm thanh.
    • Sinh học/Hóa học: Mô hình hóa phản ứng, lan truyền, tăng trưởng, …

