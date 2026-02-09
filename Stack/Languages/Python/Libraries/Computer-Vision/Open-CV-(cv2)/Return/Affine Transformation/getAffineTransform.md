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