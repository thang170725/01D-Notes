- [Re Introduction](#re-introduction)
- [.search() (Tìm vị trí đầu tiên khớp pattern)](#search-tìm-vị-trí-đầu-tiên-khớp-pattern)
- [.sub() (Thay thế chuỗi)](#sub-thay-thế-chuỗi)
- [.findall()](#findall)
- [.finditer() (dùng để tìm tất cả các kết quả khớp (match) trong chuỗi và trả về từng kết quả dưới dạng một đối tượng Match)](#finditer-dùng-để-tìm-tất-cả-các-kết-quả-khớp-match-trong-chuỗi-và-trả-về-từng-kết-quả-dưới-dạng-một-đối-tượng-match)
  - [.start()](#start)
  - [.end()](#end)
  - [.group()](#group)
  - [.fullmatch() (dùng để kiểm tra toàn bộ chuỗi có khớp với một pattern hay không)](#fullmatch-dùng-để-kiểm-tra-toàn-bộ-chuỗi-có-khớp-với-một-pattern-hay-không)
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
# .finditer() (dùng để tìm tất cả các kết quả khớp (match) trong chuỗi và trả về từng kết quả dưới dạng một đối tượng Match)
```bash
Khi nào dùng finditer()?
    - Muốn biết vị trí của kết quả.
    - Muốn xử lý từng kết quả một.
    - Làm việc với chuỗi dài để không phải tạo ngay một danh sách chứa tất cả kết quả.

Mẹo nhớ:
    - findall() → trả về danh sách (list) các chuỗi khớp.
    - finditer() → trả về iterator gồm các đối tượng Match, mỗi đối tượng chứa cả nội dung và thông tin vị trí.
```
**Ex1: Tìm tất cả các số**
```python
import re

text = "Nam 20 tuổi, Lan 18 tuổi"

for match in re.finditer(r"\d+", text):
    print(match.group())

# 20
# 18
```
## .start()
**Syn**
```bash
- Output: int
```
**Ex**
```python
import re

text = "Python 2026 Java 123"

for match in re.finditer(r"\d+", text):
    print(match.start())

# 7
# 17
```
## .end()
**Ex**
```python
import re

text = "Python 2026 Java 123"

for match in re.finditer(r"\d+", text):
    print(match.start())

# 11
# 20
```
## .group()
**Ex: Tìm các từ bắt đầu bằng chữ P**
```python
import re

text = "Python PHP Java Perl"

for match in re.finditer(r"P\w+", text):
    print(match.group())

# Python
# PHP
# Perl
```
**So sánh findall() và finditer()**
**findall()**
```python
import re

text = "A12 B34 C56"

print(re.findall(r"\d+", text)) # ['12', '34', '56'] - Chỉ lấy nội dung.
```
**finditer()**
```python
import re

text = "A12 B34 C56"

for m in re.finditer(r"\d+", text):
    print(m.group(), m.start())

# 12 1
# 34 5
# 56 9
# Lấy được nội dung và vị trí.
```
## .fullmatch() (dùng để kiểm tra toàn bộ chuỗi có khớp với một pattern hay không)
**Syn**
```bash
re.fullmatch(pattern, string)

- Output
    + Match object → khớp
    + None → không khớp
```
**Ex: Kiểm tra toàn bộ chuỗi chỉ gồm chữ số**
```python
import re

if re.fullmatch(r"\d+", "12345"):
    print("Đây là số")
```
```

1. fullmatch() khác search() như thế nào?

Đây là điểm rất quan trọng.

search()
re.search(r"\d+", "abc123xyz")

→ khớp, vì nó tìm thấy 123 ở bên trong chuỗi.

fullmatch()
re.fullmatch(r"\d+", "abc123xyz")

→ không khớp.

Vì yêu cầu của fullmatch() là:

TOÀN BỘ:
abc123xyz
^^^^^^^^^

phải khớp pattern \d+.

3. Liên quan trực tiếp đến case của bạn

Bạn muốn kiểm tra:

"594666.67" → số
"gia123.com" → không phải số

Có thể dùng:

import re


pattern = r"-?\d+(\.\d+)?"

Sau đó:

if re.fullmatch(pattern, val_str):
    print("Là số")
else:
    print("Không phải số")
Các trường hợp
re.fullmatch(r"-?\d+(\.\d+)?", "123")

→ Match ✅

re.fullmatch(r"-?\d+(\.\d+)?", "594666.67")

→ Match ✅

re.fullmatch(r"-?\d+(\.\d+)?", "-123.45")

→ Match ✅

Nhưng:

re.fullmatch(r"-?\d+(\.\d+)?", "gia123.com")

→ None ❌

re.fullmatch(r"-?\d+(\.\d+)?", "abc123")

→ None ❌

re.fullmatch(r"-?\d+(\.\d+)?", "123abc")

→ None ❌

4. Giải thích pattern

Pattern:

r"-?\d+(\.\d+)?"

tách ra:

-?
-

Dấu - có thể xuất hiện 0 hoặc 1 lần.

Nên cả hai đều được:

123
-123
\d+
\d

= một chữ số từ 0-9.

+

= xuất hiện ít nhất 1 lần.

Vậy:

\d+

khớp:

1
12
123
594666
(\.\d+)?

Phần này dành cho số thập phân:

.

Nhưng trong regex, . có ý nghĩa đặc biệt nên phải viết:

\.

sau đó:

\d+

→ phải có ít nhất một chữ số sau dấu chấm.

Ví dụ:

.67
.5
.123

Toàn bộ:

(\.\d+)?

có ? nên phần decimal là optional.

Do đó:

123
123.45

đều hợp lệ.

5. Nếu chỉ muốn kiểm tra số dương

Không cho phép -:

pattern = r"\d+(\.\d+)?"

Ví dụ:

123       ✅
594666.67 ✅
-123      ❌
6. Nếu muốn bắt buộc phải có phần thập phân

Ví dụ chỉ chấp nhận:

123.45
594666.67

thì:

pattern = r"-?\d+\.\d+"

Khi đó:

123        ❌
123.45     ✅
-123.45    ✅
7. Với parser của bạn

Tôi sẽ viết:

import re


NUMBER_PATTERN = r"-?\d+(\.\d+)?"


if re.fullmatch(NUMBER_PATTERN, val_str):
    return int(float(val_str))

Nhưng nhớ rằng:

594666.67 → 594666

là cắt phần thập phân.

Nếu bạn muốn làm tròn thì logic sẽ khác.

Một điểm nữa: nếu OCR của bạn có dạng "594,666.67" hoặc "594.666,67" thì pattern trên không match. Khi đó cần thiết kế regex theo đúng format số mà dữ liệu OCR của bạn thực tế sinh ra.
# compile() (dùng để biên dịch (compile) một biểu thức chính quy (regex) thành một đối tượng regex để có thể tái sử dụng nhiều lần mà không cần viết lại mẫu)
```bash
Khi nào nên dùng compile()?
    - Nếu chỉ tìm một lần, bạn có thể dùng trực tiếp: re.search(r"\d+", text)
    - Nếu dùng cùng một regex nhiều lần, nên compile(): pattern = re.compile(r"\d+")
        + pattern.search(text1)
        + pattern.search(text2)
        + pattern.search(text3)

        -> Viết mã ngắn gọn hơn.
        -> Không phải lặp lại biểu thức chính quy.
        -> Hiệu quả hơn khi sử dụng nhiều lần.
```
**Syn**
```bash
import re

pattern = re.compile(pattern, flags=0)

- Input:
    + pattern   : Chuỗi regex cần biên dịch
    + flags	    : Các tùy chọn thay đổi cách regex hoạt động
        - re.IGNORECASE hoặc re.I: Bỏ phân biệt hoa thường
```
**Ex1: Tìm số trong chuỗi**
```python
import re

pattern = re.compile(r"\d+")

text = "Tôi có 25 quả táo"

result = pattern.search(text)

print(result.group()) # 25
```
**Ex2: Kiểm tra nhiều chuỗi**
```python
import re

pattern = re.compile(r"\d+")

texts = [
    "abc123",
    "hello",
    "456xyz",
    "python"
]

for text in texts:
    if pattern.search(text):
        print(text, "=> Có số")
    else:
        print(text, "=> Không có số")

# abc123 => Có số
# hello => Không có số
# 456xyz => Có số
# python => Không có số
```
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
