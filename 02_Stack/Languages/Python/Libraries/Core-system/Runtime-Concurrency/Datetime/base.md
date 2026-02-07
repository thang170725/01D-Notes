- [Directory Structure](#directory-structure)
- [12/01/2026 18:35:10](#12012026-183510)
---
# Directory Structure
```bash
Datetime/
├── 01_basic_objects.md      # Các đối tượng chính: date, time, datetime (now, today)
├── 02_formatting_parsing.md # Chuyển đổi chuỗi: strftime, strptime (Format codes)
├── 03_arithmetic_delta.md   # Tính toán thời gian: timedelta (Cộng/trừ ngày giờ)
├── 04_timezone_dst.md       # Múi giờ: timezone, zoneinfo (UTC, Local time)
└── 05_timestamp_unix.md     # Làm việc với máy chủ: timestamp, fromtimestamp
```

1. Định dạng ngày giờ (strftime)

👉 Chuyển datetime → chuỗi

now = datetime.now()
formatted = now.strftime("%d/%m/%Y %H:%M:%S")
print(formatted)
# 12/01/2026 18:35:10

Các định dạng hay dùng
Ký hiệu	Ý nghĩa
%Y	Năm (2026)
%m	Tháng (01)
%d	Ngày (12)
%H	Giờ (00–23)
%M	Phút
%S	Giây
6. Chuyển chuỗi → datetime (strptime)

👉 Dùng khi đọc dữ liệu từ file, API, input

s = "12/01/2026 18:35:10"
dt = datetime.strptime(s, "%d/%m/%Y %H:%M:%S")
print(dt)

7. Tính toán ngày giờ với timedelta
a. Cộng / trừ ngày
today = date.today()
tomorrow = today + timedelta(days=1)
yesterday = today - timedelta(days=1)

b. Cộng giờ, phút
now = datetime.now()
after_2_hours = now + timedelta(hours=2)

c. Khoảng cách giữa hai ngày
d1 = date(2026, 1, 12)
d2 = date(2026, 1, 1)

delta = d1 - d2
print(delta.days)  # 11

8. So sánh ngày giờ
d1 = datetime(2026, 1, 12)
d2 = datetime(2026, 1, 10)

print(d1 > d2)  # True

9. Một số hàm hay dùng khác
a. Lấy thứ trong tuần
today = date.today()
print(today.weekday())  # 0=Thứ 2, 6=Chủ nhật

b. Lấy tên thứ
print(today.strftime("%A"))  # Monday, Tuesday...

10. Ví dụ thực tế
Kiểm tra hạn sử dụng
expiry = date(2026, 1, 20)
today = date.today()

if today > expiry:
    print("Hết hạn")
else:
    print("Còn hạn")
