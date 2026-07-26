- [00-NLP-Algorgithm Introduction (lưu trữ các thuật toán xử lý văn bản)](#00-nlp-algorgithm-introduction-lưu-trữ-các-thuật-toán-xử-lý-văn-bản)
- [Gradient](#gradient)
  - [BPTT (Backpropagation Through Time)](#bptt-backpropagation-through-time)
- [Forward RNN qua seq\_len steps](#forward-rnn-qua-seq_len-steps)
- [Loss dựa trên h cuối](#loss-dựa-trên-h-cuối)
- [BPTT](#bptt)
    - [Practice](#practice)
      - [Demo BPTT](#demo-bptt)
- [Character 5-gram (hay còn gọi là 5-shingle - là kỹ thuật chia một chuỗi văn bản thành các đoạn con liên tiếp dài đúng 5 ký tự)](#character-5-gram-hay-còn-gọi-là-5-shingle---là-kỹ-thuật-chia-một-chuỗi-văn-bản-thành-các-đoạn-con-liên-tiếp-dài-đúng-5-ký-tự)
- [Retrival Document (thuật toán tìm kiếm tài liệu, văn bản)](#retrival-document-thuật-toán-tìm-kiếm-tài-liệu-văn-bản)
  - [BM25 (Best Matching 25 - thuật toán xếp hạng văn bản để tìm tài liệu nào liên quan nhất đến từ khóa người dùng tìm kiếm)](#bm25-best-matching-25---thuật-toán-xếp-hạng-văn-bản-để-tìm-tài-liệu-nào-liên-quan-nhất-đến-từ-khóa-người-dùng-tìm-kiếm)
---
# 00-NLP-Algorgithm Introduction (lưu trữ các thuật toán xử lý văn bản)
# Gradient
## BPTT (Backpropagation Through Time)
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
### Practice
#### Demo BPTT
```python
import torch

# fake data
X = torch.tensor([[1.0, 2.0, 3.0]], requires_grad=False) # batch=1, input_dim=3
y_true = torch.tensor([0]) # label

# RNN params
Wxh = torch.randn(3, 3, requires_grad=True) # (input_dim, hidden_dim)
Whh = torch.randn(3, 3, requires_grad=True) # (hidden_dim, hidden_dim)
Why = torch.randn(3, 2, requires_grad=True) # (hidden_dim, output_dim)
bh = torch.zeros(3, requires_grad=True)
by = torch.zeros(2, requires_grad=True)

h_t = torch.zeros(1, 3)
lr = 0.01
seq_len = 2

for i in range(seq_len): # giả sử có h_0, h_1
    # forward RNN
    h_t = torch.tanh(X@Wxh + h_t@Whh + bh)

# compute loss từ h cuối
logits = h_t@Why + by
loss = torch.nn.CrossEntropyLoss()(logits, y_true)
cross_entropy = torch.nn.CrossEntropyLoss()

# BPTT: backward toàn bộ sequence
loss.backward()

# SGD update
with torch.no_grad():
    for p in [Wxh, Whh, Why, bh, by]:
        p -= lr*p.grad
        p.grad.zero_()
    
print(f'Updated params', Wxh, Whh, Why, bh, by)
```
# Character 5-gram (hay còn gọi là 5-shingle - là kỹ thuật chia một chuỗi văn bản thành các đoạn con liên tiếp dài đúng 5 ký tự)
```bash
Nó được dùng rất nhiều trong:
    - Phát hiện văn bản trùng lặp (duplicate detection)
    - MinHash
    - LSH (Locality Sensitive Hashing)
    - So sánh độ giống nhau của văn bản

Ý tưởng rất đơn giản:
    Trượt một cửa sổ dài 5 ký tự từ trái sang phải, mỗi lần dịch 1 ký tự.

Ví dụ 1
    Chuỗi: abcdefghi

    Character 5-gram sẽ là
        1. abcde
        2. bcdef
        3. cdefg
        4. defgh
        5. efghi
```
**Tại sao phải dùng n-gram?**
```bash
Nếu so sánh từng từ: hello world với hello word
    thì: world ≠ word -> mất hẳn sự tương đồng. -> Trong khi đó character 5-gram vẫn giữ được nhiều phần giống nhau.
```
# Retrival Document (thuật toán tìm kiếm tài liệu, văn bản)
## BM25 (Best Matching 25 - thuật toán xếp hạng văn bản để tìm tài liệu nào liên quan nhất đến từ khóa người dùng tìm kiếm)
```bash
Nói đơn giản:
    Người dùng nhập: "học machine learning"
    
    Có 1.000 tài liệu.
    
    BM25 sẽ chấm điểm từng tài liệu.
        Tài liệu nào có điểm cao hơn thì được xếp lên trước.

    BM25 chấm điểm dựa trên 3 yếu tố
        - Từ khóa xuất hiện hay không # Có từ "machine" và "learning" → được điểm., Không có → gần như 0 điểm.
        - Xuất hiện bao nhiêu lần (Term Frequency) # Xuất hiện nhiều lần → điểm tăng. Nhưng tăng đến một mức thì gần như không tăng nữa (tránh spam từ khóa).
        - Độ hiếm của từ (IDF) # Từ hiếm như "tensorflow" → giá trị cao. Từ phổ biến như "là", "và", "the" → giá trị thấp.
```
**Ex**
```bash
Tìm kiếm: "python OCR"

Có 3 tài liệu:
    - Tài liệu A: "Python OCR bằng Tesseract" ✅
    - Tài liệu B: "Python cơ bản" ⚠️
    - Tài liệu C: "OCR nhận dạng văn bản" ⚠️

BM25 sẽ cho điểm gần như:
    Tài liệu	Điểm BM25
    A	        9.8
    C	        6.4
    B	        3.2
⇒ Kết quả trả về: A → C → B
```
**BM25 dùng khi nào?**
```bash
- Công cụ tìm kiếm (Search Engine)
- Tìm tài liệu liên quan
- Tìm đoạn văn phù hợp trong RAG (Retrieval-Augmented Generation)
- Tìm kiếm trong PDF, Word, website,...
```
**So sánh BM25 với Embedding**
```bash
BM25	                    Embedding
So khớp theo từ khóa	    So khớp theo ý nghĩa
Nhanh	                    Chậm hơn
Không hiểu từ đồng nghĩa	Hiểu ngữ nghĩa
Không cần AI	            Cần mô hình embedding

Ví dụ tìm "xe hơi":
    - BM25 chỉ tìm tốt các tài liệu có đúng từ "xe" hoặc "hơi".
    - Embedding vẫn có thể tìm được tài liệu nói về "ô tô" dù không xuất hiện từ "xe hơi".
```
**Các thư viện python**
- [thư viện rank-bm25](../../../../../../Tech-Stacks/Languages/Python/Libraries/Data-Science/01-Data-Processing/Rank_bm25.md)