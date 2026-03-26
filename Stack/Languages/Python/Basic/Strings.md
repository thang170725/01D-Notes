- [Create (Tạo)](#create-tạo)
  - [chr ()](#chr-)
- [Display (Cung cấp thông tin)](#display-cung-cấp-thông-tin)
  - [len()](#len)
  - [ord()](#ord)
  - [.count()](#count)
- [Check (Kiểm tra)](#check-kiểm-tra)
  - [in \& not in](#in--not-in)
  - [isdigit()](#isdigit)
  - [.isidentifier()](#isidentifier)
  - [.isupper() \& .islower() \&](#isupper--islower-)
  - [.startswith() \& .endswith()](#startswith--endswith)
- [Search (Tìm kiếm)](#search-tìm-kiếm)
  - [.find() \& .rfind()](#find--rfind)
  - [.index() \& .rindex()](#index--rindex)
  - [partition()](#partition)
  - [rpartition()](#rpartition)
- [Align (Căn chuỗi)](#align-căn-chuỗi)
  - [.rjust() \& .ljust()](#rjust--ljust)
  - [.center()](#center)
- [Process (xử lý chuỗi)](#process-xử-lý-chuỗi)
  - [in \& not in](#in--not-in-1)
  - [.join()](#join)
  - [.split()](#split)
  - [.strip() \& .rstrip() \& .lstrip()](#strip--rstrip--lstrip)
  - [.title()](#title)
  - [.replace()](#replace)
  - [expandtabs()](#expandtabs)
  - [casefold()](#casefold)
  - [capitalize()](#capitalize)
  - [swapcase()](#swapcase)
  - [.splitlines()](#splitlines)
  - [.zfill()](#zfill)
- [.format()](#format)
  - [:\<](#)
  - [:\>](#-1)
  - [:^](#-2)
  - [:=](#-3)
  - [:+](#-4)
  - [:-](#-)
  - [:](#-5)
  - [:,](#-6)
  - [:\_](#_)
  - [:b](#b)
  - [:d](#d)
  - [:e](#e)
  - [:E](#e-1)
  - [:f](#f)
  - [:o](#o)
  - [:X](#x)
  - [:%](#-7)
---
# Create (Tạo)
## chr ()
```bash
Để xử lý với ký tự.
```
**Ex: chr**
```python
a = 65
print(chr(a)) # A
```
# Display (Cung cấp thông tin)
## len()
```bash
Lấy ra độ dài của chuỗi.
```
## ord() 
```bash
Để lấy giá trị ASCII của một ký tự nào đó
```
**Syn**
```bash
ord(<variable>)
```
**Ex: ord**
```python
a = ord("a")
b = ord("1")
print(a, b) # 97 49
```
## .count()
```bash
Đếm xem một ký tự nào đó xuất hiện bao nhiêu lần.
```
**Syn**
```bash
<variable>.count(substring, start=, end=)
```
**Ex**
```python
a = "le duc thang ne"
print(a.count("e"))
```
# Check (Kiểm tra)
## in & not in
Kiểm tra chuỗi này có nằm trong chuỗi kia hay không.
**Ex**
```python
a = "le duc thang"
print("thang" in a) # True
a = "le duc thang"
print("thang" not in a) # False
```
## isdigit()
```bash
Kiểm tra xem có phải kiểu số không. Trả về true false.
```
**Syn**
```bash
<variable>.isdigit()
```
## .isidentifier()
```bash
- Trả về True nếu chuỗi là một định danh hợp lệ, nếu không thì trả không thì trả về false.
- Một chuỗi được coi là một định danh hợp lệ nếu nó chỉ chứa các chữ cái và các chữ số hoặc dấu gạch dưới. 
- Một định danh hợp lệ không thể bắt đầu bằng một số hoặc chứa bất kỳ khoảng trắng nào.
```
**Syn** 
```bash
<variable>.isidentifier()
```
**Ex**
```python
tests = [
    "name",
    "_age",
    "user1",
    "1user",
    "user-name",
    "class",
    "user name"
]

for t in tests:
    print(t, "->", t.isidentifier())

# name        -> True
# _age        -> True
# user1       -> True
# 1user       -> False
# user-name   -> False
# class       -> True   ❗
# user name   -> False
``` 
## .isupper() & .islower() &
```bash
- isupper islower   : Kiểm tra viết hoa, viết thường.
```
## .startswith() & .endswith()
```bash
Kiểm tra xem chuỗi có bắt đầu, kết thúc bằng một chuỗi hay một ký tự nào đó không.
```
**Ex**
```python
a = "Viet Nam"

print(a.startswith("Viet")) # True
print(a.endswith("nam")) # False
```
# Search (Tìm kiếm)
## .find() & .rfind()
```bash
Tìm chuỗi bên trong chuỗi.
```
**Ex**
```python
a = "i am a programming"
print(a.find("a")) # 2

s = 'le duc thang ne ne'
print(s.rfind('e')) # 17
```
## .index() & .rindex()
```bash
Để tìm kiếm một chuỗi trong một chuỗi mẹ. Trả về vị trí đầu tiên.
```
**Ex**
```python
txt = "Hello, welcome to my world."
x = txt.index("welcome")
print(x) # 3
```
## partition()
```bash
Để tìm kiếm một chuỗi đã chỉ định và chia chuỗi thành một bộ gồm 3 phần tử.
    + Phần đầu tiên chứa phần trước chuỗi đã chỉ định.
    + Phần tử thứ hai chứa chuỗi chỉ định.
    + Phần tử thứ ba chứa phần sau chuỗi đã chỉ định.
```
**Syn** 
```bash
<variable>.partition(value)
```
**Ex**
```python
txt = "I could eat bananas all day"
x = txt.partition("bananas")

print(x) # ('I could eat ', 'bananas', ' all day')
```
## rpartition()
```bash
Để tìm kiếm lần xuất hiện cuối cùng của một chuỗi đã chỉ định và chia chuỗi thành một bộ gồm ba phần tử.
    + Phần đầu tiên chứa phần trước chuỗi đã chỉ định.
    + Phần tử thứ hai chứa chuỗi chỉ định.
    + Phần tử thứ ba chứa phần sau chuỗi đã chỉ định.
```
**Syn** 
```bash
<variable>.rpatition(value)
```
**Ex**
```python
txt = "I could eat bananas all day, bananas are my favorite fruit"
x = txt.rpartition("bananas")

print(x) # ('I could eat bananas all day, ', 'bananas', ' are my favorite fruit')
```
# Align (Căn chuỗi)
## .rjust() & .ljust()
```bash
căn phải, trái chuỗi, sử dụng một ký tự được chỉ định (mặc định là khoảng trắng) làm ký tự điền.
```
**Syn**
```bash
<variable>.rjust(length, character)
<variable>.ljust(length, character)
```
**Ex**
```python
txt = "banana"
x = txt.rjust(20, "O")

print(x) # 

txt = "banana"
x = txt.ljust(20, "O")
print(x) # bananaOOOOOOOOOOOOOO
```
## .center()
```bash
Phương thức này sẽ căn giữa chuỗi, sử dụng một ký tự được chỉ định (mặc định là khoảng trắng) làm ký tự điền.
```
**Syn** 
```bash
<variable>.center(length, character)
```
**Ex**
```python
txt = "banana"
x = txt.center(20, "O")

print(x) # OOOOOOObananaOOOOOOO
```
# Process (xử lý chuỗi)
## in & not in
Kiểm tra chuỗi này có nằm trong chuỗi kia hay không.
**Ex**
```python
a = "le duc thang"
print("thang" in a) # True
a = "le duc thang"
print("thang" not in a) # False
```
## .join()
```bash
Lấy tất cả các mục trong một iterable và nối chúng thành một chuỗi. Một chuỗi phải được chỉ định làm dấu phân cách.
```
**Syn**
```python
myTuple = ("John", "Peter", "Vicky")
x = "#".join(myTuple)

print(x) # John#Peter#Vicky
a = ['1', '2', '3']
print(" => ".join(a)) # 1 => 2 => 3
```
## .split()
```bash
Để tách chuỗi và gán thành một mảng.
```
**Syn**
```bash
str.split(separator, maxsplit)

**Ex**
```python
a = "Helllo world"

b = a.split(" ") # b = a.split()
print(b) # ['Helllo', 'world']
```
## .strip() & .rstrip() & .lstrip()
```bash
Xóa hết khoảng trắng ở 2 đầu, bên trái, bên phải.
```
**Ex: strip**
```python
a = '  hello  '
a.strip()
```
## .title()
Viết hoa và kiểm tất cả ký tự đầu trong một chuỗi.
```bash
a = "hello world, i am from vietnam"
print(a.title()) # Hello World, I Am From Vietnam# .upper()
```python
a = 'thang'

print(a.upper())
```
## .replace()
```bash
Để thay thế ký tự hoặc một chuỗi con trong chuỗi.
```
**Syn**
```bash
a.replace('need replace', 'replace', regex=True)
```
**Ex**
```python
a = "i am Json"
print(a.replace("i am", "My name is")) # My name is Json
```
## expandtabs()
```bash
Đặt kích thước tab theo số khoảng trắng được chỉ định.
```
**Syn** 
```bash
<variable>.expandtabs(tabsize)
```
**Ex**
```python
txt = "H\te\tl\tl\to"
x = txt.expandtabs(4)

print(x) # H    e    l    l  o
# Khoảng cách 1 tab lúc này được đặt bằng 4 dấu cách
```
## casefold()
```bash
Tương tự như phương thức lower(), nhưng phương thức casefold() mạnh hơn, tích cực hơn, nghĩa là nó sẽ chuyển đổi nhiều ký tự thành chữ thường hơn và sẽ tìm thấy nhiều kết quả khớp hơn khi so sánh hai chuỗi và cả hai đều được chuyển đổi được bằng phương thức casefold().
```
**Syn** 
```bash
<variable>.casefold
```
**Ex**
```python
txt = "Hello, And Welcome To My World!"
x = txt.casefold()

print(x) # hello, and welcome to my world!
```
## capitalize()
```bash
Viết hoa kí tự đầu tiên trong chuỗi, tất cả kí tự khác viết thường.
```
**Syn** 
```bash
<variable>.capitalize()
```
**Ex**
```python
a = "welcome to python"

print(a.capitalize()) # Welcome to python
```
## swapcase()
```bash
Kí tự viết hoa thì viết thường, kí tự viết thường thì viết hoa.
```
**Syn** 
```bash
<variable>.swapcase()
```
**Ex**
```python
a = "welcome to python"

print(a.swapcase()) # WElCoME tO pYTHON
```
## .splitlines()
```bash
Chia một chuỗi thành một danh sách. Việc chia được thực hiện tại các ngắt dòng.
```
**Syn** 
```bash
<variable>.splitlines(keeplinebreaks)

- Keeplinebreaks: Tùy chọn. Chỉ định xem có nên bao gồm ngắt dòng đúng hay sai không. Giá trị mặc định là sai.
```
**`Ex`**
```python
txt = "Thank you for the music\nWelcome to the jungle"
x = txt.splitlines()

print(x) # ['Thank you for the music', 'Welcome to the jungle']
```
**Ex2**
```python
txt = "Thank you for the music\nWelcome to the jungle"
x = txt.splitlines(True)

print(x) # ['Thank you for the music\n', 'Welcome to the jungle']
```
## .zfill()
```bash
Thêm số 0 vào đầu chuỗi, cho đến khi đạt đến độ dài nhất định. Nếu giá trị của tham số len nhỏ hơn độ dài của chuỗi, thì không được thực hiện điền.
```
**Syn** 
```bash
<variable>.zfill(n)

- n: Số lượng ký tự trong một chuỗi
```
**Ex**
```python
a = "hello"
b = "welcome to the jungle"
c = "10.000"

print(a.zfill(10)) # 00000hello
print(b.zfill(10)) # welcome to the jungle
print(c.zfill(10)) # 000010.000
```
# .format()
```bash
Định dạng các giá trị đã chỉ định và chèn chúng vào bên trong trình giữ chỗ của chuỗi. 
```
**Syn**
```bash
a = a.format(value1, value2, …)
```
**Ex**
```bash
# case 1
txt1 = "My name is {name}, i am from {country}"
txt1 = txt1.format(name = "Thang", country = "Viet Nam")
print(txt1)
# case 2
txt2 = "My name is {name}, i am from {country}".format(name = "Thang", country = "Viet Nam")
print(txt2)
# case 3
txt3 = "My name is {0}, i am from {1}".format("Thang", "Viet Nam")
print(txt3)
# case 4
txt4 = "My name is {}, i am from {}".format("Thang", "Viet Nam")
print(txt4)

# My name is Thang, i am from Viet Nam
# My name is Thang, i am from Viet Nam
# My name is Thang, i am from Viet Nam
# My name is Thang, i am from Viet Nam
```
## :<
```bash
Thiết lập khoảng trắng và căn giá trị phần tử sang trái.
```
**Ex1**
```python
print(f"{'An':<10}|")
print(f"{'Bình':<10}|")
print(f"{'Chi':<10}|")

# An        |
# Bình      |
# Chi       |
```
**Ex2**
```python
txt = "We have {:<8} chickens."

print(txt.format(49)) # We have 49       chickens.
```
## :>
```bash
Thiết lập 8 khoảng trắng và căn giá trị phần tử sang phải.
```
**Ex**
```python
txt = "We have {:>8} chickens."
print(txt.format(49)) # We have       49 chickens.
```
## :^
```bash
Thiết lập 15 khoảng trắng và căn giá trị phần tử vào giữa.
```
**Ex**
```python
txt = "He is from {:^15}".format("VietNam")
print(txt) # He is from     VietNam
```
## :=
```bash
Thiết lập 15 khoảng trắng và căn các ký dấu sang một bên, số sang một.
```
**Ex**
```python
txt = "He is from {:=15}".format(-5)
print(txt) # He is from -             5
```
## :+
```bash
Để chỉ định một số được biểu diễn là số dương hay âm.
```
**Ex**
```python
txt = "{:+5}, {:+5}".format(-3, 3)
print(txt) # -   3, +    3
```
## :-
```bash
Để luôn chỉ ra nếu số là âm, số dương được hiển thị mà không có dấu nào.
```
**Ex**
```python
txt = "{:-}, {:-}".format(-3, 3)
print(txt) # -3, 3
```
## :
```bash
Để chèn một ký tự nào đó vào chuỗi.
```
## :,
```bash
Để thêm dấu phân cách hàng nghìn.
```
**Ex**
```python
str = "{:,}".format(12300000000)

print(str) # 12,300,000,000
```
## :_
```bash
Để thêm dấu gạch dưới phân cách hàng nghìn.
```
**Ex**
```python
txt = "The universe is {:_} years old."

print(txt.format(13800000000)) # The universe is 13_800_000_000 years old.
```
## :b
```bash
Để chuyển một số sang hệ nhị phân.
```
**Ex**
```python
str = "{} = {:b}".format(5,5)

print(str) # 5 = 101
```
## :d
```bash
Để chuyển số từ hệ nhị phân sang hệ thập phân.
```
**Syn**
```bash
str = "{:d}".format(0b101)

print(str) # 5
```
## :e
```bash
txt = "We have {:e} chickens."

print(txt.format(5)) # We have 5.000000e+00 chickens.
```
## :E
```bash
txt = "We have {:E} chickens."

print(txt.format(5)) # We have 5.000000E+00.
```
## :f
```python
txt = "The price is {:.3f} dollars."

print(txt.format(45)) # The price is 45.000 dollars.
```
## :o
```python
txt = "The octal version of {0} is {0:o}"

print(txt.format(10)) # The octal version of 10 is 12
```
## :X
```python
txt = "The Hexadecimal version of {0} is {0:X}"

print(txt.format(255)) # The Hexadecimal version of 255 is FF
```
## :%
```python
txt = "You scored {:%}"

print(txt.format(0.25)) # You scored 25.000000%
```