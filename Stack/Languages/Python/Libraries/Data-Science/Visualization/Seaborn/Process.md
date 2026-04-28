- [Introduction](#introduction)
- [Installation](#installation)
- [Chart (Nhóm vẽ biểu đồ)](#chart-nhóm-vẽ-biểu-đồ)
  - [.lineplot()](#lineplot)
  - [Histplot()](#histplot)
  - [Boxplot()](#boxplot)
  - [Heatmap()](#heatmap)
---
# Introduction
```bash
- Seaborn là một thư viện vẽ biểu đồ mạnh mẽ trong Python, được xây dựng trên nền tảng Matplotlib, và tích hợp rất tốt với Pandas. Kế thừa matplotlib
```
# Installation
```bash
pip install seaborn
```
**So sánh seaborn và matplotlib**
```bash
            Matplotlib                                          Seaborn

Cấp độ      Thấp (Low-level)                                    Cao (High-level, built on Matplotlib)

Cú pháp     Tự kiểm soát từng chi tiết (trục, màu, tick...)     Dễ viết, đẹp sẵn, hiểu dữ liệu dạng bảng

Dữ liệu     Mảng, list, numpy...                                DataFrame (pandas) là chính

phù hợp     Biểu đồ cơ bản, tùy biến sâu                        Biểu đồ thống kê, phân tích quan hệ
            (line, scatter, bar, hist...)                       (countplot, boxplot, pairplot, heatmap…)


Tốc độ      Nhiều dòng hơn, linh hoạt hơn                       Ngắn gọn, tự động nhận dạng biến

Phong cách  Khá “thô” nếu không chỉnh                           Mặc định rất đẹp và hiện 
```
# Chart (Nhóm vẽ biểu đồ)
## .lineplot()
```bash
- Dùng để vẽ biểu đồ đường (line plot)
- Biểu đồ plot thường dùng để xem sự biến thiên dữ liệu
```
**Syn**
```bash
sns.lineplot(
    data=None,
    x=None,
    y=None,
    ax=axes[i],
    hue=None,
    style=None,
    size=None,
    estimator='mean',
    errorbar=('ci',95),
    markers=False,
    dashes=True
)

- Input:
    + data  : Nguồn dữ liệu (DataFrame)
    + x     : Biến trục X
    + y     : Biến trục Y
    + ax    : trong seaborn dùng để chỉ vẽ vào đâu. ax=axes[i] nghĩa là: "Vẽ lineplot này vào subplot số i"
```
**Ex: Với dữ liệu dạng time series điện năng**
```python
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt

df = pd.read_csv(
    "LD2011_2014.txt",
    sep=";",
    decimal=",",
    parse_dates=[0]
)

sns.lineplot(
    data=df,
    x=df.columns[0],   # cột thời gian
    y=df.columns[1]    # cột điện năng
)

plt.show()
```
Countplot()
Cú pháp:
sns.countplot(x='intent', data=self.df, palette='Set2', ax=ax)

Violinplot()
Lmplot()
## Histplot()
```bash
- Nó trả lời các câu hỏi như:
    + Dữ liệu tập trung quanh đâu?
    + Có lệch trái/lệch phải (skew) không?
    + Có outlier không?
    + Phân phối có giống chuẩn (normal) không?
    + Có nhiều cụm (multimodal) không?
```
**Ex**
```python
import seaborn as sns
import matplotlib.pyplot as plt

sns.histplot(
    data=df,
    x="electricity_usage",
    bins=30
)

plt.show()
```
## Boxplot()
```bash
- Boxplot (biểu đồ hộp) rất mạnh để tóm tắt phân phối và đặc biệt giỏi phát hiện outlier.
- Boxplot cho biết 5 số quan trọng (five-number summary)
    + Min (không tính outlier)
    + Q1 (25%)
    + Median (50%)
    + Q3 (75%)
    + Max (không tính outlier)
- Dùng để:
    + phát hiện outlier
    + xem độ phân tán
    + xem median
    + xem skewness
```
**Cấu trúc**
```bash
 outlier     outlier
   •            •

---|----[====|====]----|---
  min    Q1 median Q3  max
```
 sns.boxplot(x="intent", y="length", data=self.df, ax=ax)

Scatterplot()
## Heatmap()
```bash
Dùng để xem các feature tương quan với nhau như thế nào. 2 feature tương quan quá cao có thể bỏ bớt
```
Pairplot()
Barplot()

