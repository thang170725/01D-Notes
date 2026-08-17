- [.time()](#time)
- [.sleep()](#sleep)
- [trả về giờ hiện tại](#trả-về-giờ-hiện-tại)
- [khi bấm lc xong chấm sẽ xuất hiện ra các thuộc tính của hàm này](#khi-bấm-lc-xong-chấm-sẽ-xuất-hiện-ra-các-thuộc-tính-của-hàm-này)
- [.perf\_counter() (Dùng để đo thời gian chính xác cao (tính cả thời gian ngủ/ sleep))](#perf_counter-dùng-để-đo-thời-gian-chính-xác-cao-tính-cả-thời-gian-ngủ-sleep)
- [Đọc ảnh](#đọc-ảnh)
- [Resize](#resize)
- [Detect](#detect)
---
# .time()
Trả về thời gian hiện tại (timesstamp) tính bằng giây kể từ 1/1/1970 (UNIX epoch).
**Ex**
```python
import time
now = time.time()
print("timestamp hiện tại:", now) # 1744879502.9250693
```

# .sleep()
Tạm dừng chương trình trong một khoảng thời gian (tính bằng giây).
**Ex**
```python
import time
print("đây là tao trước 5s")
time.sleep(5)
print("đây là tao sau 5s") # sau 5 giây mới hiện ra câu này

# đây là tao trước 5s
# đây là tao sau 5s
```

localtime()
Trả về struct_time của thời gian hiện tại (hoặc từ timestamp).
import time
lc = time.localtime()
# trả về giờ hiện tại
print(lc.tm_hour, lc.tm_min, lc.tm_sec)
# khi bấm lc xong chấm sẽ xuất hiện ra các thuộc tính của hàm này
15 56 36
strftime()
Định dạng thời gian thành chuỗi (string) theo format.
gmtime()
Giống localtime nhưng trả về thời gian UTC (GMT).
ctime()
Chuyển timestamp thành một chuỗi dễ đọc.
# .perf_counter() (Dùng để đo thời gian chính xác cao (tính cả thời gian ngủ/ sleep))
```bash
Đây là hàm chính xác nhất để đo thời gian thực thi của một đoạn code trong Python vì nó có độ phân giải rất cao (micro/nanosecond tùy hệ điều hành).
```
**Syn**
```bash
import time

start = time.perf_counter()

# Đoạn code cần đo
for i in range(1000000):
    pass

end = time.perf_counter()

print(f"Thời gian: {end - start:.6f} giây") # Thời gian: 0.021534 giây
```
Đo tốc độ của YOLO

Giả sử:

import time

start = time.perf_counter()

results = model.predict(image)

end = time.perf_counter()

print(f"YOLO mất: {(end-start)*1000:.2f} ms")

Nếu in ra

YOLO mất: 132.56 ms

thì nghĩa là detect một ảnh mất khoảng 132 ms.

Đo từng bước

Đây là cách bạn nên làm để tìm bottleneck.

import time

# Đọc ảnh
t0 = time.perf_counter()
img = cv2.imread(path)
t1 = time.perf_counter()

# Resize
img = cv2.resize(img, (1280, 1280))
t2 = time.perf_counter()

# Detect
results = model.predict(img)
t3 = time.perf_counter()

print(f"Đọc ảnh : {(t1-t0)*1000:.2f} ms")
print(f"Resize  : {(t2-t1)*1000:.2f} ms")
print(f"YOLO    : {(t3-t2)*1000:.2f} ms")
print(f"Tổng    : {(t3-t0)*1000:.2f} ms")

Ví dụ:

Đọc ảnh : 18.45 ms
Resize  : 7.81 ms
YOLO    : 128.30 ms
Tổng    : 154.56 ms

Lúc này bạn sẽ biết phần nào chậm.

Đo nhiều lần để lấy trung bình

Một lần đo có thể bị dao động, nên thường đo nhiều lần.

import time

times = []

for _ in range(20):
    start = time.perf_counter()
    model.predict(img, verbose=False)
    end = time.perf_counter()

    times.append(end - start)

print(f"Trung bình: {sum(times)/len(times)*1000:.2f} ms")
So sánh với time.time()
Hàm	Độ chính xác	Nên dùng
time.time()	Thấp hơn	Lấy thời gian hiện tại
time.perf_counter()	Rất cao	✅ Benchmark tốc độ
time.process_time()	Chỉ tính thời gian CPU	Ít dùng để benchmark AI

Đối với việc tối ưu pipeline PDF → JPEG → Resize → YOLO như bạn đang làm, time.perf_counter() là lựa chọn phù hợp nhất để đo thời gian của từng bước và xác định chính xác nút thắt hiệu năng.
process_time()
Đo thời gian CPU thực thi (không tính thời gian sleep).