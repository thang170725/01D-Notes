- [ACF (AutoCorrelation Function — hàm tự tương quan)](#acf-autocorrelation-function--hàm-tự-tương-quan)
---
# ACF (AutoCorrelation Function — hàm tự tương quan) 
```bash
- Là biểu đồ rất quan trọng trong time series.
- Nó trả lời: Giá trị hiện tại có liên hệ với các giá trị quá khứ bao nhiêu?
- Nói đơn giản:
    + Hôm nay dùng điện có liên quan hôm qua không?
    + Giờ 10h hôm nay có liên quan giờ 10h hôm qua không?
    + Có chu kỳ 24h không?
- ACF dùng để làm gì?
    (a) Phát hiện seasonality / chu kỳ
        + Ví dụ dữ liệu điện theo giờ:
        + Nếu có chu kỳ 24h:
            - lag 24 tương quan cao
            - lag 48 cũng cao
        => pattern lặp mỗi ngày. Đây là ứng dụng rất hay.
    (b) Xem chuỗi có autocorrelation không
        + Nếu các lag đều gần 0: chuỗi gần random.
        + Nếu nhiều lag cao: chuỗi phụ thuộc quá khứ.
    (c) Hỗ trợ chọn tham số ARIMA
ACF dùng chọn q (MA order).
(PACF thường dùng chọn p.)

(d) Kiểm tra stationarity sơ bộ

ACF decay chậm:

có thể non-stationary.
2. "Lag" là gì?

Lag k:

x_t  so với x_(t-k)

Lag 1:

hiện tại với 1 bước trước

Lag 24:

hiện tại với 24 bước trước.
3. Công thức

Tự tương quan tại lag k:

ρ
k
	​

=
Var(X
t
	​

)
Cov(X
t
	​

,X
t−k
	​

)
	​


Giá trị:

gần 1 → tương quan mạnh
gần 0 → ít liên quan
âm → quan hệ ngược
4. Vẽ ACF

Thường dùng statsmodels

Cài:

pip install statsmodels
Cú pháp cơ bản
from statsmodels.graphics.tsaplots import plot_acf
import matplotlib.pyplot as plt

plot_acf(df["usage"], lags=50)

plt.show()
Nếu là time series điện theo giờ:
plot_acf(
    df["usage"],
    lags=72
)

72 lag = 3 ngày nếu dữ liệu theo giờ.

5. Đọc biểu đồ ACF
lag
1  |████
2  |███
3  |██
...
24 |█████

Spike lớn ở 24:

=> seasonal 24 giờ.

Nếu:

24
48
72

đều spike

=> daily seasonality rất rõ.

Hai đường xanh (confidence interval)

Nếu cột vượt khoảng đó:

autocorrelation có ý nghĩa.

Nếu nằm trong:

có thể chỉ là noise.
6. Với dữ liệu điện của bạn

Cực đáng vẽ.

plot_acf(
    df["load"],
    lags=48
)

Có thể thấy:

lag 1 mạnh
lag 24 mạnh

=> điện có memory + seasonality.

Rất hay cho forecasting.

7. Trước khi vẽ hay differencing

Nếu chuỗi trend mạnh:

series_diff = df["load"].diff().dropna()

plot_acf(series_diff)

đôi khi hợp lý hơn.

8. ACF vs PACF

ACF:

tổng ảnh hưởng trực tiếp + gián tiếp

PACF:

chỉ ảnh hưởng trực tiếp
from statsmodels.graphics.tsaplots import plot_pacf

plot_pacf(series)

Hay vẽ cặp:

plot_acf(series)
plot_pacf(series)
9. Ví dụ pattern thường gặp
White noise
mọi lag gần 0
AR process

ACF giảm dần:

████
███
██
█
Seasonal

Spike ở:

24
48
72
10. Nếu dùng pandas + seaborn không?

ACF thường không dùng seaborn.

Chuẩn nhất:

statsmodels.plot_acf
11. Với EDA time series thường combo:
Line plot
Rolling mean
ACF
PACF
Seasonal decomposition

Ví dụ decomposition còn hay nữa:

from statsmodels.tsa.seasonal import seasonal_decompose
Với project LightGBM điện năng

ACF giúp biết nên tạo feature:

Nếu lag 24 mạnh:

df["lag24"] = df["load"].shift(24)

Nếu lag 168 mạnh (7 ngày):

df["lag168"] = df["load"].shift(168)

ACF thường dẫn trực tiếp đến feature engineering.

Nếu muốn mình có thể chỉ cách đọc ACF để tạo lag features cho LightGBM forecasting nữa.