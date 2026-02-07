- [.rename()](#rename)
- [.duplicated()](#duplicated)
- [.drop() \& .dropna() \& .drop\_duplicates()](#drop--dropna--drop_duplicates)
- [fillna()](#fillna)
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
DataFrame.duplicated(subset=None, keep='first')
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
# .drop() & .dropna() & .drop_duplicates()
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
# fillna()
```bash
- Điền giá trị còn thiếu
```