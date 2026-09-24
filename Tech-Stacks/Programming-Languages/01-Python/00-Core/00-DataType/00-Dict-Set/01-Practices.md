- [Exercise 1](#exercise-1)
- [Sắp xếp danh sách sự kiện](#sắp-xếp-danh-sách-sự-kiện)
    - [Tạo một dictionaries với keys là mã sinh viên, values là điểm trung bình](#tạo-một-dictionaries-với-keys-là-mã-sinh-viên-values-là-điểm-trung-bình)
    - [Tạo một dictionaries với 2 keys là mã sinh viên, điểm trung bình, values lưu list giá trị của keys tương ứng](#tạo-một-dictionaries-với-2-keys-là-mã-sinh-viên-điểm-trung-bình-values-lưu-list-giá-trị-của-keys-tương-ứng)
---
# Exercise 1
**Topic**
```bash
1. Khởi tạo một từ điển gồm n sinh viên, keys lưu mã sinh viên, values lưu điểm trung bình.
2. Hiển thị dưới dạng bảng.
```
**Answer**
```python
def input_dict():
    n = int(input('Số lượng sinh viên: '))

    dic = {
        input(f'mã của sinh viên thứ {i+1}: '): 
        float(input(f'Điểm của sinh viên thứ {i+1}: '))
        for i in range(n)
    }

    return dic

def print_table(dic: dict):
    headers = ['Mã sinh viên', 'Điểm trung bình']

    widths_id = max(len(headers[0]), max(len(k) for k in dic))
    width_score = max(len(headers[1]), max(len(str(v)) for v in dic.values()))

    print(f'{headers[0]:<{widths_id}} | {headers[1]:<{width_score}}')
    print(f'{"-"*widths_id}-+-{"-"*width_score}')

    for k, v in dic.items():
        print(f'{k:<{widths_id}} | {v:<{width_score}}')

dic = input_dict()
print_table(dic)
```
# Sắp xếp danh sách sự kiện
```bash
# cột 1 là địa điểm, cột 2 là số lượng khách.
data = {
    'event1': ['hanoi', 30],
    'event2': ['hanoi', 10],
    'event3': ['hanoi', 40],
    'event4': ['hanoi', 35],
}
```
```python
sorted_data = dict(
    sorted(data.items(), key=lambda item: item[1][1])
)
```
### Tạo một dictionaries với keys là mã sinh viên, values là điểm trung bình
**Comprehension**
```bash
- Comprehesion chỉ nên sử dụng khi dữ liệu sạch, chỉ cần biến đổi, vì rất khó bắt lỗi. 
```
```python
n = int(input('Số lượng phần tử: '))

dic = {
    input(f'mã sinh viên thứ {i+1}: '): float(input('điểm tb: '))
    for i in range(n)
}

print(dic)
```
**Try ... Except**
```python
while True:
    try:
        n = int(input('Số lượng sinh viên: '))
        if n > 0:
            break
        print('Phải nhập số nguyên dương!')
    except ValueError:
        print('Không phải số nguyên!')

def nhap_diem():
    while True:
        try:
            d = float(input('Điểm trung bình: '))
            if 0 <= d <= 10:
                return d
            print('Điểm phải từ 0 đến 10!')
        except ValueError:
            print('Phải nhập số!')

dic = {
    input(f'Mã sinh viên thứ {i+1}: '): nhap_diem()
    for i in range(n)
}
```

### Tạo một dictionaries với 2 keys là mã sinh viên, điểm trung bình, values lưu list giá trị của keys tương ứng
```python
n = int(input('Số lượng sinh viên: '))

dic = {
    'students_id': [input(f'mã sinh viên thứ {i+1}: ') for i in range(n)],
    'means_point': [input(f'điểm trung bình thứ {i+1}: ') for i in range(n)],
}

print(dic)
```