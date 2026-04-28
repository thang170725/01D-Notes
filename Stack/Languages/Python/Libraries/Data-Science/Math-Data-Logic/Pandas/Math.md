- [.sum()](#sum)
- [.cumsum() (cumulative sum)](#cumsum-cumulative-sum)
- [.mean()](#mean)
---
# .sum() 
# .cumsum() (cumulative sum)
```bash
- Là tổng tích lũy / cộng dồn. Nó không cộng tất cả một lần như sum(), mà cộng dồn từng bước.
```
**Syn**
```bash
Với series: series.cumsum()

Với dataframe:
df.cumsum(axis=0)

- Input:
    + axis=0 (mặc định): cộng dồn theo cột
    + axis=1: cộng dồn theo hàng
```
**Ex1: cumsum với series**
```python
import pandas as pd

s = pd.Series([2, 4, 6, 8])

print(s.cumsum())
# 0     2
# 1     6
# 2    12
# 3    20
```
**Ex2: Với dataframe**
```python
df = pd.DataFrame({
    'A':[1,2,3],
    'B':[4,5,6]
})

print(df.cumsum())
#    A   B
# 0  1   4
# 1  3   9
# 2  6  15
```
# .mean()
```bash
Dùng để tính giá trị trung bình
```
**Ex1: mean với series**
```python
import pandas as pd

scores = pd.Series([8, 7, 9, 6, 10])

print(scores.mean()) # 8.0
```
**Ex2: mean với Dataframe**
```python
import pandas as pd

df = pd.DataFrame({
    'Math': [8, 7, 9],
    'English': [6, 8, 7]
})

print(df.mean())
# Math       8.0
# English    7.0
# dtype: float64
```