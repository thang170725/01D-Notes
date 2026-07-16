- [Re Introduction](#re-introduction)
- [.search() (Tìm vị trí đầu tiên khớp pattern)](#search-tìm-vị-trí-đầu-tiên-khớp-pattern)
  - [.group()](#group)
- [.sub() (Thay thế chuỗi)](#sub-thay-thế-chuỗi)
- [.findall()](#findall)
- [compile()](#compile)
- [Practices](#practices)
  - [Bắt email](#bắt-email)
  - [Nhập một số nguyên có 5 chữ số](#nhập-một-số-nguyên-có-5-chữ-số)

---
# Re Introduction
```bash
re = Regular Expression là thư viện built-in không cần tải

dùng để:
    + Tìm chuỗi
    + Kiểm tra định dạng
    + Trích xuất dữ liệu
    + Thay thế text
```
**các ký tự Regex cơ bản**
```bash
- .             : Bất kỳ ký tự nào (trừ dòng mới)
- \d            : Bất kỳ chữ số nào (0-9) # \d khớp với "12", "99"
- \w	        : Chữ cái, chữ số và dấu gạch dưới	
- \w+           : khớp với "Python_3"
- \s	        : Khoảng trắng (space, tab, newline)	
+ \s+           : khớp với các khoảng trống
- \S            : không phải khoảng trắng
- ^	            : Bắt đầu một dòng	^Hello
- $	            : Kết thúc một dòng	Bye$
- a*	        : Lặp lại 0 hoặc nhiều lần chữ a ("", "a", "aaaa")
- a+	        : Lặp lại 1 hoặc nhiều lần chữ a (khớp với "a", "aaaa") 
- a?	        : Lặp lại 0 hoặc 1 lần ('a', 'aa')
- {n}, {n, m} 
- []            : nhóm ký tự ([a-zA-Z])
- |             : hoặc
- (ab)+         : ('ab', 'abab', 'ababab')
```
# .search() (Tìm vị trí đầu tiên khớp pattern) 
```bash
Dùng khi: Cần kiểm tra có tồn tại hay không. Không cần tất cả kết quả.
```
## .group()
# .sub() (Thay thế chuỗi)
```bash
Dùng cực nhiều để:
    - Clean data
    - Chuẩn hóa text
    - Xóa ký tự thừa
```
**Ex**
```python
text = "Số điện thoại: 0987-654-321"
clean = re.sub(r"\D", "", text)
print(clean)   # 0987654321
``` 
# .findall()
```bash
Lấy tất cả các chuỗi khớp. Rất hay dùng để: Crawl dữ liệu, Parse log. Trích số / email / URL.
```
**Ex**
```python
text = "Các số: 10, 20 và 30"
nums = re.findall(r"\d+", text)
print(nums)   # ['10', '20', '30']
```
# compile()
# Practices
## Bắt email
```bash
^[\w\.]+@\w+\.\w+$
```
## Nhập một số nguyên có 5 chữ số
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
