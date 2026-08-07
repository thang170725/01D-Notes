- [comment](#comment)
- [input() \& print()](#input--print)
  - [Hiển thị list of dict ra dạng bảng đẹp](#hiển-thị-list-of-dict-ra-dạng-bảng-đẹp)
  - [Hiển thị list of list ra dạng bảng đẹp](#hiển-thị-list-of-list-ra-dạng-bảng-đẹp)
  - [Nhập tên (Dữ liệu dạng chữ)](#nhập-tên-dữ-liệu-dạng-chữ)
  - [Nhập số và thực hiện phép tính (Ép kiểu)](#nhập-số-và-thực-hiện-phép-tính-ép-kiểu)
  - [Nhập nhiều giá trị trên một dòng](#nhập-nhiều-giá-trị-trên-một-dòng)
  - [Nhập ma trận (nxm)](#nhập-ma-trận-nxm)
  - [Tạo ra dict lưu tọa độ n điểm](#tạo-ra-dict-lưu-tọa-độ-n-điểm)
  - [Nhập một số nguyên có ít hơn 5 chữ số](#nhập-một-số-nguyên-có-ít-hơn-5-chữ-số)
---
# comment 
```bash
# content
```
# input() & print()
**Syn: input**
```bash
variable = input(prompt) # kiểu dữ liệu là str

- prompt    : Chuỗi ký tự để gợi ý.
- variable  : Là biến dùng để lưu trữ dữ liệu mà người dùng nhập vào từ bàn phím.
```
**Syn: print**
```bash
print(“…”, end=‘ ‘)

- end: thêm dấu nào đó khi in
```
## Hiển thị list of dict ra dạng bảng đẹp
**Ex1**
**Resource**
```python
data = [
    {"name": "An", "age": 20, "score": 8.5},
    {"name": "Bình", "age": 21, "score": 9.25},
    {"name": "Chi", "age": 19, "score": 7},
]
```
**Output**
```python
name | age | score
-----+-----+------
An   | 20  | 8.5  
Bình | 21  | 9.25 
Chi  | 19  | 7 
```
```python
def print_table(data: list) -> None:
    headers = list(data[0].keys())

    # Tính độ rộng mỗi cột
    col_widths = {
        h: max(len(str(h)), max(len(str(row[h])) for row in data))
        for h in headers
    }

    # In header
    header_line = " | ".join(f"{h:<{col_widths[h]}}" for h in headers)
    separator = "-+-".join("-" * col_widths[h] for h in headers)

    print(header_line)
    print(separator)

    # In dữ liệu
    for row in data:
        print(" | ".join(f"{str(row[h]):<{col_widths[h]}}" for h in headers))

data = [
    {"name": "An", "age": 20, "score": 8.5},
    {"name": "Bình", "age": 21, "score": 9.25},
    {"name": "Chi", "age": 19, "score": 7},
]

print_table(data)
```
**Ex2**
**Resource**
```python
data = {
    'names': ['Thang', "Minh", "Nghia", "Quy"],
    'ages': [18, 20, 23, 16],
    'scores': [10, 9, 6, 7]
}
```
**Output**
```python
names | ages | scores
------+------+-------
Thang | 18   | 10    
Minh  | 20   | 9     
Nghia | 23   | 6     
Quy   | 16   | 7 
```
**Answer**
```python
def convert_to_list_of_dict(data: dict):
    return [ 
        dict(zip(data.keys(), values))
        for values in zip(*data.values())
    ]

def print_table(data: list):
    headers = list(data[0].keys())
    
    col_widths = {
        h: max(len(h), max(len(str(row[h])) for row in data) )
        for h in headers
    }

    headers_line = ' | '.join(f'{h:<{col_widths[h]}}' for h in headers)
    separator = '-+-'.join('-'*col_widths[h] for h in headers)

    print(headers_line)
    print(separator)

    for row in data:
        print(" | ".join(f'{row[h]:<{col_widths[h]}}' for h in headers))
data = {
    'names': ['Thang', "Minh", "Nghia", "Quy"],
    'ages': [18, 20, 23, 16],
    'scores': [10, 9, 6, 7]
}

data = convert_to_list_of_dict(data)

print_table(data)
```

## Hiển thị list of list ra dạng bảng đẹp
**Resource**
```python
data = [
    ["Name", "Age", "Score"],
    ["An", 20, 8.5],
    ["Bình", 21, 9.25],
    ["Chi", 19, 7],
]
```
**Answer**
```python
def print_table_list(data):
    col_count = len(data[0])

    col_widths = [
        max(len(str(row[i])) for row in data)
        for i in range(col_count)
    ]

    for idx, row in enumerate(data):
        line = " | ".join(f"{str(cell):<{col_widths[i]}}" for i, cell in enumerate(row))
        print(line)

        if idx == 0:
            print("-+-".join("-" * w for w in col_widths))
```
## Nhập tên (Dữ liệu dạng chữ)
```bash
Đây là cách dùng cơ bản nhất để lấy thông tin văn bản.
```
```python
ten = input("Chào bạn, bạn tên là gì? ")
print("Rất vui được gặp bạn, " + ten + "!")
```

## Nhập số và thực hiện phép tính (Ép kiểu)
```bash
Vì input() trả về chuỗi, nên nếu bạn muốn tính toán, bạn phải ép kiểu nó sang số nguyên (int) hoặc số thực (float).
```
```python
nam_sinh_str = input("Bạn sinh năm bao nhiêu? ") # Nhập năm sinh
nam_sinh = int(nam_sinh_str) # Chuyển đổi từ chuỗi sang số nguyên để tính toán

tuoi = 2026 - nam_sinh
print(f"Vậy là năm nay bạn {tuoi} tuổi rồi!")
```

## Nhập nhiều giá trị trên một dòng
```bash
Đôi khi bạn muốn người dùng nhập nhiều thông tin cùng lúc (ví dụ: họ và tên cách nhau bởi dấu cách), bạn có thể dùng phương thức .split().
```
```python
ho, ten = input("Nhập Họ và Tên của bạn (cách nhau bởi dấu cách): ").split()
print(f"Họ của bạn là: {ho}")
print(f"Tên của bạn là: {ten}")
```

## Nhập ma trận (nxm)
```bash
2 3
1 2 3
4 5 6
```
**Ex1**
```python
# Nhập số hàng và số cột
n, m = map(int, input().split())

# Nhập ma trận
a = []
for _ in range(n):
    row = list(map(int, input().split()))
    a.append(row)

for row in a:
    print(*row)
```
**Ex2**
```python
n, m = map(int, input().split())
a = [list(map(int, input().split())) for _ in range(n)]

for row in a:
    print(*row)
```

## Tạo ra dict lưu tọa độ n điểm
**Topic**
```bash
Nhập vào tọa độ n điểm và lưu các tọa độ đó vào một dict
```
**Answer**
```python
n = int(input("Number of points: "))

print("=== Ex: A(x1, y1) ====")
coordinates = [input().strip() for _ in range(n)]

local_coordinates = {}

for c in coordinates:
    name, rest = c.split("(", 1)
    x, y = rest.rstrip(")").split(",")

    local_coordinates[name.strip()] = (int(x), int(y))

print(local_coordinates)

# Number of points: 2
# === Ex: A(x1, y1) ====
# A(1,2)
# B(3,6)
# {'A': (1, 2), 'B': (3, 6)}
```
## Nhập một số nguyên có ít hơn 5 chữ số
```python
num = None
while True:
    val = input('Input: ')
    
    if val.isdigit() and len(val) < 5:
        num = int(val)
        break
    else:
        print('Input must be Integer!!!')

print(num)

# isdigit không xử lý được số âm (-123) nếu nhập vào số âm sẽ cho ra kết quả sai.
# nếu vẫn muốn dùng isdigit cần xử lý thêm trường hợp số âm.
```