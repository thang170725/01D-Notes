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