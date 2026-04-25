# Directory Structure
```bash
NLP/                            # mình dùng thư mục này để xem kiến thức NLP trong AI
├── LLMS.md                     # mình dùng file này để hiểu kiến thức về các mô hình LLM cụ thể
├── Architecture/             # mình dùng thư mục này để xem các kiến trúc trong NLP
├── Math_Technical/           # mình dùng thư mục này để xem các kĩ thuật và toán học trong NLP
├── Practices.md                # mình dùng file này để xem code mẫu, bài tập
├── Text_Preprocessing.md       # mình dùng file này để thao tác tiền dữ liệu (tất cả những thao tác với dữ liệu trước khi embedding)
├── 05_LLMs_Generative.md       # Kỷ nguyên Generative: GPT, Llama, Prompt Engineering, Fine-tuning
└── 06_RAG_Systems.md           # Hệ thống thực tế: Vector DB, Retrieval, LangChain/LlamaIndex
```
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


sentence segmentation
Embedding & Vector Representation
CBOW
Skip-gram
Glove

PhoBERT


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
