```bash
- Đây nơi chứa các hàm, phương thức về xử lý file.
```

JSON
Là cú pháp để lưu trữ và trao đổi dữ liệu.
JSON là văn bản, được viết bằng ký hiệu đối tượng Javascript.
json.loads()
Để phân tích cú pháp nhằm mục đích chuyển từ JSON sang Python.
Cú pháp:
json.loads(<variable>)
json.dumps()# .name
```bash
Trả về tên của file đang được mở.
```
**Ex**
```python
txt = open("D:\\workspace\Python_box\\a.txt", "rt")
print(txt.name) # D:\workspace\Python_box\a.txt
```# open() & .close()
```bash
Để mở file và đóng file.
```
**Syn**
```bash
open(‘data.txt’, ‘w’, encoding=’utf8’)
    + r – Đọc – Giá trị mặc định. Mở tệp để đọc, báo lỗi nếu tệp không tồn tại.
    + a – Thêm – Mở tệp để thêm, tạo tệp nếu tệp không tồn tại. Thêm vào cuối file.
    + w – Ghi – Mở tệp để ghi, tạo tệp nếu tệp không tồn tại. Ghi đè nếu file có nội dung trước đó.
    + t – Văn bản – Giá trị mặc định. Chế độ văn bản.
    + b – Nhị phân – Chế độ nhị phân (Ví dụ: hình ảnh).
    + "w+"  : Đọc + ghi đè	
    + "a+"  : Đọc + ghi tiếp	
    + "r+"  : Đọc + ghi (không xóa)	
```# .read()
```bash
Dùng để đọc nội dung một file.
```
**Syn**
```bash
name.read(n)
    + n: Đọc ra n nội dụng. Không truyền tham số gì mặc định là đọc toàn bộ file
```
**Ex**
```python
txt = open("E:\\Python\Text.txt", "rt")
print(txt.read()) # Hello world, i am Thang and i am coder, welcome to my world,
txt.close()
```

# .readline()
```bash
Đọc nội dung file theo dòng. Chỉ đọc một dòng.
```
**Syn**
```bash
<variable>.readline()
```
**Ex**
```python
txt = open("E:\\Python\Text.txt", "rt")
print(txt.readline()) # Hello
txt.close()
```

# .readlines()
```bash
Tạo ra một mảng. Mỗi dòng trong file sẽ tương ứng với một phần tử trong mảng.
```
**Syn**
```bash
<variable>.readlines()
```
**Ex**
```python
txt = open("E:\\Python\Text.txt", "rt")
print(txt.readlines()) # ['Hello\n', 'My name is Thang\n', 'I am from VietNam']
txt.close()
```# .write()
```bash
Để ghi vào một file.
```
**Syn**
```python
txt = open("E:\\Python\Text.txt", "wt") # Tại file Text.txt có nội dung: Hello world
txt.write("i am from VietNam") # 'i am from VietNam' sẽ được ghi vào file
# With … as
```bash
- with dùng để quản lý tài nguyên tự động:
    + Tự mở → tự đóng (file, database, network, lock…)
    + Tự giải phóng tài nguyên kể cả khi code bị lỗi
    + Không cần viết try / finally

- Nó hoạt động dựa trên giao thức context manager:
    + __enter__()
    + __exit__()
```
**Ex1: Không dùng with ... as**
```python
f = open("data.txt", "w")
f.write("hello")
f.close()  # nếu quên close → rò rỉ tài nguyên

# Nếu code bị lỗi trước khi close() → file không được đóng.
```
**Ex2: Có dùng with ... as**
```python
with open("data.txt", "w") as f:
    f.write("hello world")

# File tự đóng dù có lỗi trong block
```
**Ex3**
```python
with open("data.txt", "r", encoding="utf8") as f:
    content = f.read()
    print(content)

# Khi block with kết thúc → file tự đóng.
```
**Ex4**
```python
with open("input.txt") as inp, open("output.txt", "w") as out:
    for line in inp:
        out.write(line.upper())

# Rất tiện để xử lý nhiều file.
```# Đọc ghi file
**Resources**
**input.txt**
```bash
Hello world
File handling is important
Hello file
I love programming
```
**Topic**
```bash
- Đọc toàn bộ nội dung từ file input.txt.
- Thực hiện các xử lý sau:
    + Đếm số dòng trong file.
    + Đếm tổng số từ trong file.
    + Đếm số lần xuất hiện của từ "hello" (không phân biệt hoa/thường).
    + Ghi kết quả ra file output.txt theo định dạng:
- output.txt
Number of lines: X
Number of words: Y
Occurrences of 'hello': Z
```
**Answer**
```python
import os

input_file = 'input.txt'
output_file = 'output.txt'

if not os.path.exists(input_file):
    print("Input file does not exist")
else:
    with open(input_file, 'r') as inp, open(output_file, 'w') as out:
        lines = [line.strip() for line in inp]

        num_lines = len(lines)
        words = [word.lower() for line in lines for word in line.split()]
        num_words = len(words)
        hello_count = words.count('hello')

        print('Number of lines:', num_lines)
        print('Number of words:', num_words)
        print("Occurrences of 'hello':", hello_count)

        out.write(f"Number of lines: {num_lines}\n")
        out.write(f"Number of words: {num_words}\n")
        out.write(f"Occurrences of 'hello': {hello_count}\n")
        out.write('-' * 30 + '\n')
```