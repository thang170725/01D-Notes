colorsys là thư viện chuẩn của Python dùng để chuyển đổi giữa các hệ màu. Nó không cần cài đặt bằng pip.

Chỉ cần:

import colorsys
colorsys dùng để làm gì?

Nó hỗ trợ chuyển đổi giữa các hệ màu phổ biến:

RGB (Red, Green, Blue)
HSV (Hue, Saturation, Value)
HLS (Hue, Lightness, Saturation)
YIQ (hệ màu dùng trong truyền hình NTSC)

Các hàm chính:

Hàm	Chức năng
rgb_to_hsv(r, g, b)	RGB → HSV
hsv_to_rgb(h, s, v)	HSV → RGB
rgb_to_hls(r, g, b)	RGB → HLS
hls_to_rgb(h, l, s)	HLS → RGB
rgb_to_yiq(r, g, b)	RGB → YIQ
yiq_to_rgb(y, i, q)	YIQ → RGB
Ví dụ
RGB → HSV
import colorsys

r, g, b = 1.0, 0.0, 0.0  # Màu đỏ

h, s, v = colorsys.rgb_to_hsv(r, g, b)

print(h, s, v)

Kết quả:

0.0 1.0 1.0
HSV → RGB
import colorsys

r, g, b = colorsys.hsv_to_rgb(0.5, 1.0, 1.0)

print(r, g, b)
Lưu ý quan trọng

colorsys không dùng thang màu 0–255 như nhiều thư viện khác.

Nó dùng số thực từ 0.0 đến 1.0.

Ví dụ, nếu có màu RGB:

(255, 128, 0)

thì phải đổi sang:

r = 255 / 255
g = 128 / 255
b = 0 / 255

h, s, v = colorsys.rgb_to_hsv(r, g, b)
Khi nào nên dùng?
Tạo hiệu ứng chuyển màu (gradient, rainbow).
Thay đổi độ sáng hoặc độ bão hòa của màu.
Sinh màu ngẫu nhiên nhưng vẫn hài hòa.
Kết hợp với turtle, matplotlib, pygame, hoặc các thư viện đồ họa khác để tạo hiệu ứng màu sắc.

Kết luận: colorsys là thư viện chuẩn (standard library) của Python, nên không cần cài đặt, chỉ cần import colorsys là dùng được.
# hsv_to_rgb()
HSV là gì?

RGB

Red
Green
Blue

HSV

Hue
Saturation
Value

Hue nghĩa là "vị trí trên vòng màu".

Ví dụ

0.0
↓

Đỏ

0.15

Cam

0.33

Lục

0.66

Xanh dương

0.83

Tím

1.0

Đỏ lại

Ví dụ

import colorsys

print(colorsys.hsv_to_rgb(0,1,1))

Kết quả

(1,0,0)

đỏ.

print(colorsys.hsv_to_rgb(0.33,1,1))
(0,1,0)

xanh lá.

print(colorsys.hsv_to_rgb(0.66,1,1))
(0,0,1)

xanh dương.

Ví dụ Turtle
from turtle import *
import colorsys

colormode(1)

for i in range(20):

    color = colorsys.hsv_to_rgb(i/20,1,1)

    pencolor(color)

    forward(20)

done()

Mỗi đoạn thẳng sẽ có màu khác nhau.

Vì sao trong code lại có
h += 0.002

Ban đầu

h = 0

↓

Đỏ

h = 0.1

↓

Cam

h = 0.2

↓

Vàng

h = 0.3

↓

Lục

...

Đến

h = 1

quay lại đỏ.

Nó tạo hiệu ứng cầu vồng liên tục.