- [Transform (làm ảnh mới khác ảnh gốc)](#transform-làm-ảnh-mới-khác-ảnh-gốc)
  - [\[\] (Crop ảnh)](#-crop-ảnh)
  - [getRotationMatrix2d()](#getrotationmatrix2d)
  - [.warpAffine()](#warpaffine)
  - [cv2.findHomography()](#cv2findhomography)
  - [cv2.warpPerspective()](#cv2warpperspective)
  - [GetPerspectiveTransform()](#getperspectivetransform)
  - [PerspectiveTransform()](#perspectivetransform)
  - [.resize()](#resize)
  - [.resizeWindow()](#resizewindow)
- [Display (cung cấp thông tin)](#display-cung-cấp-thông-tin)
  - [.shape](#shape)
  - [.get()](#get)
- [Event (bắt sự kiên)](#event-bắt-sự-kiên)
  - [EVENT\_LBUTTONDOWN](#event_lbuttondown)
  - [cv2.EVENT\_LBUTTONUP](#cv2event_lbuttonup)
  - [cv2.EVENT\_MOUSEMOVE](#cv2event_mousemove)
  - [cv2.EVENT\_RBUTTONDOWN](#cv2event_rbuttondown)
  - [.SetMouseCallback()](#setmousecallback)
- [Shape / Geometry (Hình học)](#shape--geometry-hình-học)
  - [MinAreaRect()](#minarearect)
- [Blur Process (các thao tác để làm mờ)](#blur-process-các-thao-tác-để-làm-mờ)
  - [GaussianBlur()](#gaussianblur)
  - [MedianBlur()](#medianblur)
- [Edge Process (xử lý cạnh)](#edge-process-xử-lý-cạnh)
  - [Canny()](#canny)
- [Color Process (Xử lý màu sắc)](#color-process-xử-lý-màu-sắc)
  - [.cvtColor()](#cvtcolor)
  - [divide()](#divide)
- [Filter](#filter)
  - [filter2D()](#filter2d)
  - [bilateralFilter()](#bilateralfilter)
- [ROI Process](#roi-process)
  - [PointPolygonTest()](#pointpolygontest)
  - [InRange()](#inrange)
  - [FindContours()](#findcontours)
- [BoundingRect()](#boundingrect)
---
# Transform (làm ảnh mới khác ảnh gốc)
## [] (Crop ảnh)
**Syn**
```bash
cropped = image[y1:y2, x1:x2]

- x1, y1: tọa độ góc trên bên trái
- x2, y2: tọa độ góc dưới bên phải
- image: ảnh gốc (ma trận numpy)
```
**Ex**
```python
import cv2

# Đọc ảnh
img = cv2.imread("image.jpg")

# Kiểm tra kích thước ảnh
print(img.shape)  # (height, width, channels)

# Crop vùng từ (x=100, y=50) đến (x=300, y=200)
cropped = img[50:200, 100:300]

# Hiển thị
cv2.imshow("Original", img)
cv2.imshow("Cropped", cropped)

cv2.waitKey(0)
cv2.destroyAllWindows()
```
## getRotationMatrix2d()
```bash
- Xoay góc bất kỳ bằng getRotationMatrix2D() + warpAffine()
```
**Syn**
```bash
M = cv2.getRotationMatrix2D(center, angle, scale)
dst = cv2.warpAffine(src, M, (width, height))

- center: tâm xoay (x, y)
- angle: góc xoay (độ, dương = ngược chiều kim đồng hồ)
- scale: tỉ lệ (1.0 = giữ nguyên)
```
**Ex1: demo xoay 45°**
```python
import cv2

img = cv2.imread("image.jpg")
(h, w) = img.shape[:2]

center = (w // 2, h // 2)

M = cv2.getRotationMatrix2D(center, 45, 1.0)
rotated = cv2.warpAffine(img, M, (w, h))

cv2.imshow("Original", img)
cv2.imshow("Rotate 45 degrees", rotated)

cv2.waitKey(0)
cv2.destroyAllWindows()

#  Lưu ý: Ảnh có thể bị cắt góc nếu xoay nhiều
# angle > 0 → xoay ngược chiều kim đồng hồ
```
**Ex2: Xoay mà không bị cắt ảnh**
```python
import cv2
import numpy as np

img = cv2.imread("image.jpg")
(h, w) = img.shape[:2]

center = (w // 2, h // 2)
angle = 45

M = cv2.getRotationMatrix2D(center, angle, 1.0)

cos = np.abs(M[0, 0])
sin = np.abs(M[0, 1])

new_w = int((h * sin) + (w * cos))
new_h = int((h * cos) + (w * sin))

M[0, 2] += (new_w / 2) - center[0]
M[1, 2] += (new_h / 2) - center[1]

rotated = cv2.warpAffine(img, M, (new_w, new_h))

cv2.imshow("Rotate no crop", rotated)
cv2.waitKey(0)
cv2.destroyAllWindows()
```
## .warpAffine() 
```bash
- Để áp dụng ma trận Affine lên ảnh
- Input: ảnh + ma trận
- Output: ảnh mới đã biến đổi
```
**Syn**
```bash
dst = cv2.warpAffine(
    src,        # ảnh đầu vào
    M,          # ma trận Affine (2x3)
    dsize,      # (width, height)
    flags=cv2.INTER_LINEAR,
    borderMode=cv2.BORDER_CONSTANT,
    borderValue=0
)

- src               : Ảnh gốc
- M                 : Ma trận Affine 2×3:
    [a b tx]
    [c d ty]
- dsize             : (width, height)
- flags (nội suy)
    + INTER_LINEAR	: mặc định, tốt
    + INTER_NEAREST	: nhanh, răng cưa
    + INTER_CUBIC	: đẹp, chậm
- borderMode        : Xử lý vùng ngoài ảnh
    + BORDER_CONSTANT   : tô màu
    + BORDER_REFLECT	: phản chiếu
    + BORDER_REPLICATE	: lặp pixel biên
    + borderValue       : Màu nền khi dùng BORDER_CONSTANT
- borderValue=(255,255,255)  # nền trắng
```
## cv2.findHomography()
```bash
- Tìm ma trận Homography (3×3) biến đổi tập điểm src → dst
- Dùng khi:
    + Sửa méo ảnh
    + Bird-eye view
    + Ghép ảnh (stitching)
    + Chuyển mặt phẳng (mặt đường, biển báo, giấy A4…)
```
**Syn**
```bash
H, mask = cv2.findHomography(src, dst, method=cv2.RANSAC, ransacReprojThreshold=3.0)

- src	    : Nx2 điểm nguồn
- dst	    : Nx2 điểm đích
- method	: 0, RANSAC, LMEDS
- mask	    : 0/1 cho biết điểm nào hợp lệ

Kết quả trả về
H (numpy array)
[[ h11  h12  h13 ]
 [ h21  h22  h23 ]
 [ h31  h32  h33 ]]
Ma trận biến đổi phối cảnh
```
## cv2.warpPerspective()
```bash
- Áp dụng ma trận Homography để biến đổi ảnh
```
**Syn**
```bash
warped = cv2.warpPerspective(
    src_image,
    H,
    dsize=(width, height)
)

- src_image	    : Ảnh gốc
- H	            : Ma trận Homography
- dsize	        : Kích thước ảnh output
```
```bash
- getAffineTransform() dùng để tính ma trận Affine (2×3) từ 3 cặp điểm tương ứng.
- Nói cách khác: “Cho tôi biết ảnh A bị xoay / nghiêng / co / tịnh tiến như thế nào để 3 điểm này khớp với 3 điểm kia”
- Hàm KHÔNG biến đổi ảnh, nó CHỈ TÍNH MA TRẬN → sau đó ta dùng warpAffine() để áp dụng.
```
**Syn**
```bash
M = cv2.getAffineTransform(srcPoints, dstPoints)
    + srcPoints: mảng 3 điểm gốc (x, y)
    + dstPoints: mảng 3 điểm đích (x', y')
    + Kiểu dữ liệu: np.float32
    + Shape: (3, 2)
    + Giá trị trả về. M: ma trận Affine 2×3
```
**Ma trận Affine (in ra sẽ thấy cái này)**
```bash
[a  b  tx]
[c  d  ty]
```
**Áp dụng cho mỗi điểm**
```bash
x' = a*x + b*y + t*x
y' = c*x + d*y + t*y

- 4 số (a, b, c, d): xoay, co giãn, shear
- 2 số (tx, ty): tịnh tiến
```
**Ex: chỉ tịnh tiến + nghiêng nhẹ**
```python
import cv2
import numpy as np

img = cv2.imread("image.jpg")
(h, w) = img.shape[:2]

# 3 điểm gốc
src = np.float32([
    [0, 0],
    [w, 0],
    [0, h]
])

# 3 điểm đích (dịch + nghiêng)
dst = np.float32([
    [50, 50],
    [w + 30, 80],
    [80, h + 20]
])

# Tính ma trận Affine
M = cv2.getAffineTransform(src, dst)

print("Affine Matrix M:\n", M)

# Áp dụng Affine
affine_img = cv2.warpAffine(img, M, (w + 100, h + 100))

cv2.imshow("Original", img)
cv2.imshow("Affine", affine_img)
cv2.waitKey(0)
cv2.destroyAllWindows()

# Affine Matrix M:
# [[ 1.02  0.15  50.  ]
#  [ 0.08  1.01  50.  ]]

# Diễn giải từng số
# [ 1.02  0.15 | 50 ]
# [ 0.08  1.01 | 50 ]

# Giá trị	Ý nghĩa
# 1.02	phóng to trục x
# 0.15	shear / xoay
# 0.08	shear / xoay
# 1.01	phóng to trục y
# 50, 50	dịch ảnh sang phải & xuống

# Ví dụ kiểm chứng bằng tay (rất quan trọng)
# Lấy điểm (0, 0):

# x' = 1.02*0 + 0.15*0 + 50 = 50
# y' = 0.08*0 + 1.01*0 + 50 = 50
# Khớp với dst[0] = (50, 50)
```
## GetPerspectiveTransform()
```bash
- Dùng để tính toán một ma trận chuyển đổi kích thước 3×3 (gọi là ma trận biến đổi phối cảnh). 
- Ma trận này cho phép bạn chuyển một vùng hình ảnh từ góc nhìn nghiêng (3D perspective) về một góc nhìn thẳng từ trên xuống (2D bird's-eye view).
```
**Syn**
```bash
M = cv2.getPerspectiveTransform(
   src, 
   dst
)

- src: Mảng chứa tọa độ 4 điểm trên hình ảnh gốc (ảnh bị nghiêng). kiểu np.float32
- dst: Mảng chứa tọa độ 4 điểm tương ứng trên hình ảnh đích (hình chữ nhật chuẩn).
- M: Kết quả trả về là ma trận 3×3. kiểu np.float32
```
**Ex**
```python
import cv2
import numpy as np

# 1. Tọa độ 4 điểm góc của sân trên ảnh gốc (ảnh nghiêng)
# Thứ tự: Top-Left, Top-Right, Bottom-Right, Bottom-Left
pts_src = np.array([
    [200, 150], [450, 150], 
    [550, 450], [100, 450]
], dtype="float32")

# 2. Tọa độ 4 điểm tương ứng bạn muốn hiển thị trên ảnh mới (hình chữ nhật)
# Giả sử ta muốn kết quả là ảnh 300x500
width, height = 300, 500
pts_dst = np.array([
    [0, 0], [width, 0], 
    [width, height], [0, height]
], dtype="float32")

# 3. Tính ma trận biến đổi M
M = cv2.getPerspectiveTransform(pts_src, pts_dst)

# 4. Áp dụng ma trận M để biến đổi ảnh (warp)
# Giả sử 'img' là ảnh đầu vào của bạn
# result = cv2.warpPerspective(img, M, (width, height))

print("Ma trận biến đổi M:")
print(M)
```
## PerspectiveTransform()
```bash
- Dùng để tính toán tọa độ mới của các điểm (tập hợp các điểm x, y).
- Ví dụ: Trong bài toán sân cầu lông, hàm này cực kỳ hữu ích để bạn lấy tọa độ quả cầu hoặc vận động viên trên camera rồi chuyển nó thành tọa độ x,y trên sơ đồ sân 2D.
```
**Syn**
```bash
dst_points = cv2.perspectiveTransform(src_points, M)

- src_points: Mảng các điểm cần chuyển đổi.
    + Lưu ý cực kỳ quan trọng: Mảng này phải có cấu trúc 3 chiều với định dạng (N, 1, 2), trong đó N là số lượng điểm. Kiểu dữ liệu phải là float32.
- M: Ma trận biến đổi 3×3 (đã tính được từ hàm cv2.getPerspectiveTransform).
- dst_points: Kết quả trả về là tọa độ các điểm sau khi đã "trải phẳng" về 2D.
```
**Ex**
```python
import cv2
import numpy as np

# --- Bước 1: Giả lập ma trận M (thực tế bạn lấy từ getPerspectiveTransform) ---
# Tọa độ 4 góc sân trên Camera (ảnh bị nghiêng)
src_corners = np.array([[100, 100], [500, 100], [600, 500], [0, 500]], dtype="float32")
# Tọa độ 4 góc sân trên sơ đồ 2D (hình chữ nhật chuẩn)
dst_corners = np.array([[0, 0], [610, 0], [610, 1340], [0, 1340]], dtype="float32")

M = cv2.getPerspectiveTransform(src_corners, dst_corners)

# --- Bước 2: Tọa độ một điểm cụ thể cần map (ví dụ: Quả cầu) ---
# Giả sử quả cầu đang ở tọa độ (300, 400) trên frame camera
ball_x, ball_y = 300, 400

# Chuyển điểm về định dạng mảng 3 chiều (N, 1, 2)
points_to_map = np.array([[[ball_x, ball_y]]], dtype="float32")

# --- Bước 3: Sử dụng perspectiveTransform ---
mapped_points = cv2.perspectiveTransform(points_to_map, M)

# Lấy kết quả x, y mới
new_x = mapped_points[0][0][0]
new_y = mapped_points[0][0][1]

print(f"Tọa độ gốc trên Camera: ({ball_x}, {ball_y})")
print(f"Tọa độ sau khi map vào sân 2D: ({new_x:.2f}, {new_y:.2f})")

# --- Bonus: Map nhiều điểm cùng lúc ---
# Nếu bạn có cả tọa độ cầu và 2 người chơi
many_points = np.array([
    [[300, 400]], # Quả cầu
    [[150, 450]], # Người chơi A
    [[450, 200]]  # Người chơi B
], dtype="float32")

mapped_many = cv2.perspectiveTransform(many_points, M)
print("\nDanh sách các điểm đã map:")
for i, pt in enumerate(mapped_many):
    print(f"Điểm {i+1}: {pt[0]}")
```
## .resize()
**Syn**
```bash
cv2.resize(
   src=frame, 
   dsize=(300, 200),
)

    + src: Ảnh gốc
    + dsize: Kích thước đích dưới dạng (width, height) (bắt buộc nếu không dùng fx, fy)
```
**Ex**
```python
import cv2

image = cv2.imread('night.jpg')
if image is None:
    print("Không thể tải ảnh")
else:
    print("Kích thước gốc:", image.shape)

    resized = cv2.resize(image, (400, 300))  # Resize về 400x300
    print("Kích thước mới:", resized.shape)

    cv2.imshow("Resized Image", resized)
    cv2.waitKey(0)
    cv2.destroyAllWindows()
```
## .resizeWindow()
```bash
Dùng để thay đổi kích thước cửa sổ hiển thị
```
**Ex**
```python
import cv2

img = cv2.imread("image.jpg")

cv2.namedWindow("window", cv2.WINDOW_NORMAL)   # cho phép resize
cv2.resizeWindow("window", 800, 600)           # set kích thước cửa sổ

cv2.imshow("window", img)
cv2.waitKey(0)
cv2.destroyAllWindows()
```
# Display (cung cấp thông tin)
## .shape
```bash
- Là một thuộc tính của mảng ảnh NumPy vì cv2.imread() trả về một numpy.ndarray. 
- Nó cho biết kích thức và một số kênh màu.
- Trả về 3 giá trị height, width, depth
    + h – chiểu cao của ảnh, pixels
    + w – chiều rộng của ảnh, pixels
    + 3 – số kênh màu (BGR)
    + 4 – số kênh màu + alpha (BGR + trong suốt)
```
**Ex1**
```python
import cv2
def main():
    # Load an image
    image = cv2.imread('night.jpg', cv2.IMREAD_GRAYSCALE)
    # Check if the image was loaded successfully
    if image is None:
        print("Error: Could not load image.")
        return
    else:
        h, w, c = image.shape
        print("kích thước ảnh:", image.shape)
        print("Chiều cao:", h)
        print("Chiều rộng:", w)
        print("Số kênh màu:", c)
        return
main()

# ValueError: not enough values to unpack (expected 3, got 2)
# lỗi vì đang sử dụng cv2.IMREAD_GRAYSCALE tức là ảnh chỉ có một kênh màu (đen trắng). Trong trường hợp đó image.shape chỉ trả về 2 giá trị là height và width
```
**Ex2**
```python
import cv2
def main():   
    image = cv2.imread('night.jpg') # Load an image
    
    if image is None: # Check if the image was loaded successfully
        print("Error: Could not load image.")
        return
    else:
        h, w, c = image.shape
        print("kích thước ảnh:", image.shape)
        print("Chiều cao:", h)
        print("Chiều rộng:", w)
        print("Số kênh màu:", c)
        return
main()

# kích thước ảnh: (719, 1200, 3)
# Chiều cao: 719
# Chiều rộng: 1200
# Số kênh màu: 3
```
## .get()
```bash
Lấy kích thước của video.
```
**Syn**
```bash
cap.get(input)

- cv2.CAP_PROP_FPS: lấy ra tốc độ của video gốc
- cv2.CAP_PROP_FRAME_WIDTH: lấy chiều rộng của video
- cv2.CAP_PROP_FRAME_HEIGHT: Lấy chiều cao của video
```
**Ex**
```python
import cv2

cap = cv2.VideoCapture('video/output.mp4')

width  = int(cap.get(cv2.CAP_PROP_FRAME_WIDTH))
height = int(cap.get(cv2.CAP_PROP_FRAME_HEIGHT))

print(height, width)
```
# Event (bắt sự kiên)
## EVENT_LBUTTONDOWN
```bash
- Là một hằng số đại diện cho sự kiện nhấn chuột trái. 
- Để sử dụng nó, bạn cần thiết lập một hàm gọi là Callback function và gắn nó vào một cửa sổ hiển thị bằng lệnh cv2.setMouseCallback.
- Quy trình thực hiện gồm 3 bước chính:
    + Định nghĩa hàm Callback: Hàm này sẽ tự động được gọi mỗi khi có sự kiện chuột xảy ra.
    + Tạo một cửa sổ: Phải có một cửa sổ với tên cụ thể (ví dụ: "Image Window").
    + Kết nối: Dùng cv2.setMouseCallback("Tên cửa sổ", tên_hàm_callback) để liên kết.
```
**Ex**
```python
import cv2
import numpy as np

# 1. Định nghĩa hàm callback xử lý sự kiện chuột
def handle_mouse_click(event, x, y, flags, param):
    # Kiểm tra xem sự kiện có phải là nhấn chuột trái không
    if event == cv2.EVENT_LBUTTONDOWN:
        print(f"Bạn vừa click vào tọa độ: x={x}, y={y}")
        
        # Vẽ một hình tròn nhỏ màu xanh tại điểm click
        # (img, center, radius, color, thickness)
        cv2.circle(img, (x, y), 5, (255, 0, 0), -1)
        
        # Cập nhật lại hình ảnh hiển thị
        cv2.imshow("Mouse Event Demo", img)

# 2. Tạo một ảnh nền đen (512x512 pixel)
img = np.zeros((512, 512, 3), np.uint8)

# 3. Tạo cửa sổ và đặt tên cho nó (rất quan trọng)
cv2.namedWindow("Mouse Event Demo")

# 4. Gắn hàm callback vào cửa sổ đã tạo
cv2.setMouseCallback("Mouse Event Demo", handle_mouse_click)

print("Hướng dẫn: Click chuột trái lên cửa sổ ảnh để vẽ điểm.")
print("Nhấn phím 'q' hoặc 'Esc' để thoát.")

# 5. Vòng lặp chính để giữ cửa sổ mở
while True:
    cv2.imshow("Mouse Event Demo", img)
    
    # Đợi phím bấm (20ms)
    key = cv2.waitKey(20) & 0xFF
    if key == ord('q') or key == 27: # Thoát khi nhấn 'q' hoặc Esc
        break

cv2.destroyAllWindows()
```
## cv2.EVENT_LBUTTONUP	
```bash
Nhả chuột trái
```
## cv2.EVENT_MOUSEMOVE	
```bash
Di chuyển chuột
```
## cv2.EVENT_RBUTTONDOWN	
```bash
Nhấn chuột phải
```
## .SetMouseCallback()
```bash
Để lấy tọa độ điểm khi click chuột.
```
**Syn**
```bash
cv2.setMouseCallback(window_name, callback_function)

- window_name: tên cửa sổ hiển thị ảnh
- callback_function: hàm xử lý sự kiện chuột
```
# Shape / Geometry (Hình học)
## MinAreaRect()
```bash
Hàm này tìm một hình chữ nhật bao quanh có diện tích nhỏ nhất cho một tập hợp điểm. Khác với cv2.boundingRect (luôn thẳng đứng), minAreaRect có thể xoay theo hướng của vật thể.
```
# Blur Process (các thao tác để làm mờ)
## GaussianBlur()
**Syn**
```bash
cv2.GaussianBlur(src=, ksize=, sigmaX=0)
- src: ảnh gốc (ảnh đầu vào).
- ksize: bộ lọc (kernel size), dạng (width, height), phải là số lẻ (ví dụ: (5,5)).
- sigmaX: độ lệch chuẩn theo trục X.
```
**Ex**
```python
import cv2

anh = cv2.imread('anh1.jpg', -1)
blur = cv2.GaussianBlur(anh, (11,11), 0)

cv2.imshow("anh", blur)
cv2.waitKey(0)
cv2.destroyAllWindows()
# (11,11) là độ mờ, số càng lớn mờ càng nhiều, số này phải là số lẻ
```
## MedianBlur()
```bash
- Median là bộ loc giảm nhiễu, đặc biệt hiệu quả với “salt & pepper noise” nhiễu muối tiêu - tức là các điểm trắng/đen ngẫu nhiên.
- Cách hoạt động:
    + Với mỗi pixel trong ảnh, ta lấy một vùng lân cận (3x3, 5x5, …)
    + sắp xếp tất cả cấc giá trị pixel trong vùng đó theo thứ tự.
    + Thay pixel trung tâm bằng giá trị median của vùng đó.
```
**Ex**
```python
import cv2

img = cv2.imread('anh3.jpg')
cv2.imshow("original", img)

median = cv2.medianBlur(img, 5)
cv2.imshow("test", median)
cv2.waitKey(0)
cv2.destroyAllWindows()
```
# Edge Process (xử lý cạnh)
## Canny()
```bash
- Là hàm dùng để phát hiện cạnh trong ảnh, rất phổ biến và hiệu quả.
- Các bước hoạt động:
    1. Làm mờ ảnh bằng bộ lọc gaussian: Giảm nhiễu, nhiễu có thể gây ra các cạnh giả.
    2. Tính toán gradient cường độ và hướng gradient: Xác định các vùng có sự thay đổi cường độ sáng lớn nhất.
    3. Làm trong hướng
    4. Loại bỏ các điểm không phải là cực đại cục bộ.
    5. Ngưỡng kép.
    6. Theo dõi cạnh bằng độ trễ
```
**Syn** 
```bash
edges = cv2.Canny(image, threshold1, threshold2)

- image: ảnh đầu vào (thường là ảnh xám – grayscale).
- threshold1, threshold2: ngưỡng dưới và trên để xác định cạnh.
```
**Ex**
```python
import cv2

anh = cv2.imread('anh1.jpg', 0)
edge = cv2.Canny(anh, 100,200)

cv2.imshow("anh", edge)

cv2.waitKey(0)
cv2.destroyAllWindows()
```
# Color Process (Xử lý màu sắc)
## .cvtColor()
```bash
Là hàm dùng để chuyển đổi không gian màu của ảnh, ví dụ từ ảnh màu ảnh xám, RGB sang HSV, …
```
**Syn** 
```bash
dst = cv2.cvtColor(src, code)

- src: ảnh gốc (đầu vào).
- code: mã chuyển đổi màu, ví dụ:
    + cv2.COLOR_BGR2GRAY: chuyển ảnh từ BGR sang ảnh xám.
    + cv2.COLOR_BGR2RGB: chuyển từ BGR (mặc định OpenCV) sang RGB.
    + cv2.COLOR_BGR2HSV: chuyển từ BGR sang HSV.
```
**Ex**
```python
import cv2

anh = cv2.imread('anh1.jpg')
gray = cv2.cvtColor(anh, cv2.COLOR_BGR2GRAY)

cv2.imshow("anh", gray)

cv2.waitKey(0)
cv2.destroyAllWindows()
```
## divide()
```bash
Dùng để chia từng pixel của 2 ảnh (hoặc ảnh với số) – hay dùng làm ảnh sáng, tạo hiệu ứng ảnh phác thảo (sketch).
```
**Syn** 
```bash
output = cv2.divide(src1, src2[, scale])

- src1, src2: hai ảnh cùng kích thước.
- scale (tùy chọn): hệ số nhân sau khi chia (mặc định = 1).
```
**Ex**
```python
import cv2

gray = cv2.imread('anh1.jpg', 0)

inv = 255 - gray

blur = cv2.GaussianBlur(inv, (21,21), 0)
sketch = cv2.divide(gray, 255-blur, scale=256)

cv2.imshow("anh", sketch)
cv2.waitKey(0)
cv2.destroyAllWindows()

# giống hiệu ứng nét bút chì
```
# Filter
## filter2D()
```bash
Dùng để áp dụng để áp dụng bộ lọc tùy chỉnh lên ảnh – giúp làm mờ, làm sắc nét, phát hiện cạnh, …
```
**Syn** 
```bash
dst = cv2.filter2D(src, depth, kernel)

- src: ảnh đầu vào.
- depth: độ sâu ảnh đầu ra (-1 để giữ nguyên độ sâu ảnh gốc).
- kernel: ma trận lọc (numpy array), ví dụ:
    kernel = np.array([[0, -1, 0],
                       [-1, 5, -1],
                       [0, -1, 0]])
```
**Ex**
```python
import cv2
import numpy as np

img = cv2.imread('anh1.jpg')
kernel = np.array([[0,-1,0],
                  [-1,5,-1],
                  [0,-1,0]])

sharrpend = cv2.filter2D(img, -1, kernel)

cv2.imshow("anh", sharrpend)
cv2.waitKey(0)
cv2.destroyAllWindows()
```
## bilateralFilter()
```bash
- Bilateral filter (lọc song phương) là một bộ lọc phi tuyến tính, thực hiện làm mịn ảnh bằng cách kết hợp thông tịn không gian và cường độ màu (độ sáng) của điểm ảnh. Nó giữ cạnh rõ ràng vì:
    + Không làm mờ các pixel có giá trị màu khác biệt lớn (ví dụ tại rìa cạnh).
    + Chỉ làm mịn các pixel có màu tương tự và nằm gần nhau.
- Hiểu đơn giản thì nó dùng một kernel có thể thay đổi giá trị. kernel này chứa
    + Gaussian theo không gian -> đảm bảo các điểm gần được ưu tiên.
    + Gaussian theo độ sáng -> loại bỏ các pixel có độ sáng quá khác biệt.
- Dùng để:
    • Làm mịn ảnh mà vẫn giữ được cạnh sắc nét (khác với Gaussian blur).
    • Tiền xử lý cho nhận diện khuôn mặt, OCR, …
    • Trong làm đẹp ảnh (beautify filter).
    • Tách nền / foreground-background segmentation.
    • Trước khi phân đoạn ảnh (image segmentation)
```
**Syn** 
```bash
cv2.bilateralFilter(src, d, sigmaColor, sigmaSpace)

- src: Ảnh đầu vào.
- d: Đường kính của pixel lân cận (cửa sổ) - ma trận kernel  
- sigmaColor: Độ nhạy với khác biệt màu. Càng lớn thì càng mịn, bỏ qua sự khác biệt màu nhỏ. - kiểm soát mức độ quan tâm đến độ khác biệt màu sắc. 
- sigmaSpace: Độ nhay với khoảng cách không gian. Càng lớn thì ảnh hưởng pixel xa hơn càng nhiều - Kiểm soát khoảng cách không gian trong kernel.
```
# ROI Process
## PointPolygonTest()
```bash
Kiểm tra điểm có nằm trong ROI không. Dùng để: Check bbox center có trong ROI không
```
**Ex**
```python
cx, cy = 500, 600
inside = cv2.pointPolygonTest(pts, (cx, cy), False)

if inside >= 0:
    print("Object inside ROI")
```
## InRange()
```bash
- ROI theo màu (nâng cao) Thường dùng cho:
    + Làn đường
    + Biển báo
    + Vạch kẻ
- mask = cv2.inRange(hsv, lower, upper)
```
## FindContours()
```bash
- ROI dựa trên hình dạng
- Dùng khi:
    + ROI không cố định
    + ROI sinh ra từ segmentation
```
**Syn**
```python
contours, _ = cv2.findContours(mask, cv2.RETR_EXTERNAL, cv2.CHAIN_APPROX_SIMPLE)
```
# BoundingRect()
```bash
chuyển contour → ROI rectangle
```
**Ex**
```python
x, y, w, h = cv2.boundingRect(cnt)
roi = frame[y:y+h, x:x+w]
```