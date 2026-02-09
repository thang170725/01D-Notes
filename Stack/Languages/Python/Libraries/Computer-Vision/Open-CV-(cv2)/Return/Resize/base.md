# .resize()
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
