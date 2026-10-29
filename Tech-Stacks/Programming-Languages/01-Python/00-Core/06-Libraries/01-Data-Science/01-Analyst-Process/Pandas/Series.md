- [.sum() (tính tổng)](#sum-tính-tổng)
- [.cumsum() (cumulative sum) (Là tổng tích lũy / cộng dồn)](#cumsum-cumulative-sum-là-tổng-tích-lũy--cộng-dồn)
- [.mean() (Dùng để tính giá trị trung bình)](#mean-dùng-để-tính-giá-trị-trung-bình)
- [.median() (Trung vị)](#median-trung-vị)
- [.std() (Độ lệch chuẩn)](#std-độ-lệch-chuẩn)
- [.var() (Phương sai)](#var-phương-sai)
- [.quantile() (Lấy percentile)](#quantile-lấy-percentile)
- [.round() (làm tròn sau dấu thập phân)](#round-làm-tròn-sau-dấu-thập-phân)
---
# .sum() (tính tổng)
**Syn**
```bash
df.sum()

Input: Dataframe | Series
    + axis=:
        - 0: tính theo cột
        - 1: tính theo hàng
Output: Series
```
**Ex**
```python
import pandas as pd

df = pd.DataFrame({
    "A": [1,2,3],
    "B": [4,5,6]
})

print(df.sum())
# A     6
# B    15
```
# .cumsum() (cumulative sum) (Là tổng tích lũy / cộng dồn)
```bash
Nó không cộng tất cả một lần như sum(), mà cộng dồn từng bước.
```
**Syn**
```bash
series.cumsum() hoặc df.cumsum(axis=0)

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
# .mean() (Dùng để tính giá trị trung bình)
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
# .median() (Trung vị)
```bash
Rất hay dùng khi dữ liệu có outlier
```
**Syn**
```bash
import pandas as pd
Dataframe | Series.median(
    axis=
) 
```
**Ex**
```python
import pandas as pd

df = pd.DataFrame({
    "A": [1,2,3],
    "B": [4,5,6]
})
print(f"{df}\n")

df.loc[len(df)] = df.median(axis=0)
df.rename(index={3: "Median"}, inplace=True)
print(df)
#    A  B
# 0  1  4
# 1  2  5
# 2  3  6

#           A    B
# 0       1.0  4.0
# 1       2.0  5.0
# 2       3.0  6.0
# Median  2.0  5.0
```
# .std() (Độ lệch chuẩn)
```bash
df["salary"].std()
```
# .var() (Phương sai)
```bash
df["salary"].var()
```
# .quantile() (Lấy percentile)
```bash
Dùng nhiều trong phát hiện outlier.
```
```bash
df["salary"].quantile(0.25)
df["salary"].quantile([0.25,0.5,0.75])
```
# .round() (làm tròn sau dấu thập phân)
```python
df = pd.DataFrame({
    "A": [1.2345, 2.3456],
    "B": [3.4567, 4.5678]
})

df = df.round(2)
#       A     B
# 0  1.23  3.46
# 1  2.35  4.57
```
# ewm() (Trung bình động có trọng số)
```python
Dùng nhiều trong tài chính.
```
**Syn**
```python
df["sales"].ewm(span=5).mean()
```
# .expanding() (Tính từ đầu đến hiện tại)
**Ex**
```bash
df["sales"].expanding().mean()
```
# .pct_change() (Tính phần trăm thay đổi)
```python
df["sales"].pct_change()
```
# .diff() (Sai phân)
```python
df["sales"].diff()
```