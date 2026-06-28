- [lọc có điều kiện trong dataframe](#lọc-có-điều-kiện-trong-dataframe)
- [Quản lý nhân viên bằng pandas](#quản-lý-nhân-viên-bằng-pandas)
- [Quản lý danh sách công nhân](#quản-lý-danh-sách-công-nhân)
---
# lọc có điều kiện trong dataframe
```python
import pandas as pd
data = {
    'name': ['thang', 'tien', 'thuy', 'thanh', 'hong'],
    'salary': [10, 20, 8, 5, 9]
}

df = pd.DataFrame(data)
new_df = df[df['salary'] > 8.5]

print(new_df)

#     name  salary
# 0  thang      10
# 1   tien      20
# 4   hong       9
```
# Quản lý nhân viên bằng pandas
**Data**
```python
import pandas as pd

data = {
    'name': ['thang', 'minh', 'nghia', 'thinh', 'thanh', 'tu'],
    'salary': [20, 12, 10, None , 7, 5],
    'city': ['hanoi', 'hcm', 'danang', 'canthoi', 'hanoi', 'haiphong']
}
df = pd.DataFrame(data)
print(df)
```
**Tìm xem ai chưa có lương rồi hiển thị**
```python
non_salary = df[df['salary'].isnull()]
print(non_salary)
```
**ai chưa có lương thì thêm 10 vào lương**
```python
df.loc[df['salary'].isnull(), 'salary'] = 10
print(df)
```
**sắp xếp theo lương tăng dần**
```python
df.sort_values('salary', ascending=True, inplace=True)
print(df)
```
**tìm xem name có người tên trí chưa nếu chưa thì thêm vào**
```python
if 'tri' not in df['name'].values:
    df.loc[len(df)] = ['tri', 8, 'hanoi']
print(df)
```
# Quản lý danh sách công nhân
**Topic**
```bash
Quản lý danh sách công nhân gồm:
- id – mã công nhân
- name – họ tên
- salary – lương ngày
- days_work – số ngày làm việc
- allowance – phụ cấp
Yêu cầu:
- Tạo DataFrame
- Tính tổng lương
- Lọc công nhân có tổng lương > 15 triệu
- Đếm số công nhân thỏa điều kiện
- Sắp xếp theo tổng lương giảm dần
- Sửa phụ cấp theo điều kiện
- Xóa công nhân có lương = 0
- Ghi ra file CSV
```
```python
import pandas as pd

def input_workers():
    n = int(input("Số lượng công nhân: "))
    
    data = []
    for i in range(n):
        print(f"\nNhập công nhân thứ {i+1}")

        worker = {
            'worker_id': input('Mã công nhân: '),
            'name': input('Họ tên: '),
            'days_work': float(input('Số ngày làm việc: ')),
            'salary': float(input('Lương ngày: ')),
            'sum_salary': None
        }

        data.append(worker)

    df = pd.DataFrame(data)

    return df

def calculate_salary(df):
    df['sum_salary'] = df['salary'] * df['days_work'] + df['allowance']
    print("\n=== Đã tính tổng lương ===")
    print(df)

def filter_high_salary(df):
    df_high = df[df['sum_salary'] > 15_000_000]
    print("\n=== Công nhân có thu nhập > 15 triệu ===")
    print(df_high)
    print("Số lượng:", df_high.shape[0])

def sort_by_salary(df):
    df_sorted = df.sort_values(by='sum_salary', ascending=False)
    print("\n=== Danh sách sắp xếp theo tổng lương giảm dần ===")
    print(df_sorted)
    return df_sorted

def update_allowance(df):
    df.loc[df['days_work'] > 26, 'allowance'] += 200_000
    df['sum_salary'] = df['salary'] * df['days_work'] + df['allowance']
    print("\n=== Đã cập nhật phụ cấp ===")
    print(df)

def delete_zero_salary(df):
    df = df[df['salary'] != 0]
    print("\n=== Sau khi xóa công nhân có lương = 0 ===")
    print(df)
    return df

def save_csv(df):
    df.to_csv("cong_nhan.csv", index=False, encoding="utf-8-sig")
    print("\nĐã ghi file cong_nhan.csv")


def main():
    df = None

    print("=== MENU ===")
    print("0. Thoát")
    print("1. Nhập danh sách công nhân")
    print("2. Tính tổng lương")
    print("3. Lọc & đếm thu nhập > 15 triệu")
    print("4. Sắp xếp theo tổng lương")
    print("5. Sửa phụ cấp")
    print("6. Xóa công nhân lương = 0")
    print("7. Ghi ra file CSV")

    while True:
        option = int(input("\nChọn chức năng: "))

        if option == 0:
            break
        elif option == 1:
            df = input_workers()
            print(df)
        elif option == 2:
            calculate_salary(df)
        elif option == 3:
            filter_high_salary(df)
        elif option == 4:
            df = sort_by_salary(df)
        elif option == 5:
            update_allowance(df)
        elif option == 6:
            df = delete_zero_salary(df)
        elif option == 7:
            save_csv(df)
main()
```
**Ex2**
```python
import pandas as pd

# ===== KHỞI TẠO DATAFRAME =====
def init_df():
    return pd.DataFrame(
        columns=["worker_id", "name", "salary", "days_work", "allowance", "sum_salary"]
    )


# ===== NHẬP DANH SÁCH =====
def input_workers():
    n = int(input("Số lượng công nhân: "))
    data = []

    for i in range(n):
        print(f"--- Công nhân {i+1} ---")
        wid = input("Mã: ")
        name = input("Họ tên: ")
        salary = float(input("Lương/ngày: "))
        days = int(input("Số ngày làm: "))
        allowance = float(input("Phụ cấp: "))

        data.append({
            "worker_id": wid,
            "name": name,
            "salary": salary,
            "days_work": days,
            "allowance": allowance,
            "sum_salary": salary * days + allowance
        })

    return pd.DataFrame(data)

# ===== IN BẢNG =====
def print_table(df):
    if df.empty:
        print("Danh sách rỗng")
    else:
        print(df.to_string(index=False))


# ===== THÊM CÔNG NHÂN =====
def add_worker(df):
    wid = input("Mã: ")
    name = input("Họ tên: ")
    salary = float(input("Lương/ngày: "))
    days = int(input("Số ngày làm: "))
    allowance = float(input("Phụ cấp: "))

    new_row = {
        "worker_id": wid,
        "name": name,
        "salary": salary,
        "days_work": days,
        "allowance": allowance,
        "sum_salary": salary * days + allowance
    }

    return pd.concat([df, pd.DataFrame([new_row])], ignore_index=True)


# ===== TÍNH LẠI LƯƠNG =====
def calc_salary(df):
    df["sum_salary"] = df["salary"] * df["days_work"] + df["allowance"]


# ===== SỬA THEO MÃ =====
def update_worker(df):
    wid = input("Nhập mã cần sửa: ")

    if wid not in df["worker_id"].values:
        print("Không tìm thấy!")
        return

    df.loc[df["worker_id"] == wid, "salary"] = float(input("Lương mới: "))
    df.loc[df["worker_id"] == wid, "days_work"] = int(input("Ngày làm mới: "))
    df.loc[df["worker_id"] == wid, "allowance"] = float(input("Phụ cấp mới: "))

    calc_salary(df)


# ===== XÓA THEO MÃ =====
def delete_worker(df):
    wid = input("Nhập mã cần xóa: ")
    return df[df["worker_id"] != wid]


# ===== LỌC + ĐẾM =====
def filter_high_salary(df):
    df_high = df[df["sum_salary"] > 15_000_000]
    print("\n=== Thu nhập > 15 triệu ===")
    print_table(df_high)
    print("Số lượng:", len(df_high))


# ===== SẮP XẾP =====
def sort_by_salary(df):
    return df.sort_values(by="sum_salary", ascending=False)


# ===== GHI FILE CSV =====
def save_to_csv(df):
    df.to_csv("workers.csv", index=False)
    print("Đã ghi file workers.csv")


# ===== MENU =====
def main():
    df = init_df()

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
9. Ghi ra file CSV
""")
        choice = int(input("Chọn: "))

        if choice == 0:
            break
        elif choice == 1:
            df = input_workers()
        elif choice == 2:
            print_table(df)
        elif choice == 3:
            calc_salary(df)
            print("Đã tính lương")
        elif choice == 4:
            df = add_worker(df)
        elif choice == 5:
            update_worker(df)
        elif choice == 6:
            df = delete_worker(df)
        elif choice == 7:
            filter_high_salary(df)
        elif choice == 8:
            df = sort_by_salary(df)
            print("Đã sắp xếp")
        elif choice == 9:
            save_to_csv(df)

main()
```