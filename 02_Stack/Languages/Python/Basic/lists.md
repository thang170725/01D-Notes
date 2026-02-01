- [list() \& len() \& in](#list--len--in)
  - [Ép từ dict -\> list of dict](#ép-từ-dict---list-of-dict)
- [\* (unpack)](#-unpack)
- [.count()](#count)
- [.index()](#index)
- [.insert()](#insert)
- [.clear() \& del \& .remove() \& .pop()](#clear--del--remove--pop)
  - [xóa phần tử nhỏ hơn 2 trong list](#xóa-phần-tử-nhỏ-hơn-2-trong-list)
- [max()](#max)
- [\[\]](#)
- [.sort() \& sorted()](#sort--sorted)
  - [Sắp xếp danh sách sự kiện](#sắp-xếp-danh-sách-sự-kiện)
- [sum()](#sum)
---
# list() & len() & in
```bash
- list  : Ép kiểu khác về list thường.
- len   : Trả về độ dài của một mảng.
- in    : Lặp qua các phần tử trong một mảng, list.
```
**Syn: list**
```bash
li = list(a) # 
```
**Syn: len**
```bash
l = len(li)
```
**EX**
```python
a = "My name is " # str
a = list(a)

print(len(a)) # 12
for character in a:
    print(character, end=' ') # M y   n a m e   i s  
```
## Ép từ dict -> list of dict
**Ex1**
**Topic**
```bash
Cho một từ điển gồm có các khóa là mã sinh viên, các giá trị lưu trữ là điểm tổng kết. Hãy chuyển từ dạng dict -> list of dict
```
**Answer**
```python
scores = {
    "SV001": 8.5,
    "SV002": 7.0,
    "SV003": 9.25
}

result = [
    {"student_id": k, "score": v}
    for k, v in scores.items()
]

print(result) # [{'student_id': 'SV001', 'score': 8.5}, {'student_id': 'SV002', 'score': 7.0}, {'student_id': 'SV003', 'score': 9.25}]
```
**Ex2**
```python
data = {
    "SV001": [8.5, 7.0, 9.0],
    "SV002": [6.5, 7.5, 8.0],
    "SV003": [9.0, 9.5, 9.0]
}

subjects = ["toan", "ly", "hoa"]

result = [
    {
        "mssv": k,
        **dict(zip(subjects, v))
    }
    for k, v in data.items()
]

# [
#     {'mssv': 'SV001', 'toan': 8.5, 'ly': 7.0, 'hoa': 9.0},
#     {'mssv': 'SV002', 'toan': 6.5, 'ly': 7.5, 'hoa': 8.0},
#     {'mssv': 'SV003', 'toan': 9.0, 'ly': 9.5, 'hoa': 9.0}
# ]
```
**Ex3**
```python
data = {
    'msv': ['v1', 'v2'],
    'points': [2, 3]
}

result = [
    dict(zip(data.keys(), values))
    for values in zip(*data.values())
]

# [
#     {'msv': 'v1', 'points': 2},
#     {'msv': 'v2', 'points': 3}
# ]
```
# * (unpack)
```bash
- * : Trải các phần tử của list ra thành nhiều đối số.
```
**Ex: Không dùng *row**
```python
row = [1, 2, 3]

print(row) # [1, 2, 3]. Không đúng định dạng đề bài (có dấu [ ] và dấu ,)
print(*row) # 1 2 3. Đúng định dạng mỗi phần tử cách nhau bằng dấu cách
```
# .count()
```bash
- Trả về số lượng phần tử có giá trị được chỉ định.
```
**Ex**
```python
fruits = ["apple", "banana", "cherry"]
x = fruits.count("cherry") # 1
```
# .index()
```bash
- Trả về vị trí đầu tiên xuất hiện của giá trị được chỉ định.
```
**Ex**
```python
fruits = ['apple', 'banana', 'cherry']
x = fruits.index("cherry")
print(x) # 2
```
# .insert()
```bash
- Để thêm phần tử vào một vị trí nào đó trong mảng.
```
**Ex**
```python
fruits = ['apple', 'banana', 'cherry']
fruits.insert(1, "orange")

print(fruits) # ['apple', 'orange', 'banana', 'cherry']
```
# .clear() & del & .remove() & .pop()
```bash
- clear     : Xóa toàn bộ list. List vẫn tồn tại, chỉ trở thành list rỗng.
- del       : Xóa phần tử theo scling (lát cắt).
- remove    : Xóa phần tử đầu tiên có giá trị = value.
- pop       : Lấy phần tử  ra khỏi mảng.
```
**Syn: clear**
```bash
list.clear()
```
**Syn: del**
```bash
- del list[index]
- del list[start:end]
- del list
```
**Syn: remove**
```python
li.remove(value)
```
**Ex: del**
```python
a = [1, 2, 3, 4, 5]

del a[2]        # xóa phần tử tại index 2
print(a)        # [1, 2, 4, 5]

del a[1:3]     # xóa các phần tử từ index 1 đến 2
print(a)        # [1, 5]

del a
print(a)   # ❌ NameError (a không còn tồn tại vì đã xóa)
```
**Ex: clear**
```python
a = [1, 2, 3]
a.clear()
print(a)   # []
```
**Ex: remove**
```python
a = [1, 2, 3, 2, 4]
a.remove(2)
print(a)   # [1, 3, 2, 4]
```
## xóa phần tử nhỏ hơn 2 trong list
**Ex1**
```python
a = [1, 2, 3, 4, 2, 1.5]
a = [x for x in a if x >= 2]

print(a)
```
**Ex2: Duyệt ngược index**
```python
a = [1, 2, 3, 4, 2, 1.5]

for i in range(len(a) - 1, -1, -1):
    if a[i] < 2:
        del a[i]

print(a)
```
# max() 
```bash
- Tìm max của một danh sách.
```
**Syn**
```bash
max(n1, n2, key= )
```
**Ex1**
```python
print(max(1,2,3)) 
print(max([1,2,3]))
```
**EX2**

# []
```bash
Lấy phần tử trong mảng.
```
**Ex**
```python
a = ["VietNam", "America", "Island", "Porland", "Canada"]
print(a[2:4]) # ['Island', 'Porland']
```## .reverse()
```bash
- Để đảo ngược một mảng.
```
**Ex**
```python
a = [1,2,3,4]
a.reverse()

print(a)
```
# .sort() & sorted()
```bash
Sắp xếp các phần tử trong mảng. Nếu là chuỗi thì sắp xếp theo thứ tự alphabet.
```
**Syn**
```bash
a.sort(reverse=True)

- a: Là tên biến
- reverse=True: Sắp giảm. Mặc định là False
```
**Ex1: Sắp xếp list dict**
```python
events = [
    {'name': 'A', 'people': 50},
    {'name': 'B', 'people': 20},
    {'name': 'C', 'people': 100}
]

events.sort(key=lambda x: x['people']) # 20 → 50 → 100
```
**Ex2: Sắp xếp theo nhiều tiêu chí**
```python
events.sort(key=lambda x: (x['people'], x['name']))
```
**Ex3: Sắp xếp list object (class)**
```python
class Event:
    def __init__(self, name, people):
        self.name = name
        self.people = people

events = [
    Event("A", 50),
    Event("B", 20),
    Event("C", 100)
]

events.sort(key=lambda e: e.people)
```
## Sắp xếp danh sách sự kiện
```bash
# cột 1 là địa điểm, cột 2 là số lượng khách.
data = {
    'event1': ['hanoi', 30],
    'event2': ['hanoi', 10],
    'event3': ['hanoi', 40],
    'event4': ['hanoi', 35],
}
```
```python
sorted_data = dict(
    sorted(data.items(), key=lambda item: item[1][1])
)
```
# sum()
**EX**
```python
a = sum((1,2,3))
print(a) # 6
```
```python
my_dict = {'a': 10, 'b': 50, 'c': 25}

max_key = max(my_dict, key=my_dict.get) # Lấy Key có Value lớn nhất
max_value = my_dict[max_key] # Lấy Value tương ứng

print(f"Key lớn nhất là: {max_key}, Value là: {max_value}") # Kết quả: Key lớn nhất là: b, Value là: 50
```