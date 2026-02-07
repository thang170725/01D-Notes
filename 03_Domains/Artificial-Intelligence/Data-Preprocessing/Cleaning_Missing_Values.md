- [Missing data](#missing-data)
  - [Đếm số Missing của từng cột](#đếm-số-missing-của-từng-cột)
  - [Tính phần trăm missing](#tính-phần-trăm-missing)
---
# Missing data
## Đếm số Missing của từng cột
```python
import pandas as pd

data = {
    'age': [25,None,30],
    'salary': [10, 12, None],
    'gender': ['male', 'female', None]
}

df = pd.DataFrame(data)

print(df.isnull().sum())

# age       1
# salary    1
# gender    1
# dtype: int64
```
## Tính phần trăm missing
```python
import pandas as pd

data = {
    'age': [25,None,30],
    'salary': [10, 12, None],
    'gender': ['male', 'female', None]
}

df = pd.DataFrame(data)

print(df.isnull().mean() * 100)

# age       33.333333
# salary    33.333333
# gender    33.333333
# dtype: float64
```