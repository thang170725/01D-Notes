Seaborn
Là một thư viện vẽ biểu đồ mạnh mẽ trong Python, được xây dựng trên nền tảng Matplotlib, và tích hợp rất tốt với Pandas. Kế thừa matplotlib
pip install seaborn
So sánh seaborn và matplotlib:

Matplotlib
Seaborn
Cấp độ
Thấp (Low-level)
Cao (High-level, built on Matplotlib)
Cú pháp
Tự kiểm soát từng chi tiết (trục, màu, tick...)
Dễ viết, đẹp sẵn, hiểu dữ liệu dạng bảng
Dữ liệu truyền vào
Mảng, list, numpy...
DataFrame (pandas) là chính
Biểu đồ phù hợp
Biểu đồ cơ bản, tùy biến sâu (line, scatter, bar, hist...)
Biểu đồ thống kê, phân tích quan hệ (countplot, boxplot, pairplot, heatmap…)
Tốc độ viết code
Nhiều dòng hơn, linh hoạt hơn
Ngắn gọn, tự động nhận dạng biến
Phong cách mặc định
Khá “thô” nếu không chỉnh
Mặc định rất đẹp và hiện đại
Countplot()
Cú pháp:
sns.countplot(x='intent', data=self.df, palette='Set2', ax=ax)

Violinplot()
Lmplot()
Histplot()
Boxplot()
 sns.boxplot(x="intent", y="length", data=self.df, ax=ax)

Scatterplot()
Lineplot()
Heatmap()
Pairplot()
Barplot()
Vispy
    • Một thư viện mạnh mẽ cho việc trực quan hóa dữ liệu 2D và 3D hiệu suất cao bằng Python, sử dụng OpenGL. 
    • Một thư viện đồ họa hiệu năng cao. Nó không dùng CPU để vẽ từng điểm, mà gửi toàn bộ dữ liệu xuống Card đồ họa (GPU) để xử lý song song.
App
Thành phần này quản lý vòng lặp sự kiện (event loop) và hiển thị cửa sổ
use_app()
from vispy import app
app.use_app('pyqt5')
import numpy as np
from vispy import scene
app.use_app('pyqt5'): Vispy cần một cửa sổ để hiển thị. Ở đây nó ép buộc sử dụng PyQt5 (một thư viện giao diện mạnh mẽ) làm nền tảng hiển thị cửa sổ.
Run()
    • Chức năng: Khởi động vòng lặp ứng dụng chính (main event loop) của VisPy. Đây là hàm chặn (blocking) và cần thiết để cửa sổ hiển thị và tương tác hoạt động.
    • Cách dùng: Gọi ở cuối script của bạn.
Quit()
Chức năng: Thoát khỏi vòng lặp ứng dụng.
Timer
start
stop
Connect
Scene
Thành phần này xây dựng cấu trúc cảnh 3D (scene graph), quản lý các đối tượng trực quan (visuals), camera, và các widget.
SceneCanvas()
Tạo cửa sổ chính (canvas) để hiển thị cảnh. Nó là lớp cơ sở cho mọi ứng dụng VisPy.
Cú pháp:
canvas = scene.SceneCanvas(keys='interactive', size=(800, 600), show=True, title=’Demo’)
    • size=(W, H): Kích thước cửa sổ.
    • keys='interactive': Kích hoạt các phím tắt tương tác cơ bản (ví dụ: Escape để đóng, F11 để toàn màn hình).
    • bgcolor=‘black’: màu nền.
    • show=True: Hiển thị cửa sổ ngay lập tức.
    • Title=: thêm tiêu đề cho cửa sổ

central_widget

add_view()
Thêm một ViewBox vào cửa sổ. ViewBox là "cửa sổ nhìn" vào cảnh 3D, nơi chứa camera và các đối tượng trực quan.
Cú pháp:
view = canvas.central_widget.add_view()
camera
view.camera = 'turntable'
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

Visuals
Markers()
    • Vẽ Điểm rời rạc: Hiển thị một tập hợp các điểm được xác định bởi tọa độ (x,y) hoặc (x,y,z).
    • Tùy chỉnh Hình dạng: Cho phép định rõ hình dạng của mỗi điểm (ví dụ: tròn, vuông, kim cương, mũi tên, v.v.).
    • Tô màu và Kích thước Đa dạng: Bạn có thể gán màu sắc và kích thước khác nhau cho từng điểm riêng lẻ trong cùng một lần gọi hàm, giúp mã hóa thông tin bổ sung.
    • Hiệu suất cao: Được tối ưu hóa để vẽ hàng nghìn đến hàng triệu điểm một cách nhanh chóng nhờ sử dụng OpenGL.
Cú pháp:
single_marker = scene.visuals.Markers(
    parent=view.scene,
    antialias=0 # tắt khử răng cưa
)

