- [Introduction](#introduction)
- [Create (Nhóm khởi tạo)](#create-nhóm-khởi-tạo)
  - [.scene](#scene)
    - [scene.add()](#sceneadd)
  - [FogExp2](#fogexp2)
  - [WebGLRenderer](#webglrenderer)
  - [DirectionalLight()](#directionallight)
  - [AmbientLight()](#ambientlight)
    - [.position.set()](#positionset)
  - [MeshStandardMaterial](#meshstandardmaterial)
  - [SphereGeometry()](#spheregeometry)
  - [Mesh()](#mesh)
- [Camera (Nhóm xử lý camera)](#camera-nhóm-xử-lý-camera)
  - [PerspectiveCamera](#perspectivecamera)
- [Process (Nhóm xử lý)](#process-nhóm-xử-lý)
  - [setSize](#setsize)
  - [THREE.MathUtils.degToRad()](#threemathutilsdegtorad)
---
# Introduction
```bash
- Three.js là một thư viện giúp bạn tạo và hiển thị đồ họa 3D trên web (trong trình duyệt) bằng WebGL, nhưng dễ dùng hơn rất nhiều so với việc viết WebGL thuần.
```
# Create (Nhóm khởi tạo)
## .scene 
```bash
Tạo ra không gian 3D.
```
### scene.add() 
```bash
- Thêm vào thế giới
- Thêm object (đèn, vật thể…) vào scene
```
**Syn**
```bash
scene.add(object);
```
**Ex**
```python
scene.add(light);

#  Nếu không add → đèn không có tác dụng
```
**Syn**
```bash
const scene = new THREE.Scene();
```
## FogExp2 
```bash
- Tạo hiệu ứng sương mù dày dần theo khoảng cách → vật càng xa càng mờ (giống ngoài đời).
- dùng khi:
    + Làm không gian sâu hơn
    + Tạo cảm giác “cinematic” (như cảnh vũ trụ, núi, sương)
```
**Syn**
```bash
scene.fog = new THREE.FogExp2(color, density);

- color: màu sương
- density: độ dày (0.001 → nhẹ, 0.1 → rất dày)
```
**Ex**
```js
const scene = new THREE.Scene();
scene.fog = new THREE.FogExp2(0xcccccc, 0.02);

// Vật gần → rõ
// Vật xa → mờ dần
```
## WebGLRenderer 
```bash
- Vẽ ra màn hình. bắt buộc có trong three nếu muốn hiển thị ra màn hình.
- Nó là máy vẽ:
    + lấy scene + camera → render thành hình ảnh
```
**Syn**
```bash
const renderer = new THREE.WebGLRenderer(options);
```
**Ex**
```js
const renderer = new THREE.WebGLRenderer({ antialias: true });
document.body.appendChild(renderer.domElement);

//  renderer.domElement = thẻ <canvas> hiển thị 3D
```
## DirectionalLight()
```bash
- ánh sáng như mặt trời
- Dùng để tạo ánh sáng chiếu theo một hướng cố định (giống ánh sáng từ Mặt Trời 🌞)
```
**Syn**
```bash
new THREE.DirectionalLight(color, intensity)

- color: màu ánh sáng
- intensity: độ mạnh (1 = bình thường, >1 = sáng hơn)
```
## AmbientLight() 
```bash
- ánh sáng nền
- Chiếu sáng mọi hướng, làm sáng nhẹ toàn cảnh (tránh bị tối đen)
```
**Syn**
```bash
new THREE.AmbientLight(color, intensity?)
```
**Ex**
```js
scene.add(new THREE.AmbientLight(0x222222));

// Ánh sáng xám nhẹ → làm mềm bóng
```
### .position.set()
```bash
- đặt vị trí ánh sáng
- Dùng để xác định hướng chiếu của ánh sáng
```
**Syn**
```bash
light.position.set(x, y, z);
```
**Ex**
```js
light.position.set(5, 3, 5);

//  Ánh sáng chiếu từ góc trên bên phải
```
## MeshStandardMaterial 
```bash
- vật liệu thật
- Material có ánh sáng thật (phản chiếu, roughness…)
```
**Syn**
```bash
new THREE.MeshStandardMaterial({
  map,
  roughness,
  metalness
});
```
**Ex**
```js
new THREE.MeshStandardMaterial({
  map: createSaturnTexture(),
  roughness: 0.85,
  metalness: 0.05
})

map: texture sao Thổ
roughness: độ nhám (0 → bóng, 1 → lì)
metalness: độ kim loại
```
## SphereGeometry() 
```bash
- hình cầu
- Tạo hình cầu (hành tinh)
```
**Syn**
```python
new THREE.SphereGeometry(radius, widthSegments, heightSegments);
```
**Ex**
```python
new THREE.SphereGeometry(1, 256, 256);

# bán kính = 1
# cực mịn (256 segments)
```
## Mesh() 
```bash
- tạo vật thể 3D
- Kết hợp:
    + Geometry (hình dạng)
    + Material (vật liệu)
```
**Syn**
```bash
new THREE.Mesh(geometry, material);
```
# Camera (Nhóm xử lý camera)
## PerspectiveCamera 
```bash 
- camera phối cảnh
- Giống mắt người:
    + Vật gần → to
    + Vật xa → nhỏ
```
**Syn**
```bash
const camera = new THREE.PerspectiveCamera(fov, aspect, near, far);

# fov: góc nhìn (thường 60–75)
# aspect: tỉ lệ màn hình (width / height)
# near: khoảng gần nhất
# far: khoảng xa nhất
```
**Ex**
```js
const camera = new THREE.PerspectiveCamera(
  75, 
  window.innerWidth / window.innerHeight,
  0.1,
  1000
);

camera.position.z = 5;

// Kết quả: nhìn thấy vật thể 3D theo kiểu “thật”
```
# Process (Nhóm xử lý)
## setSize 
```bash
- chỉnh kích thước màn hình
- Set kích thước cho canvas render
```
**Syn**
```bash
renderer.setSize(width, height);
```
**Ex**
```js
renderer.setSize(window.innerWidth, window.innerHeight);

// Canvas full màn hình
//  Thường dùng thêm resize
// window.addEventListener('resize', () => {
//   renderer.setSize(window.innerWidth, window.innerHeight);
//   camera.aspect = window.innerWidth / window.innerHeight;
//   camera.updateProjectionMatrix();
// });
```
## THREE.MathUtils.degToRad()
```bash
- Đổi độ → radian (Three.js dùng radian)
```
**Syn**
```bash
rad = deg * (Math.PI / 180)
✅ Code của bạn
saturn.rotation.z = THREE.MathUtils.degToRad(60);

👉 Nghiêng 60° → giống sao Thổ thật
```