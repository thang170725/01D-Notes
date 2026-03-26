- [Read (đọc, lấy)](#read-đọc-lấy)
- [imread()](#imread)
- [NameWindow()](#namewindow)
- [Imshow() \& WaitKey() \& destroyAllWindows()](#imshow--waitkey--destroyallwindows)
- [VideoCapture() \& .read() \& .release()](#videocapture--read--release)
- [Draw](#draw)
  - [.putText()](#puttext)
  - [.circle()](#circle)
  - [.rectangle()](#rectangle)
  - [.polylines()](#polylines)
- [FillPoly()](#fillpoly)
- [bitwise\_and()](#bitwise_and)
  - [imdecode](#imdecode)
  - [imencode](#imencode)
---
# Read (đọc, lấy)
# imread()
```bash
- Được sử dụng để đọc một hình ảnh từ ổ đĩa và lưu nó dưới dạng một mảng NumPy để xử lý trong các ứng dụng xử lý ảnh.
```
**Syn**
```bash
cv2.imread(filename, flags)

- Filename: Đường dẫn đến ảnh (có thể là tuyệt đối hoặc tương đối).
- Flags: Chế độ đọc ảnh, mặc định là cv2.IMREAD_COLOR
    + cv2.IMREAD_COLOR (hoặc 1): Đọc ảnh màu bỏ kênh anpha.
    + cv2.IMREAD_GRAYSCALE (hoặc 0): Đọc ảnh ở dạng grayscale (đen trắng).
    + cv2.IMREAD_UNCHANGED (hoặc -1): Giữ nguyên ảnh, kể cả kênh alpha nếu có.
```
# NameWindow()
```bash
Tạo ra một cửa số có tên.
```
**Syn**
```bash
cv2.namedWindow("Get Tọa Độ")
```
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

- 0: Dừng vô thời hạn – chờ đến khi người dùng bấm phím thì chương trình mới thoát. (1000: Dừng 1 giây). Đối với video waitkey để càng lớn tốc độ video sẽ càng chậm
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
# VideoCapture() & .read() & .release()
```bash
- Là một class được sử dụng để, mở video từ file (mp4, avi, …) truy cập webcam hoặc camera khác để chụp ảnh hoặc quay video trên thời gian thực.
```
**Syn**
```bash
cv2.VideoCapture(source)
source có thể là:
    + Một số nguyên: 0, 1, 2, ... → chỉ số của webcam (0 là webcam mặc định).
    + Một chuỗi đường dẫn: "video.mp4" → mở video từ file.
```
**Ex**
```python
import cv2

def main():
cap = cv2.VideoCapture(0)

    if not cap.isOpened():
        print("Không thể mở webcam")
        return
    else:
        while True:
            ret, frame = cap.read()
            if not ret:
                break
            cv2.imshow("Webcam", frame)
            if cv2.waitKey(25) & 0xFF == ord('q'):
                break
    cap.release()
    cv2.destroyAllWindows()
main()

# bạn không tự động thấy ảnh từ camera. Bạn phải liên tục lấy ảnh từ webcam – và mỗi lần chụp ra tại một thời điểm, người ta gọi là một frame (giống như một khung hình trong video)
# webcam là nguồn video, và video thực ra là nhiều ảnh nối tiếp nhau gọi là các frame
```
# Draw
## .putText()
**Syn**
```bash
cv2.putText(img, text, org, fontFace, fontScale, color, thickness, lineType)

- img	    : Ảnh hoặc khung hình (frame) bạn muốn vẽ lên.
- text	    : Nội dung chữ (Kiểu String). Lưu ý: OpenCV mặc định không viết được tiếng Việt có dấu.
- org	    : Tọa độ điểm bắt đầu (góc dưới bên trái của chữ) dạng (x, y).
- fontFace	: Loại font chữ (Ví dụ: cv2.FONT_HERSHEY_SIMPLEX, cv2.FONT_HERSHEY_COMPLEX).
- fontScale	: Tỷ lệ kích thước chữ (Số thực, ví dụ: 1.0, 0.5).
- color	Màu : sắc theo hệ BGR (ví dụ: (0, 255, 0) là màu xanh lá).
- thickness	: Độ dày nét chữ (Số nguyên).
- lineType	: Loại đường nét. Nên dùng cv2.LINE_AA (Anti-Aliased) để chữ mịn, không bị răng cưa.
```
## .circle()
```bash
cv2.circle(
   img=frame, 
   center=(x, y), 
   radius=5, 
   color=(0, 0, 255), 
   thickness=-1
   lineType,
   shift
)

- Thickness:     Độ dày đường viền. Nếu để số âm (ví dụ: -1), hình tròn sẽ được tô đặc. 2 hoặc -1
```
## .rectangle()
```bash
Dùng để vẽ hình chữ nhật.
```
**Syn**
```bash
cv2.rectangle(
    frame,
    pt1=(x1, y1),
    pt2=(x2, y2),
    color=(0, 255, 0),
    thickness=2
)
```
## .polylines()
```bash
Dùng để vẽ đa giác.
```
**Ex**
```bash
pts = np.array([
    [300, 700],
    [600, 400],
    [1200, 400],
    [1600, 700]
], np.int32)

cv2.polylines(frame, [pts], True, (255, 0, 0), 2)
```
# FillPoly()
```bash
Dùng để tạo mask
```
**Ex**
```bash
mask = np.zeros(frame.shape[:2], dtype=np.uint8)

cv2.fillPoly(mask, [pts], 255)
```
# bitwise_and()
```bash
Dùng để áp mask ROI
```
**Syn**
```bash
roi = cv2.bitwise_and(frame, frame, mask=mask)
```
## imdecode
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
## imencode
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