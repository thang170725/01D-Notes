- [str() \& len()](#str--len)
- [\[\]](#)
- [in \& not in](#in--not-in)
- [isdigit()](#isdigit)
- [.isidentifier()](#isidentifier)
- [.isupper() \& .islower() \&](#isupper--islower-)
- [.startswith() \& .endswith()](#startswith--endswith)
- [.find() \& .rfind()](#find--rfind)
- [.index() \& .rindex()](#index--rindex)
- [ord() \& chr()](#ord--chr)
- [.count()](#count)
- [.join()](#join)
- [.split()](#split)
- [.rsplit() \& .lsplit()# .strip()](#rsplit--lsplit-strip)
- [.rstrip()](#rstrip)
- [.title()](#title)
- [.replace()](#replace)
- [.format()](#format)
- [:\<](#-1)
---
# str() & len()
```bash
- len   : Lấy ra độ dài của chuỗi.
```
**Ex: str** 
```python
a = 1
print(str(a))
```
# []
**Syn**
```bash
[start : end : step]
- start : vị trí bắt đầu (tính từ 0)
- end : vị trí kết thúc (không lấy end)
- step : bước nhảy
```
**Ex**
```python
text = "abcdef"

text[0] # 'a'
text[-1] # 'f'
text[1:4] # 'bcd'
text[:3] # 'abc'
text[3:] # 'def'
text[::] # 'abcdef'
text[::2] # 'ace'
text[::-1] # 'fedcba'
```
# in & not in
Kiểm tra chuỗi này có nằm trong chuỗi kia hay không.
**Ex**
```python
a = "le duc thang"
print("thang" in a) # True
a = "le duc thang"
print("thang" not in a) # False
```
# isdigit()
```bash
Kiểm tra xem có phải kiểu số không. Trả về true false.
```
**Syn**
```bash
<variable>.isdigit()
```
# .isidentifier()
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
# .isupper() & .islower() &
```bash
- isupper islower   : Kiểm tra viết hoa, viết thường.
```
# .startswith() & .endswith()
```bash
Kiểm tra xem chuỗi có bắt đầu, kết thúc bằng một chuỗi hay một ký tự nào đó không.
```
**Ex**
```python
a = "Viet Nam"

print(a.startswith("Viet")) # True
print(a.endswith("nam")) # False
```
# .find() & .rfind()
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
# .index() & .rindex()
Để tìm kiếm một chuỗi trong một chuỗi mẹ. Trả về vị trí đầu tiên.
**Ex**
```python
txt = "Hello, welcome to my world."
x = txt.index("welcome")
print(x) # 3
```
# ord() & chr()
```bash
- ord   : Để lấy giá trị ASCII của một ký tự nào đó.
- char  : Để xử lý với ký tự.
```
**Syn**
```bash
ord(<variable>)
```
**Ex: chr**
```python
a = 65
print(chr(a)) # A
```
**Ex: ord**
```python
a = ord("a")
b = ord("1")
print(a, b) # 97 49
```
# .count()
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
# .join()
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

# .split()
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

# .rsplit() & .lsplit()# .strip()
```bash
Xóa hết khoảng trắng ở 2 đầu, bên trái, bên phải.
```
**Ex**
```python
a = '  hello  '
a.strip()

print(a.strip())
```

# .rstrip()
**Ex**
```python
a = 'aaab'

a = a.rstrip('b')
print(a)
```
# .title()
Viết hoa và kiểm tất cả ký tự đầu trong một chuỗi.
```bash
a = "hello world, i am from vietnam"
print(a.title()) # Hello World, I Am From Vietnam# .upper()
```python
a = 'thang'

print(a.upper())
```
# .replace()
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
expandtabs()
Đặt kích thước tab theo số khoảng trắng được chỉ định.
Cú pháp: <variable>.expandtabs(tabsize)
txt = "H\te\tl\tl\to"
x = txt.expandtabs(4)
print(x)
H    e    l    l  o
Khoảng cách 1 tab lúc này được đặt bằng 4 dấu cách
isalnum()
Trả về True nếu trong chuỗi chỉ có các chữ cái [a-z] và số [0-9].
Cú pháp: <variable>.isalnum()
txt = "Company12"
x = txt.isalnum()
print(x)
True
isalpha()
Trả về True nếu chuỗi có ít nhất 1 ký tự và tất cả ký tự là chữ cái [a-z]. Nếu không phương thức sẽ trả về false.
Cú pháp: <variable>.isalpha()
a = "thang1"
print(a.isalpha())
False
isascii()
Trả về True nếu tất cả các ký tự đều thuộc trong bảng mã ASCII.
Cú pháp: <variable>.isascii()
isdecimal()
Trả về True nếu tất cả các ký tự trong chuỗi đều là số.
Cú pháp: <variable>.isdecimal()

isnumeric()
    • Trả về True nếu tất cả các ký tự đều là số, nếu không thì trả về false.
    • Các số mũ, như 2 và ¾ cũng được coi là các giá số.
    • -1 và 1.5 không được được coi là các giá trị số, vì tất cả các ký tự trong chuỗi phải là số còn – và . thì không.
Cú pháp: <variable>.isnumeric()
isspace()
Trả về true nếu tất cả ký tự trong chuỗi đều là khoảng trắng.
Cú pháp: <variable>.isspace()
isprintable()
Trả về Tue nếu tất cả các ký tự trong chuỗi đều có thể in được.
Cú pháp: <variable>.isprintable()
casefold()
Tương tự như phương thức lower(), nhưng phương thức casefold() mạnh hơn, tích cực hơn, nghĩa là nó sẽ chuyển đổi nhiều ký tự thành chữ thường hơn và sẽ tìm thấy nhiều kết quả khớp hơn khi so sánh hai chuỗi và cả hai đều được chuyển đổi được bằng phương thức casefold().
Cú pháp: <variable>.casefold
txt = "Hello, And Welcome To My World!"
x = txt.casefold()
print(x)
hello, and welcome to my world!


```


```

capitalize()
Viết hoa kí tự đầu tiên trong chuỗi, tất cả kí tự khác viết thường.
Cú pháp: <variable>.capitalize()
a = "welcome to python"
print(a.capitalize())
Welcome to python
swapcase()
Kí tự viết hoa thì viết thường, kí tự viết thường thì viết hoa.
Cú pháp: <variable>.swapcase()
a = "welcome to python"
print(a.swapcase())
WElCoME tO pYTHON
partition()
Để tìm kiếm một chuỗi đã chỉ định và chia chuỗi thành một bộ gồm 3 phần tử.
    • Phần đầu tiên chứa phần trước chuỗi đã chỉ định.
    • Phần tử thứ hai chứa chuỗi chỉ định.
    • Phần tử thứ ba chứa phần sau chuỗi đã chỉ định.
Cú pháp: <variable>.partition(value)
txt = "I could eat bananas all day"
x = txt.partition("bananas")
print(x)
('I could eat ', 'bananas', ' all day')
rpartition()
Để tìm kiếm lần xuất hiện cuối cùng của một chuỗi đã chỉ định và chia chuỗi thành một bộ gồm ba phần tử.
    • Phần đầu tiên chứa phần trước chuỗi đã chỉ định.
    • Phần tử thứ hai chứa chuỗi chỉ định.
    • Phần tử thứ ba chứa phần sau chuỗi đã chỉ định.
Cú pháp: <variable>.rpatition(value)
txt = "I could eat bananas all day, bananas are my favorite fruit"
x = txt.rpartition("bananas")
print(x)
('I could eat bananas all day, ', 'bananas', ' are my favorite fruit')
.rjust() & .ljust()
căn phải, trái chuỗi, sử dụng một ký tự được chỉ định (mặc định là khoảng trắng) làm ký tự điền.
Cú pháp: 
<variable>.rjust(length, character)
<variable>.ljust(length, character)
txt = "banana"
x = txt.rjust(20, "O")
print(x) # OOOOOOOOOOOOOObanana
txt = "banana"
x = txt.ljust(20, "O")
print(x) # bananaOOOOOOOOOOOOOO
center()
Phương thức này sẽ căn giữa chuỗi, sử dụng một ký tự được chỉ định (mặc định là khoảng trắng) làm ký tự điền.
Cú pháp: <variable>.center(length, character)
txt = "banana"
x = txt.center(20, "O")
print(x)
OOOOOOObananaOOOOOOO

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
# :<
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
:>
Thiết lập 8 khoảng trắng và căn giá trị phần tử sang phải.
txt = "We have {:>8} chickens."
print(txt.format(49))
We have       49 chickens.
:^
Thiết lập 15 khoảng trắng và căn giá trị phần tử vào giữa.
txt = "He is from {:^15}".format("VietNam")
print(txt)
He is from     VietNam
:=
Thiết lập 15 khoảng trắng và căn các ký dấu sang một bên, số sang một.
txt = "He is from {:=15}".format(-5)
print(txt)
He is from -             5
:+
Để chỉ định một số được biểu diễn là số dương hay âm.
txt = "{:+5}, {:+5}".format(-3, 3)
print(txt)
-   3, +    3
:-
Để luôn chỉ ra nếu số là âm, số dương được hiển thị mà không có dấu nào.
txt = "{:-}, {:-}".format(-3, 3)
print(txt)
-3, 3
:
Để chèn một ký tự nào đó vào chuỗi.
:,
Để thêm dấu phân cách hàng nghìn.
str = "{:,}".format(12300000000)
print(str)
12,300,000,000
:_
Để thêm dấu gạch dưới phân cách hàng nghìn.
txt = "The universe is {:_} years old."
print(txt.format(13800000000))
The universe is 13_800_000_000 years old.
:b
Để chuyển một số sang hệ nhị phân.
str = "{} = {:b}".format(5,5)
print(str)
5 = 101
:d
Để chuyển số từ hệ nhị phân sang hệ thập phân.
str = "{:d}".format(0b101)
print(str)
5
:e
txt = "We have {:e} chickens."
print(txt.format(5))
We have 5.000000e+00 chickens.
:E
txt = "We have {:E} chickens."
print(txt.format(5))
We have 5.000000E+00.
:f
txt = "The price is {:.3f} dollars."
print(txt.format(45))
txt = "The price is {:f} dollars."
print(txt.format(45))
The price is 45.000 dollars.
The price is 45.000000 dollars.

:F
x = float('inf')
txt = "The price is {:F} dollars."
print(txt.format(x))
txt = "The price is {:f} dollars."
print(txt.format(x))
The price is INF dollars.
The price is inf dollars.
:o
txt = "The octal version of {0} is {0:o}"
print(txt.format(10))
The octal version of 10 is 12
:X
txt = "The Hexadecimal version of {0} is {0:X}"
print(txt.format(255))
The Hexadecimal version of 255 is FF
:%
txt = "You scored {:%}"
print(txt.format(0.25))
txt = "You scored {:.0%}"
print(txt.format(0.25))
You scored 25.000000%
You scored 25%
Format_map
Hàm này cho phép chúng ta thực hiện ddinhj dạng chuỗi sử dụng các giá trị tù một bản đồ dữ liệu (mapping). 
Cú pháp:
String.fomat_map(mapping)
    • String là chuỗi mình muốn định dạng.
    • Mapping là đối tượng bản đồ dữ liệu (dictionary-like object) chứa các giá trị cho việc định dạng chuỗi.
person = {'name': 'Alice', 'age': 25}
message = 'My name is {name} and I am {age} years old.'
formatted_message = message.format_map(person)
print(formatted_message)
My name is Alice and I am 25 years old.
encode()
Để mã hóa chuỗi, sử dụng mã hóa được chỉ định. Nếu không chỉ định mã hóa, UTF-8 sẽ được sử dụng.
Cú pháp: <variable>.encode(encoding=encoding, errors=errors)
Parameter
Description
encoding
Optional. A String specifying the encoding to use. Default is UTF-8
errors
Optional. A String specifying the error method. Legal values are:
'backslashreplace'
- uses a backslash instead of the character that could not be encoded
'ignore'
- ignores the characters that cannot be encoded
'namereplace'
- replaces the character with a text explaining the character
'strict'
- Default, raises an error on failure
'replace'
- replaces the character with a questionmark
'xmlcharrefreplace'
- replaces the character with an xml character



translate()
Trả về một chuỗi trong chuỗi trong đó một số ký tự được chỉ định được thay thế bằng ký tự được mô tả trong từ điển hoặc trong bảng ánh ánh xạ. Nếu sử dụng từ điển, bạn phải sử dụng mã ASCII thayy vì ký tự.
Cú pháp: string.translate(table)
#use a dictionary with ascii codes to replace 83 (S) with 80 (P):
mydict = {83:  80}
txt = "Hello Sam!"
print(txt.translate(mydict))
Hello Pam!
makestrans()
Trả về một bảng ánh xạ có thể được sử dụng với phương thức translate() để thay thế các ký tự đã chỉ định.
Cú pháp: str.maketrans(x, y, z)
    • x: Bắt buộc. Nếu chỉ có một tham số được chỉ định, thì đây phải là một từ điển mô tả cách thực hiện thay thế. Nếu có hai hoặc nhiều tham số được chỉ định, thì tham số này phải là một chuỗi chỉ định các ký tự bạn muốn thay thế.
    • y: Tùy chọn. Một chuỗi có cùng độ dài với tham số x. Mỗi ký tự trong tham số đầu tiên sẽ được thay thế bằng ký tự tương ứng trong chuỗi này.
    • z: Tùy chọn. Một chuỗi mô tả các ký tự nào sẽ xóa khỏi chuỗi gốc.
txt = "Hello Sam!"
mytable = str.maketrans("S", "P")
print(txt.translate(mytable))
Hello Pam!

txt = "Hi Sam!"
x = "mSa"
y = "eJo"
mytable = str.maketrans(x, y)
print(txt.translate(mytable))
Hi Joe!

txt = "Good night Sam!"
x = "mSa"
y = "eJo"
z = "odnght"
mytable = str.maketrans(x, y, z)
print(txt.translate(mytable))
G i Joe!
splitlines()
Chia một chuỗi thành một danh sách. Việc chia được thực hiện tại các ngắt dòng.
Cú pháp: <variable>.splitlines(keeplinebreaks)
Keeplinebreaks: Tùy chọn. Chỉ định cem có nên bao gồm ngắt dòng đúng hay sai không. Giá trị mặc định là sai.
txt = "Thank you for the music\nWelcome to the jungle"
x = txt.splitlines()
print(x)
['Thank you for the music', 'Welcome to the jungle']

txt = "Thank you for the music\nWelcome to the jungle"
x = txt.splitlines(True)
print(x)
['Thank you for the music\n', 'Welcome to the jungle']
zfill()
Thêm số 0 vào đầu chuỗi, cho đến khi đạt đến độ dài nhất định. Nếu giá trị của tham số len nhỏ hơn độ dài của chuỗi, thì không được thực hiện điền.
Cú pháp: <variable>.zfill(len)
a = "hello"
b = "welcome to the jungle"
c = "10.000"
print(a.zfill(10))
print(b.zfill(10))
print(c.zfill(10))
00000hello
welcome to the jungle
000010.000
a = 5
print(f"{a:.5f}")
