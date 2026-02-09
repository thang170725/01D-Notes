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