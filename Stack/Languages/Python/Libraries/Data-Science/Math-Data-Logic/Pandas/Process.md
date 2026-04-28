- [Create (Nhóm khởi tạo)](#create-nhóm-khởi-tạo)
  - [DataFrame \& Series](#dataframe--series)
- [Display (Nhóm cung cấp thông tin)](#display-nhóm-cung-cấp-thông-tin)
  - [.head()](#head)
  - [.shape](#shape)
  - [.colums](#colums)
  - [.tail()](#tail)
  - [.value\_counts()](#value_counts)
  - [pd.options.display.max\_rows](#pdoptionsdisplaymax_rows)
  - [unique()](#unique)
  - [.nunique()](#nunique)
- [Tạo thêm cột mới trong dataframe](#tạo-thêm-cột-mới-trong-dataframe)
  - [pd.notnull()](#pdnotnull)
  - [.isna() \& .isnull()](#isna--isnull)
- [Search (nhóm tìm kiếm, lọc)](#search-nhóm-tìm-kiếm-lọc)
  - [loc](#loc)
  - [iloc](#iloc)
  - [.notna()](#notna)
  - [.where()](#where)
- [Process (thao tác xử lý)](#process-thao-tác-xử-lý)
  - [Basic Process (xử lý dữ liệu cơ bản)](#basic-process-xử-lý-dữ-liệu-cơ-bản)
    - [.drop() \& .dropna()](#drop--dropna)
  - [Duplicate Process (xử lý dữ liệu trùng)](#duplicate-process-xử-lý-dữ-liệu-trùng)
    - [.duplicated()](#duplicated)
    - [.drop\_duplicates()](#drop_duplicates)
- [Time (Nhóm xử lý ngày giờ)](#time-nhóm-xử-lý-ngày-giờ)
  - [Display (Nhóm cung cấp thông tin)](#display-nhóm-cung-cấp-thông-tin-1)
    - [.dt.date](#dtdate)
    - [.dt.hour](#dthour)
    - [.dt.minute](#dtminute)
    - [.dt.day\_name()](#dtday_name)
    - [.dt.dayofweek](#dtdayofweek)
  - [Transform (Nhóm biển đổi dữ liệu, cấu trúc dữ liệu)](#transform-nhóm-biển-đổi-dữ-liệu-cấu-trúc-dữ-liệu)
    - [to\_datetime()](#to_datetime)
    - [resample()](#resample)
---
# Create (Nhóm khởi tạo)
## DataFrame & Series
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
**Ex: Tạo tên cột cho dataframe**
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
# Display (Nhóm cung cấp thông tin)
## .head()
```bash
- Một trong những phương pháp được sử dụng nhiều nhất để có được cái nhìn tổng quan nhanh về DataFrame là phương pháp head().
- head() trả về các tiêu đề và số lượng hàng được chỉ định, bắt đầu từ trên cùng hoặc lấy ra n dòng đầu tiên.
```
**Ex**
```python
import pandas as pd

df = pd.read_csv('data.csv')

print(df.head(10)) # lấy ra 10 dòng dầu tiên
print(df.head()) # tự động lấy ra 5 dòng đầu tiên (mặc địch)

#    Duration  Pulse  Maxpulse  Calories
# 0        60    110       130     409.1
# 1        60    117       145     479.0
# 2        60    103       135     340.0
# 3        45    109       175     282.4
# 4        45    117       148     406.0
# 5        60    102       127     300.5
# 6        60    110       136     374.0
# 7        45    104       134     253.3
# 8        30    109       133     195.1
# 9        60     98       124     269.0
#    Duration  Pulse  Maxpulse  Calories
# 0        60    110       130     409.1
# 1        60    117       145     479.0
# 2        60    103       135     340.0
# 3        45    109       175     282.4
# 4        45    117       148     406.0
```
## .shape
```bash
- Trả về số lượng hàng cột có trong dataFrame
```
**Ex**
```python
print(df.shape)
```
## .colums
```bash
Là một thuộc tính kiểu index. Nó chứa danh sách tên các cột của dataframe.
```
**Ex** 
```python
df.columns
print(df.columns)
```
## .tail()
```bash
Để xem các hàng cuối cùng cùng của DataFrame. Trả về tiêu đề và số lượng hàng được chỉ định bắt đầu từ dưới cùng.
```
## .value_counts()
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
## pd.options.display.max_rows
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
## unique()
unique() dùng để lấy các giá trị không trùng lặp trong một Series/cột.

Cú pháp
df["column"].unique()
Ví dụ đơn giản
import pandas as pd

df = pd.DataFrame({
    "city": [
        "Ha Noi",
        "Da Nang",
        "Ha Noi",
        "HCM",
        "Da Nang"
    ]
})

print(df["city"].unique())
Kết quả giả định
['Ha Noi' 'Da Nang' 'HCM']

Chỉ giữ giá trị duy nhất, bỏ trùng.

Với số
df = pd.DataFrame({
 "hour":[8,8,9,10,10,10]
})

print(df["hour"].unique())

Kết quả:

[8 9 10]
Đếm số giá trị unique

Dùng:

df["city"].nunique()

Kết quả:

3
## .nunique()
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
## pd.notnull() 
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
## .isna() & .isnull()
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
# Search (nhóm tìm kiếm, lọc)
## loc
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
## iloc 
```bash
dùng để truy cập dữ liệu theo vị trí chỉ số (index số nguyên) trong pandas.
```
**Syn**
```bash
df.iloc[hàng, cột]
```
**Ex1: Lấy 1 ô**
```python
import pandas as pd

data = {
    'name': ['thang', 'minh', 'long', 'quyen', 'hue'],
    'age': [18,19,20,21,22]
}
df = pd.DataFrame(data)

print(df.iloc[0,1]) # lấy hàng 0 cột 1
# 18

print(df.iloc[0:3,0:1]) # lấy hàng 0 -> 2, cột 0
#     name
# 0  thang
# 1   minh
# 2   long

print(df.iloc[::2]) # lấy theo hàng bước nhảy 2. nó bằng với print(df.iloc[::2, :])
#     name  age
# 0  thang   18
# 2   long   20
# 4    hue   22
```
## .notna()
**Ex: tìm người đã có lương**
```python
has_salary = df[df['salary'].notna()]
```
## .where()
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
# Process (thao tác xử lý)
## Basic Process (xử lý dữ liệu cơ bản)
### .drop() & .dropna()
```bash
- drop              : Xóa hàng (row) hoặc cột (column) khỏi DataFrame.
- dropna            : xóa dòng có giá trị thiếu.
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
## Duplicate Process (xử lý dữ liệu trùng)
### .duplicated()
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
### .drop_duplicates()
```bash
xóa dòng trùng
```
**Syn**
```bash
df_no_dup = df.drop_duplicates(subset='ID', keep='first')
```
**Ex**
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
# Time (Nhóm xử lý ngày giờ)
## Display (Nhóm cung cấp thông tin)
### .dt.date 
```bash
dùng để lấy phần ngày (date) từ cột datetime, bỏ giờ phút giây.
```
**Syn**
```bash
df["col"].dt.date
```
**Ex**
```python
import pandas as pd

df = pd.DataFrame({
    "time": pd.to_datetime([
        "2024-01-10 08:30:00",
        "2024-01-10 14:45:00",
        "2024-01-11 09:15:00"
    ])
})

df["date_only"] = df["time"].dt.date

print(df)
#                  time   date_only
# 0 2024-01-10 08:30:00  2024-01-10
# 1 2024-01-10 14:45:00  2024-01-10
# 2 2024-01-11 09:15:00  2024-01-11
```
### .dt.hour
```bash
Lấy giờ
```
**Ex**
```python
import pandas as pd

df = pd.DataFrame({
    "time": [
        "2024-05-01 08:30:00",
        "2024-05-02 14:45:00",
        "2024-05-03 21:15:00"
    ]
})

df["time"] = pd.to_datetime(df["time"])
df["hour"] = df["time"].dt.hour

print(df)
#                  time  hour
# 0 2024-05-01 08:30:00     8
# 1 2024-05-02 14:45:00    14
# 2 2024-05-03 21:15:00    21
```
### .dt.minute
### .dt.day_name()
```bash
Lấy tên thứ
```
**Ex**
```python
import pandas as pd

df = pd.DataFrame({
    "time": [
        "2024-05-01 08:30:00",
        "2024-05-02 14:45:00",
        "2024-05-03 21:15:00"
    ]
})

df["time"] = pd.to_datetime(df["time"])
df["day_name"] = df["time"].dt.day_name()

print(df)
#                  time   day_name
# 0 2024-05-01 08:30:00  Wednesday
# 1 2024-05-02 14:45:00   Thursday
# 2 2024-05-03 21:15:00     Friday
```
### .dt.dayofweek
```bash
Lấy số thứ trong tuần
```
**Syn**
```bash
df["time"].dt.dayofweek

- Output:
    + Monday    = 0
    + Tuesday   = 1
    + Wednesday = 2
    + Thursday  = 3
    + Friday    = 4
    + Saturday  = 5
    + Sunday    = 6
```
**Ex**
```python
import pandas as pd

df = pd.DataFrame({
    "time": [
        "2024-05-01 08:30:00",
        "2024-05-02 14:45:00",
        "2024-05-03 21:15:00"
    ]
})

df["time"] = pd.to_datetime(df["time"])
df["day_num"] = df["time"].dt.dayofweek

print(df)
#                  time  day_num
# 0 2024-05-01 08:30:00        2
# 1 2024-05-02 14:45:00        3
# 2 2024-05-03 21:15:00        4
```
## Transform (Nhóm biển đổi dữ liệu, cấu trúc dữ liệu)
### to_datetime() 
```bash
- dùng để chuyển dữ liệu thành kiểu ngày giờ (datetime).
- Rất hay dùng khi cột ngày đang là string: "2024-01-15"
    + chuyển thành datetime để:
        - lọc theo ngày
        - resample time series
        - trích xuất năm/tháng/ngày
        - vẽ time series
        - forecast
```
**Syn**
```bash
pd.to_datetime(
    arg,
    format=None,
    errors='raise',
    dayfirst=False
)

- Input: 
    + arg           : Dữ liệu đầu vào (string, list, series, cột dataframe)
    + format        : Định dạng ngày, ví dụ "%Y-%m-%d"
        | `%Y` | năm 4 số |
        | `%m` | tháng    |
        | `%d` | ngày     |
        | `%H` | giờ      |
        | `%M` | phút     |
        | `%S` | giây     |
    + error         : Xử lý lỗi, sai thì thành NaT
    + dayfirst=True : Cho định dạng kiểu 15/01/2024
```
**Ex1: chuyển cột dataframe**
```python
df = pd.DataFrame({"date":["2024-01-01", "2024-01-02"]})

df["date"] = pd.to_datetime(df["date"])

# print(df)

#         date
# 0 2024-01-01
# 1 2024-01-02
```
**Ex2: Có format**
```python
print(pd.to_datetime(
    "26-04-2026",
    format="%d-%m-%Y"
)) # 2026-04-26
```
### resample()
```bash
- resample() = đổi tần suất thời gian.
- Ví dụ:
    + dữ liệu 15 phút → theo giờ
    + theo ngày
    + theo tháng
- Giống groupby cho thời gian
```
**Syn**
```bash
df.resample(rule).mean()

- Input:
    + rule:
        - "D": ngày
        - "H" giờ
        - "W" tuần
        - "M" tháng
```
**Ex**
```python
import pandas as pd

df = pd.DataFrame(
    {
      "load":[10,20,30,40]
    },
    index=pd.date_range(
       "2024-01-01",
       periods=4,
       freq="H"
    )
)

print(df)
#                      load
# 2024-01-01 00:00      10
# 2024-01-01 01:00      20
# 2024-01-01 02:00      30
# 2024-01-01 03:00      40

df.resample("2H").sum()
#                      load
# 00:00                30
# 02:00                70
```