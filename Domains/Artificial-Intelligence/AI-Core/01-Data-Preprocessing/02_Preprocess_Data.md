- [Missing values (kỹ thuật xử lý giá trị thiếu)](#missing-values-kỹ-thuật-xử-lý-giá-trị-thiếu)
  - [Drop (Xóa sample hoặc cột có giá trị thiếu)](#drop-xóa-sample-hoặc-cột-có-giá-trị-thiếu)
  - [Mean Imputation (Điền giá trị trung bình của toàn cột)](#mean-imputation-điền-giá-trị-trung-bình-của-toàn-cột)
  - [Median Imputation (Điền giá trị trung vị)](#median-imputation-điền-giá-trị-trung-vị)
  - [conditional imputation (điền theo nhóm)](#conditional-imputation-điền-theo-nhóm)
  - [KNN Imputer (dùng KNN để tìm nhóm và điền)](#knn-imputer-dùng-knn-để-tìm-nhóm-và-điền)
  - [Predictive Imputation (huấn luyện model từ các dòng không thiếu dự đoán ra giá trị của dòng thiếu)](#predictive-imputation-huấn-luyện-model-từ-các-dòng-không-thiếu-dự-đoán-ra-giá-trị-của-dòng-thiếu)
  - [Mode Imputation (Điền giá trị xuất hiện nhiều nhất)](#mode-imputation-điền-giá-trị-xuất-hiện-nhiều-nhất)
  - [Fill Constant (Điền giá trị cố định)](#fill-constant-điền-giá-trị-cố-định)
  - [Forward Fill (ffill - Hay dùng với dữ liệu thời gian)](#forward-fill-ffill---hay-dùng-với-dữ-liệu-thời-gian)
  - [Backward Fill (bfill)](#backward-fill-bfill)
  - [Interpolation (Nội suy giữa các điểm)](#interpolation-nội-suy-giữa-các-điểm)
  - [Tạo cột flag (Tạo cột cờ)](#tạo-cột-flag-tạo-cột-cờ)
  - [Yếu vị (Mode)](#yếu-vị-mode)
  - [Phân vị (Percentiles - ví dụ Q1, Q3, P95, P99)](#phân-vị-percentiles---ví-dụ-q1-q3-p95-p99)
- [Outlier (Phát hiện \& xử lý giá trị ngoại lai)](#outlier-phát-hiện--xử-lý-giá-trị-ngoại-lai)
  - [Boxplot / IQR (Interquartile Range) (Khoảng tứ phân vị)](#boxplot--iqr-interquartile-range-khoảng-tứ-phân-vị)
  - [Z-Score (Giá trị này cách mức trung bình bao nhiêu độ lệch chuẩn)](#z-score-giá-trị-này-cách-mức-trung-bình-bao-nhiêu-độ-lệch-chuẩn)
  - [Modified Z-Score (Median Absolute Deviation)](#modified-z-score-median-absolute-deviation)
  - [Histogram (biểu đồ tần suất)](#histogram-biểu-đồ-tần-suất)
  - [Scatter Plot](#scatter-plot)
  - [Percentile](#percentile)
  - [Distance-Based (Khoảng cách)](#distance-based-khoảng-cách)
  - [KNN Outlier Detection](#knn-outlier-detection)
  - [Local Outlier Factor (LOF) (Không chỉ xem khoảng cách mà còn xem mật độ lân cận)](#local-outlier-factor-lof-không-chỉ-xem-khoảng-cách-mà-còn-xem-mật-độ-lân-cận)
  - [Isolation Forest](#isolation-forest)
  - [DBSCAN](#dbscan)
- [Normalization (chuẩn hóa dữ liệu - Đưa feature về cùng thang đo)](#normalization-chuẩn-hóa-dữ-liệu---đưa-feature-về-cùng-thang-đo)
  - [Standardization (Z-score) (Đưa dữ liệu về phân phối có mean = 0, std = 1)](#standardization-z-score-đưa-dữ-liệu-về-phân-phối-có-mean--0-std--1)
  - [Min-Max Scaling](#min-max-scaling)
  - [Robust Scaling](#robust-scaling)
- [Encode (Máy học không hiểu chữ, nên phải biến thành số. Có 3 cách phổ biến)](#encode-máy-học-không-hiểu-chữ-nên-phải-biến-thành-số-có-3-cách-phổ-biến)
  - [One-Hot Encoding](#one-hot-encoding)
  - [Label Encoding (Gán số cho từng giá trị)](#label-encoding-gán-số-cho-từng-giá-trị)
  - [Target Encoding (Thay mỗi giá trị bằng trung bình của biến mục tiêu)](#target-encoding-thay-mỗi-giá-trị-bằng-trung-bình-của-biến-mục-tiêu)
- [Imbalanced Data (Mất cân bằng dữ liệu)](#imbalanced-data-mất-cân-bằng-dữ-liệu)
  - [SMOTE (Oversampling) (Tạo thêm dữ liệu giả cho lớp ít)](#smote-oversampling-tạo-thêm-dữ-liệu-giả-cho-lớp-ít)
  - [Downsampling (Giảm bớt dữ liệu lớp nhiều)](#downsampling-giảm-bớt-dữ-liệu-lớp-nhiều)
  - [Class Weights (Không thay đổi dữ liệu, nhưng phạt lỗi lớp ít nặng hơn)](#class-weights-không-thay-đổi-dữ-liệu-nhưng-phạt-lỗi-lớp-ít-nặng-hơn)
- [Data Leakage (Rò rỉ dữ liệu)](#data-leakage-rò-rỉ-dữ-liệu)
---
# Missing values (kỹ thuật xử lý giá trị thiếu)
```bash
Một điểm rất quan trọng: 
    đôi khi giá trị bị thiếu tự nó là thông tin.
    
    Ví dụ hồ sơ vay vốn:
        Thu nhập
        20 triệu
        ?
        15 triệu
        
        Người không khai thu nhập có thể có hành vi khác với người khai đầy đủ.
        
        Nhiều đội ML sẽ tạo thêm:
            income_missing200? → median1150
            
            để mô hình học được rằng "thiếu dữ liệu" cũng là một tín hiệu. Đây là kỹ thuật rất hay trong các bài toán tín dụng và dự báo rủi ro.

Một quy tắc khá hữu ích:
    - Thiếu dưới 5% → median/mode thường đủ tốt.
    - Thiếu 5–30% → cân nhắc kỹ nguyên nhân thiếu.
    - Thiếu trên 50–70% → thường xem xét bỏ cột đó nếu nó không quá quan trọng.

Điều quan trọng không chỉ là "điền bằng gì", mà còn phải hiểu vì sao dữ liệu bị thiếu. 
    Ví dụ cột "Thu nhập" bị thiếu vì khách hàng từ chối khai báo có thể mang ý nghĩa khác hẳn việc bị thiếu do lỗi nhập liệu.
        Trong nhiều bài toán, việc thêm một cột cờ như income_missing = 1/0 còn giúp mô hình học được thông tin từ chính việc thiếu dữ liệu đó.
```
**Trong thực tế khi nào dùng cách nào gì?**
```bash
- Dataset nhỏ hoặc bài tập
    MedianMode là đủ.

- Dataset nhà đất, tín dụng, khách hàng
    Median theo nhóm

- Dự án ML nghiêm túc
    + Median
    + KNN Imputer
    + Iterative Imputer
    + Model-based Imputer
    + sau đó so sánh bằng cross-validation xem cách nào cho mô hình cuối cùng tốt hơn.
```
## Drop (Xóa sample hoặc cột có giá trị thiếu)
```bash
Nếu số lượng missing của sample rất ít hoặc cột bị thiếu quá nhiều.
```
**Ex1: Xóa hàng**
```bash
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
| ID | Tuổi | Email                                 |
| -- | ---- | ------------------------------------- |
| 1  | 25   | ?                                     |
| 2  | 30   | ?                                     |
| 3  | 40   | [abc@gmail.com](mailto:abc@gmail.com) |

90% email bị thiếu. Có thể bỏ luôn
```
## Mean Imputation (Điền giá trị trung bình của toàn cột)
**Ex**
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
## Median Imputation (Điền giá trị trung vị)
```bash
Đây là cách thường dùng hơn Mean.
```
**Tại sao người ta dùng median?**
```bash
Vì nó:
    - Nhanh
    - Dễ triển khai
    - Không bị ảnh hưởng mạnh bởi outlier như mean
    - Thường là baseline khá tốt
```
**Ex**
```bash
| Lương |
| ----- |
| 10    | 
| 12    |
| 15    |
| 1000  |
| ?     |

Nếu điền Mean:
    (10+12+15+1000)/4 = 259.25 -> Rất vô lý.

Nếu điền Median: 13.5 -> hợp lý

Thay:
    df["Salary"] = df["Salary"].fillna(df["Salary"].median())
```
## conditional imputation (điền theo nhóm)
```bash
Thay vì: → Diện tích thiếu → median của toàn bộ dữ liệu
    Ta làm: Diện tích thiếu → tìm nhóm nhà tương tự → median trong nhóm đó
```
**Ex**
```bash
Quận        Phòng ngủ   Diện tích
Cầu Giấy    2           50     
Cầu Giấy    2           55
Cầu Giấy    2           ?
Ba Đình     5           200
```
```bash
Ta chỉ xét:
    Quận = Cầu Giấy
    Phòng ngủ = 2
Median: (50,55) → 52.5 → Điền: 52.5
```
## KNN Imputer (dùng KNN để tìm nhóm và điền)
**Ex**
```bash
Area    Bedroom     Frontage
50      2           45
52      5           ?
24.5    2           41

KNN sẽ tìm những điểm gần nhất:
    sau đó lấy trung bình hoặc trọng số:
        (50 + 55)/2 = 52.5

Đây chính xác là ý tưởng:
    "xem những căn nhà giống nó nhất"
```
## Predictive Imputation (huấn luyện model từ các dòng không thiếu dự đoán ra giá trị của dòng thiếu)
## Mode Imputation (Điền giá trị xuất hiện nhiều nhất)
```bash
Dùng cho dữ liệu categorical.
    Ví dụ:
        Thành phố
        Hà Nội
        Hà Nội
        TP.HCM
        ?
```
## Fill Constant (Điền giá trị cố định)
## Forward Fill (ffill - Hay dùng với dữ liệu thời gian)
**Ex**
```python
df.fillna(method="ffill")
```
## Backward Fill (bfill)
**Ex**
```python
df.fillna(method="bfill")
```
## Interpolation (Nội suy giữa các điểm)
**Ex**
```python
df.interpolate()
```
## Tạo cột flag (Tạo cột cờ)
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
## Yếu vị (Mode)
```bash
Con số chi phí xuất hiện nhiều nhất trong tập dữ liệu (ví dụ: mức phí khám lâm sàng thông thường).
```
## Phân vị (Percentiles - ví dụ Q1, Q3, P95, P99)
```bash
Cực kỳ quan trọng trong bảo hiểm. Ví dụ, chỉ số P99 (99th Percentile) sẽ cho công ty biết: "99% các ca khám bệnh có chi phí dưới mức X, và chỉ có 1% ca đặc biệt vượt qua mức X". Điều này giúp công ty ước lượng được quỹ dự phòng rủi ro tối đa cần chuẩn bị.
```
# Outlier (Phát hiện & xử lý giá trị ngoại lai)
## Boxplot / IQR (Interquartile Range) (Khoảng tứ phân vị)
```bash
IQR là khoảng cách 50% dữ liệu ở giữa
    IQR = Q3−Q1
```
**Tính ngưỡng để phát hiện outlier**
```bash
Ta tạo hai "hàng rào":
    - Ngưỡng dưới: Lower = Q1 − 1.5×IQR
    - Ngưỡng trên: Upper = Q3 + 1.5×IQR
=> Điểm nằm ngoài khoảng này được xem là outlier.

Ví dụ: [10, 11, 12, 13, 15, 16, 17, 100] => 100 sẽ bị đánh dấu.
    Ưu điểm:
        - Đơn giản.
        - Không giả định phân phối chuẩn.
    Nhược điểm:
        - Dữ liệu lệch mạnh có thể đánh dấu hơi nhiều.
```
## Z-Score (Giá trị này cách mức trung bình bao nhiêu độ lệch chuẩn)
```bash
Dùng để tìm outlier
    Quy tắc thường dùng:
        Nếu |z| > 3 thì coi là outlier. Nghĩa là giá trị đó cách trung bình hơn 3 lần độ lệch chuẩn, khá bất thường.

Khi nào dùng?
    ✅ Dùng tốt khi dữ liệu có dạng chuông (gần phân phối chuẩn).
    ❌ Nếu dữ liệu bị lệch mạnh, Z-score có thể cho kết quả không tốt.
```
**Fomula**
```bash
z = (x-μ)/σ

- x: là giá trị cần kiểm tra
- μ (mean): giá trị trung bình
- σ (độ lệch chuẩn): mức độ dữ liệu phân tán
```
**Ex**
```bash
Giả sử chiều cao học sinh trong lớp:
    - Trung bình: 170 cm
    - Độ lệch chuẩn: 5 cm

Một bạn cao 180 cm:
    z = (180−170)/5 = 2
=> Bạn này cao hơn trung bình 2 độ lệch chuẩn.
```
## Modified Z-Score (Median Absolute Deviation)
```bash
Z-score dùng mean nên dễ bị outlier kéo lệch.
    Ví dụ: [10, 11, 12, 13, 1000]. Mean bị kéo lên rất mạnh.
        Người ta thay bằng: Median - MAD (Median Absolute Deviation)
            - Ổn định hơn nhiều.
            - Hay dùng trong dữ liệu tài chính.
```
## Histogram (biểu đồ tần suất)
**Ex**
```bash
20-30 ██████████
30-40 ████████
40-50 ██████
50-60 ███
200   █
# Nhìn phát thấy 200 đứng riêng.
```
## Scatter Plot
```bash
Rất hữu ích với dữ liệu nhiều biến.
```
## Percentile
## Distance-Based (Khoảng cách)
```bash
Ý tưởng: Điểm nào nằm quá xa các điểm khác→ Outlier
    Ví dụ: (1,1)(1,2)(2,1)(50,50)
        Điểm: (50,50) - rất xa cụm còn lại.
```
## KNN Outlier Detection
```bash
Dựa trên khoảng cách tới k láng giềng gần nhất.
```
## Local Outlier Factor (LOF) (Không chỉ xem khoảng cách mà còn xem mật độ lân cận)
## Isolation Forest
```bash
Đây là kỹ thuật cực kỳ phổ biến trong ML hiện đại. Ý tưởng:
    Outlier thường dễ tách ra khỏi dữ liệu

Ví dụ: 100
    - rất dễ bị cô lập.
    - Trong khi: 10,11,12,13. khó tách hơn.
```
## DBSCAN
```bash
Thuật toán clustering. Ý tưởng: Các điểm không thuộc cụm nào → Outlier
    Ví dụ:
        ●●●●●      ●●●●●●
        Điểm ở giữa không thuộc cụm nào. DBSCAN sẽ gắn: label = -1
```
# Normalization (chuẩn hóa dữ liệu - Đưa feature về cùng thang đo)
**Ex**
```bash
Giả sử bạn có 2 feature:
    - Chiều cao: 150 → 180 (cm)
    - Lương: 5,000 → 50,000 (USD)

Nếu không scale: Model sẽ “nghĩ” lương quan trọng hơn nhiều (vì số lớn hơn)
Sau khi scaling về [0,1]: Cả 2 feature đều nằm cùng range → model học công bằng hơn
```
## Standardization (Z-score) (Đưa dữ liệu về phân phối có mean = 0, std = 1)
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
# Encode (Máy học không hiểu chữ, nên phải biến thành số. Có 3 cách phổ biến)
```bash
Có thứ tự?
    Ví dụ:
        - Nhỏ / Vừa / Lớn
        - Junior / Mid / Senior
👉 Label Encoding

Không có thứ tự và số category ít?
    Ví dụ:
        - Màu sắc
        - Giới tính
        - Hãng xe
👉 One-Hot Encoding

Không có thứ tự nhưng category rất nhiều?
    Ví dụ:
        - Zip code
        - Product ID
        - User ID
        - Thành phố (hàng nghìn loại)
👉 Target Encoding

Mẹo thực tế khi đi làm Nếu số category:
    - < 10 → thường One-Hot
    - 10–50 → cân nhắc One-Hot
    - 100 → bắt đầu xem xét Target Encoding
    - 1000 → gần như không muốn One-Hot nữa
```
## One-Hot Encoding
```bash
Biến mỗi giá trị thành một cột riêng.
    Màu	    Đỏ	Xanh	Vàng
    Đỏ	    1	0	    0
    Xanh	0	1	    0
    Vàng	0	0	    1

Dùng khi nào?
    Khi các giá trị không có thứ tự.
        Ví dụ:
            - Giới tính
            - Thành phố (ít loại)
            - Màu sắc
            - Hãng xe
        Vì:
            - Đỏ không lớn hơn Xanh
            - Toyota không lớn hơn Honda

Nhược điểm:
    - Nếu có 1000 thành phố: → tạo ra 1000 cột.
    - Đó là cái gọi là "tăng chiều dữ liệu vô tội vạ".
```
## Label Encoding (Gán số cho từng giá trị)
```bash
Dùng khi nào?
    Khi dữ liệu có thứ tự thật sự. => Không nên dùng cho dữ liệu không có thứ tự

Ví dụ:
    Mức độ
        - Thấp
        - Trung bình
        - Cao
    Encode:
        - Thấp = 0
        - Trung bình = 1
        - Cao = 2

Điều này hợp lý vì:

Cao>Trung bình > Thấp
```
## Target Encoding (Thay mỗi giá trị bằng trung bình của biến mục tiêu)
```bash
Dùng khi nào?
    Khi có rất nhiều category.

Ví dụ:
    - 10.000 sản phẩm
    - 5.000 mã bưu điện
    - 20.000 user ID

Nếu One-Hot:
    → hàng nghìn cột.

Nếu Target Encoding:
    → chỉ 1 cột.

Nhược điểm
    - Dễ bị data leakage.
    - Ví dụ bạn dùng toàn bộ dữ liệu để tính tỷ lệ mua rồi train.
    - Mô hình đã "nhìn trước đáp án".

Vì vậy thường phải:
    - K-Fold Target Encoding
    - Leave-One-Out Encoding
    - CatBoost Encoding
```
**Ex: dự đoán khách có mua hàng hay không**
```bash
Thành phố	Tỷ lệ mua
Hà Nội	    80%
TP.HCM	    60%
Đà Nẵng	    30%

Encode thành:
    Thành phố
        Hà Nội → 0.8
        TP.HCM → 0.6
        Đà Nẵng → 0.3
```
PCA: Nén dữ liệu bằng cách giữ lại những thông tin quan trọng nhất.
Dùng khi dữ liệu có nhiều cột (nhiều đặc trưng).
Giúp giảm chiều, tăng tốc huấn luyện, giảm nhiễu.
Ví dụ: từ 1000 đặc trưng giảm còn 50 đặc trưng.
t-SNE: Vẽ dữ liệu nhiều chiều xuống 2D/3D để nhìn xem các nhóm có tách biệt không.
Chủ yếu để trực quan hóa.
Ví dụ: kiểm tra ảnh mèo, chó, chim có tự động tụ thành các cụm riêng không.
UMAP: Giống t-SNE nhưng nhanh hơn, giữ được cấu trúc tổng thể tốt hơn.
Thường được dùng thay t-SNE trên tập dữ liệu lớn.
Ghi nhớ một câu
PCA → "nén dữ liệu để mô hình học nhanh hơn".
t-SNE / UMAP → "vẽ dữ liệu để con người nhìn và hiểu nó".
Tuyến tính vs Phi tuyến tính
PCA (tuyến tính): giả sử dữ liệu có thể được mô tả bằng các đường/thành phần tuyến tính.
t-SNE, UMAP (phi tuyến tính): xử lý được các hình dạng phức tạp như vòng tròn, xoắn ốc, cụm cong mà PCA thường không tách được.
Ví dụ rất dễ hiểu:
PCA (nén dữ liệu)
Giả sử mỗi người có:


Chiều cao


Cân nặng


Cỡ áo


Ba thông tin này liên quan khá chặt với nhau. Người cao thường nặng hơn và mặc áo lớn hơn.
PCA có thể gộp chúng thành một chỉ số mới như:

"Kích thước cơ thể"

Thay vì lưu 3 cột, chỉ cần 1 cột mà vẫn giữ phần lớn thông tin.
➡️ Trong AI: giảm số đặc trưng để mô hình học nhanh hơn.

t-SNE / UMAP (vẽ dữ liệu)
Giả sử AI đã biến mỗi ảnh thành 1000 con số.
Con người không thể nhìn dữ liệu 1000 chiều.
t-SNE hoặc UMAP sẽ vẽ chúng xuống mặt phẳng 2D:


Ảnh chó tụ thành một đám.


Ảnh mèo tụ thành một đám khác.


Ảnh chim tụ thành một đám khác.


Ta nhìn biểu đồ và thấy:
🐶🐶🐶🐶        🐱🐱🐱🐱                    🐦🐦🐦🐦
➡️ Trong AI: kiểm tra xem dữ liệu hoặc embedding có tự động phân nhóm tốt không.
Tóm tắt


PCA = "nén dữ liệu".


t-SNE / UMAP = "vẽ dữ liệu nhiều chiều thành hình để nhìn các cụm".

# Imbalanced Data (Mất cân bằng dữ liệu)
```bash
Là khi dữ liệu bị lệch rất nhiều giữa các lớp.

Ví dụ:
- 95%: không gian lận
- 5%: gian lận
👉 Model dễ “học lệch” → chỉ đoán lớp nhiều (95%)
```
## SMOTE (Oversampling) (Tạo thêm dữ liệu giả cho lớp ít)
```bash
Lớp ít (fraud) → bị thiếu. SMOTE sẽ tạo thêm dữ liệu giống nó
👉 giống như “nhân bản thông minh”

📌 Ví dụ:
- 100 gian lận → tạo thêm thành 1000
```
## Downsampling (Giảm bớt dữ liệu lớp nhiều)
```bash
Lớp nhiều (không gian lận) → bỏ bớt

📌 Ví dụ:
- 10,000 bình thường → giảm còn 1000
```
## Class Weights (Không thay đổi dữ liệu, nhưng phạt lỗi lớp ít nặng hơn)
```bash
Model bị ép phải quan tâm hơn tới lớp hiếm


📌 Ví dụ:
- Sai gian lận → bị phạt nặng hơn sai bình thường
```
# Data Leakage (Rò rỉ dữ liệu)
```bash
👉 Là khi model “nhìn thấy trước đáp án” trong dữ liệu test hoặc tương lai trong lúc học.
➡️ Kết quả: model học “giả giỏi”, nhưng ra thực tế thì dở.

🧠 Hiểu đơn giản:
    Bạn cho học sinh làm đề thi, nhưng lỡ “cho xem đáp án trước”

    👉 Học sinh làm bài rất cao
    ❌ nhưng không phải vì giỏi thật


🚨 Tại sao nguy hiểm?
    - Model test accuracy rất cao (ảo)
    - Nhưng khi deploy → sai nhiều

🔥 Nguyên tắc quan trọng:
    👉 Chỉ được fit trên tập train, tuyệt đối không fit trên toàn bộ data.
    🧠 Vì sao?
        - fit = học thông tin từ dữ liệu (mean, std, min, max…)
        - Nếu fit cả dataset → model đã “nhìn thấy test”
        ➡️ Test không còn là dữ liệu “chưa biết” nữa → bị data leakage
```
**Ex**
```bash
❌ Sai (bị leakage):
    Bạn làm preprocessing như này:
        scaler.fit(all_data)
        train, test = split(all_data)
    👉 Nghĩa là:
        scaler đã “nhìn toàn bộ dữ liệu” (có cả test)
        ➡️ Test không còn “bí mật” nữa → bị rò rỉ thông tin
✅ Đúng:
    train, test = split(data)
    scaler.fit(train)
    train_scaled = scaler.transform(train)
    test_scaled = scaler.transform(test)
👉 scaler chỉ học từ train thôi
```