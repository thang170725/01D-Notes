- [DataFrame \& Series](#dataframe--series)
- [.shape](#shape)
- [pd.notnull()](#pdnotnull)
- [Tạo thêm cột mới trong dataframe](#tạo-thêm-cột-mới-trong-dataframe)
- [Tạo tên cột cho dataframe](#tạo-tên-cột-cho-dataframe)
- [lọc có điều kiện trong dataframe](#lọc-có-điều-kiện-trong-dataframe)
- [pd.options.display.max\_rows](#pdoptionsdisplaymax_rows)
- [.value\_counts()](#value_counts)
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