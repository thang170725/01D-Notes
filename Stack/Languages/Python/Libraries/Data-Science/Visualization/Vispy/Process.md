- [Create \& Config # Run (tạo \& cấu hình \& Chạy)](#create--config--run-tạo--cấu-hình--chạy)
  - [vispy.app](#vispyapp)
    - [use\_app()](#use_app)
  - [scene](#scene)
    - [.SceneCanvas()](#scenecanvas)
  - [central\_widget](#central_widget)
    - [.add\_view()](#add_view)
      - [.camera](#camera)
  - [GridLines()](#gridlines)
  - [XYZAxis()](#xyzaxis)
    - [ViewBox](#viewbox)
- [Run()](#run)
- [Draw (Vẽ)](#draw-vẽ)
  - [visuals](#visuals)
    - [.Sphere()](#sphere)
- [Location (xử lý vị trí)](#location-xử-lý-vị-trí)
  - [.transform](#transform)
  - [.STTransform (Scale + translate transform)](#sttransform-scale--translate-transform)
  - [TurntableCamera()](#turntablecamera)
  - [Markers()](#markers)
  - [.set\_data()](#set_data)
  - [Text()](#text)
- [color (xử lý màu)](#color-xử-lý-màu)
  - [Color()](#color)
  - [canvas.bgcolor()](#canvasbgcolor)
---
# Create & Config # Run (tạo & cấu hình & Chạy)
## vispy.app
```bash
- Thành phần này quản lý vòng lặp sự kiện (event loop) và hiển thị cửa sổ
- Giống game loop
```
### use_app()
**Ex**
```python
from vispy import app

app.use_app('pyqt5')

import numpy as np
from vispy import scene

app.use_app('pyqt5')
# Vispy cần một cửa sổ để hiển thị. Ở đây nó ép buộc sử dụng PyQt5 (một thư viện giao diện mạnh mẽ) làm nền tảng hiển thị cửa sổ.
```
## scene
```bash
- Để xây dựng cấu trúc cảnh 3D (scene graph), quản lý các đối tượng trực quan (visuals), camera, và các widget.
- Hiểu đơn giản thì đây là hệ thống vẽ 3D.
```
### .SceneCanvas()
```bash
Tạo cửa sổ chính (canvas) để hiển thị cảnh. Nó là lớp cơ sở cho mọi ứng dụng VisPy.
```
**Syn**
```bash
canvas = scene.SceneCanvas(keys='interactive', size=(800, 600), show=True, title=’Demo’)

- size=(W, H): Kích thước cửa sổ.
- keys:
    + 'interactive': Kích hoạt các phím tắt tương tác cơ bản (ví dụ: Escape để đóng, F11 để toàn màn hình).
- bgcolor=‘black’: màu nền.
- show=True: Hiển thị cửa sổ ngay lập tức.
- Title=: thêm tiêu đề cho cửa sổ
```
## central_widget
### .add_view()
```bash
- Thêm một ViewBox vào cửa sổ. ViewBox là "cửa sổ nhìn" vào cảnh 3D, nơi chứa camera và các đối tượng trực quan.
```
**Syn**
```bash
view = canvas.central_widget.add_view()

- Ouput trả về một ViewBox
```
#### .camera
**Ex**
```python
view = canvas.central_widget.add_view()

view.camera = 'turntable' # cho phép xoay bằng chuột
```
## GridLines()
```bash
Thêm lưới toạ độ (Grid)
```
**Syn**
```bash
grid = scene.visuals.GridLines(parent=view.scene)
```
## XYZAxis()
```bash
Vẽ tọa độ trục Oxyz
```
**Syn**
```bash
axis = scene.visuals.XYZAxis(parent=view.scene)

- Trục X → đỏ
- Trục Y → xanh lá
- Trục Z → xanh dương
```
### ViewBox
```bash
Vùng hiển thị (camera nhìn vào đây)
```
# Run()
```bash
- Khởi động vòng lặp ứng dụng chính (main event loop) của VisPy. Đây là hàm chặn (blocking) và cần thiết để cửa sổ hiển thị và tương tác hoạt động.
- Cách dùng: Gọi ở cuối script của bạn.
```
Quit()
Chức năng: Thoát khỏi vòng lặp ứng dụng.
Timer
start
stop
Connect

.set_range()
.azimuth
.elevation
.scene


update
on_draw()
Camera
Camera xác định cách bạn nhìn vào cảnh.

    Thuộc tính/Hàm thường dùng trên ViewBox:

        view.camera = 'turntable': Thiết lập loại camera. Các loại phổ biến:

            'turntable' (hay TurntableCamera): Xoay quanh một điểm trung tâm, thích hợp cho việc xem đối tượng 3D.

            'arcball' (hay ArcballCamera): Tương tự turntable nhưng mượt mà hơn.

            'panzoom' (hay PanZoomCamera): Phổ biến cho trực quan hóa 2D (kéo và thu phóng).

        view.camera.set_range(x_min, x_max, y_min, y_max, z_min, z_max): Thiết lập phạm vi tọa độ của cảnh.
.title
canvas.title = 'One Point'
# Draw (Vẽ)
## visuals
### .Sphere()
```bash
- Bản chất Sphere = một đối tượng hình cầu 3D
- Nó thuộc: scene.visuals.Sphere
- Dùng để 
    + Vẽ hành tinh 🌍
    + Vẽ mặt trời 🌞
    + Vẽ object tròn trong 3D
```
**Syn**
```bash
scene.visuals.Sphere(
    radius=1.0,
    method='latitude',
    parent=view.scene,
    color=(1, 0, 0, 1)
)

- Input
    + radius: bán kính
    + method: cách dựng mesh (thường để 'latitude')
        - latitude: vĩ độ (giống bản đồ trái đất)
            + vĩ độ -> các vòng tròn ngang
            + kinh độ -> các đường dọc
        - ico: bắt đầu từ khối 20 mặt chia nhỏ ra tam giác đều hơn
            + dùng khi cần: mesh đẹp, shading tốt
    + parent: nó nằm trong scene nào
    + color: màu (RGBA)
- Output: Object (<vispy.scene.visuals.sphere.Sphere object at 0x7f8c12345678>)
    + bên trong object chứa:
        - mesh (tam giác hóa hình cầu)
        - shader (GPU)
        - transform
        - state để vẽ
```
# Location (xử lý vị trí)
## .transform
```bash
- transform = cách bạn thay đổi vị trí / kích thước / xoay object
- Hiểu đơn giản: object nằm đâu trong không gian
- Nó làm được gì?
    + Di chuyển (translate)
    + Phóng to / thu nhỏ (scale)
    + Xoay (rotate)
```
## .STTransform (Scale + translate transform)
**Syn**
```bash
sun.transform = scene.transforms.STTransform(
    translate=(x, y, z),
    scale=(sx, sy, sz)
)

- Input
    + sun: đối tượng xuất hiện trong Vispy
    + translate: Di chuyển
    + scale: to, nhỏ
```
**Ex: Di chuyển sang phải**
```python
sun.transform = scene.transforms.STTransform(
    translate=(3, 0, 0)
)
```
**Ex: phóng to**
```python
sun.transform = scene.transforms.STTransform(
    scale=(2, 2, 2)
)
```
## TurntableCamera()
**Syn**
```bash
view.camera = scene.cameras.TurntableCamera(
    fov=45,
    distance=10,
    elevation=10,
    azimuth=0,
    distance=12
)

- fov       : góc nhìn (perspective)
- distance  : Khoảng cách camera
```
## Markers()
```bash
- Vẽ Điểm rời rạc: Hiển thị một tập hợp các điểm được xác định bởi tọa độ (x,y) hoặc (x,y,z).
- Tùy chỉnh Hình dạng: Cho phép định rõ hình dạng của mỗi điểm (ví dụ: tròn, vuông, kim cương, mũi tên, v.v.).
- Tô màu và Kích thước Đa dạng: Bạn có thể gán màu sắc và kích thước khác nhau cho từng điểm riêng lẻ trong cùng một lần gọi hàm, giúp mã hóa thông tin bổ sung.
- Hiệu suất cao: Được tối ưu hóa để vẽ hàng nghìn đến hàng triệu điểm một cách nhanh chóng nhờ sử dụng OpenGL.
```
**Syn**
```bash
single_marker = scene.visuals.Markers(
    parent=view.scene,
    antialias=0 # tắt khử răng cưa
)
```
## .set_data()
**Syn**
```bash
scatter.set_data(pos, edge_color=None, face_color=color, size=10)

- pos: (N, 2) hoặc (N, 3) NumPy array. Bắt buộc. Mảng tọa độ của N điểm.
- Size: Số nguyên hoặc (N,) NumPy array. Kích thước của các điểm (tính bằng pixel). Nếu là một số, tất cả các điểm có cùng kích thước. Nếu là mảng, mỗi điểm có một kích thước riêng.
- Symbol: Chuỗi (string). Hình dạng của các điểm. Ví dụ: 'circle' (mặc định), 'square', 'diamond', 'cross', 'star', 'arrow'.
- face_color	Màu (string, tuple, hoặc (N, 3) / (N, 4) array)Màu bên trong (mặt) của các điểm. Có thể là một màu duy nhất hoặc màu khác nhau cho mỗi điểm.
- edge_color: Màu (string, tuple, hoặc (N, 3) / (N, 4) array). Màu của đường viền (cạnh) của các điểm.
- Scaling: Chuỗi (string). Cách thức kích thước điểm được xử lý. Ví dụ: 'fixed' (kích thước cố định trên màn hình) hoặc 'scene' (kích thước thay đổi theo mức zoom/khoảng cách 3D).
- parent: ViewBox hoặc SceneNode. Nút cha (Node) mà visual này sẽ thuộc về trong scene graph.
```
## Text()
**Syn**
```bash
from vispy import scene

# Tạo đối tượng chữ
text = scene.visuals.Text(
    text='Chào VisPy!', 
    parent=view.scene, 
    color='white', 
    font_size=24, 
    pos=(0, 0, 0) # Vị trí x, y, z
)

- text: 	Chuỗi nội dung bạn muốn hiển thị (hoặc một danh sách các chuỗi).
- Pos:	Tọa độ (x, y) hoặc (x, y, z).
- color:	Màu sắc của chữ.
- font_size:	Kích thước phông chữ (đơn vị point).
- anchor_x:	Căn lề ngang: 'left', 'center', 'right'.
- anchor_y:	Căn lề dọc: 'top', 'center', 'bottom', 'baseline'.
- Rotation:	Góc xoay của chữ (tính bằng độ).
- Face:	Tên phông chữ (ví dụ: 'Arial', 'sans-serif').
```
# color (xử lý màu)
## Color()
```bash
from vispy.color import Color
point_color = Color('red')
```
## canvas.bgcolor()