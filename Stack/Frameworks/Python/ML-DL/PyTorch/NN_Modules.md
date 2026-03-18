- [Nn](#nn)
  - [Module](#module)
  - [.Linear()](#linear)
- [tensor đầu ra của mô hình](#tensor-đầu-ra-của-mô-hình)
  - [.eval()](#eval)
- [TRAIN](#train)
- [TEST](#test)
---
# Nn
```bash
- Để xây dựng mạng nơ ron nhanh chóng.
```
nn
├── Layers
│   ├── Linear
│   ├── Conv2d
│   ├── Embedding
│
├── Activations
│   ├── ReLU
│   ├── Tanh
│   ├── Sigmoid
│
├── Loss Functions
│   ├── CrossEntropyLoss
│   ├── MSELoss
│
└── Model Tools
    ├── Module
    ├── Sequential
Sequential()
Khởi tạo mô hình mạng nơ ron
Cú pháp:
self.net = nn.Sequential(
            nn.Linear(input_size, 128),
            nn.ReLU(),
            nn.Linear(128, 64),
            nn.ReLU(),
            nn.Linear(64, num_classes)
        )
.train()
Bật chế độ training mode.

## Module
## .Linear()
```bash
Là lớp fully connected (FC).
```
**Syn** 
```bash
nn.Linear(in_features, out_features)

- in_features: số chiều input
- out_features: số chiều output (số class nếu phân loại)
```
**Ex**
```python
import torch.nn as nn

fc = nn.Linear(10, 5)
print(fc) # Linear(in_features=10, out_features=5, bias=True)
```
conv2d
functional
import torch
import torch.nn.functional as F

# tensor đầu ra của mô hình
logits = torch.tensor([2.0, 1.0, 0.1])
probs = F.softmax(logits, dim=0)
print(probs)
print(probs.sum())  # Kiểm tra tổng = 1
Softmax()
import tensorflow as tf

logits = tf.constant([2.0, 1.0, 0.1])
probs = tf.nn.softmax(logits)
print(probs.numpy())
print(tf.reduce_sum(probs).numpy())

fc = nn.Linear(in_features=8, out_features=3)

x = torch.randn(2, 5, 8)  # batch 2, 5 bước, mỗi bước 8 chiều
y = fc(x)
print(y.shape)  # (2, 5, 3)

Embedding
Biểu diễn từ (hoặc số nguyên) dưới dạng vector liên tục có ý nghĩa ngữ nghĩa.
Giống kiểu “tra bảng tra cứu” để ánh xạ từ ID sang vector. 
Cú pháp: 
nn.Embedding(num_embeddings, embedding_dim)
    • num_embeddings: Số lượng từ trong từ vựng (vocab size)
    • embedding_dim: Số chiều của vector biểu diễn mỗi từ
embedding = nn.Embedding(num_embeddings=4, embedding_dim=5)

input_ids = torch.tensor([1, 2, 3])
output = embedding(input_ids)

print(output)
tensor([[-2.2608, 0.2584, 0.0430, 0.6564, 0.0903], [-0.0245, 1.9173, 1.0353, 1.4358, 0.1202], [ 0.7551, 1.0152, -0.4208, 0.5330, -0.3870]], grad_fn=<EmbeddingBackward0>)
RNN
Là một lớp để xử lý dữ liệu chuỗi: văn bản, dữ liệu thời gian, âm thanh. RNN ghi nhớ trạng thái trước đó và sử dụng nó để xử lý phần tử tiếp theo.
Cú pháp: torch.nn.RNN(input_size, hidden_size, num_layers=1, batch_first=False)
    • Input_size: Số chiều của mỗi phần tử trong chuỗi.
    • Hidden_size: Số chiều của trạng thái ẩn.
    • Num_layers: Số tầng (lớp RNN)
    • Batch_first: Nếu true, input có dạng (batch, seq_len, input_size)
import torch
import torch.nn as nn

x = torch.randn(2,5,4)
rnn = nn.RNN(input_size=4, hidden_size=6, batch_first=True)
out, hidden = rnn(x)

print(out)
print(hidden)
tensor([[[ 0.3732, -0.3084, -0.0086, 0.0545, -0.2229, -0.2923], [-0.4432, -0.5456, 0.3753, 0.4180, 0.4578, -0.2580], [-0.8133, -0.6375, -0.6581, -0.2354, 0.9065, 0.3951], [-0.2597, -0.8807, -0.5363, -0.5203, 0.7042, -0.4658], [-0.4765, -0.6938, -0.0969, -0.1936, 0.4945, 0.1496]], [[-0.6179, 0.5726, 0.5082, -0.2073, 0.2589, 0.5827], [ 0.5372, -0.8405, -0.4114, -0.0832, 0.4964, -0.6965], [-0.4667, -0.2090, 0.6394, 0.6679, 0.3059, -0.0806], [ 0.0017, 0.1926, 0.0041, 0.5061, 0.4831, 0.2032], [-0.1841, 0.4566, -0.5709, -0.3381, 0.2512, 0.5089]]], grad_fn=<TransposeBackward1>) tensor([[[-0.4765, -0.6938, -0.0969, -0.1936, 0.4945, 0.1496], [-0.1841, 0.4566, -0.5709, -0.3381, 0.2512, 0.5089]]], grad_fn=<StackBackward0>)
LSTM
GRU
ReLU()
Sigmoid()
self.sigmoid = nn.Sigmoid()
logits = self.w*X + self.b # linear
y_pred = self.sigmoid(logits) # sigmoid

Tanh()
tanh là lớp, phải gọi hàm kích hoạt

Softmax()
LeakyReLU
CrossEntropyLoss()
    • Là hàm mất mát (loss function) dùng trong các bài toán phân loại (classification). Nó đo mức độ khác nhau giữa xác suất dữ đoán của mô hình và nhãn thật.
    • Dùng khi đầu ra của mô hình là xác suất cho nhiều lớn (multi-class)
    • Nó kết kết hợp LogSoftmax + Negative Log Likelihood Loss (NLLLoss)
Cú pháp:
loss_fn = nn.CrossEntropyLoss()
loss = loss_fn(output, target)
    • Output: Tensor đầu ra từ mô hình (logits - chưa softmax), kích thước [batch_size, num_classes]
    • Target: tensor chứa nhãn thật, là chỉ số lớp (int), kích thước [batch_size]
out = torch.tensor([[2.0, 1.2, 1]])
target = torch.tensor([0])

loss_fn = nn.CrossEntropyLoss()
loss = loss_fn(out, target)
print(loss.item())
print(loss)
0.5973015427589417 tensor(0.5973)
BCELoss()
self.loss_fn = nn.BCELoss()
loss = self.loss_fn(y_pred, y)

MSELoss()
MLLLoss()
BCEWithLogitsLoss()
ModuleList()
ModuleDict
parameters()
Optim
Cần import torch.optim as optim
SGD()
    • SGD phù hợp khi:
        ◦ Dữ liệu lớn & nhiễu nhiều → SGD ổn định hơn. Các mô hình rất lớn (ví dụ ResNet, ViT, YOLO) thường ưu tiên SGD vì:
            ▪ Adam quá nhanh → dễ rơi vào cực trị kém (bad minima)
            ▪ SGD mượt hơn → tổng quát hoá tốt hơn (generalization)
            ▪ Deep Learning các mô hình lớn = thường dùng SGD + momentum
    • Ví dụ:
        ◦ esNet → SGD
        ◦ EfficientNet → SGD
        ◦ YOLO → SGD
    • Bài toán cần generalization mạnh
        ◦ SGD đôi khi cho kết quả test accuracy tốt hơn Adam.
        ◦ Khi muốn mô hình không “nhảy loạn”
        ◦ Adam điều chỉnh tốc độ theo từng tham số → đôi khi bước nhảy quá mạnh.
Kết luận: SGD tốt cho mô hình lớn, bài toán thị giác (CV), bài toán cần generalization.

Adam()
    • Để tạo trình tối ưu hóa (optimizer), cụ thể nó là một thuật toán giúp giảm loss nhanh và hiệu quả.
    • Adam phù hợp khi:
        ◦ Mô hình nhỏ, vừa, hoặc bài toán khó tối ưu
        ◦ Adam tự điều chỉnh learning rate cho từng tham số → hội tụ nhanh và rất tiện.
    • Ví dụ dùng Adam là hợp lý:
        ◦ NLP (transformer các phiên bản nhỏ)
        ◦ Bài toán regression nhỏ
        ◦ Bài toán phi tuyến, phức tạp
        ◦ Autoencoder, GAN
        ◦ Recommender systems
        ◦ RL
    • Khi mới thử nghiệm mô hình → Adam dễ ra kết quả hơn
        ◦ Thay đổi lr không cần tuning quá nhiều.
        ◦ Batch size nhỏ
        ◦ Adam rất hợp với batch nhỏ, vì:
        ◦ Mức nhiễu gradient lớn → Adam làm mượt tốt hơn
Kết luận: Adam tốt cho bài toán nhỏ, nhanh, exploratory, NLP, hoặc khi gradient nhiễu.
Cú pháp: 
torch.optim.Adam(model.parameters(), lr=learning_rate)
    • model.parameters(): Láy các tham số cần tối ưu từ mô hình.
    • lr: learning rate - tốc độ học.
import torch
import torch.nn as nn

model = nn.Linear(2,1)
optimizer = torch.optim.Adam(model.parameters(), lr=0.1)
print(optimizer)

AdamW()
RMSprop()
.zero_grad()
Trong PyTorch, mỗi lần gọi loss.backward(), gradient không bị reset, mà sẽ cộng dồn vào thuộc tính .grad của từng tham số. Vì gradient bị cộng dồn, nên bạn phải xóa gradient cũ trước khi tính gradient mới, nếu không tham số sẽ cập nhật sai.
Cú pháp:
optimizer.zero_grad()
.step()
Dùng để cập nhật trong số tự động
Cú pháp:
optimizer.step()
### .eval()
```bash
- eval() không phải là hàm tính toán, mà là chế độ (mode) của model.
- Nó nói với model rằng: “Tôi đang đánh giá / suy luận, không huấn luyện nữa.”
- Khi gọi: model.eval() PyTorch sẽ:
    + Tắt Dropout (không random neuron nữa)
    + BatchNorm dùng mean/var đã học, không cập nhật tiếp
    + Model chạy ổn định & đúng khi test/inference
    + Không gọi eval() → kết quả test có thể sai.
```
**Ex: Model có Dropout**
```python
import torch
import torch.nn as nn

model = nn.Sequential(
    nn.Linear(10, 10),
    nn.Dropout(p=0.5),
    nn.Linear(10, 1)
)

x = torch.randn(1, 10)

model.train()
print(model(x))
print(model(x))

# Hai lần chạy ra kết quả khác nhau (do Dropout)

model.eval()
print(model(x))
print(model(x))

# Hai lần chạy ra cùng kết quả
```