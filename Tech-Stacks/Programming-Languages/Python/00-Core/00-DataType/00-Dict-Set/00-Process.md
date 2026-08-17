- [Dictionary (lưu dữ liệu theo cặp key: value để tra cứu nhanh)](#dictionary-lưu-dữ-liệu-theo-cặp-key-value-để-tra-cứu-nhanh)
  - [{} \& dict (Để tạo dict)](#--dict-để-tạo-dict)
  - [Remove (thao tác xóa)](#remove-thao-tác-xóa)
    - [.pop() (xóa mục có tên khóa được chỉ định)](#pop-xóa-mục-có-tên-khóa-được-chỉ-định)
    - [del (Để xóa cặp key: value trong dictionary)](#del-để-xóa-cặp-key-value-trong-dictionary)
    - [.clear() (Để xóa sạch dictionary)](#clear-để-xóa-sạch-dictionary)
    - [.popitem() (Xóa một phần tử được chèn cuối cùng)](#popitem-xóa-một-phần-tử-được-chèn-cuối-cùng)
  - [Display (cung cấp thông tin)](#display-cung-cấp-thông-tin)
    - [.keys() (Để lấy ra tên các key)](#keys-để-lấy-ra-tên-các-key)
    - [.values() (Trả về danh sách các giá trị của dictionary)](#values-trả-về-danh-sách-các-giá-trị-của-dictionary)
    - [.get() (trả về value của một key nào đó)](#get-trả-về-value-của-một-key-nào-đó)
    - [.items() (Dùng để lấy ra các cặp key, value)](#items-dùng-để-lấy-ra-các-cặp-key-value)
  - [Process (nhóm xử lý)](#process-nhóm-xử-lý)
    - [.copy()](#copy)
    - [\[\] \& .update()](#--update)
    - [\*\* (unpack dict)](#-unpack-dict)
- [Set (không được sắp xếp theo thứ tự, không thể thay đổi và không cho phép các giá trị trùng lặp)](#set-không-được-sắp-xếp-theo-thứ-tự-không-thể-thay-đổi-và-không-cho-phép-các-giá-trị-trùng-lặp)
  - [.clear()](#clear)
  - [del](#del)
  - [.remove()](#remove)
  - [.discard()](#discard)
  - [.intersection()](#intersection)
  - [\& (tìm phần tử chung)](#-tìm-phần-tử-chung)
  - [.union()](#union)
  - [.add() (Để thêm một phần tử vào trong một set)](#add-để-thêm-một-phần-tử-vào-trong-một-set)
- [.update() (Để thêm các mục từ tập hợp khác vào tập hợp hiện tại)](#update-để-thêm-các-mục-từ-tập-hợp-khác-vào-tập-hợp-hiện-tại)
  - [intersection\_update() (Chỉ giữ lại các phần tử trùng lặp, nhưng nó sẽ thay đổi tập hợp gốc thay vì trả về tập hợp mới)](#intersection_update-chỉ-giữ-lại-các-phần-tử-trùng-lặp-nhưng-nó-sẽ-thay-đổi-tập-hợp-gốc-thay-vì-trả-về-tập-hợp-mới)
  - [.pop() (xóa một mục, nhưng phương thức này sẽ xóa một mục ngẫu nhiên, do đó bạn không thể chắc chắn mục nào sẽ bị xóa)](#pop-xóa-một-mục-nhưng-phương-thức-này-sẽ-xóa-một-mục-ngẫu-nhiên-do-đó-bạn-không-thể-chắc-chắn-mục-nào-sẽ-bị-xóa)
---
# Dictionary (lưu dữ liệu theo cặp key: value để tra cứu nhanh)
## {} & dict (Để tạo dict)
**Syn**
```bash
dic = {key: value, …}
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
## Remove (thao tác xóa)
### .pop() (xóa mục có tên khóa được chỉ định)
**Ex**
```python
thisdict =	{
  "brand": "Ford",
  "model": "Mustang",
  "year": 1964
}

thisdict.pop("model")

print(thisdict) # {'brand': 'Ford', 'year': 1964}
```
### del (Để xóa cặp key: value trong dictionary)
**Ex**
```python
thisdict =	{
  "brand": "Ford",
  "model": "Mustang",
  "year": 1964
}

del thisdict["model"]

print(thisdict) # {'brand': 'Ford', 'year': 1964}
```
### .clear() (Để xóa sạch dictionary)
**Ex**
```python
thisdict =	{
  "brand": "Ford",
  "model": "Mustang",
  "year": 1964
}

thisdict.clear()

print(thisdict) # {}
```
### .popitem() (Xóa một phần tử được chèn cuối cùng)
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
## Display (cung cấp thông tin)
### .keys() (Để lấy ra tên các key)
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
### .values() (Trả về danh sách các giá trị của dictionary)
```bash
<variable>.keys()
```
**Ex1: values**
```python
data = {
    'names': ['Thang', "Minh", "Nghia", "Quy"],
    'ages': [18, 20, 23, 16],
    'scores': [10, 9, 6, 7]
}

print(data.values()) # dict_values([['Thang', 'Minh', 'Nghia', 'Quy'], [18, 20, 23, 16], [10, 9, 6, 7]])
```
**Ex4: values**
```python
data = {
    'size': 850,
    'bedrooms': 2,
    'age': 10,
    'price': 200000
}


print(list(data.values())) # [850, 2, 10, 200000]
```
### .get() (trả về value của một key nào đó)
**Syn**
```bash
a = <variable>.get(<key>, default) 

- Input:
  + default: Nếu key chưa có thì trả về giá trị defaule
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
### .items() (Dùng để lấy ra các cặp key, value)
```bash
Thường dùng trong vòng lặp để lặp qua các key, value. 

Phương thức này trả về từng mục trong từ điển dưới dạng các bộ trong danh sách.
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
## Process (nhóm xử lý)
### .copy()
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
### [] & .update()
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
**Ex3: Use [] to add items**
```python
thisdict =	{
  "brand": "Ford",
  "model": "Mustang",
  "year": 1964
}

thisdict["color"] = "red"

print(thisdict) # {'brand': 'Ford', 'model': 'Mustang', 'year': 1964, 'color': 'red'}
```
### ** (unpack dict)

# Set (không được sắp xếp theo thứ tự, không thể thay đổi và không cho phép các giá trị trùng lặp)
```bash
Sử dụng set để:
    - Loại bỏ các phần tử trùng lặp.
    - Kiểm tra sự tồn tại của một phần tử.
    - Thực hiện các phép toán tập hợp.
    - Lưu trữ dữ liệu không có thứ tự và duy nhất.
    - Tối ưu hóa hiệu năng.
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
## .clear()
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
```
## del
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
```
## .remove()
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
## .discard()
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
```
## .intersection()
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
## & (tìm phần tử chung)
**Ex2**
```python
mySet= {"apple", "banana", "orange", "Lemon"}
orther = {"orange", "Lemon", "Passion"}
Set = mySet & orther

print(Set) # {'Lemon', 'orange'}
```
## .union()
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
```
## .add() (Để thêm một phần tử vào trong một set)
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

# .update() (Để thêm các mục từ tập hợp khác vào tập hợp hiện tại)
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
```
## intersection_update() (Chỉ giữ lại các phần tử trùng lặp, nhưng nó sẽ thay đổi tập hợp gốc thay vì trả về tập hợp mới)
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
```
## .pop() (xóa một mục, nhưng phương thức này sẽ xóa một mục ngẫu nhiên, do đó bạn không thể chắc chắn mục nào sẽ bị xóa)
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