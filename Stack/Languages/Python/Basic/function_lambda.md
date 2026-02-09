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
## lambda
```bash
Là một hàm ẩn danh nhỏ.
```
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