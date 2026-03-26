 [\*args](#args)
- [Keyword Arguments](#keyword-arguments)
- [Keyword-Only Arguments](#keyword-only-arguments)
- [Tìm UCLN](#tìm-ucln)
  - [Bài tập](#bài-tập)
    - [Thuật toán tìm ước chung lớn nhất](#thuật-toán-tìm-ước-chung-lớn-nhất)

---

id()
Để xem địa chỉ id của một biến trong bộ nhớ.
Cú pháp: id(<variable>)
Ép kiểu
Để ép từ một kiểu bất kỳ sang kiểu int (nếu ép được). Nếu biến cần ép không phải là số thì sẽ bị lỗi.
Cú pháp: int(<variable>)
a = "10"
b = int(a)
print(type(b))
<class 'int'>
```bash
Trả về true nếu đối tượng được chỉ định thuộc loại được chỉ định, nếu không thì trả về false.
```
**Ex**
```python
isinstance(object, type)
x = isinstance("Hello", (str, float, int, str, list, dict, tuple))
print(x) # True
```
# Keyword Arguments
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

# Keyword-Only Arguments
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


# Tìm UCLN
**Ex1**
```python
def UCLN(n1,n2):
    result = 1
    
    while n1 % 2 == 0  and n2 % 2 == 0: # xử lý riêng trường hợp 2 số đó chia hết cho 2 (chẵn)
        n1 //= 2
        n2 //= 2
        result *= 2
    # xử lý các trường hợp còn lại (lẻ)
    for i in range(3, min(n1,n2)+1, 2):
        while n1 % i == 0 and n2 % i == 0:
            n1 /= i
            n2 /= i
            result *= i
    return result
def main():
    print(UCLN(12, 18))
main()
```
**Ex2: Cải tiến code**
```python
def UCLN(n1,n2):
    while n2 != 0:
        r = n1 % n2
        n1 = n2
        n2 = r
    return n1
def main():
    print(UCLN(12, 18))
main()
```
**Ex3: Bằng hàm đệ quy**
```python
def UCLN(n1,n2,result = 1):
    if(n1 == 1 or n2 == 1): return 1
    # xử lý riêng trường hợp 2 số đó chia hết cho 2 (chẵn)
    while n1 % 2 == 0  and n2 % 2 == 0:
        return UCLN(n1//2, n2//2, result*2)
    # xử lý các trường hợp còn lại (lẻ)
    i = 3
    while i <= min(n1,n2):
        if n1 % i == 0 and n2 % i == 0:
            return UCLN(n1//i, n2//i, result*i)
        i += 2
    return result
def main():
    print(UCLN(22, 18))
main()
```

**Ex: Cải tiến code**
```python
def UCLN(n1,n2):
    if n2 == 0:
        return n1
    return UCLN(n2, n1 % n2)
def main():
    print(UCLN(22, 18))
main()
```



## Bài tập
### Thuật toán tìm ước chung lớn nhất
```python
def gcd(a, b):
    while b != 0:
        a, b = b, a % b
    return a
```
