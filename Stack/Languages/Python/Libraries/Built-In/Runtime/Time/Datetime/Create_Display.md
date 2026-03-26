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