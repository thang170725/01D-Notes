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