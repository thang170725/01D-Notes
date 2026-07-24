- [Computer Introduction (tất tần tật về máy tính)](#computer-introduction-tất-tần-tật-về-máy-tính)
- [Cách máy tính thao tác với những dòng code](#cách-máy-tính-thao-tác-với-những-dòng-code)
  - [interpreter (Dịch và chạy từng dòng)](#interpreter-dịch-và-chạy-từng-dòng)
  - [compiler (dịch ngôn ngữ lập trình (chuyển từ thứ con người viết -\> thứ máy hiểu))](#compiler-dịch-ngôn-ngữ-lập-trình-chuyển-từ-thứ-con-người-viết---thứ-máy-hiểu)
  - [System Call (cổng an toàn để chương trình nói chuyện với kernel = lõi hệ điều hành)](#system-call-cổng-an-toàn-để-chương-trình-nói-chuyện-với-kernel--lõi-hệ-điều-hành)
  - [Process (tiến trình = một chương trình đang chạy)](#process-tiến-trình--một-chương-trình-đang-chạy)
  - [Thread (luồng = đơn vị thực thi nhỏ nhất bên trong process)](#thread-luồng--đơn-vị-thực-thi-nhỏ-nhất-bên-trong-process)
- [Computer Component (thành phần máy tính)](#computer-component-thành-phần-máy-tính)
  - [cpu](#cpu)
  - [ram](#ram)
  - [Heap (bộ nhớ cấp phát động)](#heap-bộ-nhớ-cấp-phát-động)
  - [Stack (bộ nhớ cho lời gọi hàm)](#stack-bộ-nhớ-cho-lời-gọi-hàm)
- [Ask (Câu hỏi)](#ask-câu-hỏi)
  - [Vì sao hacker quan tâm stack/heap?](#vì-sao-hacker-quan-tâm-stackheap)
---
# Computer Introduction (tất tần tật về máy tính)
# Cách máy tính thao tác với những dòng code
## interpreter (Dịch và chạy từng dòng)
**Ex: python**
```bash
trong Python, interpreter dịch đến đâu, chạy đến đó (không tạo file mã máy riêng, lỗi dòng 100, 99 dòng trước vẫn chạy)
Python đánh đổi tốc độ để lấy dễ dùng nên sử dụng interpreter
```
## compiler (dịch ngôn ngữ lập trình (chuyển từ thứ con người viết -> thứ máy hiểu))
```bash
Sử dụng trong C++, compliler dịch trước (dịch xong hết rồi mới chạy) -> chạy nhanh, lỗi cú pháp biết ngay từ đầu
```
**Ex**
```bash
z = x + y # compiler biến code thành kiểu

LOAD  R1, [0x7ffd1234]   ; x
LOAD  R2, [0x7ffd1238]   ; y
ADD   R3, R1, R2
STORE [0x7ffd1240], R3  ; z
```
## System Call (cổng an toàn để chương trình nói chuyện với kernel = lõi hệ điều hành)
```bash
Vấn đề: chương trình không được làm mọi thứ
  Chương trình user KHÔNG ĐƯỢC:
    - Truy cập ổ cứng trực tiếp
    - Tạo process khác
    - Gửi gói mạng
    - Đụng vào phần cứng
  👉 Vì nguy hiểm

System call cho phép:
  - Đọc / ghi file
  - Tạo process (fork)
  - Tạo thread
  - Cấp phát bộ nhớ
  - Giao tiếp mạng
  - 🔐 Phân tầng quyền:
    User Mode
      ↓ (system call)
    Kernel Mode
👉 Chỉ kernel mới được:
  - Đụng phần cứng
  - Quản lý memory
  - Quản lý process
```
**🔥 Hacker nhìn system call như thế nào?**
```bash
Lợi dụng bug kernel
  👉 90% rootkit = thao túng system call
```
## Process (tiến trình = một chương trình đang chạy)
```bash
Khi bạn chạy:
  - Chrome
  - VS Code
  - Python script
👉 Mỗi cái đó là một process.

Đặc điểm của process:
  - Có không gian bộ nhớ riêng biệt
  - Có:
    + Code
    + Data
    + Stack
    + Heap

Process không thể truy cập trực tiếp bộ nhớ của process khác
  👉 Hệ điều hành cách ly process để:
    - Tăng ổn định
    - Tăng bảo mật
    - Một process crash không làm sập process khác
```
## Thread (luồng = đơn vị thực thi nhỏ nhất bên trong process)
```bash
Một process có thể có nhiều thread.

Các thread trong cùng process:
  ✅ Chia sẻ chung bộ nhớ (heap, global variables)
  ❌ Mỗi thread có stack riêng

Đặc điểm:
  - Nhẹ hơn process
  - Tạo nhanh hơn
  - Giao tiếp với nhau rất nhanh
  - Nhưng dễ gây lỗi race condition

Ví dụ:
  Chrome có nhiều tab:
    - Mỗi tab = thread (hoặc nhóm thread)

  Game:
    - 1 thread render
    - 1 thread xử lý input
    - 1 thread AI
```
# Computer Component (thành phần máy tính)
## cpu
**cấu trúc**
```bash
1. ALU: Là một mạch điện (có điện -> 1, không điện -> 0)
```
## ram
**cấu trúc**
```bash
1. Code segment: Mã máy do compiler tạo ra
2. Data: Lưu biến toàn cục đã khởi tạo, dữ liệu này sẽ cố định ngay khi compile
   Ví dụ: int g = 10;  // biến toàn cục khởi tạo → data segment
3. BSS: lưu biến toàn cục chưa khởi tạo
   Ví dụ: int h;  // biến toàn cục chưa khởi tạo → BSS
4. Heap: Dùng để cấp phát bộ nhớ động, OS cấp vùng nhớ -> CPU đọc/ghi
5. Stack: Lưu biến cục bộ của hàm, địa chỉ trả về
```
## Heap (bộ nhớ cấp phát động)
```bash
Đặc điểm:
  - Dùng cho dữ liệu sống lâu
  - Do lập trình viên quản lý (malloc / new)
  - Chậm hơn stack
  - Dễ lỗi nếu quản lý sai
```
**Ex**
```c++
int* p = malloc(sizeof(int)); // heap, p tồn tại cho tới khi free()
```
**So sánh Stack vs Heap**
```bash
Stack	                    Heap
Tự động	                  Thủ công
Nhanh	                    Chậm
Kích thước nhỏ            Rất lớn
An toàn	                  Dễ leak
Mỗi thread có stack	      Chia sẻ giữa thread
```
## Stack (bộ nhớ cho lời gọi hàm)
```bash
Đặc điểm:
  Lưu:
    - Biến cục bộ
    - Tham số hàm
    - Return address
  
  Tự động cấp phát / giải phóng
  Rất nhanh
  Có kích thước giới hạn

Nguyên tắc:
  👉 LIFO (Last In – First Out)

Ví dụ:
  void f() {
      int x = 10; // nằm trên stack
  } # Khi f() kết thúc → x biến mất
```
# Ask (Câu hỏi)
## Vì sao hacker quan tâm stack/heap?
```bash
Stack overflow → chiếm quyền thực thi
Heap overflow / use-after-free → RCE
Buffer overflow là nền tảng hacking cổ điển
👉 Đây là kiến thức bắt buộc nếu học security / low-level.
```