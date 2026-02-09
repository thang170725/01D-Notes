# interpreter
- Dịch và chạy từng dòng
- Sử dụng trong Python, interpreter dịch đến đâu, chạy đến đó (không tạo file mã máy riêng, lỗi dòng 100, 99 dòng trước vẫn chạy)
- Python đánh đổi tốc độ để lấy dễ dùng nên sử dụng interpreter

# compiler
- dịch ngôn ngữ lập trình (chuyển từ thứ con người viết -> thứ máy hiểu)
- Sử dụng trong C++, compliler dịch trước (dịch xong hết rồi mới chạy) -> chạy nhanh, lỗi cú pháp biết ngay từ đầu
**Ex**
z = x + y
compiler biến code thành kiểu
```text
LOAD  R1, [0x7ffd1234]   ; x
LOAD  R2, [0x7ffd1238]   ; y
ADD   R3, R1, R2
STORE [0x7ffd1240], R3  ; z
```

# cpu
**cấu trúc**
1. ALU
    Là một mạch điện (có điện -> 1, không điện -> 0)

# ram
**cấu trúc**
1. Code segment: Mã máy do compiler tạo ra
2. Data: Lưu biến toàn cục đã khởi tạo, dữ liệu này sẽ cố định ngay khi compile
   Ví dụ: int g = 10;  // biến toàn cục khởi tạo → data segment
3. BSS: lưu biến toàn cục chưa khởi tạo
   Ví dụ: int h;  // biến toàn cục chưa khởi tạo → BSS
4. Heap: Dùng để cấp phát bộ nhớ động, OS cấp vùng nhớ -> CPU đọc/ghi
5. Stack: Lưu biến cục bộ của hàm, địa chỉ trả về