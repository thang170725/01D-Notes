- [app (Thành phần này quản lý vòng lặp sự kiện (event loop) và hiển thị cửa sổ)](#app-thành-phần-này-quản-lý-vòng-lặp-sự-kiện-event-loop-và-hiển-thị-cửa-sổ)
  - [.use\_app()](#use_app)
- [scene (xây dựng cấu trúc cảnh 3D (scene graph), quản lý các đối tượng trực quan (visuals), camera, và các widget)](#scene-xây-dựng-cấu-trúc-cảnh-3d-scene-graph-quản-lý-các-đối-tượng-trực-quan-visuals-camera-và-các-widget)
  - [.SceneCanvas() (Tạo cửa sổ chính (canvas) để hiển thị cảnh. Nó là lớp cơ sở cho mọi ứng dụng VisPy)](#scenecanvas-tạo-cửa-sổ-chính-canvas-để-hiển-thị-cảnh-nó-là-lớp-cơ-sở-cho-mọi-ứng-dụng-vispy)
    - [.title (Tạo tiêu đề)](#title-tạo-tiêu-đề)
    - [.central\_widget (quản lý bố cục (layout), chứa các widget và ViewBox)](#central_widget-quản-lý-bố-cục-layout-chứa-các-widget-và-viewbox)
    - [.add\_view() (Thêm một ViewBox vào cửa sổ)](#add_view-thêm-một-viewbox-vào-cửa-sổ)
      - [.camera (xác định cách bạn nhìn vào cảnh)](#camera-xác-định-cách-bạn-nhìn-vào-cảnh)
- [visuals](#visuals)
  - [GridLines() (Thêm lưới toạ độ (Grid))](#gridlines-thêm-lưới-toạ-độ-grid)
  - [XYZAxis() (Vẽ tọa độ trục Oxyz)](#xyzaxis-vẽ-tọa-độ-trục-oxyz)
  - [.Sphere() (một đối tượng hình cầu 3D)](#sphere-một-đối-tượng-hình-cầu-3d)
    - [ViewBox](#viewbox)
- [Run() (Khởi động vòng lặp ứng dụng chính (main event loop) của VisPy. Đây là hàm chặn (blocking) và cần thiết để cửa sổ hiển thị và tương tác hoạt động)](#run-khởi-động-vòng-lặp-ứng-dụng-chính-main-event-loop-của-vispy-đây-là-hàm-chặn-blocking-và-cần-thiết-để-cửa-sổ-hiển-thị-và-tương-tác-hoạt-động)
- [Quit() (Thoát khỏi vòng lặp ứng dụng)](#quit-thoát-khỏi-vòng-lặp-ứng-dụng)
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
# app (Thành phần này quản lý vòng lặp sự kiện (event loop) và hiển thị cửa sổ)
## .use_app()
**Ex**
```python
from vispy import app
import numpy as np
from vispy import scene

app.use_app('pyqt5') # Vispy cần một cửa sổ để hiển thị. Ở đây nó ép buộc sử dụng PyQt5 (một thư viện giao diện mạnh mẽ) làm nền tảng hiển thị cửa sổ.
```
# scene (xây dựng cấu trúc cảnh 3D (scene graph), quản lý các đối tượng trực quan (visuals), camera, và các widget)
```bash
Hiểu đơn giản thì đây là hệ thống vẽ 3D.
```
## .SceneCanvas() (Tạo cửa sổ chính (canvas) để hiển thị cảnh. Nó là lớp cơ sở cho mọi ứng dụng VisPy)
**Syn**
```bash
canvas = scene.SceneCanvas(keys='interactive', size=(800, 600), show=True, title=’Demo’)

- Input
  + size=(W, H): Kích thước cửa sổ.
  + keys:
    - 'interactive': Kích hoạt các phím tắt tương tác cơ bản (ví dụ: Escape để đóng, F11 để toàn màn hình).
  + bgcolor=‘black’: màu nền.
  + show=True: Hiển thị cửa sổ ngay lập tức.
  + Title='': thêm tiêu đề cho cửa sổ
```
### .title (Tạo tiêu đề)
### .central_widget (quản lý bố cục (layout), chứa các widget và ViewBox)
### .add_view() (Thêm một ViewBox vào cửa sổ)
```bash
ViewBox là "cửa sổ nhìn" vào cảnh 3D, nơi chứa camera và các đối tượng trực quan.
```
**Syn**
```bash
view = canvas.central_widget.add_view()

- Ouput: trả về một ViewBox
```
#### .camera (xác định cách bạn nhìn vào cảnh)
**Syn**
```bash
view.camera = 'turntable': Thiết lập loại camera. Các loại phổ biến:

- 'turntable' (hay TurntableCamera): Xoay quanh một điểm trung tâm, thích hợp cho việc xem đối tượng 3D.
- 'arcball' (hay ArcballCamera): Tương tự turntable nhưng mượt mà hơn.
- 'panzoom' (hay PanZoomCamera): Phổ biến cho trực quan hóa 2D (kéo và thu phóng).
```
**Ex: Tạo ra không gian 3d**
```python
from vispy import app, scene

app.use_app('pyqt5')

canvas = scene.SceneCanvas(
    keys='interactive',
    size=(800, 600),
    show=True,
    title="TEST GRAPHIC 3D"
)

view = canvas.central_widget.add_view()
view.camera = "turntable" # tạo không gian 3d

grid = scene.visuals.GridLines(parent=view.scene) # tạo lưới

if __name__ == '__main__':
    app.run()
```
# visuals
## GridLines() (Thêm lưới toạ độ (Grid))
**Syn**
```bash
grid = scene.visuals.GridLines(parent=view.scene)
```
**Ex**
```python
from vispy import app
from vispy import scene

app.use_app('pyqt5')

canvas = scene.SceneCanvas(
    keys='interactive',
    size=(800, 600),
    show=True,
    title="TEST GRAPHIC 3D"
)

view = canvas.central_widget.add_view()

grid = scene.visuals.GridLines(parent=view.scene)

if __name__ == '__main__':
    app.run()

# chương trình sẽ mở một cửa sổ có lưới 2d
```
## XYZAxis() (Vẽ tọa độ trục Oxyz)
**Syn**
```bash
axis = scene.visuals.XYZAxis(parent=view.scene)

- Trục X → đỏ
- Trục Y → xanh lá
- Trục Z → xanh dương
```
**Ex: vẽ trục tọa độ Oxyz**
```python
from vispy import app, scene

app.use_app('pyqt5')

canvas = scene.SceneCanvas(
    keys='interactive',
    size=(800, 600),
    show=True,
    title="TEST GRAPHIC 3D"
)

view = canvas.central_widget.add_view()
view.camera = "turntable"

grid = scene.visuals.GridLines(parent=view.scene)
axis = scene.visuals.XYZAxis(parent=view.scene)

if __name__ == '__main__':
    app.run()
```
## .Sphere() (một đối tượng hình cầu 3D)
```bash
Nó thuộc: scene.visuals.Sphere

Dùng để:
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
### ViewBox
```bash
Vùng hiển thị (camera nhìn vào đây)
```
# Run() (Khởi động vòng lặp ứng dụng chính (main event loop) của VisPy. Đây là hàm chặn (blocking) và cần thiết để cửa sổ hiển thị và tương tác hoạt động)
```bash
Cách dùng: Gọi ở cuối script của bạn.
```
# Quit() (Thoát khỏi vòng lặp ứng dụng)
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


canvas.title = 'One Point'
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
