- [các ký tự Regex cơ bản cần nhớ](#các-ký-tự-regex-cơ-bản-cần-nhớ)
- [.search()](#search)
- [.match()](#match)
- [.sub()](#sub)
  - [Bài tập](#bài-tập)
    - [Bắt email](#bắt-email)

---

```text
- re = Regular Expression Dùng để:
    + Tìm chuỗi
    + Kiểm tra định dạng
    + Trích xuất dữ liệu
    + Thay thế text
- không cần tải. Cần import re
```
# các ký tự Regex cơ bản cần nhớ
```bash
.   :Bất kỳ ký tự nào (trừ dòng mới)	a.c khớp với "abc", "a1c"
\d          :Bất kỳ chữ số nào (0-9)	\d\d khớp với "12", "99"
\w	:Chữ cái, chữ số và dấu gạch dưới	\w+ khớp với "Python_3"
\s	:Khoảng trắng (space, tab, newline)	\s+ khớp với các khoảng trống
\S  :không phải khoảng trắng
^	:Bắt đầu một dòng	^Hello
$	:Kết thúc một dòng	Bye$
a*	:Lặp lại 0 hoặc nhiều lần chữ a ("", "a", "aaaa")
a+	:Lặp lại 1 hoặc nhiều lần chữ a (khớp với "a", "aaaa") 
a?	        :Lặp lại 0 hoặc 1 lần ('a', 'aa')
{n}, {n, m} 
[]          : nhóm ký tự ([a-zA-Z])
|           : hoặc
(ab)+       : ('ab', 'abab', 'ababab')
```

# .search()
Tìm vị trí đầu tiên khớp pattern. Dùng khi: Cần kiểm tra có tồn tại hay không. Không cần tất cả kết quả.

# .sub()
Thay thế chuỗi. 
Dùng cực nhiều để:
    - Clean data
    - Chuẩn hóa text
    - Xóa ký tự thừa
```python
text = "Số điện thoại: 0987-654-321"
clean = re.sub(r"\D", "", text)
print(clean)   # 0987654321
``` 

## Bài tập
### Bắt email
```bash
^[\w\.]+@\w+\.\w+$
```