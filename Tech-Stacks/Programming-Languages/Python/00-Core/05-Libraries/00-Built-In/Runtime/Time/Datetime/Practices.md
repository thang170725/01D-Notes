- [cộng 2 thời gian](#cộng-2-thời-gian)
---
# cộng 2 thời gian
```python
from datetime import datetime, timedelta

time1 = datetime.strptime('12:45:45', '%H:%M:%S')
time2 = datetime.strptime('21:02:12', '%H:%M:%S')

res = timedelta(
    hours=time1.hour + time2.hour,
    minutes=time1.minute + time2.minute,
    seconds=time1.second + time2.second
)

days = res.days
h = res.seconds // 3600
m = res.seconds // 60 % 60
s = res.seconds % 60

print(f"{days:02d}:{h:02d}:{m:02d}:{s:02d}")
```
