# Nhập một số nguyên có 5 chữ số
```python
import re

while True:
    num = input("Nhập số có 5 chữ số: ")
    # ^: Bắt đầu, \d{5}: đúng 5 chữ số, $: Kết thúc
    if re.match(r"^\d{5}$", num):
        num = int(num)
        break
    else:
        print("Không hợp lệ! Vui lòng nhập lại.")
```