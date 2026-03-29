- [Transformation (biến đổi cấu trúc dữ liệu)](#transformation-biến-đổi-cấu-trúc-dữ-liệu)
  - [.rename()](#rename)
  - [.concat()](#concat)
  - [fillna()](#fillna)
  - [.values \& to\_numpy()](#values--to_numpy)
  - [.sort\_values()](#sort_values)
  - [groupby()](#groupby)
  - [.transform()](#transform)
  - [qcut()](#qcut)
---
# Transformation (biến đổi cấu trúc dữ liệu)
## .rename()
```bash
- Dùng để đổi tên cột hoặc chỉ mục của dataframe.
```
**Syn**
```bash
DataFrame.rename(
    mapper=None,
    *,
    index=None,
    columns=None,
    axis=None,
    copy=None,
    inplace=False,
    level=None,
    errors='ignore'

- errors
    + ignore' (mặc định): không lỗi nếu tên không tồn tại
    + 'raise': báo lỗi nếu không tìm thấy tên cần đổi
)
```
**Ex**
```python
import pandas as pd

data = {
    "user_name": ['thang', 'minh'],
    "user_email": ['leducthang', 'nguyenngocminh']
}

mapping = {
"user_name": "name",
"user_email": "email"
}

df = pd.DataFrame(data)
df = df.rename(columns=mapping)

print(df)

#     name           email
# 0  thang      leducthang
# 1   minh  nguyenngocminh
```
## .concat()
```bash
nối hoặc thêm dữ liệu mới vào dataframe
```
**Ex1: thêm mới một hàng**
```python
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
```
**Ex2: nối 2 dataframe**
```python
import pandas as pd

train = pd.DataFrame({
    'age': [10, 12, 14, 16],
    'score': [80, None, 90, 100]
})
test = pd.DataFrame({
    'age': [11, 15],
    'score': [None, 200]
})
df = pd.concat([train, test])

print(df)

#    age  score
# 0   10   80.0
# 1   12    NaN
# 2   14   90.0
# 3   16  100.0
# 0   11    NaN
# 1   15  200.0
```
## fillna()
```bash
- Điền giá trị còn thiếu
```
## .values & to_numpy()
```bash
- values    : Đưa một series, cột trong Dataframe về dạng list.
- to_numpy  : Đưa một series, cột trong Dataframe về dạng numpy array.
```
**Ex1: values với dict of list**
```python
import pandas as pd

data = {
    'size': [850, 900, 1200, 1500],
    'bedrooms': [2, 3, 3, 4],
    'age': [10, 15, 20, 5],
    'price': [200000, 250000, 300000, 350000]
}
df = pd.DataFrame(data)

print(df.values)
# [[   850      2     10 200000]
#  [   900      3     15 250000]
#  [  1200      3     20 300000]
#  [  1500      4      5 350000]]

print(df["size"].values, df["size"].values[1]) # [ 850  900 1200 1500] 900
```
**Ex2: values với key-value**
```python
dataFrame = pd.read_csv("danhSach.csv")
x = dataFrame.values[:, 0]

print(x) # [180 175 167 182 175 178 170 170 178 182 167 166 169 168 175 172]
```
**Ex3: to_numpy**
```python
import pandas as pd
data = {
        'size': [850, 900, 1200, 1500],
        'bedrooms': [2, 3, 3, 4],
        'age': [10, 15, 20, 5],
        'price': [200000, 250000, 300000, 350000]
    }
df = pd.DataFrame(data)
df = df['size'].to_numpy()

print(df, type(df)) # [ 850  900 1200 1500] <class 'numpy.ndarray'>
```
## .sort_values()
```bash
- Là hàm sắp xếp của pandas.
```
**Syn**
```bash
df.sort_values(
    by=...,          # cột (hoặc danh sách cột) để sắp xếp
    ascending=True,  # True: tăng dần | False: giảm dần
    inplace=False    # False: trả về DataFrame mới
)
```
**Ex1: Sắp giảm**
```python
import pandas as pd

df = pd.DataFrame({
    'name': ['A', 'B', 'C', 'D'],
    'sum_salary': [12_000_000, 20_000_000, 15_000_000, 20_000_000]
})
df_sorted = df.sort_values(by='sum_salary', ascending=False)

print(df_sorted)

#   name  sum_salary
# 1    B    20000000
# 3    D    20000000
# 2    C    15000000
# 0    A    12000000
```
**Ex2: Sắp xếp theo nhiều cột**
```python
df.sort_values(
    by=['sum_salary', 'name'],
    ascending=[False, True]
)

# Sắp theo sum_salary giảm dần
# Nếu trùng lương → sắp theo name tăng dần
```
## groupby()
```bash
- Là bước biến đổi dữ liệu dạng bảng thô sang dạng các nhóm dữ liệu.
- Nó thay đổi cách nhìn nhận cấu trúc dữ liệu.
```
**Syn**
```bash
df.groupby(by)[col]

- by : cột để group
- col : cột cần tính
```
## .transform()
```bash
- Là phép biến đổi dữ liệu. Thực hiện tính toán trên từng nhóm nhưng giữ nguyên số hàng
```
**Ex**
```python
import pandas as pd

df = pd.DataFrame({
    "team": ["A", "A", "A", "B", "B"],
    "score": [10, 20, 30, 15, 25]
})

df["team_avg"] = df.groupby("team")["score"].transform("mean")
```
## qcut()
```bash
- Chia dữ liệu theo quantile -> mỗi nhóm có số lượng phần tử gần bằng nhau
```
**Syn**
```bash
pd.qcut(
    x,
    q,
    labels=None,
    retbins=False,
    duplicates="raise"
)

- x : Series / array cần chia
- q :
    + int → số nhóm (ví dụ 4 = chia 4 phần bằng nhau)
    + hoặc list quantile [0, .25, .5, .75, 1]
- labels : tên nhãn cho mỗi nhóm
- retbins=True : trả về cả mốc chia
```
**Ex1: chia điểm thi thành 4 nhóm**
```python
import pandas as pd

scores = pd.Series([40, 55, 60, 65, 70, 75, 80, 85, 90, 95])

print(pd.qcut(scores, q=4))

# 0    (39.999, 61.25]
# 1    (39.999, 61.25]
# 2    (39.999, 61.25]
# 3      (61.25, 72.5]
# 4      (61.25, 72.5]
# 5      (72.5, 83.75]
# 6      (72.5, 83.75]
# 7      (83.75, 95.0]
# 8      (83.75, 95.0]
# 9      (83.75, 95.0]
# dtype: category
# Categories (4, interval[float64, right]): [(39.999, 61.25] < (61.25, 72.5] < (72.5, 83.75] <
#                                            (83.75, 95.0]]
```
**Ex2: phân nhóm thu nhập**
```python
df = pd.DataFrame({
    "income": [5, 7, 10, 12, 15, 18, 20, 25, 30, 50]
})

df["income_group"] = pd.qcut(
    df["income"],
    q=3,
    labels=["Low", "Mid", "High"]
)

print(df)
```