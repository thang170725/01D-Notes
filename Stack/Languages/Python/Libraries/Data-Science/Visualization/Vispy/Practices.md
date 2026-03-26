- [Vẽ 1 điểm trong không gian 3d](#vẽ-1-điểm-trong-không-gian-3d)
- [Thêm hiệu ứng dao động và đập cho 1 điểm trong không gian 3 chiều](#thêm-hiệu-ứng-dao-động-và-đập-cho-1-điểm-trong-không-gian-3-chiều)
- [Hình trái tim](#hình-trái-tim)
- [Cây thông noel](#cây-thông-noel)
# Vẽ 1 điểm trong không gian 3d
```python
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
```
# Thêm hiệu ứng dao động và đập cho 1 điểm trong không gian 3 chiều
```python
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
```
# Hình trái tim
```python
from vispy import app, scene
import numpy as np

# =========================
# FORCE BACKEND
# =========================
app.use_app('pyqt5')


class DustHeart:
    def __init__(self):
        self.t = 0.0

    # =========================
    # BIO HEARTBEAT (STRONG)
    # =========================
    def heartbeat(self, t):
        phase = (t % (2*np.pi)) / (2*np.pi)

        if phase < 0.12:
            return phase / 0.12            # very fast squeeze
        elif phase < 0.20:
            return 1.3                     # strong peak
        else:
            x = (phase - 0.20) / 0.80
            return 1.3 * np.exp(-4.0 * x)  # long relax

    # =========================
    # GENERATE HEART PARTICLES
    # =========================
    def generate_heart(self, N=1_200_000, thickness=0.012):
        x = np.random.uniform(-1.4, 1.4, N)
        y = np.random.uniform(-1.3, 1.4, N)
        z = np.random.uniform(-1.3, 1.4, N)
        # trước F
        y += np.random.normal(0, 0.0015, size=y.shape)
        A = 1.0
        Bx = 1.05
        By = 1.35
        Bz = 0.85

        F = (
            (Bx*x**2 + (49/9)*By*y**2 + Bz*z**2 - A)**3
            - 0.85*x**2 * z**3
            - (70/9)*y**2 * z**3
        )

        Fx = 6*x*(x**2 + (49/9)*y**2 + z**2 - 1)**2 - 2*x*z**3
        Fy = (98/9)*y*(x**2 + (49/9)*y**2 + z**2 - 1)**2 - (160/9)*y*z**3
        Fz = (
            6*z*(x**2 + (49/9)*y**2 + z**2 - 1)**2
            - 3*x**2*z**2
            - (80/3)*y**2*z**2
        )

        grad = np.sqrt(Fx**2 + Fy**2 + Fz**2) + 1e-6
        dist = np.abs(F) / grad
        curvature_boost = 1.0 + 0.8 * np.abs(Fz) / grad
        y_soft = 1.0 + 0.8 * np.exp(-np.abs(y) * 3.5)
        keep = dist < thickness * curvature_boost * y_soft



        points = np.column_stack((x[keep], y[keep], z[keep])) * 4.6
        # sau khi tạo points
        y_center = (points[:,1].max() + points[:,1].min()) * 0.5
        points[:,1] -= y_center
        points[:,1] += 0.35


        dist = dist[keep]

        # ===== radial info =====
        r = np.linalg.norm(points, axis=1)
        r_norm = r / r.max()

        # ===== colors (dusty red) =====
        colors = np.zeros((len(points), 4), dtype=np.float32)
        colors[:, 0] = 1.0
        colors[:, 1] = 0.18
        colors[:, 2] = 0.25
        colors[:, 3] = np.clip(1 - dist / thickness, 0.35, 0.9)

        # ===== VERY SMALL PARTICLES =====
        sizes = np.clip(
            0.35 + 0.6 * (1 - r_norm),
            0.2,
            0.8
        ).astype(np.float32)

        print("Particles:", len(points))
        return (
            points.astype(np.float32),
            colors,
            sizes,
            r_norm.astype(np.float32)
        )

    # =========================
    # SCENE SETUP
    # =========================
    def setup(self, points, colors, sizes):
        self.canvas = scene.SceneCanvas(
            bgcolor='black',
            show=True,
            fullscreen=True,
            title='Dust Heart'
        )

        self.view = self.canvas.central_widget.add_view()
        self.view.camera = 'turntable'
        self.view.camera.set_range(x=(-6, 6), y=(-6, 6), z=(-6, 6))
        self.view.camera.azimuth = 0
        self.view.camera.elevation = 0

        self.scatter = scene.visuals.Markers(
            parent=self.view.scene,
            antialias=0
        )

        self.scatter.set_data(
            points,
            face_color=colors,
            size=sizes,
            edge_width=0
        )

        self.canvas.events.key_press.connect(self.on_key_press)


    # =========================
    # ARTISTIC ANIMATION
    # =========================
    def update(self, event):
        self.t += 0.030
        b = self.heartbeat(self.t)

        # ---- STRONG RADIAL WAVE ----
        wave = np.sin(10 * self.r_norm - self.t * 3.0)
        wave = np.clip(wave, 0, 1)

        # ---- AMPLITUDE (WIDE & STRONG) ----
        amp = (1.2 - self.r_norm)**2.2
        scale = 1.0 + 0.28 * b * amp * (0.6 + 0.8 * wave)

        # ---- MICRO DUST MOTION ----
        dust = np.random.normal(0, 0.012, self.points.shape)

        new_pos = self.points * scale[:, None] + dust

        # ---- PARTICLE BURST ON PEAK ----
        if b > 1.1:
            pick = np.random.choice(
                self.edge_ids,
                size=len(self.edge_ids)//35,
                replace=False
            )
            new_pos[pick] += np.random.normal(0, 0.22, (len(pick), 3))

        self.scatter.set_data(
            new_pos,
            face_color=self.colors,
            size=2,  #self.sizes,
            edge_width=0
        )

    # =========================
    # RUN
    # =========================
    def run(self):
        (
            self.points,
            self.colors,
            self.sizes,
            self.r_norm
        ) = self.generate_heart(
            N=1_500_000,
            thickness=0.015
        )

        # edge particles
        self.edge_ids = np.where(self.r_norm > 0.88)[0]

        self.setup(self.points, self.colors, self.sizes)

        timer = app.Timer(interval=1/60, connect=self.update, start=True)
        app.run()

    def on_key_press(self, event):
        if event.key in ('Escape', 'Q'):
            print("Exit requested")
            self.canvas.close()
            app.quit()

if __name__ == '__main__':
    DustHeart().run()
```
# Cây thông noel
```python
from vispy import app, scene
from vispy.scene import visuals
import numpy as np
from PIL import Image
import os

app.use_app('pyqt5')

class NeonLoveTree:
    def __init__(self, image_path='nguoi_yeu.jpg'):
        self.t = 0.0
        self.image_path = image_path
        self.phase = 0  # 0: tree, 1: transition, 2: galaxy

    def generate_galaxy(self, N=50000):
        """Tạo dải ngân hà sắc nét"""
        angles = np.random.uniform(0, 4*np.pi, N)
        
        radii = np.zeros(N)
        for i in range(N):
            if np.random.random() < 0.3:
                radii[i] = np.random.uniform(0, 1.5)
            elif np.random.random() < 0.6:
                radii[i] = np.random.uniform(1.5, 4)
            else:
                radii[i] = np.random.uniform(4, 8)
        
        spiral_offset = 0.8 * angles
        noise_factor = 0.1 + 0.2 * (radii / 8.0)
        
        x = radii * np.cos(angles + spiral_offset) + np.random.normal(0, noise_factor, N)
        z = radii * np.sin(angles + spiral_offset) + np.random.normal(0, noise_factor, N)
        y = np.random.normal(0, 0.2, N) * (1 + radii/10)
        
        galaxy_points = np.column_stack((x, y, z))
        
        colors = np.zeros((N, 4))
        dist = np.sqrt(x**2 + z**2)
        
        for i in range(N):
            if dist[i] < 1.5:
                colors[i] = [1.0, 1.0, 0.95, 1.0]
            elif dist[i] < 4:
                colors[i] = [0.4, 0.6, 1.0, 0.9]
            else:
                colors[i] = [0.9, 0.5, 0.8, 0.7]
        
        sizes = np.zeros(N)
        for i in range(N):
            if dist[i] < 1.5:
                sizes[i] = np.random.uniform(3, 6)
            elif dist[i] < 4:
                sizes[i] = np.random.uniform(2, 4)
            else:
                sizes[i] = np.random.uniform(1, 2.5)
        
        return galaxy_points, colors, sizes

    def generate_tree(self):
        # 1. Thân cây - THẲNG ĐỨNG theo trục Y
        N_tree = 30_000
        i = np.arange(N_tree)
        h_raw = i / N_tree
        y = 10.0 * h_raw - 5.0  # Y là chiều cao từ -5 đến 5
        
        # Bán kính giảm dần theo chiều cao
        base_radius = 3.5 * (1.0 - h_raw)**0.8
        roughness = np.random.normal(0, 0.4, N_tree) * (1.1 - h_raw)
        r = base_radius + roughness
        
        theta = i * 0.2
        x = r * np.cos(theta) + np.random.normal(0, 0.1, N_tree)
        z = r * np.sin(theta) + np.random.normal(0, 0.1, N_tree)
        
        tree_points = np.column_stack((x, y, z))
        tree_colors = np.random.uniform(0.3, 1.0, (N_tree, 3))
        tree_colors = np.hstack([tree_colors, np.full((N_tree, 1), 0.6)])

        # 2. Quả cầu - dọc theo chiều cao Y
        N_ornaments = 200
        orn_y = np.random.uniform(-4, 4, N_ornaments)  # Y là chiều cao
        h_norm = (orn_y + 5) / 10.0
        orn_radius = 3.0 * (1.0 - h_norm)**0.8
        
        orn_theta = np.random.uniform(0, 2*np.pi, N_ornaments)
        orn_r = orn_radius * np.random.uniform(0.7, 1.0, N_ornaments)
        
        orn_x = orn_r * np.cos(orn_theta)
        orn_z = orn_r * np.sin(orn_theta)
        
        ornament_points = np.column_stack((orn_x, orn_y, orn_z))
        
        color_palette = np.array([
            [1.0, 0.0, 0.0, 1.0],
            [1.0, 0.8, 0.0, 1.0],
            [0.0, 0.5, 1.0, 1.0],
            [0.8, 0.0, 1.0, 1.0],
            [1.0, 0.2, 0.6, 1.0],
            [0.0, 1.0, 0.5, 1.0],
        ])
        color_indices = np.random.choice(len(color_palette), N_ornaments)
        ornament_colors = color_palette[color_indices]

        # 3. Dây đèn - xoắn dọc theo Y
        N_lights = 500
        light_y = np.linspace(-4.5, 4.5, N_lights)  # Y là chiều cao
        h_norm_lights = (light_y + 5) / 10.0
        light_radius = 3.2 * (1.0 - h_norm_lights)**0.8
        
        light_theta = np.linspace(0, 20*np.pi, N_lights)
        light_x = light_radius * np.cos(light_theta)
        light_z = light_radius * np.sin(light_theta)
        
        light_points = np.column_stack((light_x, light_y, light_z))
        light_colors = np.full((N_lights, 4), [1.0, 1.0, 0.6, 1.0])

        # 4. Ngôi sao đỉnh - ở trên cao trục Y
        N_star = 1500
        s_r = np.random.uniform(0, 0.5, N_star)
        s_theta = np.random.uniform(0, 2*np.pi, N_star)
        s_phi = np.random.uniform(0, np.pi, N_star)
        sx = s_r * np.sin(s_phi) * np.cos(s_theta)
        sy = 5.2 + s_r * np.cos(s_phi)  # Y cao ở đỉnh
        sz = s_r * np.sin(s_phi) * np.sin(s_theta)
        
        burst = np.random.choice(N_star, N_star//4)
        sx[burst] *= 3; sy[burst] = 5.2 + (sy[burst]-5.2)*3; sz[burst] *= 3
        
        star_points = np.column_stack((sx, sy, sz))
        star_colors = np.full((N_star, 4), [1.0, 0.9, 0.0, 1.0])

        # Gộp các phần xoay
        self.rotating_pts = np.vstack([
            tree_points, ornament_points, light_points, star_points
        ]).astype(np.float32)
        
        self.rotating_cols = np.vstack([
            tree_colors, ornament_colors, light_colors, star_colors
        ]).astype(np.float32)
        
        tree_sizes = np.random.uniform(1, 2.5, len(tree_points))
        orn_sizes = np.random.uniform(8, 15, len(ornament_points))
        light_sizes = np.random.uniform(4, 7, len(light_points))
        star_sizes = np.random.uniform(2, 4, len(star_points))
        
        self.rotating_sizes = np.hstack([
            tree_sizes, orn_sizes, light_sizes, star_sizes
        ]).astype(np.float32)
        
        # Galaxy
        galaxy_points, galaxy_colors, galaxy_sizes = self.generate_galaxy()
        self.galaxy_pts = galaxy_points.astype(np.float32)
        self.galaxy_cols = galaxy_colors.astype(np.float32)
        self.galaxy_sizes = galaxy_sizes.astype(np.float32)
        
        # Indices
        self.light_start = len(tree_points) + len(ornament_points)
        self.light_end = self.light_start + len(light_points)

    def setup(self):
        self.canvas = scene.SceneCanvas(bgcolor='black', show=True, fullscreen=True)
        self.view = self.canvas.central_widget.add_view()
        self.view.camera = 'turntable'
        self.view.camera.distance = 15
        
        # Scatter cho particles
        self.scatter = scene.visuals.Markers(parent=self.view.scene, antialias=0)
        self.scatter.set_data(self.rotating_pts, face_color=self.rotating_cols, size=self.rotating_sizes)
        
        # Text CHRISTMAS - Sharp vector text
        self.text = visuals.Text(
            text="CHRISTMAS",
            pos=(0, -6.5, 0),
            color=(1.0, 0.85, 0.0, 1.0),
            font_size=120,
            bold=True,
            anchor_x='center',
            anchor_y='middle',
            parent=self.view.scene
        )
        
        self.canvas.events.key_press.connect(self.on_key_press)

    def update(self, event):
        self.t += 0.02
        
        # Phase 0: Christmas tree
        if self.phase == 0:
            if self.t < 30:
                # Xoay quanh trục Y (vertical)
                angle = 0.01
                c, s = np.cos(angle), np.sin(angle)
                
                new_x = self.rotating_pts[:, 0] * c + self.rotating_pts[:, 2] * s
                new_z = -self.rotating_pts[:, 0] * s + self.rotating_pts[:, 2] * c
                self.rotating_pts[:, 0] = new_x
                self.rotating_pts[:, 2] = new_z

                # Đèn nhấp nháy
                twinkle = 0.5 + 0.5 * np.sin(self.t * 8)
                self.rotating_cols[self.light_start:self.light_end, 3] = twinkle
                
                self.scatter.set_data(self.rotating_pts, face_color=self.rotating_cols, size=self.rotating_sizes)
            else:
                self.phase = 1
                self.transition_start = self.t
        
        # Phase 1: Transition
        elif self.phase == 1:
            progress = (self.t - self.transition_start) / 5.0
            
            if progress < 1.0:
                # Fade tree
                n_rot = len(self.rotating_pts)
                self.rotating_pts = self.rotating_pts * (1 - progress) + self.galaxy_pts[:n_rot] * progress
                self.rotating_cols[:, 3] *= (1 - progress)
                
                # Fade text
                self.text.color = (1.0, 0.85, 0.0, 1.0 - progress)
                
                self.scatter.set_data(self.rotating_pts, face_color=self.rotating_cols, size=self.rotating_sizes)
            else:
                # Hide text
                self.text.parent = None
                
                # Switch to galaxy
                self.scatter.set_data(self.galaxy_pts, face_color=self.galaxy_cols, size=self.galaxy_sizes)
                self.phase = 2
                self.current_pts = self.galaxy_pts.copy()
        
        # Phase 2: Galaxy
        elif self.phase == 2:
            # Xoay quanh trục Y (vertical)
            angle = 0.005
            c, s = np.cos(angle), np.sin(angle)
            
            new_x = self.current_pts[:, 0] * c + self.current_pts[:, 2] * s
            new_z = -self.current_pts[:, 0] * s + self.current_pts[:, 2] * c
            self.current_pts[:, 0] = new_x
            self.current_pts[:, 2] = new_z
            
            self.scatter.set_data(self.current_pts, face_color=self.galaxy_cols, size=self.galaxy_sizes)

    def run(self):
        self.generate_tree()
        self.setup()
        self.timer = app.Timer(interval=1/60, connect=self.update, start=True)
        app.run()

    def on_key_press(self, event):
        if event.key in ('Escape', 'Q'):
            self.canvas.close()
            app.quit()

if __name__ == '__main__':
    NeonLoveTree(image_path='nguoi_yeu.jpg').run()
```