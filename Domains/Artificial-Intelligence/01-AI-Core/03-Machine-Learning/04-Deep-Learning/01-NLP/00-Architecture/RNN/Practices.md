- [Mô tả Work flow của RNN cho bài toán dự đoán từ tiếp theo](#mô-tả-work-flow-của-rnn-cho-bài-toán-dự-đoán-từ-tiếp-theo)
- [Demo Research RNN](#demo-research-rnn)
---
[<<Back](Base.md)
# Mô tả Work flow của RNN cho bài toán dự đoán từ tiếp theo
```bash
Cho một câu chưa hoàn chỉnh: "I love deep _" mô hình phải dự đoán từ tiếp theo "learning"
  - Input: I love deep
  - Output: learning
```
**Dataset**
```bash
| Sentence                 |
| ------------------------ |
| I love deep learning     |
| I love machine learning  |
| I love natural language  |
| I enjoy deep learning    |
| I enjoy machine learning |
| ...                      |
```
**Step 1: Tokenization (chuyển câu thành token)**
```bash
Ví dụ câu: I love deep learning -> [I, love, deep, learning]
```
**Step 2: Vocabulary (tạo từ điển)**
```bash
| Word     | ID |
| -------- | -- |
| I        | 1  |
| love     | 2  |
| enjoy    | 3  |
| deep     | 4  |
| machine  | 5  |
| natural  | 6  |
| language | 7  |
| learning | 8  |
-> Vocabulary size: V = 8
```
**Step 3: Tạo input và target**
```bash
Ví dụ câu: I love deep learning -> [1, 2, 4, 8]
  - Input: [1, 2, 4] 
  - Output: [2, 4, 8]

Tức là:
  Input:   I     love    deep
            ↓      ↓       ↓
  Target: love   deep   learning
```
**Step 4: Encode: One hot**
```bash
Ví dụ từ deep vector one-hot: deep = [0 0 0 1 0 0 0 0] # Dimension: V = 8
```
**Step 5: Forward Pass**
```bash
Giả sử input sequence: I love deep
  Step 1: word = "I"
    - One-hot: x1 = [1 0 0 0 0 0 0 0]
    - Giả sử trọng số: Wxh = [0.2 0.1 0.0 ...] ...
    - Giả sử hidden state ban đầu: h0 = [0 0 0 0]
    - Tính: ℎ1 = 𝑡𝑎𝑛ℎ(𝑊𝑥ℎ.𝑥1 + 𝑊ℎℎ.ℎ0) = [0.21, -0.13, 0.45, 0.10]
Step 2: word = "love"
  - x2 = [0 1 0 0 0 0 0 0]
  - ℎ2 = 𝑡𝑎𝑛ℎ(𝑊𝑥ℎ.𝑥2 + 𝑊ℎℎ.ℎ1) = [0.35, 0.10, 0.41, 0.22]
Step 3: word = "deep"
  - x3 = [0 0 0 1 0 0 0 0]
  - ℎ3 = 𝑡𝑎𝑛ℎ(𝑊𝑥ℎ.𝑥3 + 𝑊ℎℎ.ℎ2) = [0.52, 0.11, 0.33, 0.40]
```
**Step 6: Output Layer**
```bash
𝑦3 = 𝑠𝑜𝑓𝑡𝑚𝑎𝑥(𝑊ℎ𝑦.ℎ3) = [0.02, 0.01, 0.03, 0.04, 0.02, 0.03, 0.05, 0.80] # Mapping lại từ: learning -> 0.80 → dự đoán: learning
```
**Step 7: Loss Function: Dùng Cross Entropy**
```bash
- Target vector: learning = [0 0 0 0 0 0 0 1]
- Loss: 𝐿 = −∑𝑦𝑡𝑟𝑢𝑒.log(𝑦𝑝𝑟𝑒𝑑) = −log(0.80) = 0.223
```
**Step 8: Backpropagation Through Time (BPTT): Gradient được lan truyền ngược theo thời gian**
```bash
- Chuỗi: I → love → deep
- Gradient flow: loss -> h3 -> h2 -> h1
- Update: Wxh, Whh, Why
```
**Step 9: Training Loop: Toàn bộ pipeline**
```bash

for epoch:
  for sentence in dataset:
     tokenize
     convert to one-ho
     forward pass (RNN)
     compute loss
     BPTT
     update weights
```
# Demo Research RNN
```python
import torch
import torch.nn as nn

class ResearchRNNCell(nn.Module):
    def __init__(self, input_size, hidden_size):
        super(ResearchRNNCell, self).__init__()
        self.input_size = input_size
        self.hidden_size = hidden_size
        
        # 1. Ma trận trọng số cho đầu vào X (Biến đổi input_size thành hidden_size)
        self.W_xh = nn.Linear(input_size, hidden_size, bias=False)
        
        # 2. Ma trận trọng số cho trạng thái ẩn trước đó H_prev (Giữ nguyên kích thước hidden_size)
        self.W_hh = nn.Linear(hidden_size, hidden_size, bias=False)
        
        # 3. Thành phần Bias (Độ lệch) cộng thêm sau khi hợp nhất hai luồng
        self.bias = nn.Parameter(torch.zeros(1, hidden_size))
        
        # 4. Hàm kích hoạt phi tuyến tính tanh (ép giá trị về khoảng -1 đến 1)
        self.tanh = nn.Tanh()

    def forward(self, x_t, h_prev):
        """
        Xử lý tại MỘT bước thời gian t cụ thể.
        Phương trình toán học: H_t = tanh(X_t * W_xh + H_prev * W_hh + bias)
        """
        # Luồng 1: Xử lý thông tin từ đầu vào hiện tại
        out_x = self.W_xh(x_t)
        
        # Luồng 2: Xử lý ký ức từ bước thời gian trước
        out_h = self.W_hh(h_prev)
        
        # Luồng tổng hợp: Cộng hai nguồn thông tin kèm bias
        sum_linear = out_x + out_h + self.bias
        
        # Kích hoạt phi tuyến tính để tạo ra trạng thái ẩn mới
        h_next = self.tanh(sum_linear)
        
        return h_next, out_x, out_h, sum_linear


# =====================================================================
# CHƯƠNG TRÌNH MÔ PHỎNG VÀ THEO DÕI LOG CHẠY THỰC TẾ
# =====================================================================
if __name__ == "__main__":
    # Cấu hình giả định cho bài toán NLP nhỏ
    BATCH_SIZE = 1     # Xử lý 1 chuỗi dữ liệu (1 câu)
    SEQ_LEN = 3        # Chuỗi có độ dài bằng 3 bước thời gian (Ví dụ: "I", "love", "AI")
    INPUT_SIZE = 4     # Mỗi từ được biểu diễn bằng vector 4 chiều (Embedding size)
    HIDDEN_SIZE = 2    # Kích thước bộ nhớ ẩn mong muốn là 2 chiều

    print("="*60)
    print(" KHỞI TẠO MÔ HÌNH VÀ DỮ LIỆU NGHIÊN CỨU RNN ")
    print("="*60)
    
    # Khởi tạo dữ liệu đầu vào ngẫu nhiên: [Batch_size, Seq_Len, Input_Size]
    # Định dạng: [1 câu, 3 từ, mỗi từ có 4 đặc trưng]
    input_sequence = torch.randn(BATCH_SIZE, SEQ_LEN, INPUT_SIZE)
    print(f"-> Ma trận chuỗi đầu vào tổng: {list(input_sequence.shape)}")
    
    # Khởi tạo lớp RNN Cell
    rnn_cell = ResearchRNNCell(input_size=INPUT_SIZE, hidden_size=HIDDEN_SIZE)
    
    # Khởi tạo Ký ức ban đầu (Hidden State H0) là một ma trận toàn số 0
    h_t = torch.zeros(BATCH_SIZE, HIDDEN_SIZE)
    print(f"-> Khởi tạo Ký ức đầu tiên (H0) toàn số 0: {h_t.tolist()}\n")

    print("="*60)
    print(" BẮT ĐẦU LUỒNG XỬ LÝ THEO TỪNG BƯỚC THỜI GIAN (TIME STEPS) ")
    print("="*60)

    # Vòng lặp duyệt qua từng bước thời gian trong chuỗi (Duyệt từ từ thứ 1 đến từ thứ 3)
    for t in range(SEQ_LEN):
        print(f"\n⏱️ --- BƯỚC THỜI GIAN t = {t} ---")
        
        # Trích xuất vector đầu vào tại thời điểm t: Kích thước [Batch_size, Input_Size]
        x_t = input_sequence[:, t, :]
        print(f"  [Đầu vào X_t]: {x_t.tolist()} | Shape: {list(x_t.shape)}")
        print(f"  [Ký ức cũ H_prev]: {h_t.tolist()} | Shape: {list(h_t.shape)}")
        
        # Đưa vào RNN Cell để tính toán ma trận
        h_t, log_x, log_h, log_sum = rnn_cell(x_t, h_t)
        
        # In log chi tiết các phép toán ma trận diễn ra bên trong Cell
        print(f"  └─► Biến đổi Đầu vào (X_t * W_xh)           = {log_x.tolist()}")
        print(f"  └─► Biến đổi Ký ức cũ (H_prev * W_hh)       = {log_h.tolist()}")
        print(f"  └─► Tổng hợp tuyến tính (+ Bias)           = {log_sum.tolist()}")
        print(f"  └─► KÝ ỨC MỚI SAU KHI QUA TANH (H_t)        = {h_t.tolist()} | Shape: {list(h_t.shape)}")
        print("  " + "-"*50)

    print("\n" + "="*60)
    print(" KẾT THÚC QUÁ TRÌNH XỬ LÝ ")
    print("="*60)
    print(f"Trạng thái ẩn tối hậu (Final Hidden State) thu được: {h_t.tolist()}")
    print("Trạng thái này chứa đựng toàn bộ ngữ cảnh cô đọng của cả chuỗi 3 bước vừa qua.")
```
```bash
============================================================
 KHỞI TẠO MÔ HÌNH VÀ DỮ LIỆU NGHIÊN CỨU RNN 
============================================================
-> Ma trận chuỗi đầu vào tổng: [1, 3, 4]
-> Khởi tạo Ký ức đầu tiên (H0) toàn số 0: [[0.0, 0.0]]

============================================================
 BẮT ĐẦU LUỒNG XỬ LÝ THEO TỪNG BƯỚC THỜI GIAN (TIME STEPS) 
============================================================

⏱️ --- BƯỚC THỜI GIAN t = 0 ---
  [Đầu vào X_t]: [[-0.029004188254475594, -0.4269711971282959, -0.8609756827354431, -0.6362969875335693]] | Shape: [1, 4]
  [Ký ức cũ H_prev]: [[0.0, 0.0]] | Shape: [1, 2]
  └─► Biến đổi Đầu vào (X_t * W_xh)           = [[0.35400715470314026, -0.5067230463027954]]
  └─► Biến đổi Ký ức cũ (H_prev * W_hh)       = [[0.0, 0.0]]
  └─► Tổng hợp tuyến tính (+ Bias)           = [[0.35400715470314026, -0.5067230463027954]]
  └─► KÝ ỨC MỚI SAU KHI QUA TANH (H_t)        = [[0.33992448449134827, -0.4673880338668823]] | Shape: [1, 2]
  --------------------------------------------------

⏱️ --- BƯỚC THỜI GIAN t = 1 ---
  [Đầu vào X_t]: [[-2.1548750400543213, 0.4023962616920471, 0.9219271540641785, -0.5887636542320251]] | Shape: [1, 4]
  [Ký ức cũ H_prev]: [[0.33992448449134827, -0.4673880338668823]] | Shape: [1, 2]
  └─► Biến đổi Đầu vào (X_t * W_xh)           = [[0.28777649998664856, 0.8024523258209229]]
  └─► Biến đổi Ký ức cũ (H_prev * W_hh)       = [[0.4648362994194031, -0.11226003617048264]]
  └─► Tổng hợp tuyến tính (+ Bias)           = [[0.752612829208374, 0.6901922821998596]]
  └─► KÝ ỨC MỚI SAU KHI QUA TANH (H_t)        = [[0.6367051601409912, 0.5981054902076721]] | Shape: [1, 2]
  --------------------------------------------------

⏱️ --- BƯỚC THỜI GIAN t = 2 ---
  [Đầu vào X_t]: [[1.2360337972640991, 0.8221803307533264, 0.13070924580097198, 1.8772333860397339]] | Shape: [1, 4]
  [Ký ức cũ H_prev]: [[0.6367051601409912, 0.5981054902076721]] | Shape: [1, 2]
  └─► Biến đổi Đầu vào (X_t * W_xh)           = [[-0.4621211290359497, 0.19252610206604004]]
  └─► Biến đổi Ký ức cũ (H_prev * W_hh)       = [[0.010766863822937012, 0.2899230420589447]]
  └─► Tổng hợp tuyến tính (+ Bias)           = [[-0.4513542652130127, 0.48244914412498474]]
  └─► KÝ ỨC MỚI SAU KHI QUA TANH (H_t)        = [[-0.42301157116889954, 0.448202908039093]] | Shape: [1, 2]
  --------------------------------------------------

============================================================
 KẾT THÚC QUÁ TRÌNH XỬ LÝ 
============================================================
Trạng thái ẩn tối hậu (Final Hidden State) thu được: [[-0.42301157116889954, 0.448202908039093]]
Trạng thái này chứa đựng toàn bộ ngữ cảnh cô đọng của cả chuỗi 3 bước vừa qua.
```