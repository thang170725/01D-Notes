- [Pipeline LLM](#pipeline-llm)
  - [Pipeline huấn luyện LLM (Training Pipeline)](#pipeline-huấn-luyện-llm-training-pipeline)
  - [Pipeline inference](#pipeline-inference)
  - [Pipeline sản phẩm (Production LLM stack)](#pipeline-sản-phẩm-production-llm-stack)
- [RAG (Retrieval-Augmented Generation)](#rag-retrieval-augmented-generation)
  - [Demo Pipeline khi có RAG (ví dụ hỏi thời tiết hôm nay)](#demo-pipeline-khi-có-rag-ví-dụ-hỏi-thời-tiết-hôm-nay)
- [Transformer](#transformer)
- [Câu demo: 5 từ](#câu-demo-5-từ)
- [Token embedding giả (random)](#token-embedding-giả-random)
- [Hàm Positional Encoding](#hàm-positional-encoding)
- [Cộng token embedding + PE](#cộng-token-embedding--pe)
- [Câu demo: 4 từ](#câu-demo-4-từ)
- [Token embedding giả](#token-embedding-giả)
- [Chia embedding cho mỗi head](#chia-embedding-cho-mỗi-head)
- [Tạo Q,K,V weights cho mỗi head](#tạo-qkv-weights-cho-mỗi-head)
- [Concat các head](#concat-các-head)
---
# Pipeline LLM
```bash
khung chung:
    1. Transformer architecture
    2. Pretraining
    3. Instruction tuning
    4. Alignment
    5. Decoding
Nhưng mỗi model khác ở:
- Architecture	    : GPT → dense, Gemini → mixture, DeepSeek → MoE
- Tokenizer	        : BPE vs SentencePiece
- Data	            : Dataset riêng
- Alignment	        : RLHF vs RLAIF
- Safety	        : Rule-based vs classifier
- Decoding	        : Sampling strategy khác
- Tool integration	: Native tool calling hay wrapper
```
**Ex: khác biệt cụ thể**
```bash
GPT
    + Dense transformer
    + RLHF
    + Tool calling mạnh
    + Multi-stage alignment
Claude
    + Constitutional AI
    + Ít RLHF truyền thống hơn
    + Alignment thiên về nguyên tắc
DeepSeek
    + MoE
    + Training tối ưu chi phí
    + LLaMA
    + Base model open-weight
    + Community fine-tune
```
## Pipeline huấn luyện LLM (Training Pipeline)
```bash
1. Thu thập dữ liệu
2. Làm sạch & xử lý dữ liệu
3. Tokenization (Text -> token)
4. Pretraining (Huấn luyện theo Object)
5. Instruction tuning (Fine-tune trên dạng prompt -> response, data có cấu trúc hướng dẫn)
6. Alignment (RLAIF, RLHF) -> chấm điểm
```
## Pipeline inference
```bash
Khi bạn gõ câu hỏi, hệ thống không chỉ “đưa vào model” là xong. Nó có pipeline riêng
```
```bash
1. Input processing
    + Thêm system prompt
    + Thêm guardrail
    + Thêm memory
    + Có thể thêm RAG
    + Thực tế input model sẽ giống:
        <System prompt>
        <Policy>
        <Conversation history>
        <User message>
2. Context assembly
    + Cắt bớt nếu quá dài
    + Inject document nếu có RAG
    + Inject tool schema nếu có function calling
3. Forward pass qua Transformer
    + Attention
    + Feed-forward
    + Layer norm
    + Lặp N layers
4. Decoding (Chọn token tiếp theo bằng)
    + Greedy
    + Top-k
    + Top-p
    + Temperature
5. Post-processing
    + Lọc nội dung unsafe
    + Kiểm tra format (JSON schema validation)
    + Streaming output
```
## Pipeline sản phẩm (Production LLM stack)
```bash
User → API Gateway
     → Moderation model
     → Prompt builder
     → RAG retriever
     → LLM
     → Tool executor
     → Output filter
     → Response
```
**Ex: nếu bạn hỏi**
```bash
“Tổng doanh thu quý 4 là bao nhiêu?”

Pipeline có thể là:
    + Embed câu hỏi
    + Tìm vector gần nhất
    + Lấy document liên quan
    + Inject vào prompt
    + Model trả lời
    + Post-filter
```
# RAG (Retrieval-Augmented Generation)
```bash
- RAG chủ yếu ứng dụng vào Generative AI, đặc biệt là LLM.
```
**Ex: Bạn hỏi: “Thời tiết hôm nay thế nào?”**
```bash
- LLM bản chất sẽ:
    + Nhìn pattern các câu hỏi tương tự trong dataset
    + Sinh câu trả lời có vẻ hợp lý
- Nếu không có RAG hoặc tool, nó có thể:
    + Trả lời chung chung
    + Hoặc hallucinate
- Vấn đề: Dataset training ≠ Thực tại hiện tại
    + Giả sử:
        - Model train đến tháng 6/2024
        - Hôm nay là 2026
        - Nó không thể biết thời tiết hôm nay, vì:
        - Nó không có sensor
        - Không có internet
        - Không có API thời tiết
        - Nó chỉ có xác suất thống kê từ dữ liệu cũ.
```
**Khi nào LLM tự sinh đủ tốt mà không cần RAG?**
```bash
Nếu câu hỏi là:
    - “Trọng lực là gì?”
    - “Giải thích Attention”
    - “Tổng thống Mỹ đầu tiên là ai?”
    → Những kiến thức ổn định
    → LLM có thể trả lời tốt chỉ dựa vào training.
```
**Khi nào cần RAG / Tool?**
```bash
Các trường hợp:
    - Kiến thức động (real-time)
        + Thời tiết hôm nay
        + Giá vàng hiện tại
        + Tỷ giá USD
        + Kết quả bóng đá tối qua
    - Kiến thức riêng tư / nội bộ
    - Chính sách công ty bạn
        + Tài liệu nội bộ
        + Hợp đồng riêng
    - Kiến thức cực mới
        + Nghiên cứu công bố tuần trước
        + Sản phẩm mới ra hôm qua
LLM không thể biết nếu không:
    - Có RAG
    - Hoặc có tool call API
```
## Demo Pipeline khi có RAG (ví dụ hỏi thời tiết hôm nay)
```bash
Giả sử bạn hỏi: "Hôm nay thời tiết Hà Nội thế nào?"
1. Retrieve
    - Hệ thống sẽ: Query → embedding → vector search → lấy document liên quan
    - Ví dụ retrieve được:
        Doc1:
        "Hà Nội ngày 11/02/2026:
        - Nhiệt độ: 18°C
        - Trời nhiều mây
        - Độ ẩm: 82%
        - Có mưa nhẹ buổi chiều"
2. Prompt thật sự gửi vào LLM
    - LLM KHÔNG chỉ nhận câu hỏi của bạn. Nó sẽ nhận dạng:
        '<System Instruction>

        Bạn là trợ lý AI.
        Chỉ trả lời dựa trên thông tin trong phần CONTEXT.
        Nếu không có thông tin, nói không biết.

        <CONTEXT>
        Hà Nội ngày 11/02/2026:
        - Nhiệt độ: 18°C
        - Trời nhiều mây
        - Độ ẩm: 82%
        - Có mưa nhẹ buổi chiều
        </CONTEXT>

        <User Question>
        Hôm nay thời tiết Hà Nội thế nào?
        </User Question>'

    -> Đây mới là input thật sự vào model.
3. Nếu là tool-based (API call) thay vì RAG
    - Lúc đó input có thể là:
        'User: Hôm nay thời tiết Hà Nội thế nào?

        Tool output (JSON):
        {
          "city": "Hà Nội",
          "temp": "18C",
          "condition": "Cloudy",
          "humidity": "82%"
        }

        Model receives:

        You are an AI assistant.
        Use the tool output below to answer the question.

        Tool result:
        {...JSON...}

        User question:
        Hôm nay thời tiết Hà Nội thế nào?'
```
# Transformer
**Architecture (Encode + Decode)**
```bash
                 ┌──────────────────────────┐
Input Tokens →   │      Encoder Stack       │
                 └──────────────────────────┘
                           ↓
                  Encoder Output (Memory)
                           ↓
                 ┌──────────────────────────┐
Target Tokens →  │      Decoder Stack       │
                 └──────────────────────────┘
                           ↓
                        Linear
                           ↓
                        Softmax
                           ↓
                      Output Tokens
```
**Pipeline**
```bash
Input Tokens
     ↓
Token Embedding
     ↓
Positional Encoding
     ↓
┌──────────────────────────────┐
│        Encoder Layer         │
│  ├─ Multi-Head Self-Attn     │
│  ├─ Add & LayerNorm          │
│  ├─ Feed Forward Network     │
│  └─ Add & LayerNorm          │
└──────────────────────────────┘
     × N Layers
     ↓
Encoder Output (Memory)
     │
     │  (được đưa vào Cross Attention)
     │
     └───────────────────────────────────────────────────────────┐
                                                                 │
Target Tokens (shifted right)                                    │
     ↓                                                           │
Token Embedding                                                  │
     ↓                                                           │
Positional Encoding                                              │
     ↓                                                           │
┌────────────────────────────────────────────────────────────┐   │
│        Decoder Layer                                       │   │
│  ├─ Masked Self-Attn                                       │   │
│  ├─ Add & LayerNorm                                        │   │
│  ├─ Cross Attention (Q từ decoder, K,V từ encoder)   ◄─────────┘
│  ├─ Add & LayerNorm                                        │
│  ├─ Feed Forward Network                                   │
│  └─ Add & LayerNorm                                        │
└────────────────────────────────────────────────────────────┘
     × N Layers
     ↓
Linear Projection (to vocab)
     ↓
Softmax
     ↓
Next Token Probability

```
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