- [PhoBERT là một lựa chọn mạnh, nhưng không nhất thiết là lựa chọn tối ưu nếu mục tiêu chính là tốc độ.](#phobert-là-một-lựa-chọn-mạnh-nhưng-không-nhất-thiết-là-lựa-chọn-tối-ưu-nếu-mục-tiêu-chính-là-tốc-độ)
---
# PhoBERT Introduction
**PhoBERT phù hợp nhất khi nào?**
```bash
- Email viết tiếng Việt và câu chữ phức tạp.
- Các Intent có nội dung gần giống nhau, khó phân biệt bằng keyword.
- Người dùng diễn đạt cùng một yêu cầu theo rất nhiều cách.
- Dataset đã có đủ dữ liệu được gán nhãn để fine-tune.
- Bạn ưu tiên accuracy hơn latency.
```
**Ưu điểm**
```bash
- 🇻🇳 Tối ưu cho tiếng Việt	Hiểu tiếng Việt tốt
- 🧠 Hiểu ngữ cảnh	Không chỉ nhìn từng keyword
- 🎯 Accuracy cao	Có thể phân biệt Intent gần nhau
- 🔀 Xử lý cách diễn đạt đa dạng	Người dùng viết mỗi người một kiểu
- 🔧 Fine-tune được	Có thể train theo Intent riêng của hệ thống
```
**Nhược điểm**
```bash
- chậm
- Tốn tài nguyên hơn
- Cần dataset tốt
- Deploy phức tạp hơn
```