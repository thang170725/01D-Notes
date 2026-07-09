# Introduction
```bash
👉 Hiểu đơn giản:
    Kernel SVM = SVM nhưng có “phép biến đổi dữ liệu” để xử lý dữ liệu KHÔNG tách được bằng đường thẳng
```
**tại sao cần dùng kernel SVM**
```bash
Tìm một đường thẳng / mặt phẳng để chia dữ liệu thành 2 nhóm rõ ràng.   
    ❌ Vấn đề: Có dữ liệu không thể chia bằng đường thẳng.

    Ví dụ:
        - điểm xanh ở giữa
        - điểm đỏ bao quanh
        👉 Không thể vẽ 1 đường thẳng để tách

Kernel SVM làm gì?
    👉 Nó dùng “kernel trick” để:
        biến dữ liệu từ 2D → 3D (hoặc không gian cao hơn) → rồi mới tách bằng mặt phẳng
        Sau đó lại “chiếu ngược” về 2D.
```
**Ex**
```bash
🟢 Trường hợp:
    - Hình tròn xanh ở giữa
    - Vòng đỏ bao quanh

Trong 2D:
    ❌ không thể tách bằng đường thẳng

💡 Kernel trick:
    - Nó “nâng dữ liệu lên”:
        + điểm ở giữa được nâng lên cao
        + điểm vòng ngoài vẫn thấp
    👉 lúc này có thể dùng mặt phẳng cắt ngang
```