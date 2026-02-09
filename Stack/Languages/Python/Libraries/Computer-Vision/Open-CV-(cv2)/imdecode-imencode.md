# imdecode
**Syn**
```bash
cv2.imdecode(buf, flags)
- buf: numpy array 1D (np.uint8)
- flags:
    + cv2.IMREAD_COLOR
    + cv2.IMREAD_GRAYSCALE
    + cv2.IMREAD_UNCHANGED
```
**Ex**
```python
image = cv2.imdecode(np_arr, cv2.IMREAD_COLOR)
# image = np.ndarray
# shape: (H, W, 3)
# BGR (không phải RGB)
# ⚠️ Nếu trả về None → ảnh không hợp lệ
```

# imencode
**Syn**
```bash
success, buffer = cv2.imencode(ext, img, params=None)
- ext: ".png", ".jpg", ".webp"
- img: np.ndarray
- params (tuỳ chọn):
    + [cv2.IMWRITE_JPEG_QUALITY, 90]
```
**Ex**
```python
success, buffer = cv2.imencode(".png", image)
# success: True / False
# buffer: numpy array 1D
```