# Introduction
```bash
👉 Hiểu đơn giản:
    Naive Bayes thuộc Supervised Learning (học có giám sát) là thuật toán dùng xác suất để đoán một thứ thuộc lớp nào.

💡 Ý tưởng chính (rất quan trọng):
    Naive Bayes dựa trên: 👉 “Nếu biết các đặc điểm, thì xác suất nó thuộc lớp A là bao nhiêu?”
```
**Formula**
```bash
P(A|B) = (P(B|A)*P(A))/P(B)
```
**Ex**
```bash
Bạn muốn biết email là Spam hay Không Spam
Email có từ:
- “giảm giá”
- “free”
- “khuyến mãi”

🧠 Naive Bayes làm gì?
    Nó tính:
        - Xác suất email là Spam khi thấy từ “free”
        - Xác suất email là Spam khi thấy “giảm giá”
        - Xác suất kết hợp tất cả lại
    👉 rồi chọn cái xác suất cao nhất
```
