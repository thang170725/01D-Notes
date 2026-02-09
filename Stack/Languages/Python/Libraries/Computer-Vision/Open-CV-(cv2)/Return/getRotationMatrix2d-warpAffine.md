Xoay góc bất kỳ bằng getRotationMatrix2D() + warpAffine()

👉 Đây là cách chuẩn và linh hoạt nhất

Cú pháp
M = cv2.getRotationMatrix2D(center, angle, scale)
dst = cv2.warpAffine(src, M, (width, height))

Ý nghĩa tham số

center: tâm xoay (x, y)

angle: góc xoay (độ, dương = ngược chiều kim đồng hồ)

scale: tỉ lệ (1.0 = giữ nguyên)

Ví dụ demo xoay 45°
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


📌 Lưu ý:

Ảnh có thể bị cắt góc nếu xoay nhiều

angle > 0 → xoay ngược chiều kim đồng hồ

3. Xoay mà không bị cắt ảnh (demo nâng cao – dễ hiểu)
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

4. Tóm tắt nhanh
Mục đích	Cách dùng
Xoay 90°, 180°	cv2.rotate()
Xoay góc bất kỳ	getRotationMatrix2D + warpAffine
Không bị cắt ảnh	Tính lại kích thước ảnh