.set_data()
scatter.set_data(pos, edge_color=None, face_color=color, size=10)
    • pos: (N, 2) hoặc (N, 3) NumPy array. Bắt buộc. Mảng tọa độ của N điểm.
    • Size: Số nguyên hoặc (N,) NumPy array. Kích thước của các điểm (tính bằng pixel). Nếu là một số, tất cả các điểm có cùng kích thước. Nếu là mảng, mỗi điểm có một kích thước riêng.
    • Symbol: Chuỗi (string). Hình dạng của các điểm. Ví dụ: 'circle' (mặc định), 'square', 'diamond', 'cross', 'star', 'arrow'.
    • face_color	Màu (string, tuple, hoặc (N, 3) / (N, 4) array)Màu bên trong (mặt) của các điểm. Có thể là một màu duy nhất hoặc màu khác nhau cho mỗi điểm.
    • edge_color: Màu (string, tuple, hoặc (N, 3) / (N, 4) array). Màu của đường viền (cạnh) của các điểm.
    • Scaling: Chuỗi (string). Cách thức kích thước điểm được xử lý. Ví dụ: 'fixed' (kích thước cố định trên màn hình) hoặc 'scene' (kích thước thay đổi theo mức zoom/khoảng cách 3D).
    • parent: ViewBox hoặc SceneNode. Nút cha (Node) mà visual này sẽ thuộc về trong scene graph.
GridLines()
Thêm lưới toạ độ (Grid)
Cú pháp:
scene.visuals.GridLines(parent=view.scene)
Text()
Cú pháp:
from vispy import scene

# Tạo đối tượng chữ
text = scene.visuals.Text(
    text='Chào VisPy!', 
    parent=view.scene, 
    color='white', 
    font_size=24, 
    pos=(0, 0, 0) # Vị trí x, y, z
)
    • text: 	Chuỗi nội dung bạn muốn hiển thị (hoặc một danh sách các chuỗi).
    • Pos:	Tọa độ (x, y) hoặc (x, y, z).
    • color:	Màu sắc của chữ.
    • font_size:	Kích thước phông chữ (đơn vị point).
    • anchor_x:	Căn lề ngang: 'left', 'center', 'right'.
    • anchor_y:	Căn lề dọc: 'top', 'center', 'bottom', 'baseline'.
    • Rotation:	Góc xoay của chữ (tính bằng độ).
    • Face:	Tên phông chữ (ví dụ: 'Arial', 'sans-serif').

color
Color()
from vispy.color import Color
point_color = Color('red')
Cameras
TurntableCamera()
view.camera = scene.cameras.TurntableCamera(
    elevation=10,
    azimuth=0,
    distance=12
)
Bài tập
Vẽ 1 điểm trong không gian 3d
import numpy as np
from vispy import app
app.use_app('pyqt5')
from vispy import scene
from vispy.color import Color

# tạo điểm
point_pos = np.array([[0.0,0.0,0.0]])
point_color = Color('red')
point_size = 10

# tạo cửa sổ hiển thị
canvas = scene.SceneCanvas(
    keys='interactive',
    size=(600, 600),
    show=True
)
canvas.title = 'One Point'

# thêm mọt view box
view = canvas.central_widget.add_view()

# thiết lập camera 'turntable' cho phép xoay và zoom 3d
view.camera = 'turntable'

# khởi tạo đối tượng markers
single_marker = scene.visuals.Markers(
    parent=view.scene,
    antialias=0 # tắt khử răng cưa
)

# gán dữ liệu (chỉ một hàng trong pos)
single_marker.set_data(
    point_pos,
    face_color=point_color,
    size=point_size,
    symbol='o', # hình tròn
    edge_color='white' # viền trắng
)

# thêm lưới tọa độ
scene.visuals.GridLines(parent=view.scene)

# Thiết lập phạm vi nhìn
view.camera.set_range(x=(-1, 1), y=(-1, 1), z=(-1, 1))

if __name__ == '__main__':
    app.run()
Thêm hiệu ứng dao động và đập cho 1 điểm trong không gian 3 chiều
import numpy as np
from vispy import app, scene
from vispy.color import Color

# =========================
# FORCE BACKEND
# =========================
app.use_app('pyqt5')

# =========================
# DỮ LIỆU BAN ĐẦU
# =========================
base_pos = np.array([[0.0, 0.0, 0.0]], dtype=np.float32)
point_color = Color('red')
base_size = 10

# =========================
# TẠO CỬA SỔ
# =========================
canvas = scene.SceneCanvas(
    keys='interactive',
    size=(600, 600),
    show=True,
    title='Animated 3D Point'
)

view = canvas.central_widget.add_view()
view.camera = 'turntable'
view.camera.set_range(x=(-1, 1), y=(-1, 1), z=(-1, 1))

# =========================
# MARKER
# =========================
marker = scene.visuals.Markers(
    parent=view.scene,
    antialias=0
)

marker.set_data(
    base_pos,
    face_color=point_color,
    size=base_size,
    symbol='o',
    edge_color='white'
)

# lưới tọa độ
scene.visuals.GridLines(parent=view.scene)

# =========================
# ANIMATION
# =========================
t = 0.0

def update(event):
    global t
    t += 0.05

    # 1️⃣ ĐẬP (thay đổi size)
    size = base_size + 4 * np.sin(t)

    # 2️⃣ DAO ĐỘNG 3D NHẸ
    offset = 0.15
    pos = np.array([[
        offset * np.sin(t),
        offset * np.cos(t * 1.3),
        offset * np.sin(t * 0.7)
    ]], dtype=np.float32)

    marker.set_data(
        pos,
        face_color=point_color,
        size=size,
        symbol='o',
        edge_color='white'
    )

    # 3️⃣ XOAY CAMERA CHẬM
    view.camera.azimuth += 0.2
    view.camera.elevation = 30 + 10 * np.sin(t * 0.3)

# timer ~60 FPS
timer = app.Timer(interval=1/60, connect=update, start=True)

if __name__ == '__main__':
    app.run()
