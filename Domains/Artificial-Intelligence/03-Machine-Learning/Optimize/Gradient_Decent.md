Batch Gradient Descent
Dùng toàn bộ dataset mỗi bước
Ổn định nhưng chậm
🔹 2. Stochastic Gradient Descent (SGD)
Cập nhật từng sample
Nhanh hơn nhưng nhiễu
🔹 3. Mini-batch Gradient Descent (phổ biến nhất)
Dùng batch nhỏ (32, 64, 128…)
Cân bằng giữa tốc độ và ổn định
4. Các thuật toán cải tiến (quan trọng nhất)

Đây là phần giải quyết đúng vấn đề bạn lo:

🚀 Momentum
Thêm “quán tính” để không bị zig-zag
Đi nhanh hơn theo hướng đúng
🚀 RMSProp
Điều chỉnh learning rate theo từng tham số
Giúp xử lý vùng dốc/phẳng khác nhau
🚀 Adam (rất phổ biến)
Kết hợp Momentum + RMSProp
Tự động điều chỉnh bước đi

👉 Đây là cái bạn nên dùng trong thực tế