- [Introduction](#introduction)
- [Create (Nhóm khởi tạo)](#create-nhóm-khởi-tạo)
  - [list() \& \[\]](#list--)
- [Display (Nhóm cung cấp thông tin)](#display-nhóm-cung-cấp-thông-tin)
  - [len()](#len)
  - [.index() (Trả về vị trí đầu tiên xuất hiện của giá trị được chỉ định)](#index-trả-về-vị-trí-đầu-tiên-xuất-hiện-của-giá-trị-được-chỉ-định)
- [Process (Nhóm xử lý list)](#process-nhóm-xử-lý-list)
  - [in](#in)
  - [\* (unpack)](#-unpack)
  - [.count()](#count)
  - [.insert()](#insert)
  - [.pop() (Lấy phần tử ra khỏi mảng)](#pop-lấy-phần-tử-ra-khỏi-mảng)
- [Remove (Xóa)](#remove-xóa)
  - [.clear() \& del \& .remove()](#clear--del--remove)
  - [max()](#max)
  - [\[\]](#)
  - [.sort() \& sorted() (Sắp xếp các phần tử trong mảng)](#sort--sorted-sắp-xếp-các-phần-tử-trong-mảng)
  - [sum()](#sum)
- [Transform (Xử lý biến dạng cấu trúc mảng)](#transform-xử-lý-biến-dạng-cấu-trúc-mảng)
  - [.append()](#append)
---
# Introduction
```bash
list (danh sách) dùng để lưu nhiều giá trị theo thứ tự và có thể thay đổi được (thêm, xóa, sửa phần tử).
```
# Create (Nhóm khởi tạo)
## list() & []
```bash
Dùng để tạo ra một list hoặc ép từ kiểu khác về list
```
**Syn**
```bash
li = list(a) 

- Input:
    + a: là một kiểu nào đó muốn chuyển sang kiểu list (Ex: a = 3 - kiểu nguyên)
- Output:
    + li: Là biến chứa danh sách
```
**EX: Chuyển từ kiểu chuỗi sang kiểu list**
```python
a = "My name is " # str
a = list(a) # chuyển sang kiểu list

print(len(a)) # 12 - số phần tử trong list

for character in a: # dùng vòng lặp để in từng phần tử trong list
    print(character, end=' ') # M y   n a m e   i s  
```
# Display (Nhóm cung cấp thông tin)
## len() 
```bash
Trả về độ dài của một mảng.
```
**Syn: len**
```bash
l = len(li)
```
## .index() (Trả về vị trí đầu tiên xuất hiện của giá trị được chỉ định)
**Syn**
```bash
x = nums.index(value)

- Input:
  + value: là giá trị trong 1 mảng
```
**Ex**
```python
fruits = ['apple', 'banana', 'cherry']
x = fruits.index("cherry")

print(x) # 2
```
# Process (Nhóm xử lý list)
## in
```bash
Lặp qua các phần tử trong một mảng, list hoặc tìm xem trong một mảng có phần tử nào đó hay không
```
## * (unpack)
```bash
- * : Trải các phần tử của list ra thành nhiều đối số.
```
**Ex: Không dùng *row**
```python
row = [1, 2, 3]

print(row) # [1, 2, 3]. Không đúng định dạng đề bài (có dấu [ ] và dấu ,)
print(*row) # 1 2 3. Đúng định dạng mỗi phần tử cách nhau bằng dấu cách
```
## .count()
```bash
- Trả về số lượng phần tử có giá trị được chỉ định.
```
**Ex**
```python
fruits = ["apple", "banana", "cherry"]
x = fruits.count("cherry") # 1
```
## .insert()
```bash
- Để thêm phần tử vào một vị trí nào đó trong mảng.
```
**Ex**
```python
fruits = ['apple', 'banana', 'cherry']
fruits.insert(1, "orange")

print(fruits) # ['apple', 'orange', 'banana', 'cherry']
```
## .pop() (Lấy phần tử ra khỏi mảng)
# Remove (Xóa)
## .clear() & del & .remove()
```bash
- clear     : Xóa toàn bộ list. List vẫn tồn tại, chỉ trở thành list rỗng.
- del       : Xóa phần tử theo scling (lát cắt).
- remove    : Xóa phần tử đầu tiên có giá trị = value.
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
## max() 
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

## []
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
## .sort() & sorted() (Sắp xếp các phần tử trong mảng)
```bash
Nếu là chuỗi thì sắp xếp theo thứ tự alphabet.
```
**Syn**
```bash
a.sort(key=, reverse=True)

- Input:
  + a: Là tên biến
  + reverse=True: Sắp giảm. Mặc định là False
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
## sum()
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
# Transform (Xử lý biến dạng cấu trúc mảng)
## .append()