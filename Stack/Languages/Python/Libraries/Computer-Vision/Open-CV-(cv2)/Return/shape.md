# .shape
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