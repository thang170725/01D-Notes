- [Intronduction](#intronduction)
  - [Architecture Encoder and Decoder](#architecture-encoder-and-decoder)
    - [Positional Encoding](#positional-encoding)
---
# Intronduction
```bash
- Transformer là kiến trúc nền tảng cho rất nhiều hệ thống AI hiện đại. Gần như mọi lĩnh vực AI lớn hiện nay đều có phiên bản dựa trên transformer. Dưới đây là các nhóm tiêu biểu và những mô hình nổi bật:
    1. Xử lý ngôn ngữ tự nhiên (NLP)
        - Đây là nơi transformer bắt đầu (từ paper Attention Is All You Need).
        - Các mô hình tiêu biểu:
            + BERT → hiểu ngữ cảnh, phân loại, QA
            + GPT → sinh văn bản (ChatGPT là ví dụ)
            + T5 → biến mọi task thành text-to-text
            + RoBERTa → cải tiến từ BERT
        - Ứng dụng:
            + Chatbot, trợ lý AI
            + Dịch máy (Google Translate)
            + Tóm tắt văn bản
            + Phân tích cảm xúc
    2. Thị giác máy tính (Computer Vision)
        - Transformer giờ không chỉ cho text nữa.
        - Các mô hình:
            + Vision Transformer → áp dụng transformer cho ảnh
            + DETR → object detection
            + Swin Transformer → xử lý ảnh phân cấp
        - Ứng dụng:
            + Nhận diện khuôn mặt
            + Phát hiện vật thể
            + OCR (nhận dạng chữ trong ảnh)
    3. Generative AI (Sinh nội dung)
        - Transformer là “xương sống” của làn sóng AI tạo sinh.
        - Các mô hình:
            + DALL·E → sinh ảnh từ text
            + Stable Diffusion → tạo ảnh (kết hợp transformer + diffusion)
            + Imagen
        - Ứng dụng:
            + Tạo ảnh, video, âm thanh
            + Thiết kế đồ họa tự động
            + Content marketing
    4. Xử lý âm thanh & giọng nói
        - Transformer giúp cải thiện mạnh speech AI.
        - Các mô hình:
            + Whisper → speech-to-text
            + Wav2Vec 2.0
        - Ứng dụng:
            + Nhận dạng giọng nói
            + Phụ đề tự động
            + Voice assistant
    5. Multimodal (đa phương thức)
        - Kết hợp text + image + audio.
            + Các mô hình:
            + CLIP → hiểu liên kết text–image
            + GPT-4
            + Gemini
        - Ứng dụng:
            + Chat với ảnh
            + Tìm kiếm bằng hình ảnh
            + AI trợ lý thông minh
    6. Khoa học & lĩnh vực chuyên sâu
        - Transformer còn lan sang các lĩnh vực ít ai ngờ:
            + AlphaFold → dự đoán cấu trúc protein
            + Bioinformatics (DNA, RNA)
            + Finance (dự đoán chuỗi thời gian)
            + Robotics (decision transformer)
```
## Architecture Encoder and Decoder
```bash
Input Text
      ↓
Tokenization
      ↓
Embedding + Positional Encoding
      ↓
┌──────────────────────────────┐
│ Encoder (N layers)           │
│  ├─ Self-Attention           │
│  ├─ FFN                      │
│  └─ Add & Norm              │
└──────────────────────────────┘
      ↓
Encoder Output (context vector)
      ↓
┌──────────────────────────────┐
│ Decoder (N layers)           │
│  ├─ Masked Self-Attention    │
│  ├─ Cross-Attention (với Encoder) 
│  ├─ FFN                      │
│  └─ Add & Norm              │
└──────────────────────────────┘
      ↓
Output Text (dịch, sinh câu...)
```
### Positional Encoding
**Ex**
```bash
- Với câu “tôi ăn cơm” Token embedding của Transformer không biết 3 từ này đang ở vị trí 1–2–3 hay 3–2–1, vì attention không có tính tuần tự như RNN. Ta phải cộng thêm 1 vectơ đại diện cho “vị trí số mấy trong câu” → Đó là positional encoding.
- Ví dụ:
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
```
**Formula**
```bash
- Với vị trí pos và chiều vector I:
    + PE(pos, 2i) = sin(pos/10000**(2i/d))
    + PE(pos, 2i+1) = cos(pos/10000**(2i/d)
    -> Tức là token ở vị trí 0,1,2,3,… sẽ có vector chứa sin/cos có tần số khác nhau. Mỗi chiều dùng tần số khác nhau → mô hình phân biệt được vị trí.
- Công thức nâng cao chuẩn Hugging Face:
    + a**b = e**(b.ln(a)) → 10000**(2i/d) = e**(ln(10000) . (2i/d))
```
**Ex**
```bash
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
```
```python
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
```