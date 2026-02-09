- [datetime() \& date \& time](#datetime--date--time)
  - [year \& month \& day \& hour \& minute \& second](#year--month--day--hour--minute--second)
- [date.today()](#datetoday)
---
# datetime() & date & time
**Syn**
```bash
a = datetime(year, month, day, hour, minute, second)
```
**Ex: Tạo ngày giờ thủ công**
```python
dt = datetime(2024, 12, 25, 10, 30, 0)
print(dt)
```
```bash
Lấy ngày + giờ hiện tại.
```
```python
now = datetime.now()
print(now)

# 2026-01-12 18:35:10.123456
```
c. Khoảng cách giữa hai ngày
d1 = date(2026, 1, 12)
d2 = date(2026, 1, 1)

delta = d1 - d2
print(delta.days)  # 11

1. So sánh ngày giờ
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
## year & month & day & hour & minute & second
```python
now = datetime.now()

print(now.year)    # năm
print(now.month)   # tháng
print(now.day)     # ngày
print(now.hour)    # giờ
print(now.minute)  # phút
print(now.second)  # giây
```
# date.today()
```bash
Chỉ lấy ngày
```
```python
today = date.today()
print(today) # 2026-01-12
```