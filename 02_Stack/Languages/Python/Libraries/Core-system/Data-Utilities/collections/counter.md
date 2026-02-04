# Counter()
Tham số truyền vào có thể là list, tuple, ...
**Ex**
```python
from collections import Counter

c = Counter(['a', 'b', 'a', 'c', 'b', 'a'])
print(c)
# Counter({'a': 3, 'b': 2, 'c': 1})
```

# .values()
```python
from collections import Counter
c = Counter(['a', 'b', 'c', 'a'])
print(c.values())

# dict_values([2, 1, 1])
```
.most_common()
Trả về n phần tử xuất hiện nhiều nhất.
Cú pháp:
c = Counter("aaabbbbccdde")
print(c.most_common(2)) # Nếu không truyền n → trả tất cả theo thứ tự giảm dần.
[('b', 4), ('a', 3)]
.elements()
Trả ra tất cả phần tử, lặp lại theo số lần đếm.
Cú pháp:
c = Counter({'a': 2, 'b': 3})
print(list(c.elements()))
['a', 'a', 'b', 'b', 'b']
.update()
Giống như cộng thêm dữ liệu mới.
Cú pháp:
c = Counter("abc")
c.update("aba")   # thêm a,b,a
print(c)
Counter({'a': 3, 'b': 2, 'c': 1})
.subtract()
Không xóa phần tử, chỉ giảm số lượng (có thể âm).
Cú pháp:
c = Counter("aabbb")
c.subtract("abb")
print(c)
Counter({'b': 2, 'a': 1})
[]
c = Counter("aabbc")
print(c['a'])  # 2
print(c['x'])  # 0, không có thì trả 0
+
c1 = Counter(a=3, b=1)
c2 = Counter(a=1, b=3)
print(c1 + c2)
Counter({'a': 4, 'b': 4})
-
c1 = Counter(a=4, b=2)
c2 = Counter(a=3, b=5)
print(c1 - c2)
Counter({'a': 1})
& (Lấy MIN theo key)
c1 = Counter(a=4, b=2)
c2 = Counter(a=3, b=5)
print(c1 & c2)
Counter({'a': 3, 'b': 2})
| (Lấy max theo key)
.clear()
del
Counter từ dict / tuple list