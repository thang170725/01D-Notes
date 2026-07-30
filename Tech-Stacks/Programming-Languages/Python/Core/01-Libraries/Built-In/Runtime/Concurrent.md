Đây là một trong những phần khó nhất khi mới học Python. Mình sẽ giải thích bằng ví dụ đời thường trước, sau đó mới đến code.

from concurrent.futures import ProcessPoolExecutor, as_completed

Có 2 thứ:

ProcessPoolExecutor
as_completed
1. ProcessPoolExecutor dùng để làm gì?

Nó dùng để chạy nhiều công việc cùng lúc bằng nhiều tiến trình (process).

Ví dụ đời thường.

Giả sử bạn có 10 quyển sách cần scan.

Cách 1: Một người làm
Người 1

Sách 1
↓

Sách 2
↓

Sách 3
↓

...

↓

Sách 10

Tổng thời gian: 10 phút

Cách 2: Có 5 người
Người 1 → Sách 1
Người 2 → Sách 2
Người 3 → Sách 3
Người 4 → Sách 4
Người 5 → Sách 5

Sau khi xong

Người 1 → Sách 6
Người 2 → Sách 7
...

Tổng thời gian chỉ khoảng 2 phút.

ProcessPoolExecutor chính là người quản lý việc chia công việc cho nhiều "người làm" (process).

Ví dụ đơn giản nhất

Giả sử mỗi công việc mất 2 giây.

from concurrent.futures import ProcessPoolExecutor
import time

def work(x):
    time.sleep(2)
    return x * x

with ProcessPoolExecutor(max_workers=4) as executor:
    results = executor.map(work, [1, 2, 3, 4])

print(list(results))

Kết quả

[1, 4, 9, 16]

Nếu chạy bình thường

2s
↓

2s
↓

2s
↓

2s

Tổng

8 giây

Còn dùng 4 process

2s

1 2 3 4 cùng chạy

Tổng

≈2 giây
2. submit()

Thường người ta không dùng map() mà dùng

future = executor.submit(work, 5)

Nó giống như

"Đây là một công việc, nhờ process làm giúp."

Ví dụ

future = executor.submit(work, 5)

Process bắt đầu chạy.

Trong khi đó chương trình chính vẫn tiếp tục.

3. Future là gì?

submit() trả về

Future

Nó giống như một phiếu hẹn.

Ví dụ

Bạn mang quần áo đi giặt.

Tiệm đưa bạn

Phiếu số 18

Quần áo chưa xong.

Nhưng bạn giữ phiếu.

Sau này

future.result()

chính là

"Đưa phiếu đây, lấy đồ."

Ví dụ

future = executor.submit(work, 5)

print("Đang chờ...")

print(future.result())

Kết quả

Đang chờ...

25
4. as_completed

Đây là phần nhiều người nhầm.

Giả sử có 3 công việc

A mất 5 giây

B mất 2 giây

C mất 3 giây

Nếu bạn

future1.result()

future2.result()

future3.result()

thì

đợi A

↓

mới đến B

↓

mới đến C

Mặc dù B làm xong từ lâu.

as_completed() thì khác.

Nó nói rằng

"Thằng nào làm xong trước thì trả kết quả trước."

Ví dụ

from concurrent.futures import ProcessPoolExecutor, as_completed
import time

def work(sec):
    time.sleep(sec)
    return sec

with ProcessPoolExecutor() as executor:

    futures = [
        executor.submit(work, 5),
        executor.submit(work, 2),
        executor.submit(work, 3),
    ]

    for future in as_completed(futures):
        print(future.result())

Kết quả

2

3

5

Không phải

5

2

3

vì as_completed() không quan tâm thứ tự gửi, mà quan tâm thứ tự hoàn thành.

Minh họa

Giả sử có ba nhân viên.

A nhận việc đầu tiên

B nhận việc thứ hai

C nhận việc thứ ba

Nhưng tốc độ khác nhau.

A ======== 8 phút

B == 2 phút

C ==== 4 phút

Không dùng as_completed

Đợi A

↓

Lấy A

↓

Lấy B

↓

Lấy C

Có dùng as_completed

B xong

↓

Lấy B

↓

C xong

↓

Lấy C

↓

A xong

↓

Lấy A
Trong xử lý PDF của bạn

Bạn đang xử lý hàng trăm file PDF.

Không dùng ProcessPoolExecutor

PDF1

↓

PDF2

↓

PDF3

↓

...

Chỉ một CPU làm việc.

Có ProcessPoolExecutor

CPU1 → PDF1

CPU2 → PDF2

CPU3 → PDF3

CPU4 → PDF4

Các CPU xử lý song song.

Sau đó

for future in as_completed(futures):

nghĩa là

PDF nào xử lý xong

↓

lưu kết quả luôn

↓

không cần đợi các PDF khác
Tóm tắt
ProcessPoolExecutor: tạo một "nhóm công nhân" (các process) để chạy nhiều công việc song song, rất phù hợp với các tác vụ nặng về CPU như xử lý ảnh, PDF, tính toán,...
as_completed: duyệt qua các công việc theo thứ tự hoàn thành, không phải theo thứ tự bạn giao việc. Nhờ vậy, bạn có thể xử lý hoặc lưu kết quả ngay khi từng công việc xong mà không phải chờ công việc chậm nhất. Đây là lý do nó thường được dùng cùng submit() khi xử lý nhiều file độc lập.