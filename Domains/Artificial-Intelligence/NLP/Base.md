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





BERT (Bidirectional Encoder Representations from Transformers)
    • Là một mô hình ngôn ngữ do Google phát triển (2018), dùng để hiểu ngữ cảnh của câu theo cả hai chiều (trái → phải và phải → trái) và được xây dựng chỉ dùng phần encoder của transformer.
    • BERT không tạo văn bản mới (như GPT), mà hiểu và biểu diễn ngữ nghĩa câu chữ. Nó được dùng như "bộ não ngôn ngữ" trong các bài toán hiểu ngôn ngữ tự nhiên (NLU).
Nhiệm cụ của BERT:
    • BERT chỉ là một bộ biểu diễn ngữ nghĩa. BERT mã hóa câu hoặc từ thành vector chứa ngữ cảnh 2 chiều. 
    • Ví dụ với hai câu: "Tôi ăn no rồi", "Tôi đã no bụng" → BERT sẽ biến mỗi câu thành một vector 768 chiều (nếu dùng bert-base), và vì nghĩa tương tự → 2 vector gần nhau trong không gian embedding.
Pipeline hoạt động của BERT:
Inputs → input Embedding + Positional Encoding → Multi-head Attention → Add & Norm → Feed Forward → Add & Norm → Linear → Softmax → Output

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

