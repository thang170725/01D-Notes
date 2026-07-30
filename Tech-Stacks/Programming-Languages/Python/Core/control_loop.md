- [if … else](#if--else)
- [Short Hand If … else](#short-hand-if--else)
- [assert](#assert)
  - [type()](#type)
- [Bài tập](#bài-tập)
  - [Demo bài tập 1](#demo-bài-tập-1)
  - [Bài tập 2](#bài-tập-2)

---

# if … else
**Ex1: Tìm kiếm 1 phần tử có nằm trong một mảng hay không**
```bash
a = ["VietNam", "America", "Island", "Porland", "Canada"]

if "ThaiLand" in a: # kiểm tra xem ThaiLand có xuất hiện trong mảng không
    print("True")
else:
    print("False")

# False
```
**Ex2: Kiểm tra xem mảng có phần tử nào không**
```python
a = ["VietNam", "America", "Island", "Porland", "Canada"]

if a:
    print("is not Empty")
else:
    print("is Empty")

# is not Empty
# mảng a đang có 5 phần từ nên in ra “is not Empty”
```

# Short Hand If … else
**Ex**
```python
a = ["VietNam", "America", "Island", "Porland", "Canada"]
print(True) if "ThaiLand" in a else print("False") # False
```

# assert
```bash
- Một cách để kiểm tra điều kiện, nếu điều kiện không đúng, Python sẽ ném ra AssertionError và có thể kèm thông điệp tùy chỉnh. Nó rất hữu ích để debug hoặc bảo vệ code khỏi dữ liệu sai.
```
**Syn**
```bash
assert condition, "Thông báo nếu điều kiện sai"
    + condition: biểu thức boolean bạn muốn kiểm tra (True hoặc False)
    + Nếu condition = True → code tiếp tục chạy bình thường
    + Nếu condition = False → ném AssertionError kèm thông báo
```
**Ex**
```python
x = 5
assert x > 0, "x phải lớn hơn 0"
print("Code tiếp tục chạy bình thường")
```
## type()
```bash
print(type(a)) # <class 'str'>
```

# Bài tập
## Demo bài tập 1
```python
from typing import List, Dict

def input_workers() -> List[Dict[str, str | float]]:
    data = []

    n = int(input('Số lượng công nhân: '))

    for i in range(n):
        print(f'\nNhập công nhân thứ {i+1}')

        worker = {
            'worker_id': input('Mã công nhân: '),
            'name': input('Họ tên công nhân: '),
            'salary': float(input('Lương: ')),
            'days_work': float(input('Số ngày làm việc: ')),
            'allowance': float(input('Phụ cấp: '))
        }

        data.append(worker)
    
    return data

def print_table(data: List[Dict[str, str | float]]) -> None:
    headers = data[0].keys()

    col_widths = {
        h: max(len(h), max(len(str(row[h])) for row in data))
        for h in headers
    }

    print(' | '.join(f'{h:<{col_widths[h]}}' for h in headers))
    print('-+-'.join('-'*col_widths[h] for h in headers))

    for row in data:
        print(' | '.join(f'{str(row[h]):<{col_widths[h]}}' for h in headers))

def salary_calculation(list_workers: List[Dict[str, str | float]]):
    for i in range(len(list_workers)):
        row = list_workers[i]
        salary = row['salary']*row['days_work']
        list_workers[i]['sum_salary'] = salary

def sum_salary_max(list_workers: list):
    max_salary = 0

    for i in range(len(list_workers)):
        row = list_workers[i]
        if max_salary < row['sum_salary']:
            max_salary = row['sum_salary']

    list_max = []
    for i in range(len(list_workers)):
        row = list_workers[i]
        if row['sum_salary'] == max_salary:
            list_max.append(row)

    print('Số người có thu nhập nhiều nhất: ', len(list_max))
    print('=== Danh sách người có thu nhập lớn nhất ===')
    print_table(list_max)

def count_workers(list_workers):
    c = 0
    for i in range(len(list_workers)):
        row = list_workers[i]
        if row['salary'] != 0 and row['sum_salary'] > 15_000_000:
            c += 1
    
    print('Số lương công nhân không có thu nhập bằng 0 và tổng thu nhập lớn hơn 15 triệu là: ', c)

def main():
    list_workers = []

    print('=== Options ===')
    print('0. Thoát')
    print('1. Khởi tạo danh sách')
    print('2. Tính lương cơ bản')
    print('3. Số người có thu nhập lớn nhất')
    print('4. Số công nhận có thu nhập khác 0 và tổng thu nhập nhiều hơn 15 triệu')
    while True:
        option = int(input('Chọn options: '))

        if option == 0:
            break
        elif option == 1:
            list_workers = input_workers()
            print_table(list_workers)
        elif option == 2:
            salary_calculation(list_workers)
            print_table(list_workers)
        elif option == 3:
            sum_salary_max(list_workers)
        elif option == 4:
            count_workers(list_workers)
main()
```

## Bài tập 2
**Topic**
```bash
BÀI ÔN TẬP: QUẢN LÝ CÔNG NHÂN (KHÔNG DÙNG PANDAS)
Thuộc tính mỗi công nhân
- worker_id
- name
- salary (lương/ngày)
- days_work
- allowance
- sum_salary (tự tính)
Các nghiệp vụ có trong bài
✔ Khởi tạo danh sách (nhập)
✔ Thêm công nhân
✔ Sửa công nhân theo mã
✔ Xóa công nhân theo mã
✔ In bảng đẹp
✔ Tính tổng lương
✔ Lọc theo điều kiện
✔ Đếm theo điều kiện
✔ Sắp xếp
✔ Menu chuẩn đề thi
```
```python
from typing import List, Dict

# ===== NHẬP DANH SÁCH =====
def input_workers() -> List[Dict]:
    workers = []
    n = int(input("Số lượng công nhân: "))

    for i in range(n):
        print(f"--- Công nhân {i+1} ---")
        worker = {
            "worker_id": input("Mã: "),
            "name": input("Họ tên: "),
            "salary": float(input("Lương/ngày: ")),
            "days_work": int(input("Số ngày làm: ")),
            "allowance": float(input("Phụ cấp: "))
        }
        workers.append(worker)
    return workers


# ===== IN BẢNG =====
def print_table(data: List[Dict]):
    if not data:
        print("Danh sách rỗng")
        return

    headers = data[0].keys()
    widths = {h: max(len(h), max(len(str(r[h])) for r in data)) for h in headers}

    print(" | ".join(f"{h:<{widths[h]}}" for h in headers))
    print("-+-".join("-" * widths[h] for h in headers))

    for r in data:
        print(" | ".join(f"{str(r[h]):<{widths[h]}}" for h in headers))


# ===== TÍNH LƯƠNG =====
def calc_salary(workers: List[Dict]):
    for w in workers:
        w["sum_salary"] = w["salary"] * w["days_work"] + w["allowance"]


# ===== THÊM CÔNG NHÂN =====
def add_worker(workers: List[Dict]):
    worker = {
        "worker_id": input("Mã: "),
        "name": input("Họ tên: "),
        "salary": float(input("Lương/ngày: ")),
        "days_work": int(input("Số ngày làm: ")),
        "allowance": float(input("Phụ cấp: "))
    }
    workers.append(worker)


# ===== SỬA THEO MÃ =====
def update_worker(workers: List[Dict]):
    wid = input("Nhập mã cần sửa: ")
    for w in workers:
        if w["worker_id"] == wid:
            w["salary"] = float(input("Lương mới: "))
            w["days_work"] = int(input("Ngày làm mới: "))
            w["allowance"] = float(input("Phụ cấp mới: "))
            return
    print("Không tìm thấy!")


# ===== XÓA THEO MÃ =====
def delete_worker(workers: List[Dict]):
    wid = input("Nhập mã cần xóa: ")
    for i in range(len(workers)):
        if workers[i]["worker_id"] == wid:
            workers.pop(i)
            return
    print("Không tìm thấy!")


# ===== LỌC THU NHẬP > 15 TRIỆU =====
def filter_high_salary(workers: List[Dict]):
    result = []
    for w in workers:
        if w.get("sum_salary", 0) > 15_000_000:
            result.append(w)
    print_table(result)
    print("Số lượng:", len(result))


# ===== SẮP XẾP THEO LƯƠNG GIẢM DẦN =====
def sort_by_salary(workers: List[Dict]):
    workers.sort(key=lambda x: x.get("sum_salary", 0), reverse=True)


# ===== MENU =====
def main():
    workers = []

    while True:
        print("""
0. Thoát
1. Nhập danh sách
2. In danh sách
3. Tính lương
4. Thêm công nhân
5. Sửa công nhân
6. Xóa công nhân
7. Lọc thu nhập > 15 triệu
8. Sắp xếp theo lương giảm dần
""")
        choice = int(input("Chọn: "))

        if choice == 0:
            break
        elif choice == 1:
            workers = input_workers()
        elif choice == 2:
            print_table(workers)
        elif choice == 3:
            calc_salary(workers)
        elif choice == 4:
            add_worker(workers)
        elif choice == 5:
            update_worker(workers)
        elif choice == 6:
            delete_worker(workers)
        elif choice == 7:
            filter_high_salary(workers)
        elif choice == 8:
            sort_by_salary(workers)
            print("Đã sắp xếp!")


main()
```
Vòng lặp
Là cấu trúc lặp. ctrl+C để thoát khỏi vòng lặp vô hạn.


Cú pháp:
while <condition>:
	statement
number = int(input("Nhập số nguyên: "))
result = ""
while number > 0:
    remainder = number%2
    result += str(remainder)
    number //= 2
print(result[::-1])
Nhập số nguyên: 524
1000001100
Range()
Là cấu trúc vòng lặp dạng basic.
Cú pháp:
    • range(start, stop, step)
    • range(start,  stop)
a = [1,2,3,4,5]
for i in range(0,len(a)):
    print(a[i])
1
2
3
4
5
for i in range(5,1,-1):
    print(i)
5
4
3
2
str = str(input("Nhập chuỗi nhị phân: "))
sum = 0
for i in range(0, len(str)):
    sum += int(str[i])*pow(2, len(str)-i-1)
print(sum)
Nhập chuỗi nhị phân: 1010101100
684
a = list(range(1, 6))
[1,2,3,4,5]
a = [i for i in range(1, 6)]
[1,2,3,4,5]

enumrate()
Để duyệt qua một chuỗi như danh sách, tuple, chuỗi ký tự, … Đồng thời lấy ra các số index và giá trị của từng phần tử trong chuỗi.
Cú pháp: enumerate(fruits, start=1)
fruits = ["táo", "chuối", "cam"]
for index, fruit in enumerate(fruits):
    print(f"Trái cây thứ {index + 1} là {fruit}")
Trái cây thứ 1 là táo
Trái cây thứ 2 là chuối
Trái cây thứ 3 là cam

