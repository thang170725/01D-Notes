- [thuật toán chuyển từ hệ 10 sang hệ 2](#thuật-toán-chuyển-từ-hệ-10-sang-hệ-2)
  - [Thuật toán tìm ước chung lớn nhất](#thuật-toán-tìm-ước-chung-lớn-nhất)
- [Tìm UCLN](#tìm-ucln)
---
# thuật toán chuyển từ hệ 10 sang hệ 2
**Ex1**
```python
num = 0
res = ""

if num == 0:
    res = "0"
else:
    while num != 0:
        res = str(num % 2) + res
        num //= 2

print(res)
```
**Ex2**
```python
num = 13
res = ""

while num:
    res = str(num & 1) + res
    num >>= 1

print(res)
```
## Thuật toán tìm ước chung lớn nhất
```python
def gcd(a, b):
    while b != 0:
        a, b = b, a % b
    return a
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