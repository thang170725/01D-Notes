Stack là gì?

Stack = bộ nhớ cho lời gọi hàm

Đặc điểm:

Lưu:

Biến cục bộ

Tham số hàm

Return address

Tự động cấp phát / giải phóng

Rất nhanh

Có kích thước giới hạn

Nguyên tắc:
👉 LIFO (Last In – First Out)

Ví dụ:

void f() {
    int x = 10; // nằm trên stack
}


Khi f() kết thúc → x biến mất

🔹 Heap là gì?

Heap = bộ nhớ cấp phát động

Đặc điểm:

Dùng cho dữ liệu sống lâu

Do lập trình viên quản lý (malloc / new)

Chậm hơn stack

Dễ lỗi nếu quản lý sai

Ví dụ:

int* p = malloc(sizeof(int)); // heap


👉 p tồn tại cho tới khi free()

🔥 So sánh Stack vs Heap
Stack	Heap
Tự động	Thủ công
Nhanh	Chậm
Kích thước nhỏ	Rất lớn
An toàn	Dễ leak
Mỗi thread có stack	Chia sẻ giữa thread
🔥 Vì sao hacker quan tâm stack/heap?

Stack overflow → chiếm quyền thực thi

Heap overflow / use-after-free → RCE

Buffer overflow là nền tảng hacking cổ điển

👉 Đây là kiến thức bắt buộc nếu học security / low-level.

3️⃣ System Call là gì? (mức khái niệm)
🔹 Vấn đề: chương trình không được làm mọi thứ

Chương trình user KHÔNG ĐƯỢC:

Truy cập ổ cứng trực tiếp

Tạo process khác

Gửi gói mạng

Đụng vào phần cứng

👉 Vì nguy hiểm

🔹 System Call là gì?

System call = cổng an toàn để chương trình nói chuyện với kernel

Kernel = lõi hệ điều hành
User program = chạy ở user mode

📌 System call cho phép:

Đọc / ghi file

Tạo process (fork)

Tạo thread

Cấp phát bộ nhớ

Giao tiếp mạng

Ví dụ:

read()
write()
open()
fork()
execve()

🔐 Phân tầng quyền:
User Mode
  ↓ (system call)
Kernel Mode


👉 Chỉ kernel mới được:

Đụng phần cứng

Quản lý memory

Quản lý process

🔥 Hacker nhìn system call như thế nào?

Hook system call

Lợi dụng bug kernel

Privilege Escalation

👉 90% rootkit = thao túng system call

4️⃣ Tổng kết nhanh (bản não bộ)

Process: chương trình đang chạy, cách ly

Thread: luồng thực thi trong process

Stack: bộ nhớ cho hàm, nhanh, tự động

Heap: bộ nhớ động, sống lâu

System call: cầu nối user ↔ kernel