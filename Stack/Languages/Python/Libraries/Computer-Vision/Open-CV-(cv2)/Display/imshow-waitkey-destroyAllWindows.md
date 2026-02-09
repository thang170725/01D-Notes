# Imshow() & WaitKey() & destroyAllWindows()
```bash
- Nhóm dùng để hiển thị hình ảnh, frame.
```
**Syn: imshow()**
```bash
cv2.imshow(<mô tả>, <attribute>)
```
**Syn: Waitkey()**
```bash
cv2.waitKey(0)

    + 0: Dừng vô thời hạn – chờ đến khi người dùng bấm phím thì chương trình mới thoát. (1000: Dừng 1 giây). Đối với video waitkey để càng lớn tốc độ video sẽ càng chậm
```
**Syn: destroyAllWindows**
```bash
cv2.destroyAllWidows()
```
**Ex**
```python
import cv2
def main():
    image = cv2.imread('night.jpg', cv2.IMREAD_GRAYSCALE) # Load an image
    
    if image is None: # Check if the image was loaded successfully
        print("Error: Could not load image.")
    
    cv2.imshow('Ảnh hạ long', image) # Display the image in a window

    # Wait for a key press and close the window
    cv2.waitKey(0)
    cv2.destroyAllWindows()
main()
```