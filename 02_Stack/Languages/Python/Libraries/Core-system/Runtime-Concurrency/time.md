- Được dung để làm việc với thời gian, như đo thời gian thực thi, lấy thời gian hiện tại, tạo độ trễ (delay), định dạng thời gian, v.v. 
- Thư viện không cần tải. Cần import time

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
perf_counter()
Dùng để đo thời gian chính xác cao (tính cả thời gian ngủ/ sleep). Rất hữu ích để đo hiệu suất.
process_time()
Đo thời gian CPU thực thi (không tính thời gian sleep).