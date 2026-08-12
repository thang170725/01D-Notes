- [<<Back](../Base.md)

- [Practices>>](Practices.md)

- [RNN Introduction (Recurrent Neural Network là một kiến trúc mạng neural dùng để xử lý dữ liệu tuần tự (sequential data))](#rnn-introduction-recurrent-neural-network-là-một-kiến-trúc-mạng-neural-dùng-để-xử-lý-dữ-liệu-tuần-tự-sequential-data)
---
# RNN Introduction (Recurrent Neural Network là một kiến trúc mạng neural dùng để xử lý dữ liệu tuần tự (sequential data))
```bash
RNN nhận một chuỗi input và xử lý nó từng phần tử theo thứ tự, đồng thời mang theo một "memory" từ bước trước sang bước sau.
```
**RNN thực sự giải quyết vấn đề gì**
```bash
Nó giải quyết một vấn đề rất quan trọng:
    Làm thế nào để xử lý dữ liệu có thứ tự mà thông tin ở quá khứ ảnh hưởng đến hiện tại?
```
**Ý tưởng**
```bash
Thông tin ở bước t−1 sẽ được kết hợp với đầu vào ở bước t để tạo ra trạng thái mới.

Điều này rất phù hợp với: 
    - Chuỗi văn bản
    - Dữ liệu thời gian (time series)
    - Chuỗi tín hiệu âm thanh, video, …
```
**Vấn đề**
```bash
- RNN quên rất nhanh.
- Không nhớ được thông tin xa.
- Bị vanishing gradient khi chuỗi dài.
- Bạn đọc câu: "Tôi ăn cơm lúc 7h sáng, và đến chiều thì tôi đói." 
    + RNN có thể không nhớ phần trước 7h sáng vì quá xa → mất ngữ cảnh 

→ RNN phù hợp với chuỗi ngắn, hoặc tác vụ đơn giản.
```
**Kiến trúc RNN**
```bash
- Một RNN đơn giản có 3 tham số chính:
Wxh  (input → hidden)
Whh  (hidden → hidden)
Why  (hidden → output)

- Giả sử:
input size = 8
hidden size = 4
output size = 8
```
**Công thức RNN**
```bash
- Hidden state: ℎ𝑡 = 𝑡𝑎𝑛ℎ(𝑊𝑥ℎ.𝑥𝑡 + 𝑊ℎℎ.ℎ𝑡−1 + 𝑏ℎ)
- Output: 𝑦𝑡 = 𝑠𝑜𝑓𝑡𝑚𝑎𝑥(𝑊ℎ𝑦.ℎ𝑡 + 𝑏𝑦)
```