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
làm sao để phân biệt được cpu nào mạnh, cpu nào yếu dựa vào tên của nó tôi biết mỗi cpu amd, itel i5,i7,i9 
Có, và nếu bạn hiểu cách đọc tên CPU, bạn có thể đoán tương đối chính xác CPU nào mạnh/yếu mà chưa cần xem benchmark.

Nhưng có một cái bẫy rất lớn:

Không được chỉ nhìn i5 < i7 < i9.

Ví dụ một i5 đời mới hoàn toàn có thể mạnh hơn i7 đời cũ.

1. Trước tiên: đọc tên CPU

Ví dụ Intel:

Intel Core i7-13700H
             ↑   ↑
           đời  phân khúc

AMD:

Ryzen 7 7840HS
       ↑   ↑
    phân khúc đời/model

Bạn cần nhìn 3 thứ:

CPU
│
├── Tier      → i3/i5/i7/i9 hoặc Ryzen 3/5/7/9
├── Generation→ đời CPU
└── Suffix    → U/H/HS/HX/K/F/... 

Trong đó generation + suffix cực kỳ quan trọng.

2. Intel: i3 < i5 < i7 < i9 — nhưng chỉ khi cùng thế hệ

Ví dụ:

i3-14100
i5-14400
i7-14700
i9-14900

Nếu cùng thế hệ và cùng dòng:

i3 < i5 < i7 < i9

thường là đúng.

Nhưng:

i7-7700

vs

i5-14600

thì i5-14600 mạnh hơn rất nhiều.

Vì:

i7     → tier
7700   → đời 7

còn:

i5     → tier
14600  → đời 14

Đời CPU quan trọng hơn cái i5/i7/i9 nếu khoảng cách thế hệ lớn.

3. Intel nhìn số như thế nào?

Ví dụ:

Intel Core i7-13700H
               ↑
               13

13 = thế hệ 13.

Ví dụ:

i5-12400
i5-13400
i5-14400

→ thế hệ 12 → 13 → 14.

Thông thường:

14400 > 13400 > 12400

nếu cùng dòng và điều kiện tương đương.

4. Nhưng hậu tố mới là thứ cực kỳ quan trọng

Ví dụ laptop:

Intel Core i7-1365U
Intel Core i7-13700H

Đều là:

i7
13th gen

nhưng 13700H mạnh hơn đáng kể.

Intel suffix thường gặp
Hậu tố	Ý nghĩa đơn giản
U	tiết kiệm điện, laptop mỏng nhẹ
P	laptop, cân bằng hiệu năng/điện
H	hiệu năng cao
HX	hiệu năng rất cao
K	desktop, mở khóa ép xung
F	không có iGPU
T	tiết kiệm điện

Ví dụ:

i7-13700U
i7-13700H
i7-13700HX

thường:

U < H < HX

về hiệu năng đa nhân.

5. AMD cũng tương tự

Ví dụ:

Ryzen 3
Ryzen 5
Ryzen 7
Ryzen 9

thường:

3 < 5 < 7 < 9

nhưng vẫn phải nhìn đời + model + suffix.

Ví dụ:

Ryzen 5 5600
Ryzen 5 7600
Ryzen 5 9600

thường:

9600 > 7600 > 5600
6. AMD laptop có một cái bẫy cực lớn

AMD đặt tên CPU laptop khá khó đọc.

Ví dụ:

Ryzen 7 7735HS

Không phải cứ thấy 7000 là kiến trúc mới hoàn toàn.

AMD có những dòng mà số model mới nhưng kiến trúc bên trong không mới tương ứng.

Cho nên với AMD laptop, chỉ nhìn:

Ryzen 7 7735HS

chưa đủ.

Bạn nên xem kiến trúc Zen và benchmark nếu đang mua máy.

7. Một thứ rất quan trọng: số core/thread

Ví dụ:

CPU A
6 cores / 12 threads

CPU B
12 cores / 20 threads

Trong các tác vụ chạy song song:

CPU B

thường mạnh hơn đáng kể.

Đặc biệt với:

compile code
Docker
render
video encoding
machine learning preprocessing
chạy VM
multitasking

thì số core rất quan trọng.

8. Nhưng đừng nghĩ nhiều core = luôn mạnh

Ví dụ:

CPU A:
4 cores
4.5 GHz

CPU B:
8 cores
3.5 GHz

Không thể chỉ nhìn:

8 > 4

rồi kết luận B nhanh gấp đôi.

Còn:

IPC
architecture
cache
power limit
thermal
boost clock
memory
workload
9. Nếu chỉ nhìn tên, hãy dùng công thức này

Khi thấy:

Ryzen 7 7840HS

hãy đọc:

Ryzen
 ↓
7              → phân khúc
 ↓
7840           → model/generation
 ↓
HS             → hiệu năng cao cho laptop

Intel:

Core i7-13700HX
      ↓
     i7       → phân khúc
      ↓
     13xxx    → thế hệ
      ↓
      HX      → hiệu năng rất cao
10. Một cheat sheet rất nhanh

Nếu đứng trước một đống laptop và chỉ có 30 giây, nhìn theo thứ tự:

Bước 1 — Tier
Intel:
i3 < i5 < i7 < i9

AMD:
Ryzen 3 < 5 < 7 < 9
Bước 2 — Generation
i5-12400
i5-13400
i5-14400

→ ưu tiên đời mới hơn.

Bước 3 — Suffix

Laptop:

U
↓
H / HS
↓
HX

thường là từ tiết kiệm điện → hiệu năng cao.

Bước 4 — Core/thread

Nếu bạn thấy:

6C/12T

vs

14C/20T

thì CPU thứ hai thường có lợi thế rất lớn trong workload đa luồng.

11. Ví dụ để bạn luyện mắt

Giả sử có 4 CPU:

A: Intel i7-7700
B: Intel i5-12400
C: Intel i7-12700H
D: AMD Ryzen 7 7840HS

Không được nghĩ:

i7
i5
i7
Ryzen 7

→ i7 chắc mạnh nhất

Mà phải đọc:

i7-7700
→ rất cũ

i5-12400
→ đời 12 desktop

i7-12700H
→ đời 12 + H

Ryzen 7 7840HS
→ Ryzen 7 + HS

Sau đó mới so architecture, core/thread, power limit và benchmark.

Và có một điều bạn nên nhớ

Nếu bạn đang hỏi cái này vì định mua máy / chọn máy công ty, thì đừng cố đoán hiệu năng bằng tên CPU đến cùng.

Tên CPU chỉ giúp bạn lọc nhanh 70–80%.

Khi cần quyết định thật sự, hãy xem:

CPU
├── Architecture
├── Core / Thread
├── Base / Boost
├── Cache
├── TDP / Power
└── Benchmark

Đặc biệt với laptop, cùng một CPU nhưng máy A có tản nhiệt tốt và cho CPU chạy 80W có thể nhanh hơn máy B dùng cùng CPU nhưng giới hạn 35W.

Nếu bạn muốn, tôi có thể làm cho bạn một “
bảng giải mã tên CPU Intel + AMD từ A→Z”, kiểu nhìn i7-14700K, i5-13400F, Ryzen 7 7800X3D, Ryzen 9 7945HX là đọc được ngay CPU đó thuộc loại nào và mạnh đến đâu.
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