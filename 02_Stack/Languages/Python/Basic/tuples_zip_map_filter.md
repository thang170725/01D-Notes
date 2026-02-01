- [tuple](#tuple)
- [zip()](#zip)
- [map](#map)
---
# tuple
```bash
- Là một kiểu dữ liệu dùng để lưu trữ các đối tượng không thay đổi về sau (giống như hằng số). Nó sử dụng để lưu trữ nhiều mục trong một biến duy nhất. 
```
**Syn**
```bash
<variable> = (value1, value2, …)
<variable> = tuple((value1, value2, …))
```
**Ex**
```python
days = ("Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday", "Sunday")
print(days)
print(type(days))

# ('Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday', 'Sunday')
# <class 'tuple'>
```# .append()
```bash
Để thêm một phần tử nào đó vào tuple. Cần phải chuyển sang kiểu dữ liệu list rồi mới thêm.
```
**syn**
```bash
<variable>.append(value)
```
**Ex**
```python
myTuple = (1,2,3)
a = list(myTuple)
a.append(4)
myTuple = tuple(a)
print(myTuple) # (1, 2, 3, 4)
```
**Ex2**
```python
myTuple = (1,2,3)
a = (4,)
myTuple += a
print(myTuple) # (1, 2, 3, 4)
```# tuple()
```bash
- Để ép từ một kiểu nào đó sang tuple.
```
**Syn**
```bash
tuple(<variable>)
```
**Ex**
```python
days = ("Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday", "Sunday", "Monday")
print(days) # ('Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday', 'Sunday', 'Monday')
```# .remove()
```bash
Để xóa một phần tử ra khỏi tuple.
```
**Syn** 
```bash
<variable>.remove(value)
```
**Ex**
```python
myTuple = (1,2,3)
a = list(myTuple)
a.remove(3)
myTuple = tuple(a)
print(myTuple) # (1, 2)
```# []
```bash
- Các mục tuple được lập chỉ mục, mục đầu tiên có chỉ mục [0], … (giống mảng).
```
**Ex**
```python
days = ("Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday", "Sunday")
print(days[0])
days[0] = "Thứ 2"
print(days[0])

# Monday
# Traceback (most recent call last):
#   File "D:\workspace\Python_box\TestPy.py", line 3, in 
#  <module>
#     days[0] = "Thứ 2"
#     ~~~~^^^
# TypeError: 'tuple' object does not support item assignment
```
# zip()
**Ex1**
```python
names = ["Alice", "Bob", "Charlie"]
ages = [25, 30, 35]

for values in zip(names, ages):
    print(values)
```
**Ex2**
```python
names = ["Alice", "Bob", "Charlie"]
ages = [25, 30, 35]

combined = zip(names, ages) # zip hai list lại với nhau
print(list(combined)) # [('Alice', 25), ('Bob', 30), ('Charlie', 35)]

for name, age in zip(names, ages):
    print(f"{name} is {age} years old")

# Alice is 25 years old
# Bob is 30 years old
# Charlie is 35 years old
```
**Ex3: zip với dict**
```python
data = {
    'msv': ['v1', 'v2'],
    'points': [2, 3]
}

print(*data)

# msv points
```
# map
**Ex**
```python
def Change(n):
    n = int(n)
    return "Số chẵn" if n % 2 == 0 else "Số lẻ"

n = input("Nhập các số cách nhau bởi dấu cách: ").split()
res = list(map(Change, n))
print(res)
```