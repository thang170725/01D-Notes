- [timedelta()](#timedelta)
- [.strftime() \& .strptime()](#strftime--strptime)
- [Create](#create)
  - [datetime()](#datetime)
- [Display (cung cấp thông tin)](#display-cung-cấp-thông-tin)
  - [.now()](#now)
  - [.weekday()](#weekday)
- [date.today()](#datetoday)
  - [timezone.utc](#timezoneutc)
---
# timedelta()
**Syn**
```bash
timedelta(
    days=0,
    seconds=0,
    microseconds=0,
    milliseconds=0,
    minutes=0,
    hours=0,
    weeks=0
)
```
**Ex1: Cộng / trừ ngày**
```python
today = date.today()
tomorrow = today + timedelta(days=1)
yesterday = today - timedelta(days=1)
```
**Ex2: Cộng giờ, phút**
```python
now = datetime.now()
after_2_hours = now + timedelta(hours=2)
```
# .strftime() & .strptime()
```bash
- strftime  : Chuyển datetime → chuỗi
- strptime  : Chuyển chuỗi → datetime
```
**Syn**
```bash
- %Y    : Năm (2026)
- %m    : Tháng (01)
- %d    : Ngày (12)
- %H    : Giờ (00–23)
- %M    : Phút
- %S    : Giây
**Ex1: strftime**
```python
now = datetime.now()
formatted = now.strftime("%d/%m/%Y %H:%M:%S")
print(formatted) # 12/01/2026 18:35:10
```
**Ex2: strptime**
```python
s = "12/01/2026 18:35:10"
dt = datetime.strptime(s, "%d/%m/%Y %H:%M:%S")
print(dt)
```
- [timedelta()](#timedelta)
- [.strftime() \& .strptime()](#strftime--strptime)
- [Create](#create)
  - [datetime()](#datetime)
- [Display (cung cấp thông tin)](#display-cung-cấp-thông-tin)
  - [.now()](#now)
  - [.weekday()](#weekday)
- [date.today()](#datetoday)
  - [timezone.utc](#timezoneutc)
---
# Create
## datetime() 
```bash
Tạo ra ngày giờ thủ công.
```
**Ex: Tạo ngày giờ thủ công**
```python
dt = datetime(2024, 12, 25, 10, 30, 0)
print(dt)
```
# Display (cung cấp thông tin)
## .now()
```bash
Lấy thời gian hiện tại.
```
**Ex**
```python
from datetime import datetime

now = datetime.now()

print(now) # 2026-01-12 18:35:10.123456
```
## .weekday()
**Ex**
```python
from datetime import datetime

date_obj = datetime.now()
weekday = date_obj.weekday()

print(weekday) # 2 (thứ 4 thì trả về 2)
```
# date.today()
```bash
Chỉ lấy ngày
```
```python
today = date.today()
print(today) # 2026-01-12
```
## timezone.utc
```bash
Lấy thời gian theo timezone
```
```python
from datetime import datetime, timezone

now_utc = datetime.now(timezone.utc)

print(now_utc) # 2026-02-08 12:34:56.123456+00:00
```