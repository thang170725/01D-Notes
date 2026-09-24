- [Chuẩn hoá thời gian](#chuẩn-hoá-thời-gian)
- [Cộng hai thời điểm](#cộng-hai-thời-điểm)
---
# Chuẩn hoá thời gian
```bash
Cho một khoảng thời gian được nhập dưới dạng số giây. Hãy chuyển đổi khoảng thời gian đó sang dạng: Giờ : Phút : Giây
```
```python 
t = int(input())
print(f"{t//3600:02d}:{t//60%60:02d}:{t%60:02d}")
```
# Cộng hai thời điểm
```bash
1. Cho hai thời điểm trong ngày, mỗi thời điểm có dạng: hh mm ss
2. Hãy cộng hai thời điểm này lại với nhau và in ra thời điểm kết quả theo định dạng: hh:mm:ss
3. Nếu thời gian vượt quá 24 giờ thì quay vòng trong ngày.
4. Ví dụ: 23:59:30 + 00:00:45 = 24:00:15. Quay vòng → 00:00:15
```
**Ex1**
```python
time = [list(map(int, input().split(':'))) for _ in range(2)]

s = (time[0][2] + time[1][2]) % 60
carry_m = (time[0][2] + time[1][2]) // 60

m = (time[0][1] + time[1][1] + carry_m) % 60
carry_h = (time[0][1] + time[1][1] + carry_m) // 60

h = (time[0][0] + time[1][0] + carry_h) % 24

print(f"{h:02d}:{m:02d}:{s:02d}")
```
**Ex2**
```python
t1 = list(map(int, input().split(':')))
t2 = list(map(int, input().split(':')))

total = (t1[0]*3600 + t1[1]*60 + t1[2] +
         t2[0]*3600 + t2[1]*60 + t2[2]) % 86400

print(f"{total//3600:02d}:{total//60%60:02d}:{total%60:02d}")
```