- [Create (Nhóm khởi tạo)](#create-nhóm-khởi-tạo)
  - [DataFrame \& Series](#dataframe--series)
- [Display (Nhóm cung cấp thông tin)](#display-nhóm-cung-cấp-thông-tin)
  - [.head()](#head)
  - [.shape](#shape)
  - [.columns (Lấy danh sách tên các cột của dataframe)](#columns-lấy-danh-sách-tên-các-cột-của-dataframe)
  - [.tail()](#tail)
  - [.value\_counts() (Dùng để đếm tần suât xuất hiện của các các giá trị trong một Series (hoặc cột của Dataframe))](#value_counts-dùng-để-đếm-tần-suât-xuất-hiện-của-các-các-giá-trị-trong-một-series-hoặc-cột-của-dataframe)
  - [pd.options.display.max\_rows](#pdoptionsdisplaymax_rows)
  - [unique() (Dùng để lấy các giá trị không trùng lặp trong một Series/cột)](#unique-dùng-để-lấy-các-giá-trị-không-trùng-lặp-trong-một-seriescột)
  - [.nunique() (Để đếm tổng số lượng các giá trị khác nhau trong một cột nào đó)](#nunique-để-đếm-tổng-số-lượng-các-giá-trị-khác-nhau-trong-một-cột-nào-đó)
  - [.index()](#index)
  - [.info() (xem nhanh cấu trúc tổng quan của dữ liệu)](#info-xem-nhanh-cấu-trúc-tổng-quan-của-dữ-liệu)
  - [.describe() (mô tả dữ liệu)](#describe-mô-tả-dữ-liệu)
  - [.dtype (Xem kiểu dữ liệu 1 series)](#dtype-xem-kiểu-dữ-liệu-1-series)
  - [.dtypes (Xem kiểu dữ liệu của tất cả các cột bằng)](#dtypes-xem-kiểu-dữ-liệu-của-tất-cả-các-cột-bằng)
  - [.isin() (kiểm tra một giá trị có nằm trong một danh sách/tập hợp giá trị hay không)](#isin-kiểm-tra-một-giá-trị-có-nằm-trong-một-danh-sáchtập-hợp-giá-trị-hay-không)
- [Tạo thêm cột mới trong dataframe](#tạo-thêm-cột-mới-trong-dataframe)
  - [pd.notnull()](#pdnotnull)
  - [.isna() \& .isnull()](#isna--isnull)
- [Search (nhóm tìm kiếm, lọc)](#search-nhóm-tìm-kiếm-lọc)
  - [loc (Chọn theo nhãn hoặc theo điều kiện)](#loc-chọn-theo-nhãn-hoặc-theo-điều-kiện)
  - [iloc (integer location) (dùng để truy cập dữ liệu theo vị trí chỉ số)](#iloc-integer-location-dùng-để-truy-cập-dữ-liệu-theo-vị-trí-chỉ-số)
  - [.notna()](#notna)
  - [.where()](#where)
  - [.sample() (Lấy mẫu ngẫu nhiên)](#sample-lấy-mẫu-ngẫu-nhiên)
- [Process (thao tác xử lý)](#process-thao-tác-xử-lý)
  - [Basic Process (xử lý dữ liệu cơ bản)](#basic-process-xử-lý-dữ-liệu-cơ-bản)
    - [.drop() \& .dropna()](#drop--dropna)
  - [Duplicate Process (xử lý dữ liệu trùng)](#duplicate-process-xử-lý-dữ-liệu-trùng)
    - [.duplicated()](#duplicated)
    - [.drop\_duplicates()](#drop_duplicates)
  - [.apply() (Áp dụng function lên Series hoặc DataFrame)](#apply-áp-dụng-function-lên-series-hoặc-dataframe)
  - [.map()](#map)
  - [replace() (Thay thế giá trị cũ bằng giá trị mới trong Series hoặc DataFrame)](#replace-thay-thế-giá-trị-cũ-bằng-giá-trị-mới-trong-series-hoặc-dataframe)
- [Time (Nhóm xử lý ngày giờ)](#time-nhóm-xử-lý-ngày-giờ)
  - [Display (Nhóm cung cấp thông tin)](#display-nhóm-cung-cấp-thông-tin-1)
    - [.dt.date (dùng để lấy phần ngày (date) từ cột datetime, bỏ giờ phút giây)](#dtdate-dùng-để-lấy-phần-ngày-date-từ-cột-datetime-bỏ-giờ-phút-giây)
    - [.dt.hour](#dthour)
    - [.dt.minute (Dùng để lấy ra phần phút (0–59) từ một cột có kiểu datetime)](#dtminute-dùng-để-lấy-ra-phần-phút-059-từ-một-cột-có-kiểu-datetime)
    - [.dt.day\_name() (Lấy tên thứ)](#dtday_name-lấy-tên-thứ)
    - [.dt.dayofweek (Lấy số thứ trong tuần)](#dtdayofweek-lấy-số-thứ-trong-tuần)
  - [Transform (Nhóm biển đổi dữ liệu, cấu trúc dữ liệu)](#transform-nhóm-biển-đổi-dữ-liệu-cấu-trúc-dữ-liệu)
    - [.to\_datetime() (chuyển dữ liệu thành kiểu ngày giờ (datetime))](#to_datetime-chuyển-dữ-liệu-thành-kiểu-ngày-giờ-datetime)
    - [resample() (đổi tần suất thời gian)](#resample-đổi-tần-suất-thời-gian)
    - [pd.Timedelta()](#pdtimedelta)
- [Compare Function (Nhóm chức năng so sánh)](#compare-function-nhóm-chức-năng-so-sánh)
  - [.eq()](#eq)
- [shift() — lấy giá trị trong quá khứ (lag)](#shift--lấy-giá-trị-trong-quá-khứ-lag)
- [rolling() — cửa sổ trượt](#rolling--cửa-sổ-trượt)
- [autocorrelation\_plot()](#autocorrelation_plot)
- [.agg() (Cho phép áp dụng nhiều hàm cùng lúc)](#agg-cho-phép-áp-dụng-nhiều-hàm-cùng-lúc)
- [.count() (Đếm số giá trị không null)](#count-đếm-số-giá-trị-không-null)
  - [.query()](#query)
  - [.format()](#format)
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
## .columns (Lấy danh sách tên các cột của dataframe)
```bash
Dùng để:
    + xem danh sách tên cột
    + đổi tên cột
```
**Ex** 
```python
import pandas as pd

df = pd.DataFrame({
    "name": ['thang', 'minh'],
    "age": [12, 13],
    "address": ["hanoi", "hcm"]
})

cols = df.columns
print(cols) # Index(['name', 'age', 'address'], dtype='object')
```
## .tail()
```bash
Để xem các hàng cuối cùng cùng của DataFrame. Trả về tiêu đề và số lượng hàng được chỉ định bắt đầu từ dưới cùng.
```
**Syn**
```bash
df.tail(n)

- Input:
    + n: số dòng muốn lấy từ cuối lên. Nếu không truyền n, mặc định là 5
```
**Ex**
```python
import pandas as pd

df = pd.DataFrame({
    "Tên": ["A","B","C","D","E","F"],
    "Điểm": [7,8,9,6,10,5]
})

print(df)
#   Tên  Điểm
# 0 A    7
# 1 B    8
# 2 C    9
# 3 D    6
# 4 E   10
# 5 F    5

df.tail(2)
#   Tên  Điểm
# 4 E   10
# 5 F    5
```
## .value_counts() (Dùng để đếm tần suât xuất hiện của các các giá trị trong một Series (hoặc cột của Dataframe))
**Syn**
```bash
Series.value_counts(
    normalize=False,
    sort=True,
    ascending=False,
    bins=None,
    dropna=True
)

- Input:
    + normalize: True là trả về tỷ lệ (%) thay vì số lượng.
    + sort: 
        - True: (mặc định sắp xếp theo tần suất)
        - False: giữ nguyên thứ tự xuất hiện
    + ascending: True là sắp xếp tăng dần
    + dropna: Có tính NaN không. False là có tính
```
**Ex**
```python
df = pd.DataFrame({
    "Color": ["Red", "Blue", "Red", "Green", "Blue", "Yellow", "Red"]
})

print(df["Color"].value_counts())
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
## unique() (Dùng để lấy các giá trị không trùng lặp trong một Series/cột)
**Syn**
```python
df["column"].unique()
```
**Ex**
```python
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

print(df["city"].unique()) # ['Ha Noi' 'Da Nang' 'HCM']
```
## .nunique() (Để đếm tổng số lượng các giá trị khác nhau trong một cột nào đó)
**Ex**
```python
df = pd.DataFrame({
    "Color": ["Red", "Blue", "Red", "Green", "Blue", "Yellow", "Red"]
})

print(df["Color"].nunique()) # 4
```
## .index()
**Ex**
```python
import pandas as pd

df = pd.DataFrame({
    'name': ['thang', 'minh'],
    'age': [12,15]
})

print(df.index)
# RangeIndex(start=0, stop=2, step=1)
```
## .info() (xem nhanh cấu trúc tổng quan của dữ liệu)
```bash
Xem được:
    - Số dòng, số cột.
    - Tên các cột.
    - Kiểu dữ liệu (dtype) của từng cột.
    - Số lượng giá trị không bị thiếu (non-null).
    - Mức sử dụng bộ nhớ
```
```python
import pandas as pd

df = pd.DataFrame({
    'name': ['thinh', 'thang', 'tu'],
    'age': [18,None,21]
})

print(df.info())
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 3 entries, 0 to 2
Data columns (total 2 columns):
 #   Column  Non-Null Count  Dtype  
---  ------  --------------  -----  
 0   name    3 non-null      object 
 1   age     2 non-null      float64
dtypes: float64(1), object(1)
memory usage: 176.0+ bytes
None
```
## .describe() (mô tả dữ liệu)
**Ex**
```python
df = pd.DataFrame({    
    'name': ['thinh', 'thang', 'tu', 'thang', 'thinh'],    
    'age': [18,None,21,20,18]
})
#         age
# count   4.00
# mean   19.25
# std     1.50
# min    18.00
# 25%    18.00
# 50%    19.00
# 75%    20.25
# max    21.00

# count = 4 → có 4 giá trị hợp lệ (bỏ qua None)
# mean = 19.25 → trung bình: (18 + 21 + 20 + 18) / 4
# std = 1.50 → độ lệch chuẩn (mức độ phân tán)
# min = 18 → nhỏ nhất
# 25% = 18 → Q1 (phần tư thứ 1)
# 50% = 19 → median (trung vị)
# 75% = 20.25 → Q3
# max = 21 → lớn nhất
```
## .dtype (Xem kiểu dữ liệu 1 series)
**Syn**
```bash
df["ten_cot"].dtype
```
**Ex**
```python
import pandas as pd

df = pd.DataFrame({
    "ten": ["An", "Bình", "Chi"],
    "tuoi": [20, 21, 22],
    "diem": [8.5, 9.0, 7.5]
})

print(df["tuoi"].dtype) # int64
```
## .dtypes (Xem kiểu dữ liệu của tất cả các cột bằng)
**Syn**
```bash
df.dtypes
```
**Ex**
```python
print(df.dtypes)
# ten      object
# tuoi      int64
# diem    float64
# dtype: object
```
## .isin() (kiểm tra một giá trị có nằm trong một danh sách/tập hợp giá trị hay không)
**Ex: Lọc dữ liệu**
```python
df = pd.DataFrame({
    "city": ["HN", "HCM", "DN", "HP"]
})

mask = df["city"].isin(["HN", "DN"])

print(mask)
# 0     True
# 1    False
# 2     True
# 3    False
# Name: city, dtype: bool
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
**Ex1: dùng với series**
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
**Ex2: Dùng với Dataframe**
```python
import pandas as pd

data = {
    'name': ['thang', 'minh', 'nghia', 'thinh', 'thanh', 'tu'],
    'salary': [20, 12, 10, None , 7, 5],
    'city': ['hanoi', 'hcm', 'danang', 'canthoi', 'hanoi', 'haiphong']
}
df = pd.DataFrame(data)
non_salary = df.isnull()

print(non_salary)
#     name  salary   city
# 0  False   False  False
# 1  False   False  False
# 2  False   False  False
# 3  False    True  False
# 4  False   False  False
# 5  False   False  False
```
# Search (nhóm tìm kiếm, lọc)
## loc (Chọn theo nhãn hoặc theo điều kiện)
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
## iloc (integer location) (dùng để truy cập dữ liệu theo vị trí chỉ số)
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
## .sample() (Lấy mẫu ngẫu nhiên)
**Syn**
```bash
df.sample(5)
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

- Input:
    + subset: cột hoặc danh sách cột để kiểm tra trùng. mặc định kiểm tất cả cột.
    + keep:
        - 'first': đánh dấu True từ dòng trùng thứ 2 trở đi
        - 'last': đánh dấu True trừ dòng cuối cùng
        - False: tất cả các dòng trùng đều được đánh dấu T
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
## .apply() (Áp dụng function lên Series hoặc DataFrame)
**Ex1: Dùng apply() trên một cột**
```python
import pandas as pd

df = pd.DataFrame({
    "name": ["alice", "bob", "charlie"]
})

print(df)
#       name
# 0    alice
# 1      bob
# 2  charlie

df["name"] = df["name"].apply(lambda x: x.capitalize())

print(df)
#       name
# 0    Alice
# 1      Bob
# 2  Charlie
```
## .map()
## replace() (Thay thế giá trị cũ bằng giá trị mới trong Series hoặc DataFrame)
**Syn**
```bash
df = df.replace(options)

- options: thường là dict
```
**Ex: Thay thế trong nhiều cột**
```python
df = pd.DataFrame({
    "status": [0, 1, 1, 0],
    "gender": ["M", "F", "M", "F"]
})

df = df.replace({
    "status": {0: "Inactive", 1: "Active"},
    "gender": {"M": "Male", "F": "Female"}
})

print(df)
     status  gender
0  Inactive    Male
1    Active  Female
2    Active    Male
3  Inactive  Female
```
# Time (Nhóm xử lý ngày giờ)
## Display (Nhóm cung cấp thông tin)
### .dt.date (dùng để lấy phần ngày (date) từ cột datetime, bỏ giờ phút giây)
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
### .dt.minute (Dùng để lấy ra phần phút (0–59) từ một cột có kiểu datetime)
**Ex**
```python
import pandas as pd

df = pd.DataFrame({
    "thoi_gian": [
        "2026-06-17 08:15:30",
        "2026-06-17 12:45:10",
        "2026-06-17 21:05:50"
    ]
})

# Chuyển sang kiểu datetime
df["thoi_gian"] = pd.to_datetime(df["thoi_gian"])

# Lấy phút
df["phut"] = df["thoi_gian"].dt.minute

print(df)
#            thoi_gian  phut
# 0 2026-06-17 08:15:30    15
# 1 2026-06-17 12:45:10    45
# 2 2026-06-17 21:05:50     5
```
### .dt.day_name() (Lấy tên thứ)
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
### .dt.dayofweek (Lấy số thứ trong tuần)
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
### .to_datetime() (chuyển dữ liệu thành kiểu ngày giờ (datetime))
```bash
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
### resample() (đổi tần suất thời gian)
```bash
Ví dụ:
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
### pd.Timedelta()
```bash
- pd.Timedelta trong pandas rất giống timedelta của module datetime, nhưng được tối ưu để làm việc với:
    + Series
    + DataFrame
    + Timestamp
    + vectorized operation trong pandas.
```
**Syn**
```bash
pd.Timedelta(
    days=1,
    hours=2,
    minutes=30,
    seconds=, # giây
    milliseconds=, # mili giây
    microseconds=, # micro giây
    weeks=, # tuần
)
```
**Ex1**
```python
import pandas as pd

delta = pd.Timedelta(hours=1)
print(delta) # 01:00:00
```
**Ex2: có thể parse string, Đây là điểm mạnh của pandas**
```python
import pandas as pd

print(pd.Timedelta("1D"))
print(pd.Timedelta("2H"))
print(pd.Timedelta("30min"))
# 1 days 00:00:00
# 0 days 02:00:00
# 0 days 00:30:00
```
# Compare Function (Nhóm chức năng so sánh)
## .eq() 
```bash
dùng để so sánh bằng (==) giữa các phần tử, nhưng có một số điểm tiện hơn so với dùng == trực tiếp.
```
**Syn**
```bash
df['col'].eq(value) # 👉 Tương đương: df['col'] == value
```
**Ex1**
```python
import pandas as pd

df = pd.DataFrame({    
    'A': [1, 2, 3, 2]
})

df['A'].eq(2)
# 0    False
# 1     True
# 2    False
# 3     True
# Name: A, dtype: bool
```
**Ex2: So sánh giữa 2 cột**
```python
df = pd.DataFrame({    
    'A': [1, 2, 3],    
    'B': [1, 0, 3]
})

df['A'].eq(df['B'])
# 0     True
# 1    False
# 2     True
```
# shift() — lấy giá trị trong quá khứ (lag)
👉 Ý tưởng:

“Lấy giá trị của n bước trước”

📌 Cách dùng
df['power_shift_1'] = df['power'].shift(1)

👉 nghĩa là:

giá trị hiện tại ← giá trị của 1 giờ trước
📊 Ví dụ
time        power
00:00       10
01:00       20
02:00       30
df['shift_1'] = df['power'].shift(1)

👉 kết quả:

time        power   shift_1
00:00       10      NaN
01:00       20      10
02:00       30      20
🔥 Dùng để làm gì?
Feature cực quan trọng:
df['lag_1'] = df['power'].shift(1)
df['lag_24'] = df['power'].shift(24)

👉 model học được:

hôm nay phụ thuộc hôm qua
giờ này phụ thuộc giờ hôm qua
# rolling() — cửa sổ trượt
👉 Ý tưởng:

“Nhìn lại N điểm gần nhất rồi tính toán”

📌 Cách dùng
df['rolling_mean_3'] = df['power'].rolling(3).mean()

👉 nghĩa là:

lấy 3 giá trị gần nhất
tính trung bình
📊 Ví dụ
time        power
00:00       10
01:00       20
02:00       30
03:00       40
df['roll_mean'] = df['power'].rolling(3).mean()

👉 kết quả:

time        power   roll_mean
00:00       10      NaN
01:00       20      NaN
02:00       30      20   (10+20+30)/3
03:00       40      30   (20+30+40)/3
# autocorrelation_plot() 
```bash
- Là một hàm trong thư viện pandas dùng để vẽ đồ thị tự tương quan (autocorrelation) của chuỗi thời gian (time series).
- Autocorrelation (tự tương quan) đo mức độ tương quan giữa:
    + X(t) và X(t-k)
        - t: thời điểm hiện tại
        - k: độ trễ (lag)
- Dùng để làm gì?
    + Phát hiện seasonality
        - Ví dụ doanh số:
            + Mỗi thứ Hai đều bán cao
            + thì: lag = 7 sẽ có tương quan mạnh.
    + Kiểm tra dữ liệu có phụ thuộc quá khứ không
        - Ví dụ: x(t) ≈ x(t-1) thì lag 1 sẽ có autocorrelation cao.
    + Hỗ trợ xây dựng mô hình ARIMA Trong phân tích chuỗi thời gian:
        - ACF (AutoCorrelation Function)
        - PACF (Partial AutoCorrelation Function)
        - được dùng để chọn tham số của mô hình.
- Tóm lại:
    + Sóng lặp lại đều đặn → có chu kỳ/seasonality.
    + Sóng lặp lại nhưng đỉnh thấp dần → có chu kỳ nhưng bị nhiễu hoặc mất dần ảnh hưởng.
    + Chỉ giảm dần về 0, không có sóng → phụ thuộc quá khứ nhưng không có chu kỳ rõ.
    + Quanh 0 ngay từ đầu → gần như ngẫu nhiên.
- Đây cũng là lý do khi nhìn ACF, người làm time series thường quan tâm:
    + Có đỉnh lặp lại theo chu kỳ nào không?
    + ACF giảm nhanh hay chậm?
    + Có đổi dấu (+/-) theo dạng sóng không?
    + Ba đặc điểm đó cho biết rất nhiều về cấu trúc của chuỗi thời gian.
```
**Ex**
```bash
Ngày hôm nay ↔ ngày hôm qua      (lag = 1)
Ngày hôm nay ↔ 7 ngày trước      (lag = 7)
Ngày hôm nay ↔ 30 ngày trước     (lag = 30)

Nếu dữ liệu có tính chu kỳ hoặc mùa vụ thì autocorrelation thường cao ở một số lag nhất định.
```
**Syn**
```bash
from pandas.plotting import autocorrelation_plot

autocorrelation_plot(series)

- Input:
    + series: là một pandas series
```
# .agg() (Cho phép áp dụng nhiều hàm cùng lúc)
```bash
Dùng khi:
    - Tổng hợp dữ liệu
    - Thay thế nhiều lệnh thống kê riêng lẻ
```
**Ex**
```python
df["salary"].agg(["mean", "max", "min"])

df.groupby("department").agg({
    "salary": ["mean", "max"],
    "age": "median"
})
```
# .count() (Đếm số giá trị không null)
```bash
df.count()
```


.applymap()

Áp dụng lên từng phần tử DataFrame.

df.applymap(str.upper)

Hiện nay thường dùng:

df.map(...)

(với các phiên bản Pandas mới).
1. Nhóm String

Cực kỳ hay dùng.

.str.contains()
df["email"].str.contains("@gmail")
.str.lower()
df["name"].str.lower()
.str.upper()
df["name"].str.upper()
.str.strip()

Xóa khoảng trắng.

df["name"].str.strip()
.str.replace()
df["phone"].str.replace("-", "")
.str.split()
df["fullname"].str.split(" ")
.str.extract()

Regex.

df["email"].str.extract(r"@(.*)")
5. Nhóm Category / Encoding


cut()

Chia khoảng theo ngưỡng.

pd.cut(
    df["age"],
    bins=[0,18,60,100],
    labels=["Child","Adult","Senior"]
)

Khác với:

qcut()
cut: khoảng cố định
qcut: số lượng mẫu gần bằng nhau
6. Nhóm Missing Value nâng cao
.fillna(method=...)
df.fillna(method="ffill")
df.fillna(method="bfill")

Hiện nay khuyến khích viết:

df.ffill()
df.bfill()
.interpolate()

Nội suy.

df["temperature"].interpolate()

Rất hữu ích cho time series.

7. Nhóm Ranking
.rank()

Xếp hạng.

df["salary"].rank(ascending=False)
.nlargest()

Top N.

df.nlargest(5, "salary")
.nsmallest()

Bottom N.

df.nsmallest(5, "salary")
8. Nhóm Time Series quan trọng

Bạn đã học khá nhiều rồi, nhưng nên thêm:

.dt.month
df["date"].dt.month
.dt.year
df["date"].dt.year
.dt.weekday
df["date"].dt.weekday
.diff()

Sai phân.

df["sales"].diff()

Ví dụ:

100
120
150

↓

NaN
20
30
.pct_change()

Phần trăm thay đổi.

df["sales"].pct_change()

Ví dụ:

100
120

↓

0.2

tức tăng 20%.

9. Nhóm Window Function

Rất quan trọng nếu làm time series.

.expanding()

Tính từ đầu đến hiện tại.

df["sales"].expanding().mean()

Ví dụ:

10
20
30

↓

10
15
20
ewm()

Exponential Weighted Mean.

df["sales"].ewm(span=5).mean()

Trung bình động có trọng số.

Dùng nhiều trong tài chính.



11. Nhóm MultiIndex
stack()

Wide → long.

df.stack()
unstack()

Long → wide.

df.unstack()


## .query()

Lọc bằng biểu thức.

df.query("age > 30 and salary > 5000")

Thường dễ đọc hơn:

df[(df.age > 30) & (df.salary > 5000)]
.eval()

Đánh giá biểu thức.

df.eval("profit = revenue - cost")

Nhanh hơn trên DataFrame lớn.
## .format()
```python
df = pd.DataFrame({
    "rate": [0.1234, 0.5678]
})

df["rate"] = df["rate"].apply(
    lambda x: "{:.1%}".format(x)
)
#     rate
# 0  12.3%
# 1  56.8%
```