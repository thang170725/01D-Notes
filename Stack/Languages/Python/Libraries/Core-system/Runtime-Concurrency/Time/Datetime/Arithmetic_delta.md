- [timedelta()](#timedelta)
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

