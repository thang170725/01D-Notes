- [Missing values (kỹ thuật xử lý giá trị thiếu)](#missing-values-kỹ-thuật-xử-lý-giá-trị-thiếu)
- [Outlier (Phát hiện \& xử lý giá trị ngoại lai)](#outlier-phát-hiện--xử-lý-giá-trị-ngoại-lai)
- [Scale (Đưa feature về cùng thang đo)](#scale-đưa-feature-về-cùng-thang-đo)
  - [Standardization (Z-score)](#standardization-z-score)
  - [Min-Max Scaling](#min-max-scaling)
  - [Robust Scaling](#robust-scaling)
---
# Missing values (kỹ thuật xử lý giá trị thiếu)
**Ex: Các kỹ thuật xử lý missing values**
```bash
Ví dụ dataset:
| ID | Tuổi | Lương | Thành phố |
| -- | ---- | ----- | --------- |
| 1  | 25   | 10    | Hà Nội    |
| 2  | 30   | ?     | TP.HCM    |
| 3  | ?    | 15    | Hà Nội    |
| 4  | 40   | 20    | ?         |
| 5  | 35   | 18    | Đà Nẵng   |
```
**1. Xóa dòng (Drop Rows)**
```bash
Nếu số lượng missing rất ít.

| ID | Tuổi | Lương |
| -- | ---- | ----- |
| 1  | 25   | 10    |
| 2  | 30   | ?     |
| 3  | 40   | 20    |

thì xóa dòng 2:
| ID | Tuổi | Lương |
| -- | ---- | ----- |
| 1  | 25   | 10    |
| 3  | 40   | 20    |
```
**2. Xóa cột (Drop Columns)**
```bash
Nếu cột bị thiếu quá nhiều.

| ID | Tuổi | Email                                 |
| -- | ---- | ------------------------------------- |
| 1  | 25   | ?                                     |
| 2  | 30   | ?                                     |
| 3  | 40   | [abc@gmail.com](mailto:abc@gmail.com) |

90% email bị thiếu. Có thể bỏ luôn
```
**3. Mean Imputation (Điều trung bình)**
```bash
| Tuổi |
| ---- |
| 20   |
| 25   |
| ?    |
| 35   |

Mean: (20+25+35)/3=26.67

Thay:
| Tuổi  |
| ----- |
| 20    |
| 25    |
| 26.67 |
| 35    |
```
**4. Median Imputation (Điền trung vị)**
```bash
Đây là cách thường dùng hơn Mean.
Lương1012151000?
Mean:
(10+12+15+1000)/4=259.25(10+12+15+1000)/4 = 259.25(10+12+15+1000)/4=259.25
Rất vô lý.
Median:
10 12 15 1000   ↑ 13.5
Thay:
df["Salary"] = df["Salary"].fillna(df["Salary"].median())
```
Bạn đang nghĩ theo hướng mà các Data Scientist thực tế thường làm, và đúng là median toàn cột không phải lúc nào cũng hợp lý.
Ví dụ bài toán giá nhà:
Diện tíchPhòng ngủQuậnGiá502Cầu Giấy5 tỷ552Cầu Giấy5.5 tỷ2005Ba Đình40 tỷ?2Cầu Giấy5.2 tỷ
Nếu điền diện tích bằng median toàn bộ cột:
[50, 55, 200]median = 55
thì khá ổn trong ví dụ này.
Nhưng nếu dữ liệu là:
Diện tích303540300400
Median:
40
Giả sử căn nhà bị thiếu diện tích thực chất là biệt thự 350m² thì điền 40m² là sai rất xa.

Tại sao người ta vẫn dùng median?
Vì nó:


Nhanh


Dễ triển khai


Không bị ảnh hưởng mạnh bởi outlier như mean


Thường là baseline khá tốt


Ví dụ:
df["area"].fillna(df["area"].median())
chỉ mất 1 dòng.

Cách bạn đề xuất thực ra là "conditional imputation"
Thay vì:
Diện tích thiếu↓median của toàn bộ dữ liệu
ta làm:
Diện tích thiếu↓tìm nhóm nhà tương tự↓median trong nhóm đó
Ví dụ:
QuậnPhòng ngủDiện tíchCầu Giấy250Cầu Giấy255Cầu Giấy2?Ba Đình5200
Ta chỉ xét:
Quận = Cầu GiấyPhòng ngủ = 2
Median:
(50,55) → 52.5
Điền:
52.5
Hợp lý hơn nhiều.

Cao cấp hơn: KNN Imputer
Đây gần giống hệt suy nghĩ của bạn.
Ví dụ:
AreaBedroomFrontage50245525?24.5200510
Dòng thiếu:
?, 2, 4.5
KNN sẽ tìm những điểm gần nhất:
50, 2, 455, 2, 5
sau đó lấy trung bình hoặc trọng số:
(50 + 55)/2 = 52.5
Đây chính xác là ý tưởng:

"xem những căn nhà giống nó nhất"


Thậm chí còn mạnh hơn: Predictive Imputation
Thay vì:
tìm hàng gần nhất
ta huấn luyện model:
(Phòng ngủ, mặt tiền, quận, ...)        ↓    Diện tích
Từ các dòng không thiếu diện tích.
Sau đó dự đoán cho dòng bị thiếu.
Ví dụ:
X = df[df["area"].notna()].drop("area", axis=1)y = df[df["area"].notna()]["area"]
Train:
RandomForestRegressor
Rồi dự đoán:
missing_area = model.predict(...)

Trong thực tế khi nào dùng gì?
Dataset nhỏ hoặc bài tập
MedianMode
là đủ.

Dataset nhà đất, tín dụng, khách hàng
Thường dùng:
Median theo nhóm
Ví dụ:
median diện tích theo quậnmedian thu nhập theo nghề nghiệpmedian lương theo cấp bậc

Dự án ML nghiêm túc
Thường thử:


Median


KNN Imputer


Iterative Imputer


Model-based Imputer


sau đó so sánh bằng cross-validation xem cách nào cho mô hình cuối cùng tốt hơn.

Một điểm rất quan trọng: đôi khi giá trị bị thiếu tự nó là thông tin.
Ví dụ hồ sơ vay vốn:
Thu nhập20 triệu?15 triệu
Người không khai thu nhập có thể có hành vi khác với người khai đầy đủ.
Nhiều đội ML sẽ tạo thêm:
incomeincome_missing200? → median1150
để mô hình học được rằng "thiếu dữ liệu" cũng là một tín hiệu. Đây là kỹ thuật rất hay trong các bài toán tín dụng và dự báo rủi ro.
5. Mode Imputation (Điền giá trị xuất hiện nhiều nhất)
Dùng cho dữ liệu categorical.
Ví dụ:
Thành phốHà NộiHà NộiTP.HCM?
Mode:
Hà Nội
Điền:
df["City"] = df["City"].fillna(df["City"].mode()[0])

6. Fill Constant
Điền giá trị cố định.
Ví dụ:
df["City"] = df["City"].fillna("Unknown")
Kết quả:
Thành phốHà NộiTP.HCMUnknown
Cách này khá phổ biến.

7. Forward Fill (ffill)
Hay dùng với dữ liệu thời gian.
Ví dụ:
NgàyGiá11002?3?4120
Forward fill:
NgàyGiá1100210031004120
df.fillna(method="ffill")

8. Backward Fill (bfill)
Ngược lại:
NgàyGiá11002?3?4120
Sau bfill:
NgàyGiá1100212031204120
df.fillna(method="bfill")

9. Interpolation
Nội suy giữa các điểm.
Ví dụ:
Thời gianNhiệt độ1202?330
Nội suy:
25
Kết quả:
Thời gianNhiệt độ120225330
df.interpolate()

10. Dùng mô hình ML để dự đoán giá trị thiếu
Ví dụ:
TuổiKinh nghiệmLương2521030515358?
Ta có thể huấn luyện model:
(Tuổi, Kinh nghiệm) → Lương
Rồi dự đoán lương bị thiếu.
Thư viện:
from sklearn.impute import KNNImputer
hoặc
IterativeImputer

11. KNN Imputation
Ví dụ:
TuổiLương2510261127?
Tìm các hàng gần nhất:
25 → 1026 → 11
Điền:
10.5
from sklearn.impute import KNNImputer

Thực tế người ta thường dùng gì?
Nếu làm dự án ML thông thường:


Numeric feature


Median (phổ biến nhất)


Mean




Categorical feature


Mode


"Unknown"




Time series


Forward fill


Interpolation




Dataset lớn, quan trọng


KNN Imputer


Iterative Imputer




Một quy tắc khá hữu ích:


Thiếu dưới 5% → median/mode thường đủ tốt.


Thiếu 5–30% → cân nhắc kỹ nguyên nhân thiếu.


Thiếu trên 50–70% → thường xem xét bỏ cột đó nếu nó không quá quan trọng.


Điều quan trọng không chỉ là "điền bằng gì", mà còn phải hiểu vì sao dữ liệu bị thiếu. Ví dụ cột "Thu nhập" bị thiếu vì khách hàng từ chối khai báo có thể mang ý nghĩa khác hẳn việc bị thiếu do lỗi nhập liệu. Trong nhiều bài toán, việc thêm một cột cờ như income_missing = 1/0 còn giúp mô hình học được thông tin từ chính việc thiếu dữ liệu đó.
```
# Tạo cột flag
**Ex**
```python
import pandas as pd

df = pd.DataFrame({
    'name': ['A', 'B', 'C', 'D'],
    'age': [15, 16, -2, 14],
    'score': [80, 120, 60, 90]
})

df['invalid_age'] = (
    (df['age'] < 5) | (df['age'] > 18)
).astype(int)

# name   age   score   invalid_age
# A      15    80      0
# B      16    120     0
# C      -2    60      1
# D      14    90      0
```
# Outlier (Phát hiện & xử lý giá trị ngoại lai)
```bash
1. Boxplot / IQR (Interquartile Range)
Bạn đã biết cách này.
Tính:


Q1 = 25%


Q3 = 75%


IQR:
IQR=Q3−Q1IQR = Q3 - Q1IQR=Q3−Q1
Ngưỡng:
Lower=Q1−1.5×IQRLower = Q1 - 1.5 \times IQRLower=Q1−1.5×IQR
Upper=Q3+1.5×IQRUpper = Q3 + 1.5 \times IQRUpper=Q3+1.5×IQR
Điểm nằm ngoài khoảng này được xem là outlier.
Ví dụ:
[10, 11, 12, 13, 15, 16, 17, 100]
100 sẽ bị đánh dấu.
Ưu điểm:


Đơn giản.


Không giả định phân phối chuẩn.


Nhược điểm:


Dữ liệu lệch mạnh có thể đánh dấu hơi nhiều.



2. Z-Score
Áp dụng khi dữ liệu gần phân phối chuẩn.
Công thức:
z=x−μσz=\frac{x-\mu}{\sigma}z=σx−μ​xxxμ\muμσ\sigmaσz=x−μσ≈1.2z=\frac{x-\mu}{\sigma}\approx 1.2z=σx−μ​≈1.2Φ(z)≈88.5%\Phi(z)\approx 88.5\%Φ(z)≈88.5%
Trong đó:


xxx: giá trị


μ\muμ: mean


σ\sigmaσ: độ lệch chuẩn


Thông thường:
|z| > 3
=> outlier
Ví dụ:
Giá trịZ-score10-0.2120.1150.51006.8
100 là outlier.
Python:
from scipy.stats import zscoredf["z"] = zscore(df["salary"])outliers = df[df["z"].abs() > 3]

3. Modified Z-Score (Median Absolute Deviation)
Z-score dùng mean nên dễ bị outlier kéo lệch.
Ví dụ:
[10, 11, 12, 13, 1000]
Mean bị kéo lên rất mạnh.
Người ta thay bằng:


Median


MAD (Median Absolute Deviation)


Ổn định hơn nhiều.
Hay dùng trong dữ liệu tài chính.

4. Histogram
Vẽ histogram.
Ví dụ:
20-30 ██████████30-40 ████████40-50 ██████50-60 ███200    █
Nhìn phát thấy 200 đứng riêng.

5. Scatter Plot
Rất hữu ích với dữ liệu nhiều biến.
Ví dụ:
AreaPrice505555.5606656.56050
Điểm:
(60, 50)
sẽ nằm tách hẳn khỏi đám đông.

6. Percentile
Ví dụ:
Top 1%Bottom 1%
coi là outlier.
Hay dùng trong:


Thu nhập


Giá nhà


Doanh thu


Ví dụ:
lower = df["salary"].quantile(0.01)upper = df["salary"].quantile(0.99)

7. Distance-Based (Khoảng cách)
Ý tưởng:
Điểm nào nằm quá xa các điểm khác→ Outlier
Ví dụ:
(1,1)(1,2)(2,1)(50,50)
Điểm:
(50,50)
rất xa cụm còn lại.

8. KNN Outlier Detection
Ý tưởng giống bạn nói lúc xử lý missing value.
Ví dụ:
Một căn nhà:100m²3 phòng ngủ
Nếu tất cả nhà gần nó đều:
Giá 4-5 tỷ
nhưng nó:
50 tỷ
thì khả năng là outlier.
Dựa trên khoảng cách tới k láng giềng gần nhất.

9. Local Outlier Factor (LOF)
Một kỹ thuật rất nổi tiếng.
Ý tưởng:
Không chỉ xem khoảng cáchmà còn xem mật độ lân cận
Ví dụ:
Cụm A: rất dàyCụm B: thưa
Một điểm có thể bình thường ở cụm B nhưng là outlier ở cụm A.
Scikit-learn:
from sklearn.neighbors import LocalOutlierFactorlof = LocalOutlierFactor()labels = lof.fit_predict(X)

10. Isolation Forest
Đây là kỹ thuật cực kỳ phổ biến trong ML hiện đại.
Ý tưởng:
Outlier thường dễ tách ra khỏi dữ liệu
Ví dụ:
100
rất dễ bị cô lập.
Trong khi:
10,11,12,13
khó tách hơn.
Scikit-learn:
from sklearn.ensemble import IsolationForestclf = IsolationForest()labels = clf.fit_predict(X)

11. DBSCAN
Thuật toán clustering.
Ý tưởng:
Các điểm không thuộc cụm nào→ Outlier
Ví dụ:
●●●●●      ●●●●●●
Điểm ở giữa không thuộc cụm nào.
DBSCAN sẽ gắn:
label = -1

Thực tế Data Scientist hay dùng gì?
Dữ liệu 1 biến
Ví dụ:


tuổi


lương


diện tích


Thường:


IQR


Boxplot


Z-score



Dữ liệu nhiều biến
Ví dụ:


diện tích


số phòng ngủ


mặt tiền


khoảng cách tới trung tâm


Thường:


Isolation Forest


LOF


DBSCAN



Với bài toán giá nhà
Nếu có:
areabedroombathroomfrontagedistrictprice
thì chỉ dùng boxplot cho price là chưa đủ.
Ví dụ:
AreaPrice505 tỷ30025 tỷ
25 tỷ không hề là outlier nếu diện tích 300m².
Nhưng:
AreaPrice5050 tỷ
thì mới đáng nghi.
Lúc này phải dùng các phương pháp đa biến như:


Scatter Plot


LOF


Isolation Forest


vì chúng xét mối quan hệ giữa nhiều đặc trưng cùng lúc, chứ không chỉ nhìn từng cột riêng lẻ.
```
- [Missing values (kỹ thuật xử lý giá trị thiếu)](#missing-values-kỹ-thuật-xử-lý-giá-trị-thiếu)
- [Outlier (Phát hiện \& xử lý giá trị ngoại lai)](#outlier-phát-hiện--xử-lý-giá-trị-ngoại-lai)
- [Scale (Đưa feature về cùng thang đo)](#scale-đưa-feature-về-cùng-thang-đo)
  - [Standardization (Z-score)](#standardization-z-score)
  - [Min-Max Scaling](#min-max-scaling)
  - [Robust Scaling](#robust-scaling)
---
# Scale (Đưa feature về cùng thang đo)
**Ex**
```bash
- Giả sử bạn có 2 feature:
    + Chiều cao: 150 → 180 (cm)
    + Lương: 5,000 → 50,000 (USD)
- Nếu không scale: Model sẽ “nghĩ” lương quan trọng hơn nhiều (vì số lớn hơn)
- Sau khi scaling về [0,1]: Cả 2 feature đều nằm cùng range → model học công bằng hơn
```
## Standardization (Z-score)
```bash
Đưa dữ liệu về phân phối có
    - mean = 0
    - std = 1
```
**Formula**
```bash
x' = (x - μ) / σ

- Input:
    + x         : giá trị gốc
    + μ (mu)    : mean — trung bình của toàn bộ feature
    + σ (sigma) : standard deviation — độ lệch chuẩn (mức độ phân tán dữ liệu)
- Output: 
    + x′        : giá trị sau khi scale
```
## Min-Max Scaling
```bash
Đưa dữ liệu về khoảng [0, 1]
```
**Formula**
```bash
x' = (x - x_min) / (x_max - x_min)
```
**Ex**
```bash
| Giá trị gốc | Giá trị mới |
| ----------- | ----------- |
| 150         | 0           |
| 160         | 0.25        |
| 170         | 0.5         |
| 180         | 0.75        |
| 190         | 1           |
Ý nghĩa:
    + Ép toàn bộ dữ liệu vào đoạn [0,1].
    + Nó giữ nguyên thứ tự và tỷ lệ tương đối.
```
## Robust Scaling
```bash
- Dùng median + IQR
- Ít bị ảnh hưởng bởi outlier
```
**Formula**
```bash
x' = (x - median) / IQR

- x                         : giá trị gốc
- median                    : giá trị trung vị (ở giữa khi sắp xếp)
- IQR (Interquartile Range) : IQR = Q3 - Q1
    + Q1: 25th percentile
    + Q3: 75th percentile
    + x′: giá trị sau scaling
```