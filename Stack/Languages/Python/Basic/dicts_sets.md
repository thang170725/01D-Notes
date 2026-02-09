- [dictionary](#dictionary)
  - [{} \& dict](#--dict)
    - [Tạo một dictionaries với keys là mã sinh viên, values là điểm trung bình](#tạo-một-dictionaries-với-keys-là-mã-sinh-viên-values-là-điểm-trung-bình)
    - [Tạo một dictionaries với 2 keys là mã sinh viên, điểm trung bình, values lưu list giá trị của keys tương ứng](#tạo-một-dictionaries-với-2-keys-là-mã-sinh-viên-điểm-trung-bình-values-lưu-list-giá-trị-của-keys-tương-ứng)
- [.pop() \& Del \& .clear()](#pop--del--clear)
- [.get()](#get)
- [.items()](#items)
- [.copy()](#copy)
- [.keys() \& # .values()](#keys---values)
- [\[\] \& # .update()](#---update)
- [.popitem()](#popitem)
  - [\*\* (unpack dict)](#-unpack-dict)
  - [Exercise 1](#exercise-1)
- [set](#set)
- [.clear()](#clear)
- [.discard()](#discard)
- [\&](#)
- [.update()](#update)
---
# dictionary
## {} & dict
```bash
- Để tạo dict.
```
**Syn**
```bash
dic = {key: value, …} – name[key]
```
**Ex**
```python
thisdict = {
  "brand": "Ford",
  "model": "Mustang",
  "year": 1964
}

print(thisdict) # {'brand': 'Ford', 'model': 'Mustang', 'year': 1964}
```
### Tạo một dictionaries với keys là mã sinh viên, values là điểm trung bình
**Comprehension**
```bash
- Comprehesion chỉ nên sử dụng khi dữ liệu sạch, chỉ cần biến đổi, vì rất khó bắt lỗi. 
```
```python
n = int(input('Số lượng phần tử: '))

dic = {
    input(f'mã sinh viên thứ {i+1}: '): float(input('điểm tb: '))
    for i in range(n)
}

print(dic)
```
**Try ... Except**
```python
while True:
    try:
        n = int(input('Số lượng sinh viên: '))
        if n > 0:
            break
        print('Phải nhập số nguyên dương!')
    except ValueError:
        print('Không phải số nguyên!')

def nhap_diem():
    while True:
        try:
            d = float(input('Điểm trung bình: '))
            if 0 <= d <= 10:
                return d
            print('Điểm phải từ 0 đến 10!')
        except ValueError:
            print('Phải nhập số!')

dic = {
    input(f'Mã sinh viên thứ {i+1}: '): nhap_diem()
    for i in range(n)
}
```

### Tạo một dictionaries với 2 keys là mã sinh viên, điểm trung bình, values lưu list giá trị của keys tương ứng
```python
n = int(input('Số lượng sinh viên: '))

dic = {
    'students_id': [input(f'mã sinh viên thứ {i+1}: ') for i in range(n)],
    'means_point': [input(f'điểm trung bình thứ {i+1}: ') for i in range(n)],
}

print(dic)
```
# .pop() & Del & .clear()
```bash
- pop   : Để xóa mục có tên khóa được chỉ định.
- del   : Để xóa cặp key: value trong dictionary.
- clear : Để xóa sạch dictionary.
```
**Ex1: pop**
```python
thisdict =	{
  "brand": "Ford",
  "model": "Mustang",
  "year": 1964
}

thisdict.pop("model")

print(thisdict) # {'brand': 'Ford', 'year': 1964}
```
**Ex2: del**
```python
thisdict =	{
  "brand": "Ford",
  "model": "Mustang",
  "year": 1964
}

del thisdict["model"]

print(thisdict) # {'brand': 'Ford', 'year': 1964}
```
**Ex3: clear**
```python
thisdict =	{
  "brand": "Ford",
  "model": "Mustang",
  "year": 1964
}

thisdict.clear()

print(thisdict) # {}
```

# .get()
```bash
Để trả về value của một key nào đó.
```
**Syn**
```bash
<variable>.get(<key>, default)

- Nếu key chưa có thì trả về giá trị defaule
```
**Ex1**
```python
dic = dict(name='John', age=25, city='New York')

print(dic.get('name')) # John
print(dic.get('address', None)) # None
```
**Ex2: Đếm số lượng phần tử**
```python
labels = ['no', 'no']
counts = {}
for label in labels:
    counts[label] = counts.get(label, 0) + 1 
print(counts)
{'no': 2}
```
# .items()
```bash
- Dùng để lấy ra các cặp key, value. Thường dùng trong vòng lặp để lặp qua các key, value. 
- Phương thức này trả về từng mục trong từ điển dưới dạng các bộ trong danh sách.
```
**Syn**
```bash
<variable>.items()
```
**Ex1**
```python
thisdict = {
  "brand": "Ford",
  "model": "Mustang",
  "year": 1964
}
x = thisdict.items()

print(x) # dict_items([('brand', 'Ford'), ('model', 'Mustang'), ('year', 1964)])
```
**Ex2**
```python
dir = dict(name='John', age=25, city='New York')
for i in dir.items():
    print(i)

# ('name', 'John')
# ('age', 25)
# ('city', 'New York')
```
# .copy()
**Ex**
```python
thisdict = {
  "brand": "Ford",
  "model": "Mustang",
  "year": 1964
}

mydict = thisdict.copy()

print(mydict) # {'brand': 'Ford', 'model': 'Mustang', 'year': 1964}
```
# .keys() & # .values()
```bash
- keys      : Để lấy ra tên các key.
- values    : Trả về danh sách các giá trị của dictionary.
```
```bash
<variable>.keys()
```
**Ex1: keys**
```python
li = [
    {'name': 'thang', 'address': 'hanoi', 'age': 20}, 
    {'name': 'minh', 'address': 'hcm', 'age': 21},
    {'name': 'chien', 'address': 'da nang', 'age': 21}
]

keys = list(li[0].keys())

print(keys) # ['name', 'address', 'age']
```
**Ex2: keys**
```python
dir = dict(name='John', age=25, city='New York')

print(dir.keys(), type(dir.keys())) # dict_keys(['name', 'age', 'city']) <class 'dict_keys'>
```
**Ex3: values**
```python
data = {
    'names': ['Thang', "Minh", "Nghia", "Quy"],
    'ages': [18, 20, 23, 16],
    'scores': [10, 9, 6, 7]
}

print(data.values()) # dict_values([['Thang', 'Minh', 'Nghia', 'Quy'], [18, 20, 23, 16], [10, 9, 6, 7]])
```
# [] & # .update()
```bash
- []        : Để thay đổi values của keys hoặc thêm keys-values mới.
- update    : để thay đổi values của keys.
```
**Ex1: update**
```python
di = {
    "name": "John",
    "age": 30,
    "address": "VietNam"
}
di.update({"age" : 40, "address": "USA"})

print(di) # {'name': 'John', 'age': 40, 'address': 'USA'}
```
**Ex2: []**
```python
di = {
    "name": "John",
    "age": 30
}

di["age"] = 10

print(di) # {'name': 'John', 'age': 10}
```
**Ex3: Add items**
```python
thisdict =	{
  "brand": "Ford",
  "model": "Mustang",
  "year": 1964
}

thisdict["color"] = "red"

print(thisdict) # {'brand': 'Ford', 'model': 'Mustang', 'year': 1964, 'color': 'red'}
```
# .popitem()
```bash
Xóa một phần tử được chèn cuối cùng.
```
**Ex**
```python
thisdict =	{
  "brand": "Ford",
  "model": "Mustang",
  "year": 1964
}

thisdict.popitem()

print(thisdict) # {'brand': 'Ford', 'model': 'Mustang'}
```
## ** (unpack dict)
## Exercise 1
**Topic**
```bash
1. Khởi tạo một từ điển gồm n sinh viên, keys lưu mã sinh viên, values lưu điểm trung bình.
2. Hiển thị dưới dạng bảng.
```
**Answer**
```python
def input_dict():
    n = int(input('Số lượng sinh viên: '))

    dic = {
        input(f'mã của sinh viên thứ {i+1}: '): 
        float(input(f'Điểm của sinh viên thứ {i+1}: '))
        for i in range(n)
    }

    return dic

def print_table(dic: dict):
    headers = ['Mã sinh viên', 'Điểm trung bình']

    widths_id = max(len(headers[0]), max(len(k) for k in dic))
    width_score = max(len(headers[1]), max(len(str(v)) for v in dic.values()))

    print(f'{headers[0]:<{widths_id}} | {headers[1]:<{width_score}}')
    print(f'{"-"*widths_id}-+-{"-"*width_score}')

    for k, v in dic.items():
        print(f'{k:<{widths_id}} | {v:<{width_score}}')

dic = input_dict()
print_table(dic)
```
# set
```bash
- Các mục set không được sắp xếp theo thứ tự, không thể thay đổi và không cho phép các giá trị trùng lặp.
- Sử dụng set để:
    + Loại bỏ các phần tử trùng lặp.
    + Kiểm tra sự tồn tại của một phần tử.
    + Thực hiện các phép toán tập hợp.
    + Lưu trữ dữ liệu không có thứ tự và duy nhất.
    + Tối ưu hóa hiệu năng.
```
**Syn**
```bash
<variable> = {value1, value2, …}
<variable> = set((value1, value2, …))
```
**Ex**
```python
thisset = {"apple", "banana", "cherry", True, 1, 2}
print(thisset)

# {True, 2, 'apple', 'banana', 'cherry'}
# 1 không xuất hiện vì nó coi 1 và true là phần tử trùng lặp.
```
# .clear()
```bash
Để xóa toàn bộ set.
```
**Syn** 
```bash
<variable>.clear()
```
**Ex**
```python
mySet= {"apple", "banana", "orange", "Lemon", "Passion"}
mySet.clear()

print(mySet) # set()
```# del
```bash
Để xóa toàn bộ set. Del sẽ xóa cả giá trị set và biến set.
```
**Syn** 
```bash
del <variable>
```
**Ex**
```python
mySet= {"apple", "banana", "orange", "Lemon", "Passion"}
del mySet

print(mySet)

# File "D:\workspace\Python_box\TestPy.py", line 3, in <module>
#    print(mySet)
#     ^^^^^
# NameError: name 'mySet' is not defined
```# .remove()
```bash
Để xóa một phần tử ra khỏi set. Nếu không tìm thấy phần tử cần xóa từ ném ra lỗi.
```
**Syn** 
```bash
<variable>.remove(value)
```
**Ex**
```python
mySet= {"apple", "banana"}
mySet.remove("banana")
print(mySet) # {'apple'}
```

# .discard()
```bash
Để xóa một phần tử ra khỏi set. Nếu không tìm thấy phần tử cần xóa thì bỏ qua lệnh này.
```
**Syn**
```bash
<variable>.discard(value)
```
**Ex**
```python
mySet= {"apple", "banana"}
mySet.discard("banana")
print(mySet) # {'apple'}
```# .intersection()
```bash
Trả về một set mới chỉ chứa các phần tử có trong cả 2 set cũ.
```
**Syn** 
```bash
<variable1>.intersection(<variable2>)
```
**Ex**
```python
mySet= {"apple", "banana", "orange", "Lemon"}
orther = {"orange", "Lemon", "Passion"}

Set = mySet.intersection(orther)

print(Set) # {'Lemon', 'orange'}
```

# &
**Ex2**
```python
mySet= {"apple", "banana", "orange", "Lemon"}
orther = {"orange", "Lemon", "Passion"}
Set = mySet & orther

print(Set) # {'Lemon', 'orange'}
```# .union()
```bash
Trả về một set mới với các giá trị phần tử là 2 set cũ.
```
**Syn**
```bash
<variable>.union(<variable1>, <variable2>, …)
<variable1> | <variable2> | …
```
**Ex1**
```python
mySet= {"apple", "banana", }
orther = {"orange", "Lemon", "Passion"}
Set = mySet.union(orther)
print(Set) # {'banana', 'apple', 'orange', 'Passion', 'Lemon'}
```
**Ex2**
```python
mySet= {"apple", "banana", }
orther = {"orange", "Lemon", "Passion"}
Set = mySet | orther
print(Set) # {'Passion', 'orange', 'Lemon', 'banana', 'apple'}
```# .add()
```bash
Để thêm một phần tử vào trong một set. 
```
**Syn**
```bash
<variable>.add(value)
```
**Ex**
```python
thisset = {"apple", "banana", "cherry"}
thisset.add("orange")
print(thisset) # {'apple', 'cherry', 'banana', 'orange'}
```

# .update()
```bash
Để thêm các mục từ tập hợp khác vào tập hợp hiện tại.
```
**Syn**  
```bash
<variable>.update(value)
```
**Ex**
```python
mySet= {"apple"}
orther = {"banana"}
mySet.update(orther)
print(mySet) # {'apple', 'banana'}
```# intersection_update()
```bash
Chỉ giữ lại các phần tử trùng lặp, nhưng nó sẽ thay đổi tập hợp gốc thay vì trả về tập hợp mới.
```
**Syn**
```bash 
<variable1>.intersection_update(<variable2>)
```
**Ex**
```python
mySet= {"apple", "banana", "orange", "Lemon"}
orther = {"orange", "Lemon", "Passion"}
mySet.intersection_update(orther)

print(mySet) # {'orange', 'Lemon'}
```# .pop()
```bash
Bạn cũng có thể sử dụng phương thức pop để xóa một mục, nhưng phương thức này sẽ xóa một mục ngẫu nhiên, do đó bạn không thể chắc chắn mục nào sẽ bị xóa.
```
**Syn** 
```bash
<variable>.pop()
```
**Ex**
```python
mySet= {"apple", "banana", "orange", "Lemon", "Passion"}
x = mySet.pop()

print(x) # orange
print(mySet) # {'apple', 'banana', 'Lemon', 'Passion'}
```