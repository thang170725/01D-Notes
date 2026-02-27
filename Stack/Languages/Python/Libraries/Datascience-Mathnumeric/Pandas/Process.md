- [.rename()](#rename)
- [.duplicated()](#duplicated)
  - [.drop() \& .dropna() \& .drop\_duplicates()](#drop--dropna--drop_duplicates)
  - [fillna()](#fillna)
- [loc](#loc)
- [pd.notnull()](#pdnotnull)
- [.isna() \& .isnull()](#isna--isnull)
- [.notna()](#notna)
- [DataFrame \& Series](#dataframe--series)
- [.shape](#shape)
- [Tạo thêm cột mới trong dataframe](#tạo-thêm-cột-mới-trong-dataframe)
- [Tạo tên cột cho dataframe](#tạo-tên-cột-cho-dataframe)
- [pd.options.display.max\_rows](#pdoptionsdisplaymax_rows)
- [.value\_counts()](#value_counts)
- [.values \& to\_numpy()](#values--to_numpy)
- [.nunique()](#nunique)
- [.sort\_values()](#sort_values)
- [.where()](#where)
- [.concat()](#concat)
- [.sum()](#sum)
- [.mean()](#mean)
- [groupby()](#groupby)
  - [.transform()](#transform)
- [qcut()](#qcut)
---
# .rename()
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
# .duplicated()
```bash
- Để phát hiện dòng trùng lặp trong DataFrame.
```
**Syn**
```bash
df.duplicated(subset=None, keep='first')

- subset: (tùy chọn) — cột hoặc danh sách cột để kiểm tra trùng (mặc định kiểm tất cả cột)
- keep:
    + 'first': đánh dấu True từ dòng trùng thứ 2 trở đi
    + 'last': đánh dấu True trừ dòng cuối cùng
    + False: tất cả các dòng trùng đều được đánh dấu T
```
**Ex**
```python
import pandas as pd

# Tạo DataFrame mẫu
df = pd.DataFrame({
    'ID': [1, 2, 2, 3, 4, 4, 4, 5],
    'Name': ['An', 'Bình', 'Bình', 'Cường', 'Dũng', 'Dũng', 'Dũng', 'Hà']
})

print("=== Dataset gốc ===")
print(df)

# 1️⃣ Phát hiện dòng trùng (toàn bộ cột)
print("\nDuplicated toàn bộ cột:")
print(df.duplicated())

# 2️⃣ Phát hiện trùng theo cột 'ID'
print("\nDuplicated theo cột ID:")
print(df.duplicated(subset='ID'))

# 3️⃣ Giữ dòng cuối cùng thay vì dòng đầu
print("\nDuplicated (keep='last'):")
print(df.duplicated(subset='ID', keep='last'))

# 4️⃣ Đánh dấu tất cả các dòng trùng
print("\nDuplicated (keep=False):")
print(df.duplicated(subset='ID', keep=False))

# 5️⃣ Lọc ra các dòng trùng
print("\nCác dòng trùng lặp:")
print(df[df.duplicated(subset='ID', keep=False)])
```
## .drop() & .dropna() & .drop_duplicates()
```bash
- drop              : Xóa hàng (row) hoặc cột (column) khỏi DataFrame.
- dropna            : xóa dòng có giá trị thiếu.
- drop_duplicates   : xóa dòng trùng
```
**Syn: drop**
```bash 
DataFrame.drop(labels=None, axis=0, inplace=False)

- labels: Tên hàng hoặc cột cần xóa.
- axis: Xác định loại đối tượng cần xóa. 0 hoặc index – xóa theo hàng, 1 hoặc columns – xóa theo cột.
- inplace: False (mặc định) trả về một bản sao mới của dataframe. True là thay đổi trực tiếp trên DataFrame gốc.
```
**Syn: dropna**
```bash
df = df.dropna(
    subset=['Age'],
    how='all',
    thresh=3
)

- subset    : chỉ cần cột Age thiếu là bỏ dòng đó
- how       : xóa dòng nếu thiếu tất cả các cột
- thresh    : xóa dòng nếu thiếu >= N cột
```
**Syn: drop_duplicates**
```bash
df_no_dup = df.drop_duplicates(subset='ID', keep='first')
```
**Ex1: drop**
```python
import pandas as pd

# dữ liệu gốc dạng chuỗi
df = pd.DataFrame({
    'name': ['Lan', 'Mai', 'Huy'],
    'age': [19, 20, 21]}
)

print("DataFrame ban đầu\n", df)

newDf = df.drop('age', axis=1) # xóa cột age
print(newDf)

newDf1 = df.drop(0, axis=0) # xóa hàng đầu tiên
print(newDf1)

# DataFrame ban đầu
# name  age
# 0  Lan   19
# 1  Mai   20
# 2  Huy   21
#  name
# 0  Lan
# 1  Mai
# 2  Huy
# name  age
# 1  Mai   20
# 2  Huy   21
```
**Ex2: drop_duplicates**
```python
# Tạo DataFrame mẫu
df = pd.DataFrame({
    'ID': [1, 2, 2, 3, 4, 4, 4, 5],
    'Name': ['An', 'Bình', 'Bình', 'Cường', 'Dũng', 'Dũng', 'Dũng', 'Hà']
})

df = df.drop_duplicates(subset=['ID'], keep='first')
print(df)

#    ID   Name
# 0   1     An
# 1   2   Bình
# 3   3  Cường
# 4   4   Dũng
# 7   5     Hà
```
## fillna()
```bash
- Điền giá trị còn thiếu
```
- [loc](#loc)
- [pd.notnull()](#pdnotnull)
- [.isna() \& .isnull()](#isna--isnull)
- [.notna()](#notna)
---
# loc
```bash
- Chọn theo nhãn hoặc theo điều kiện.
```
**Ex1: Lấy ra một hàng theo index**
```python
import pandas as pd

data = {
    "full_name": ["John", "Jane", "Tom", 'Quoc'],
    "address": ["New York", "HaNoi", "Tokyo", 'HCM'],
    'country': ['USA', 'Viet Nam', 'Japan', 'Viet Nam']
    }
df = pd.DataFrame(data)

print(df.loc[1])
print(list(df.loc[1]))

# full_name        Jane
# address         HaNoi
# country      Viet Nam
# Name: 1, dtype: object
# ['Jane', 'HaNoi', 'Viet Nam']
```
**Ex2: lấy nhiều hàng theo nhiều index**
```python
import pandas as pd

data = {
    "full_name": ["John", "Jane", "Tom", 'Quoc'],
    "address": ["New York", "HaNoi", "Tokyo", 'HCM'],
    'country': ['USA', 'Viet Nam', 'Japan', 'Viet Nam']
    }
df = pd.DataFrame(data)

print(df.loc[[1, 2]])
```
**Ex3: Lấy theo điều kiện**
```python
import pandas as pd

data = {
    "full_name": ["John", "Jane", "Tom", 'Quoc'],
    "address": ["New York", "HaNoi", "Tokyo", 'HCM'],
    'country': ['USA', 'Viet Nam', 'Japan', 'Viet Nam']
    }
df = pd.DataFrame(data)

print(df.loc[df['country'] == 'Viet Nam'])
```
**Ex4: lấy theo điều kiện đồng thời thay đổi theo điều kiện**
```python
import pandas as pd

data = {
    "full_name": ["John", "Jane", "Tom", 'Quoc'],
    "address": ["New York", "HaNoi", "Tokyo", 'HCM'],
    'country': ['USA', 'Viet Nam', 'Japan', 'Viet Nam'],
    'salary': [10, 20, 30, 10]
    }
df = pd.DataFrame(data)
df.loc[df['country'] == 'Viet Nam', 'salary'] += 10
print(df)
```
# pd.notnull() 
```bash
- Là hàm kiểm tra dữ liệu KHÔNG bị thiếu trong pandas.
- pd.notnull(df) = giá trị có dữ liệu → True, bị thiếu → False
- Pandas coi các giá trị sau là missing:
    + NaN
    + None
    + NaT (thời gian)
    + pd.NA
```
**Syn**
```bash
pd.notnull(obj)

- obj có thể là: scalar, Series, DataFrame
```
**Ex**
```python
iimport pandas as pd
import numpy as np

df = pd.DataFrame({
    'name': ['An', None, 'Chi'],
    'age': [20, np.nan, 25]
})
check = pd.notnull(df)

print(df)
print(check)

   name   age
0    An  20.0
1  None   NaN
2   Chi  25.0
    name    age
0   True   True
1  False  False
2   True   True
```
# .isna() & .isnull()
```bash
Dùng để tìm giá trị NaN trong một cột dữ liệu, thường để lọc data.
```
**Ex**
```python
import pandas as pd

data = {
    'name': ['thang', 'minh', 'nghia', 'thinh', 'thanh', 'tu'],
    'salary': [20, 12, 10, None , 7, 5],
    'city': ['hanoi', 'hcm', 'danang', 'canthoi', 'hanoi', 'haiphong']
}
df = pd.DataFrame(data)
non_salary = df['salary'].isna() # df['salary'].isnull()

print(non_salary)

# 0    False
# 1    False
# 2    False
# 3     True
# 4    False
# 5    False
# Name: salary, dtype: bool
```
# .notna()
**Ex: tìm người đã có lương**
```python
has_salary = df[df['salary'].notna()]
```
- [.rename()](#rename)
- [.duplicated()](#duplicated)
  - [.drop() \& .dropna() \& .drop\_duplicates()](#drop--dropna--drop_duplicates)
  - [fillna()](#fillna)
- [loc](#loc)
- [pd.notnull()](#pdnotnull)
- [.isna() \& .isnull()](#isna--isnull)
- [.notna()](#notna)
- [DataFrame \& Series](#dataframe--series)
- [.shape](#shape)
- [Tạo thêm cột mới trong dataframe](#tạo-thêm-cột-mới-trong-dataframe)
- [Tạo tên cột cho dataframe](#tạo-tên-cột-cho-dataframe)
- [pd.options.display.max\_rows](#pdoptionsdisplaymax_rows)
- [.value\_counts()](#value_counts)
- [.values \& to\_numpy()](#values--to_numpy)
- [.nunique()](#nunique)
- [.sort\_values()](#sort_values)
- [.where()](#where)
- [.concat()](#concat)
- [.sum()](#sum)
- [.mean()](#mean)
- [groupby()](#groupby)
  - [.transform()](#transform)
- [qcut()](#qcut)
---
# DataFrame & Series
```bash
- series    : Cấu trúc dữ liệu 1 chiều.
- DataFrame : Cấu trúc dữ liêụ 2 chiều (dạng bảng).
```
**Syn: DataFrame**
```bash
df = pd.DataFrame(data, index=None, columns=None, dtype=None, copy=False)
- data (dict, list, numpy array, …): Dữ liệu gốc tạo nên bảng.
- index (list hoặc array): Nhãn cho các dòng, mặc địn là 0,1,2, …
- columns (list hoặc array): Tên cho các cột (nếu không sẽ tự động lấy từ data).
- dtype: Ép kiểu dữ liệu cho toàn bộ bảng.
- copy (bool): Nếu True tạo bản sao của dữ liệu gốc.
```
**Ex1: DataFrame**
```python
data = {
        "fullName": ["John", "Duo", "Chicago"],
        "address": ["New York", "Hanoi", "Tokyo"]
}
li = pd.DataFrame(data)
print(li)

#    fullName   address
# 0     John  New York
# 1      Duo     Hanoi
# 2  Chicago     Tokyo
```
**Ex2: Series**
```python
s = pd.Series([0,1,2,3], index=["a","b","c","d"])

# a    0
# b    1
# c    2
# d    3
# dtype: int64
```
# .shape
```bash
- Trả về số lượng hàng cột có trong dataFrame
```
**Ex**
print(df.shape)
# Tạo thêm cột mới trong dataframe
```python
import pandas as pd

data = {
    "full_name": ["John", "Duo", "Chicago"],
    "address": ["New York", "Hanoi", "Tokyo"]
}

df = pd.DataFrame(data)
df['sum'] = df['full_name'] + ' ' + df['address']

print(df)

#   full_name   address            sum
# 0      John  New York  John New York
# 1       Duo     Hanoi      Duo Hanoi
# 2   Chicago     Tokyo  Chicago Tokyo
```

# Tạo tên cột cho dataframe
```python
import pandas as pd

data = [[1,2,3,4,5]] # 1 dòng, 5 cột

df = pd.DataFrame(
    data,
    columns=['1','2','3','4','5']
)
print(df)

#    1  2  3  4  5
# 0  1  2  3  4  5
```


.colums
Là một thuộc tính kiểu index. Nó chứa danh sách tên các cột của dataframe.
Cú pháp: df.columns
print(df.columns)
# pd.options.display.max_rows
```bash
- Để kiểm tra số hàng tối đa của hệ thống.
```
**Ex**
```python
import pandas as pd

def main():
    pd.options.display.max_rows = 2
    data = {
        "fullName": ["John", "Jane", "Tom"],
        "address": ["New York", "HaNoi", "Tokyo"]
    }
    df = pd.DataFrame(data)
    print(pd.options.display.max_rows)
    print(df)
main()

# 2
#    fullName   address
# 0      John  New York
# ..      ...       ...
# 2       Tom     Tokyo

# [3 rows x 2 columns]
```
tail()
Để xem các hàng cuối cùng cùng của DataFrame. Trả về tiêu đề và số lượng hàng được chỉ định bắt đầu từ dưới cùng.
# .value_counts()
```bash
Đếm số lượng giá trị trong một cột.
```
**Syn**
```python
c = self.df[column].value_counts()
df = pd.DataFrame({
    "Color": ["Red", "Blue", "Red", "Green", "Blue", "Yellow", "Red"]
})

# Đếm số lần xuất hiện mỗi giá trị
# print(df["Color"].value_counts())
# Red       3
# Blue      2
# Green     1
# Yellow    1
```
- [.values \& to\_numpy()](#values--to_numpy)
- [.nunique()](#nunique)
- [.sort\_values()](#sort_values)
- [.where()](#where)
- [.concat()](#concat)
- [.sum()](#sum)
- [.mean()](#mean)
- [groupby()](#groupby)
  - [.transform()](#transform)
- [qcut()](#qcut)
---
# .values & to_numpy()
```bash
- values    : Đưa một series, cột trong Dataframe về dạng list.
- to_numpy  : Đưa một series, cột trong Dataframe về dạng numpy array.
```
**Ex1: values**
```python
data = {
        'size': [850, 900, 1200, 1500],
        'bedrooms': [2, 3, 3, 4],
        'age': [10, 15, 20, 5],
        'price': [200000, 250000, 300000, 350000]
    }
df = pd.DataFrame(data)
print(df['size'], df['size'].values)

# 0     850
# 1     900
# 2    1200
# 3    1500
# Name: size, dtype: int64 
# [ 850  900 1200 1500]
```
**Ex2: values[]**
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
# .nunique()
```bash
- Để đếm tổng số lượng các giá trị khác nhau trong một cột nào đó.
```
**Ex**
```python
df = pd.DataFrame({
    "Color": ["Red", "Blue", "Red", "Green", "Blue", "Yellow", "Red"]
})

print(df["Color"].nunique()) # 4
```
# .sort_values()
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
# .where()
```bash
- Trong pandas, hàm where() dùng để giữ giá trị khi điều kiện đúng, còn khi sai thì thay bằng giá trị khác (thường là NaN).
- where = “nếu đúng thì giữ, nếu sai thì thay”
```
**Syn**
```bash
DataFrame.where(
    cond,
    other=nan,
    inplace=False,
    axis=None,
    level=None,
    errors='raise',
    try_cast=False
)

- cond      : (bắt buộc). Kiểu: bool, DataFrame/Series boolean, hoặc hàm
- other     : Giá trị thay thế khi điều kiện sai. Mặc định: NaN
- inplace   : False (mặc định): trả về DataFrame mới. True: sửa trực tiếp DataFrame
- axis      : Xác định áp dụng điều kiện theo hàng hay cột. Thường không cần dùng
- level     : Dùng cho MultiIndex. Ít gặp
- error
    + 'raise': báo lỗi nếu cond không khớp shape
    + 'ignore': bỏ qua lỗi
- try_cast  : Cố gắng giữ kiểu dữ liệu cũ. Hiếm khi dùng
```
**Ex**
**Topic**
```bash
Giữ lại lương ≥ 10 triệu, còn lại thay bằng 0
```
**Answer**
```python
import pandas as pd

df = pd.DataFrame({
    'name': ['An', 'Bình', 'Chi'],
    'salary': [8_000_000, 12_000_000, 15_000_000]
})

print(df)

#    name   salary
# 0   An   8000000
# 1  Bình 12000000
# 2  Chi  15000000

df_new = df.where(df['salary'] >= 10_000_000, other=0)

print(df_new)

#    name   salary
# 0   0        0
# 1  Bình 12000000
# 2  Chi  15000000
```
# .concat()
```bash
nối hoặc thêm dữ liệu mới vào dataframe
```
**Ex1: thêm mới**
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
**Ex2: nối**
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
# .sum() 
# .mean()
# groupby()
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
# qcut()
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