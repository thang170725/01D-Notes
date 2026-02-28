- [✅ Tạo mảng kết quả có kích thước sẵn](#-tạo-mảng-kết-quả-có-kích-thước-sẵn)
- [Hàm in mã ASCII của phím bấm (dùng OpenCV)](#hàm-in-mã-ascii-của-phím-bấm-dùng-opencv)
- [lấy tọa độ điểm khi click chuột vào frame](#lấy-tọa-độ-điểm-khi-click-chuột-vào-frame)
- [resize giữ tỉ lệ khi biết chiều rộng, tự tính chiều cao](#resize-giữ-tỉ-lệ-khi-biết-chiều-rộng-tự-tính-chiều-cao)
- [Biển đổi 4 điểm từ chụp nghiêng sang chụp thẳng](#biển-đổi-4-điểm-từ-chụp-nghiêng-sang-chụp-thẳng)
---
Bài tập
Cho một ma trận ảnh 5×5 và một kernel 3×3, hãy tính kết quả tích chập (convolution)
import numpy as np

img = np.array([
    [1,2,3,4,5], 
    [6,7,8,9,10],
    [11,12,13,14,15],
    [16,17,18,19,20],
    [21,22,23,24,25]
])
kernel = np.array([
    [2,4,6],
    [1,2,3],
    [3,4,5]
])

h, w = img.shape
kh, kw = kernel.shape
out_h = h - kh + 1
out_w = w - kw + 1

# ✅ Tạo mảng kết quả có kích thước sẵn
out = np.zeros((out_h, out_w))

for i in range(out_h):
    for j in range(out_w):
        out[i, j] = np.sum(img[i:i+kh, j:j+kw] * kernel)

print(out)
[[178. 202. 226.]
 [298. 322. 346.]
 [418. 442. 466.]]
Chuẩn hóa
Bài tập
Chuẩn hóa ảnh về [0,1]
x_train = x_train.astype('float32') / 255.0
x_test  = x_test.astype('float32') / 255.0
# Hàm in mã ASCII của phím bấm (dùng OpenCV)
```python
import cv2
import numpy as np

def print_ascii_key():
    img = np.zeros((200, 400, 3), dtype=np.uint8)
    cv2.putText(img, "Press any key (ESC to exit)",
                (20, 100),
                cv2.FONT_HERSHEY_SIMPLEX,
                0.6, (255, 255, 255), 1)

    while True:
        cv2.imshow("Key ASCII Detector", img)
        key = cv2.waitKey(0) & 0xFF   # đợi bấm phím

        print(f"Key pressed: ASCII = {key}, char = {chr(key) if key < 128 else 'N/A'}")

        if key == 27:  # ESC
            break

    cv2.destroyAllWindows()

print_ascii_key()
```
# lấy tọa độ điểm khi click chuột vào frame
**Ex1: Lấy tọa độ 1 điểm**
```python
import cv2

def mouse_callback(event, x, y, flags, param):
    if event == cv2.EVENT_LBUTTONDOWN:
        print(f"Toa do: x={x}, y={y}")

img = cv2.imread("image.jpg")
cv2.imshow("Image", img)

cv2.setMouseCallback("Image", mouse_callback)

cv2.waitKey(0)
cv2.destroyAllWindows()

# Khi bạn click chuột trái vào ảnh, tọa độ (x, y) sẽ được in ra.
```
**Ex2: Lấy nhiều điểm (ví dụ chọn 4 điểm)**
```python
import cv2
import numpy as np

points = []
def mouse_callback(event, x, y, flags, param):
    if event == cv2.EVENT_LBUTTONDOWN:
        cv2.circle(img, (x, y), 5, (0, 0, 255), -1)
        cv2.imshow("Image", img)
        points.append((x, y))

img = cv2.imread("./images/car.jpg")

cv2.imshow("Image", img)

cv2.setMouseCallback("Image", mouse_callback)

cv2.waitKey(0)
cv2.destroyAllWindows()

print(points)
```
**Ex4**
```python
Bài tập
Lấy tọa độ điểm bằng frame đầu của video
import cv2

points = []

def get_coords(event, x, y, flags, param):
    if event == cv2.EVENT_LBUTTONDOWN:
        points.append((x, y))
        print(f"Click: {x}, {y}")

cap = cv2.VideoCapture("video.mp4")

cv2.namedWindow("Video")
cv2.setMouseCallback("Video", get_coords)

while True:
    ret, frame = cap.read()
    if not ret:
        break

    # vẽ điểm đã click
    for p in points:
        cv2.circle(frame, p, 5, (0, 0, 255), -1)

    cv2.imshow("Video", frame)

    if cv2.waitKey(30) & 0xFF == ord('q'):
        break

cap.release()
cv2.destroyAllWindows()
import cv2

points = []

def get_coords(event, x, y, flags, param):
    if event == cv2.EVENT_LBUTTONDOWN:
        points.append((x, y))
        print(points)

cap = cv2.VideoCapture("video.mp4")

ret, frame = cap.read()   # 👈 CHỈ đọc 1 frame
if not ret:
    print("Không đọc được video")
    exit()

cv2.namedWindow("Frame 0")
cv2.setMouseCallback("Frame 0", get_coords)

while True:
    show = frame.copy()

    for p in points:
        cv2.circle(show, p, 5, (0, 0, 255), -1)

    cv2.imshow("Frame 0", show)

    key = cv2.waitKey(1) & 0xFF
    if key == ord('q'):   # nhấn q để thoát
        break

cap.release()
cv2.destroyAllWindows()

print("Tọa độ cuối cùng:", points)
```
# resize giữ tỉ lệ khi biết chiều rộng, tự tính chiều cao
```python
import cv2

h, w = frame.shape[:2]
new_w = 640
new_h = int(h * new_w / w)

resized = cv2.resize(frame, (new_w, new_h))
resize giữ tỉ lệ khi biết chiều cao, tự tính chiều rộng
new_h = 480
new_w = int(w * new_h / h)

resized = cv2.resize(frame, (new_w, new_h))
```
# Biển đổi 4 điểm từ chụp nghiêng sang chụp thẳng
```python
import cv2
import numpy as np

# ===============================
# 1. Sắp xếp 4 điểm đúng thứ tự
# ===============================
def order_points(pts):
    rect = np.zeros((4, 2), dtype="float32")

    s = pts.sum(axis=1)
    rect[0] = pts[np.argmin(s)]      # Top-left
    rect[2] = pts[np.argmax(s)]      # Bottom-right

    diff = np.diff(pts, axis=1)
    rect[1] = pts[np.argmin(diff)]   # Top-right
    rect[3] = pts[np.argmax(diff)]   # Bottom-left

    return rect


# ===============================
# 2. Mouse callback
# ===============================
points = []

def mouse_callback(event, x, y, flags, param):
    global points, img_show

    if event == cv2.EVENT_LBUTTONDOWN and len(points) < 4:
        points.append([x, y])
        cv2.circle(img_show, (x, y), 5, (0, 0, 255), -1)
        cv2.imshow("Image", img_show)

        print(f"Point {len(points)}: ({x}, {y})")


# ===============================
# 3. Load image
# ===============================
img = cv2.imread("plate.jpg")   # <-- đổi tên ảnh tại đây
if img is None:
    print("Không đọc được ảnh")
    exit()

img_show = img.copy()

cv2.namedWindow("Image")
cv2.setMouseCallback("Image", mouse_callback)

print("Click 4 góc biển số theo thứ tự BẤT KỲ")
print("Sau khi đủ 4 điểm, nhấn phím ENTER")

# ===============================
# 4. Chờ click đủ 4 điểm
# ===============================
while True:
    cv2.imshow("Image", img_show)
    key = cv2.waitKey(1)

    if key == 13 and len(points) == 4:   # ENTER
        break
    if key == 27:                        # ESC
        cv2.destroyAllWindows()
        exit()

cv2.destroyWindow("Image")

# ===============================
# 5. Xử lý Homography
# ===============================
src = np.array(points, dtype="float32")
src = order_points(src)

# Tính kích thước ảnh đích
w1 = np.linalg.norm(src[1] - src[0])
w2 = np.linalg.norm(src[2] - src[3])
h1 = np.linalg.norm(src[3] - src[0])
h2 = np.linalg.norm(src[2] - src[1])

W = int(max(w1, w2))
H = int(max(h1, h2))

dst = np.float32([
    [0, 0],
    [W - 1, 0],
    [W - 1, H - 1],
    [0, H - 1]
])

# ===============================
# 6. Homography + Warp
# ===============================
H_mat, _ = cv2.findHomography(src, dst)
warped = cv2.warpPerspective(img, H_mat, (W, H))

# ===============================
# 7. Hiển thị kết quả
# ===============================
cv2.imshow("Original", img)
cv2.imshow("Warped (Plate Straightened)", warped)

cv2.waitKey(0)
cv2.destroyAllWindows()

Click 4 góc biển số theo thứ tự BẤT KỲ
Sau khi đủ 4 điểm, nhấn phím ENTER
Point 1: (151, 523)
Point 2: (248, 450)
Point 3: (257, 489)
Point 4: (159, 556)
```
