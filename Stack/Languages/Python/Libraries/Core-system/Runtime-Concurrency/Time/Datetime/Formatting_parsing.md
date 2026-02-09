- [strftime](#strftime)
- [12/01/2026 18:35:10](#12012026-183510)
---
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
