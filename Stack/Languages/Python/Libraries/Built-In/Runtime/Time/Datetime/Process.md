- [timedelta()](#timedelta)
- [.strftime() \& .strptime()](#strftime--strptime)
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

