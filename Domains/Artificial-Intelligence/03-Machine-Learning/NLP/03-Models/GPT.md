- [Introduction](#introduction)
- [Practises](#practises)
  - [Demo GPT với sinh tiếp câu](#demo-gpt-với-sinh-tiếp-câu)
---
# Introduction
```bash
- Là mô hình của OpenAI dùng decoder của Transformer để: Sinh văn bản (generate), chứ không phải hiểu như BERT.
- GPT được huấn luyện để:
    + Dự đoán token tiếp theo trong chuỗi
    + Học cách viết mượt, logic, tự nhiên
    + Hoàn thành câu, sinh câu trả lời, dịch, viết code,…
    + Bạn có thể xem GPT như bộ não viết/generate, trong khi BERT là bộ não phân tích/understand.
- Dùng để làm gì:
    + Sinh văn bản: viết bài, viết code, tóm tắt
    + Chatbot hội thoại: ChatGPT chính là GPT + RLHF
    + Hoàn thành câu / dự đoán token tiếp theo: Cho nửa câu, GPT viết tiếp
    + Dịch, rewrite, paraphrase
    + Sinh câu trả lời hỏi đáp (free-form)
```
**Pipline của GPT**
```bash
Input: "Tôi đang đói nên tôi muốn"
GPT làm:
  1. Tokenize câu
  2. Áp vào Transformer Decoder
  3. Dự đoán token tiếp theo: "ăn"
  4. Ghép vào chuỗi → tiếp tục dự đoán token tiếp theo nữa
  5. Dừng khi gặp token kết thúc
```
**Architecture**
```bash
Input Text (VD: "I love")
      ↓
Tokenization
      ↓
Token IDs
      ↓
Embedding + Positional Encoding
      ↓
┌──────────────────────────────────────────────────────────────────────────────┐
│ GPT Decoder Stack (N layers, vd: 12, 24, 96...)                             │
│                                                                              │
│  ├─ Masked Multi-Head Self-Attention                                         │
│  │     ├─ Q, K, V từ input                                                   │
│  │     ├─ Mask: KHÔNG nhìn token phía sau                                    │
│  │     └─ Chỉ attention về bên trái                                          │
│  │                                                                           │
│  ├─ Add & LayerNorm                                                         │
│  │                                                                           │
│  ├─ Feed Forward Network (FFN)                                               │
│  │     ├─ Linear (d → 4d)                                                    │
│  │     ├─ Activation (GELU)                                                  │
│  │     └─ Linear (4d → d)                                                    │
│  │                                                                           │
│  └─ Add & LayerNorm                                                         │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘
      ↓
Linear (project ra vocab)
      ↓
Softmax
      ↓
Xác suất token tiếp theo
      ↓
Sampling (argmax / top-k / top-p)
      ↓
Append token → lặp lại

🔥 Điểm cốt lõi của GPT
1. Masked Attention
Token i chỉ nhìn được:
← tất cả token trước đó
✖ không thấy tương lai
2. Objective (cực quan trọng)
Dự đoán token tiếp theo:
P(x_t | x_1, x_2, ..., x_{t-1})
```
# Practises
## Demo GPT với sinh tiếp câu
```bash
Bài toán: Sinh tiếp câu

Input:
"I love"
```
```bash
"

🔪 Bước 1: Tokenization
["I", "love"]
🔢 Bước 2: Token IDs (giả định)
[101, 2057]
📊 Bước 3: Embedding
"I" → vector
"love" → vector
🔥 Bước 4: Masked Self-Attention
👉 Quan trọng:
"love" chỉ nhìn:
← "I"

Không thấy:

"pizza", "you", "AI" (tương lai)
🧠 Bước 5: Dự đoán token tiếp theo

Model tính xác suất:

"you"   → 0.35
"it"    → 0.25
"pizza" → 0.20
"AI"    → 0.10

👉 Chọn (giả sử greedy):

"you"
➡️ Bước 6: Cập nhật chuỗi
"I love you"
🔁 Bước 7: Lặp lại
Lần 2:

Input:

"I love you"

Attention:

"you" ← "I", "love"

Dự đoán tiếp:

"so"     → 0.4
"very"   → 0.3
"much"   → 0.2

👉 chọn "so"

Lần 3:
"I love you so"

Dự đoán:

"much" → 0.7
"deep" → 0.1

👉 chọn "much"

✅ KẾT QUẢ CUỐI
"I love you so much"
🧩 Toàn bộ flow
"I love"
→ predict "you"
→ predict "so"
→ predict "much"
→ DONE
```