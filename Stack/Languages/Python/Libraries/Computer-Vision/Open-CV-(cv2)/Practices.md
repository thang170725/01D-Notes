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
- [lấy tọa độ 1 điểm khi click chuột trái](#lấy-tọa-độ-1-điểm-khi-click-chuột-trái)
- [lấy tọa độ 1 điểm khi click chuột trái và vẽ lại điểm đó](#lấy-tọa-độ-1-điểm-khi-click-chuột-trái-và-vẽ-lại-điểm-đó)
- [Lấy nhiều điểm (ví dụ chọn 4 điểm)](#lấy-nhiều-điểm-ví-dụ-chọn-4-điểm)

---

# lấy tọa độ 1 điểm khi click chuột trái
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

# lấy tọa độ 1 điểm khi click chuột trái và vẽ lại điểm đó
```python
def mouse_callback(event, x, y, flags, param):
    if event == cv2.EVENT_LBUTTONDOWN:
        cv2.circle(img, (x, y), 5, (0, 0, 255), -1)
        cv2.imshow("Image", img)
        print(x, y)
```

# Lấy nhiều điểm (ví dụ chọn 4 điểm)
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