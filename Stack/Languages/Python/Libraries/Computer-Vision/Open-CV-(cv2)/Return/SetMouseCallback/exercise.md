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
