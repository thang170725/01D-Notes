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