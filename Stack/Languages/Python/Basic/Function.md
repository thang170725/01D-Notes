- [function](#function)
  - [\*args](#args)
  - [\*\*kwargs](#kwargs)
  - [Keyword Arguments](#keyword-arguments)
  - [Keyword-Only Arguments](#keyword-only-arguments)
  - [lambda (hàm ẩn danh)](#lambda-hàm-ẩn-danh)
- [nonlocal](#nonlocal)
- [global](#global)
- [yield](#yield)
- [map](#map)
---
# function
## *args
```bash
- Hàm sẽ nhận được một bộ đối số và có thể truy cập theo list.
```
**Ex**
```python
def my_function(*kids):
  print("The youngest child is " + kids[2])
my_function("Emil", "Tobias", "Linus") # The youngest child is Linus
```
## **kwargs
```bash
- Hàm sẽ nhận được một từ điển đối số và có thể truy cập được vào các mục tương ứng.
```
**Ex**
```python
def my_function(**kid):
  print("His last name is " + kid["lname"])
my_function(fname = "Tobias", lname = "Refsnes") # His last name is Refsnes
```
## Keyword Arguments
```bash
Bạn cũng có thể gửi đối số với cú pháp key = value. Theo cách này, thứ tự của các đối số không quan trọng.
```
**Ex1**
```python
def my_function(child3, child2, child1):
  print("The youngest child is " + child3)
my_function(child1 = "Emil", child2 = "Tobias", child3 = "Linus") # The youngest child is Linus
```
**Ex2**
```python
def my_function(country = "Norway"):
  print("I am from " + country)
my_function("Sweden") # I am from Sweden
my_function("India") # I am from India
my_function() # I am from Norway
my_function("Brazil") # I am from Brazil
```
## Keyword-Only Arguments
```bash
Để chỉ rõ ràng một hàm chỉ có thể có đối số từ khóa, hãy thêm *, trước các đối số.
```
**Ex1**
```python
def my_function(*, x):
  print(x)
my_function(x = 3) # 3

def my_function(*, x):
  print(x)
my_function(3) # lỗi
```
## lambda (hàm ẩn danh)
**Syn** 
```bash
lambda arguments : expression
```
**Ex**
```python
def myfunc(n):
  return lambda a : a * n
  
mydoubler = myfunc(2)
mytripler = myfunc(3)
print(mydoubler(11)) # 22
print(mytripler(11)) # 33
```
# nonlocal
**Ex**
```python
def outer():
    x = 10

    def inner():
        nonlocal x
        x += 1
        print(x)

    inner()
```

# global
**Ex1: Không dùng global**
```python
count = 0

def increase():
    count += 1

increase() # lỗi
print(count)
```
**Ex2: Dùng global**
```python
count = 0

def increase():
    global count
    count += 1

increase() 
print(count) # 1
```
# yield 
```bash
- Dùng để tạo generator function.
- Khi hàm có yield:
  + Không trả về toàn bộ kết quả ngay
  + Trả từng phần một
  + Tạm dừng và tiếp tục khi được gọi lại
```
**Ex1**
```bash
def count_up_to(n):
    i = 1
    while i <= n:
        yield i
        i += 1

gen = count_up_to(3)

print(next(gen))  # 1
print(next(gen))  # 2
print(next(gen))  # 3
# Mỗi lần next() chạy đến yield rồi dừng.
```
**Ex2: đọc file lớn**
```python
def read_file(path):
    with open(path) as f:
        for line in f:
            yield line

# Không load toàn bộ file vào bộ nhớ.
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