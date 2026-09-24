- [Introduction](#introduction)
- [Installation](#installation)
- [Chart (Nhóm vẽ biểu đồ)](#chart-nhóm-vẽ-biểu-đồ)
  - [.lineplot() (vẽ biểu đồ đường )](#lineplot-vẽ-biểu-đồ-đường-)
  - [.histplot() (Xem phân bố dữ liệu)](#histplot-xem-phân-bố-dữ-liệu)
  - [.Boxplot() (Phát hiện ngoại lai (outlier), xem median và quartile)](#boxplot-phát-hiện-ngoại-lai-outlier-xem-median-và-quartile)
  - [.Heatmap() (Biểu diễn dữ liệu bằng màu sắc)](#heatmap-biểu-diễn-dữ-liệu-bằng-màu-sắc)
  - [.scatterplot() (Xem mối quan hệ giữa 2 biến số)](#scatterplot-xem-mối-quan-hệ-giữa-2-biến-số)
  - [.barplot() (So sánh giá trị trung bình giữa các nhóm)](#barplot-so-sánh-giá-trị-trung-bình-giữa-các-nhóm)
  - [.countplot (Đếm số lượng từng nhóm)](#countplot-đếm-số-lượng-từng-nhóm)
  - [sns.kdeplot() (Ước lượng mật độ xác suất)](#snskdeplot-ước-lượng-mật-độ-xác-suất)
  - [sns.ecdfplot() (Vẽ hàm phân phối tích lũy)](#snsecdfplot-vẽ-hàm-phân-phối-tích-lũy)
  - [sns.violinplot() (Boxplot + KDE)](#snsviolinplot-boxplot--kde)
  - [stripplot()](#stripplot)
  - [sns.swarmplot()](#snsswarmplot)
  - [sns.boxenplot()](#snsboxenplot)
  - [sns.pairplot()](#snspairplot)
  - [sns.jointplot()](#snsjointplot)
  - [sns.relplot()](#snsrelplot)
  - [sns.catplot()](#snscatplot)
  - [sns.pointplot() (Hiển thị trung bình và khoảng tin cậy)](#snspointplot-hiển-thị-trung-bình-và-khoảng-tin-cậy)
  - [sns.regplot() (Scatter + đường hồi quy)](#snsregplot-scatter--đường-hồi-quy)
  - [sns.lmplot() (Figure-level của regplot)](#snslmplot-figure-level-của-regplot)
  - [sns.clustermap() (Heatmap có phân cụm tự động)](#snsclustermap-heatmap-có-phân-cụm-tự-động)
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
## .lineplot() (vẽ biểu đồ đường )
```bash
Dùng để làm gì?
    - Hiển thị xu hướng theo thời gian hoặc thứ tự.
```
**Syn**
```bash
sns.lineplot(
    data=df,
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
    + ax    : dùng để chỉ vẽ vào đâu. ax=axes[i] nghĩa là: "Vẽ lineplot này vào subplot số i"
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
## .histplot() (Xem phân bố dữ liệu)
```bash
- Nó trả lời các câu hỏi như:
    + Dữ liệu tập trung quanh đâu?
    + Có lệch trái/lệch phải (skew) không?
    + Có outlier không?
    + Phân phối có giống chuẩn (normal) không?
    + Có nhiều cụm (multimodal) không?
```
**Syn**
```bash
sns.histplot(
    data=df, 
    x="age",
    bin=,
    kde=True,
    color="skyblue",
    ax=
)

- kde=True: Thêm một đường cong mượt thể hiện xu hướng phân bố
```
**Ex: chiều cao của 20 học sinh**
```python
import seaborn as sns
import matplotlib.pyplot as plt

heights = [
    150, 152, 153, 154,
    155, 156, 156, 157,
    158, 158, 159, 160,
    160, 161, 162, 163,
    165, 166, 168, 170
]

sns.histplot(heights, bins=5)

plt.title("Phân bố chiều cao học sinh")
plt.xlabel("Chiều cao (cm)")
plt.ylabel("Số học sinh")
plt.show()

# Giả sử bins=5, Seaborn sẽ chia khoảng chiều cao thành 5 nhóm
# | Khoảng chiều cao (cm) | Số học sinh |
# | --------------------- | ----------: |
# | 150 – 154             |           4 |
# | 154 – 158             |           5 |
# | 158 – 162             |           6 |
# | 162 – 166             |           3 |
# | 166 – 170             |           2 |

# Histogram sẽ trông gần giống thế này
# Số học sinh

# 6 |             █
# 5 |       █     █
# 4 | █     █     █
# 3 | █     █     █     █
# 2 | █     █     █     █     █
# 1 | █     █     █     █     █
#   +--------------------------------
#     150   154   158   162   166 170
#           Chiều cao (cm)
```
## .Boxplot() (Phát hiện ngoại lai (outlier), xem median và quartile)
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
## .Heatmap() (Biểu diễn dữ liệu bằng màu sắc)
```bash
Dùng để xem các feature tương quan với nhau như thế nào. 2 feature tương quan quá cao có thể bỏ bớt
```
**Syn**
```bash
sns.heatmap(data)

- df: ma trận dữ liệu cần vẽ.
- annot=True: hiện giá trị số trong từng ô.
- cmap="YlOrRd": bảng màu (Yellow → Orange → Red).
- linewidths=0.5: độ dày đường kẻ giữa các ô.
```
**Ex: Xem điểm số trung bình của học sinh theo môn học và lớp học.**
```bash
| Lớp | Toán |  Lý | Hóa |
| --- | ---: | --: | --: |
| 10A |  8.5 | 7.0 | 6.5 |
| 10B |  7.5 | 8.0 | 7.0 |
| 10C |  9.0 | 8.5 | 8.0 |
```
```python
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt

# Dữ liệu giả định
df = pd.DataFrame({
    "Toán": [8.5, 7.5, 9.0],
    "Lý":   [7.0, 8.0, 8.5],
    "Hóa":  [6.5, 7.0, 8.0]
}, index=["10A", "10B", "10C"])

print(df)

# Vẽ heatmap
plt.figure(figsize=(6, 4))

sns.heatmap(
    df,
    annot=True,      # hiện số trong ô
    cmap="YlOrRd",   # màu từ vàng → đỏ
    linewidths=0.5
)

plt.title("Điểm trung bình các lớp")
plt.xlabel("Môn học")
plt.ylabel("Lớp")
plt.show()

print(df)
#      Toán   Lý  Hóa
# 10A   8.5  7.0  6.5
# 10B   7.5  8.0  7.0
# 10C   9.0  8.5  8.0

# 🟨 = thấp, 🟧 = trung bình, 🟥 = cao
# | Lớp | Toán   | Lý     | Hóa    |
# | --- | ------ | ------ | ------ |
# | 10A | 🟥 8.5 | 🟧 7.0 | 🟨 6.5 |
# | 10B | 🟧 7.5 | 🟧 8.0 | 🟨 7.0 |
# | 10C | 🟥 9.0 | 🟥 8.5 | 🟧 8.0 |
# Nhìn vào màu, ta thấy ngay:
#     - Lớp 10C học đều và khá nhất.
#     - Lớp 10A học Toán tốt nhưng Hóa yếu hơn.
#     - Lớp 10B ở mức trung bình.
```
## .scatterplot() (Xem mối quan hệ giữa 2 biến số)
**Syn**
```bash
sns.scatterplot(data=df, x="x", y="y")
```
**Ex**
```python
sns.scatterplot(data=df, x="height", y="weight")
```
## .barplot() (So sánh giá trị trung bình giữa các nhóm)
```bash
sns.barplot(data=df, x="group", y="value")
```
**Ex**
```python
sns.barplot(data=df, x="department", y="salary")
```
## .countplot (Đếm số lượng từng nhóm)
```bash
sns.countplot(data=df, x="category")
```
**Ex**
```python
sns.countplot(data=df, x="gender")
```
## sns.kdeplot() (Ước lượng mật độ xác suất)
```bash
Ứng dụng
    - Xem phân bố mượt hơn histogram
```
**Syn**
```bash
sns.kdeplot(data=df, x="value")
```
**Ex**
```python
sns.kdeplot(df["salary"])
```
## sns.ecdfplot() (Vẽ hàm phân phối tích lũy)
```bash
Ứng dụng
    - Xem bao nhiêu % dữ liệu nhỏ hơn giá trị nào đó.
```
**Syn**
```bash
sns.ecdfplot(data=df, x="value")
```
**Ex**
```python
sns.ecdfplot(df["score"])
```
## sns.violinplot() (Boxplot + KDE)
Ứng dụng
So sánh hình dạng phân bố.
Cú pháp
sns.violinplot(data=df, x="group", y="value")
Ví dụ
sns.violinplot(data=df, x="gender", y="salary")
## stripplot()
Dùng để làm gì

Hiển thị từng điểm dữ liệu.

Ứng dụng
Dataset nhỏ.
Cú pháp
sns.stripplot(data=df, x="group", y="value")
Ví dụ
sns.stripplot(data=df, x="class", y="score")
## sns.swarmplot()
Dùng để làm gì

Giống stripplot nhưng tránh chồng điểm.

Ứng dụng
Quan sát dữ liệu chi tiết.
Cú pháp
sns.swarmplot(data=df, x="group", y="value")
Ví dụ
sns.swarmplot(data=df, x="species", y="petal_length")
## sns.boxenplot()
Dùng để làm gì

Phiên bản boxplot cho dữ liệu lớn.

Ứng dụng
Dataset hàng nghìn dòng.
Cú pháp
sns.boxenplot(data=df, x="group", y="value")
Ví dụ
sns.boxenplot(data=df, x="city", y="income")
IV. Quan hệ nhiều biến
## sns.pairplot()
Dùng để làm gì

So sánh mọi cặp biến số.

Ứng dụng
EDA.
Khám phá dữ liệu ban đầu.
Cú pháp
sns.pairplot(df)
Ví dụ
sns.pairplot(iris, hue="species")
## sns.jointplot()
Dùng để làm gì

Scatter + phân bố từng biến.

Ứng dụng
Phân tích quan hệ hai biến.
Cú pháp
sns.jointplot(data=df, x="x", y="y")
Ví dụ
sns.jointplot(data=df, x="height", y="weight")
## sns.relplot()
Dùng để làm gì

Phiên bản figure-level của lineplot/scatterplot.

Ứng dụng
Chia thành nhiều subplot.
Cú pháp
sns.relplot(data=df, x="x", y="y", col="group")
Ví dụ
sns.relplot(data=df, x="time", y="sales",
            kind="line", col="region")
V. So sánh nhóm nâng cao
## sns.catplot()
Dùng để làm gì

Giao diện tổng quát cho biểu đồ phân loại.

Ứng dụng
Tạo boxplot, violinplot, barplot nhiều nhóm.
Cú pháp
sns.catplot(data=df, x="x", y="y", kind="box")
Ví dụ
sns.catplot(data=df,
            x="gender",
            y="salary",
            kind="violin")
## sns.pointplot() (Hiển thị trung bình và khoảng tin cậy)
Dùng để làm gì
Ứng dụng
So sánh xu hướng giữa nhóm.
Cú pháp
sns.pointplot(data=df, x="group", y="value")
Ví dụ
sns.pointplot(data=df, x="month", y="sales")
VI. Hồi quy
## sns.regplot() (Scatter + đường hồi quy)
Dùng để làm gì
Ứng dụng
Kiểm tra tương quan tuyến tính.
Cú pháp
sns.regplot(data=df, x="x", y="y")
Ví dụ
sns.regplot(data=df, x="study_hour", y="score")
## sns.lmplot() (Figure-level của regplot)
Ứng dụng
Hồi quy theo nhiều nhóm.
Cú pháp
sns.lmplot(data=df, x="x", y="y", hue="group")
Ví dụ
sns.lmplot(data=df,
           x="height",
           y="weight",
           hue="gender")
VII. Biểu đồ ma trận
## sns.clustermap() (Heatmap có phân cụm tự động)
Ứng dụng
Gene expression.
Phân cụm khách hàng.
Cú pháp
sns.clustermap(data)
Ví dụ
sns.clustermap(df.corr())