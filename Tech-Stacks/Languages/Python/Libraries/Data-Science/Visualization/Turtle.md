turtle là thư viện có sẵn trong Python dùng để vẽ đồ họa 2D bằng cách điều khiển một "con rùa" (turtle) di chuyển trên màn hình.

Nó thường được dùng để:

Học lập trình cho người mới bắt đầu.
Hiểu cách hoạt động của tọa độ, góc và hình học.
Minh họa thuật toán.
Vẽ các hình đơn giản hoặc hình lặp (fractal, hoa văn,...).
1. Ý tưởng của turtle

Hãy tưởng tượng có một con rùa đang đứng trên màn hình.

Nó có thể:

Đi thẳng
Lùi lại
Quay trái
Quay phải
Nhấc bút lên
Đặt bút xuống

Mỗi khi rùa di chuyển và bút đang đặt xuống, nó sẽ để lại một đường vẽ.

Ban đầu

      ↑
      🐢

forward(100)

      |
      |
      |
      🐢
2. Ví dụ đơn giản
import turtle

t = turtle.Turtle()

t.forward(100)

turtle.done()

Kết quả:

Mở một cửa sổ.
Con rùa đi thẳng 100 pixel.
Vẽ một đoạn thẳng dài 100 pixel.
3. Vẽ hình vuông
import turtle

t = turtle.Turtle()

for _ in range(4):
    t.forward(100)
    t.right(90)

turtle.done()

Giải thích:

Đi 100
↓

Rẽ phải 90°

↓

Đi 100

↓

Rẽ phải 90°

↓

...

Kết quả:

+---------+
|         |
|         |
|         |
+---------+
4. Một số lệnh quan trọng
Hàm	Ý nghĩa
forward(100)	Đi tới 100 pixel
backward(100)	Đi lùi
left(90)	Quay trái 90°
right(90)	Quay phải 90°
penup()	Nhấc bút lên (di chuyển không vẽ)
pendown()	Đặt bút xuống (bắt đầu vẽ)
goto(x, y)	Đi tới tọa độ (x, y)
circle(50)	Vẽ hình tròn bán kính 50
color("red")	Đổi màu bút
pensize(5)	Độ dày nét vẽ
speed(5)	Tốc độ vẽ (1–10 hoặc 0 là nhanh nhất)
5. Vẽ hình tròn
import turtle

t = turtle.Turtle()

t.circle(80)

turtle.done()
6. Vẽ ngôi sao
import turtle

t = turtle.Turtle()

for _ in range(5):
    t.forward(150)
    t.right(144)

turtle.done()
7. Đổi màu
import turtle

t = turtle.Turtle()

t.color("blue")
t.pensize(3)

for _ in range(3):
    t.forward(100)
    t.left(120)

turtle.done()
8. Di chuyển không vẽ
import turtle

t = turtle.Turtle()

t.penup()
t.goto(-100, 0)

t.pendown()
t.circle(50)

turtle.done()
9. Tọa độ

Màn hình turtle có hệ trục tọa độ giống toán học:

           y
           ↑
           |
(-200,100) | (200,100)
-----------+----------→ x
           |
(-200,-100)| (200,-100)
           |

Ví dụ:

t.goto(100, 50)

Con rùa sẽ đi đến điểm (100, 50).

10. Ứng dụng của turtle

turtle không thường được dùng để phát triển ứng dụng thực tế, nhưng rất hữu ích để:

Học lập trình.
Học vòng lặp (for, while).
Học hàm.
Học lập trình hướng đối tượng.
Hiểu hệ tọa độ và hình học.
Vẽ các hình lặp, hoa văn, fractal (như cây fractal, bông tuyết Koch).

Ví dụ, chỉ với một vòng lặp:

import turtle

t = turtle.Turtle()
t.speed(0)

for i in range(36):
    t.circle(100)
    t.left(10)

turtle.done()

bạn có thể tạo ra một họa tiết hình bông hoa rất đẹp.

Khi nào nên học turtle?
Nên học nếu bạn mới bắt đầu với Python và muốn hiểu trực quan về vòng lặp, hàm và tọa độ.
Không cần tập trung nhiều nếu mục tiêu của bạn là phát triển web, AI/Machine Learning, xử lý dữ liệu hoặc tự động hóa. Trong những lĩnh vực đó, turtle hầu như không được sử dụng. Nó chủ yếu là công cụ học tập và minh họa thuật toán.