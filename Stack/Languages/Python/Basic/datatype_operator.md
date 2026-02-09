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
```# ^ (XOR)
```bash
- Kết quả ĐÚNG (1) khi 2 toán hạng KHÁC nhau
- Kết quả SAI (0) khi 2 toán hạng GIỐNG nhau
```
**Formula**
```bash
A	B	A XOR B
0	0	0
0	1	1
1	0	1
1	1	0
```
**Property**
```bash
XOR có 3 tính chất cực quan trọng:
1. Tự triệt tiêu: a ^ a = 0
2. XOR với 0 giữ nguyên: a ^ 0 = a
3. XOR là phép TOÁN NGHỊCH ĐẢO (invertible): a ^ b = c  ⇔  c ^ a = b  ⇔  c ^ b = a
```
**Ex**
```python
print(1 ^ 1)  # 0
print(1 ^ 0)  # 1
print(0 ^ 1)  # 1
print(0 ^ 0)  # 0
```
**
**Ex2: XOR trên số nguyên (bitwise XOR)**
```python
a = 5   # 0101
b = 3   # 0011

print(a ^ b)

# Phân tích
#   0101  (5)
# ^ 0011  (3)
# ------
#   0110  (6)
# Kết quả: 6
```
4️⃣ XOR với boolean
print(True ^ False)  # True
print(True ^ True)   # False
print(False ^ False) # False


✔ Python cho phép XOR boolean trực tiếp

5️⃣ XOR với nhiều toán hạng
print(1 ^ 0 ^ 1)  # 0


Vì:

(1 ^ 0) ^ 1 = 1 ^ 1 = 0

6️⃣ Các tính chất QUAN TRỌNG của XOR (rất hay dùng)
6.1 XOR với chính nó → 0
a ^ a == 0

6.2 XOR với 0 → giữ nguyên
a ^ 0 == a

6.3 XOR có tính giao hoán & kết hợp
a ^ b == b ^ a
(a ^ b) ^ c == a ^ (b ^ c)

7️⃣ Ứng dụng XOR cực hay (phỏng vấn hay hỏi)
🔹 7.1 Tìm số xuất hiện 1 lần (các số khác xuất hiện 2 lần)
arr = [4, 1, 2, 1, 2]
result = 0
for x in arr:
    result ^= x

print(result)  # 4


👉 Vì:

a ^ a = 0
0 ^ b = b

🔹 7.2 Swap 2 biến KHÔNG cần biến tạm
a = 10
b = 20

a ^= b
b ^= a
a ^= b

print(a, b)  # 20 10

🔹 7.3 Toggle (bật / tắt) cờ bit
flag = 0b1010
mask = 0b0010

flag ^= mask
print(bin(flag))

8️⃣ XOR với NumPy (bonus)
import numpy as np

a = np.array([1, 0, 1, 0])
b = np.array([0, 1, 1, 0])

print(a ^ b)


👉 Kết quả:

[1 1 0 0]

9️⃣ Phân biệt XOR với OR & AND
Toán tử	Ký hiệu	Khi nào TRUE
AND	&	cả hai đúng
OR	`	`
XOR	^	chỉ một đúng
🔟 Tóm tắt nhanh

✔ XOR trong Python dùng ^
✔ XOR = khác thì 1, giống thì 0
✔ Là bitwise operator
✔ Rất mạnh trong xử lý bit, thuật toán# Có 5 ^ 3 = 6 → biết 5 và 6, tìm 3
**Idea**
```bash
Ta làm:

6 ^ 5 = 3

Kiểm chứng bằng bit
5 = 0101
3 = 0011
---------
6 = 0110

6 ^ 5:
0110
0101
----
0011 = 3


👉 XOR tự đảo ngược được

Bài 2: 5 ^ 7 ^ 2 = 0 → biết 5, 7, 0 tìm 2
Bước 1: Viết lại biểu thức
5 ^ 7 ^ 2 = 0


XOR có tính giao hoán & kết hợp, nên:

2 = 0 ^ 5 ^ 7

Bước 2: Tính
0 ^ 5 ^ 7

5 ^ 7 = 2


👉 2 chính là đáp án```bash
- Đây là thư mục chứa các phương pháp xử lý số.
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
