# Process (tiến trình)
Process = một chương trình đang chạy

Khi bạn chạy:

Chrome

VS Code

Python script

👉 Mỗi cái đó là một process.

Đặc điểm của process:

Có không gian bộ nhớ riêng biệt

Có:

Code

Data

Stack

Heap

Process không thể truy cập trực tiếp bộ nhớ của process khác

👉 Hệ điều hành cách ly process để:

Tăng ổn định

Tăng bảo mật
(Một process crash không làm sập process khác)

Ví dụ đời thường:

Process giống như mỗi căn nhà riêng

Nhà nào có đồ đạc nhà nấy

Muốn nói chuyện phải gọi điện (IPC)

# Thread (luồng)

Thread = đơn vị thực thi nhỏ nhất bên trong process

Một process có thể có nhiều thread.

Các thread trong cùng process:

✅ Chia sẻ chung bộ nhớ (heap, global variables)

❌ Mỗi thread có stack riêng

Đặc điểm:

Nhẹ hơn process

Tạo nhanh hơn

Giao tiếp với nhau rất nhanh

Nhưng dễ gây lỗi race condition

Ví dụ:

Chrome có nhiều tab:

Mỗi tab = thread (hoặc nhóm thread)

Game:

1 thread render

1 thread xử lý input

1 thread AI
Hacker rất thích lỗi thread (race condition, deadlock).