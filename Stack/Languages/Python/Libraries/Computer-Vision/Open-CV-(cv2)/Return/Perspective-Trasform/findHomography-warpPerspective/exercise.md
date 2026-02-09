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