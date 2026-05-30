- [Introduction](#introduction)
- [Tabular Data (Dữ liệu dạng bảng)](#tabular-data-dữ-liệu-dạng-bảng)
  - [The Big Picture (kiểm tra cấu trúc tổng thể)](#the-big-picture-kiểm-tra-cấu-trúc-tổng-thể)
  - [Missing data (kiểm tra dữ liệu thiếu)](#missing-data-kiểm-tra-dữ-liệu-thiếu)
  - [Duplicates (kiểm tra dữ liệu trùng lặp)](#duplicates-kiểm-tra-dữ-liệu-trùng-lặp)
  - [Outliers (Giá trị ngoại lai)](#outliers-giá-trị-ngoại-lai)
  - [Statistical Check (Kiểm tra phân phối và thống kê)](#statistical-check-kiểm-tra-phân-phối-và-thống-kê)
- [Visualization (Trực quan dữ liệu)](#visualization-trực-quan-dữ-liệu)
  - [Line Plot (Biểu đồ đường)](#line-plot-biểu-đồ-đường)
  - [Histogram (Biểu đồ phân phối)](#histogram-biểu-đồ-phân-phối)
  - [Heatmap (Bản đồ nhiệt)](#heatmap-bản-đồ-nhiệt)
  - [Boxplot (Biểu đồ hộp)](#boxplot-biểu-đồ-hộp)
  - [ACF](#acf)
---
# Introduction
```bash
EDA (Exploratory Data Analysis - Phân tích khám phá dữ liệu) là bước kiểm tra để biết dữ liệu khỏe hay bệnh.
```
# Tabular Data (Dữ liệu dạng bảng)
## The Big Picture (kiểm tra cấu trúc tổng thể)
**Ex**
```python
import pandas as pd

df = pd.DataFrame({
    'name': ['thinh', 'thang', 'tu'],
    'age': [18,None,21]
})

print(df.shape)
print(df.info())
print(df.head(5))
# (.venv) thang@PhatToNhuLai:~/workspace/lightgbm$ python -m backend.test
# (3, 2)
# <class 'pandas.core.frame.DataFrame'>
# RangeIndex: 3 entries, 0 to 2
# Data columns (total 2 columns):
#  #   Column  Non-Null Count  Dtype  
# ---  ------  --------------  -----  
#  0   name    3 non-null      object 
#  1   age     2 non-null      float64
# dtypes: float64(1), object(1)
# memory usage: 176.0+ bytes
# None
#     name   age
# 0  thinh  18.0
# 1  thang   NaN
# 2     tu  21.0
```
## Missing data (kiểm tra dữ liệu thiếu)
**Ex1: Đếm số Missing của từng cột**
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
**Ex2: Tính phần trăm missing**
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
## Duplicates (kiểm tra dữ liệu trùng lặp)
```bash
- Có hàng nào bị lặp lại hoàn toàn không? Điều này làm sai lệch kết quả huấn luyện. 
- Có thể sử dụng:
    + duplicated().sum()
    + ...
```
## Outliers (Giá trị ngoại lai)
```bash
- Có con số nào "vô lý" không? Ví dụ: Tuổi người là 200, hoặc lương là một số âm. 
- Có thể sử dụng:
    + biểu đồ Boxplot
    + df.describe().
```
## Statistical Check (Kiểm tra phân phối và thống kê)
```bash 
- Bước này giúp bạn hiểu về đặc tính của từng biến số:
    + Đối với biến số (Numerical): Xem giá trị trung bình (mean), trung vị (median), giá trị lớn nhất, nhỏ nhất và độ lệch chuẩn. (Sử dụng df.describe()).
    + Đối với biến phân loại (Categorical): Xem mỗi nhóm có bao nhiêu quan sát. Dữ liệu có bị mất cân bằng không? (Ví dụ: Dự đoán bệnh nhưng 99% dữ liệu là người khỏe). (Sử dụng df['column'].value_counts()).
```
# Visualization (Trực quan dữ liệu)
## Line Plot (Biểu đồ đường)
## Histogram (Biểu đồ phân phối)
```bash
- Histogram là biểu đồ cột dùng để xem:
    + dữ liệu tập trung ở đâu
    + phân phối như thế nào
    + có lệch hay không
- Nó chia dữ liệu thành các “khoảng” (bins).
- Dùng để làm gì?
    + xem dữ liệu có: phân phối chuẩn không, lệch trái/phải không, nhiều cụm không
    + phát hiện outlier
    + hiểu đặc tính dữ liệu trước khi train model
- Khi nào dùng?
    + dữ liệu số liên tục: tuổi, lương, doanh thu, nhiệt độ
```
**Ex**
```bash
- Điểm thi: 4 5 5 6 6 6 7 7 8 9
- Histogram sẽ cho thấy:
    + nhiều điểm nằm quanh 6–7
    + ít điểm quá thấp hoặc quá cao
```
## Heatmap (Bản đồ nhiệt)
```bash
- Heatmap dùng màu sắc để biểu diễn độ mạnh/yếu của giá trị.
    + màu đậm → giá trị lớn
    + màu nhạt → giá trị nhỏ
- Dùng để làm gì?
    + ma trận tương quan (correlation matrix) (Phổ biến nhất)
    + Ví dụ: tuổi và lương tương quan mạnh. chiều cao và điểm toán gần như không liên quan
    + Ứng dụng khác
        - AI/computer vision theo dõi click website
        - phân tích dữ liệu lớn
        - attention map trong deep learning
- Khi nào dùng?
    + Khi dữ liệu có dạng: ma trận, nhiều biến, muốn nhìn pattern nhanh
```
## Boxplot (Biểu đồ hộp)
```bash
- Boxplot tóm tắt phân phối dữ liệu bằng:
    + median (trung vị)
    + quartiles
    + outlier
- Nó cho biết:
    + dữ liệu trải rộng bao nhiêu
    + có lệch không
    + có outlier không
- Thành phần chính: Q1 ≤ Median ≤ Q3
    + đường giữa = median
    + hộp = 50% dữ liệu trung tâm
    + “râu” = phạm vi bình thường
    + điểm lẻ = outlier
- Dùng để làm gì?
    + phát hiện outlier cực mạnh
    + so sánh nhiều nhóm dữ liệu    
    + xem độ phân tán
```
## ACF 
```bash
- AutoCorrelation Function đo: dữ liệu hiện tại liên quan bao nhiêu với dữ liệu trong quá khứ.
- Dùng chủ yếu cho: chuỗi thời gian (time series)
- Ý tưởng
    + Ví dụ:
        - nhiệt độ hôm nay thường giống hôm qua
        - giá cổ phiếu hôm nay liên quan vài ngày trước
```
**Ex**
```bash 
Nếu: ACF cao ở lag 24 → có thể dữ liệu lặp theo 24 giờ
```