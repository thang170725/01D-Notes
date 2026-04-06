- [GPT (Generative Pre-trained Transformer)](#gpt-generative-pre-trained-transformer)
---
# GPT (Generative Pre-trained Transformer)
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
