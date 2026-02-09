# .SetMouseCallback()
```bash
Để lấy tọa độ điểm khi click chuột.
```
**Syn**
```bash
cv2.setMouseCallback(window_name, callback_function)

- window_name: tên cửa sổ hiển thị ảnh
- callback_function: hàm xử lý sự kiện chuột
```


EVENT_LBUTTONDOWN
Là một hằng số đại diện cho sự kiện nhấn chuột trái. Để sử dụng nó, bạn cần thiết lập một hàm gọi là Callback function và gắn nó vào một cửa sổ hiển thị bằng lệnh cv2.setMouseCallback.
Cách thức hoạt động:
Quy trình thực hiện gồm 3 bước chính:
    • Định nghĩa hàm Callback: Hàm này sẽ tự động được gọi mỗi khi có sự kiện chuột xảy ra.
    • Tạo một cửa sổ: Phải có một cửa sổ với tên cụ thể (ví dụ: "Image Window").
    • Kết nối: Dùng cv2.setMouseCallback("Tên cửa sổ", tên_hàm_callback) để liên kết.
Cú pháp:
import cv2
import numpy as np

# 1. Định nghĩa hàm callback xử lý sự kiện chuột
def handle_mouse_click(event, x, y, flags, param):
    # Kiểm tra xem sự kiện có phải là nhấn chuột trái không
    if event == cv2.EVENT_LBUTTONDOWN:
        print(f"Bạn vừa click vào tọa độ: x={x}, y={y}")
        
        # Vẽ một hình tròn nhỏ màu xanh tại điểm click
        # (img, center, radius, color, thickness)
        cv2.circle(img, (x, y), 5, (255, 0, 0), -1)
        
        # Cập nhật lại hình ảnh hiển thị
        cv2.imshow("Mouse Event Demo", img)

# 2. Tạo một ảnh nền đen (512x512 pixel)
img = np.zeros((512, 512, 3), np.uint8)

# 3. Tạo cửa sổ và đặt tên cho nó (rất quan trọng)
cv2.namedWindow("Mouse Event Demo")

# 4. Gắn hàm callback vào cửa sổ đã tạo
cv2.setMouseCallback("Mouse Event Demo", handle_mouse_click)

print("Hướng dẫn: Click chuột trái lên cửa sổ ảnh để vẽ điểm.")
print("Nhấn phím 'q' hoặc 'Esc' để thoát.")

# 5. Vòng lặp chính để giữ cửa sổ mở
while True:
    cv2.imshow("Mouse Event Demo", img)
    
    # Đợi phím bấm (20ms)
    key = cv2.waitKey(20) & 0xFF
    if key == ord('q') or key == 27: # Thoát khi nhấn 'q' hoặc Esc
        break

cv2.destroyAllWindows()


Bài tập
Lấy tọa độ điểm bằng frame đầu của video
import cv2

points = []

def get_coords(event, x, y, flags, param):
    if event == cv2.EVENT_LBUTTONDOWN:
        points.append((x, y))
        print(f"Click: {x}, {y}")

cap = cv2.VideoCapture("video.mp4")

cv2.namedWindow("Video")
cv2.setMouseCallback("Video", get_coords)

while True:
    ret, frame = cap.read()
    if not ret:
        break

    # vẽ điểm đã click
    for p in points:
        cv2.circle(frame, p, 5, (0, 0, 255), -1)

    cv2.imshow("Video", frame)

    if cv2.waitKey(30) & 0xFF == ord('q'):
        break

cap.release()
cv2.destroyAllWindows()
import cv2

points = []

def get_coords(event, x, y, flags, param):
    if event == cv2.EVENT_LBUTTONDOWN:
        points.append((x, y))
        print(points)

cap = cv2.VideoCapture("video.mp4")

ret, frame = cap.read()   # 👈 CHỈ đọc 1 frame
if not ret:
    print("Không đọc được video")
    exit()

cv2.namedWindow("Frame 0")
cv2.setMouseCallback("Frame 0", get_coords)

while True:
    show = frame.copy()

    for p in points:
        cv2.circle(show, p, 5, (0, 0, 255), -1)

    cv2.imshow("Frame 0", show)

    key = cv2.waitKey(1) & 0xFF
    if key == ord('q'):   # nhấn q để thoát
        break

cap.release()
cv2.destroyAllWindows()

print("Tọa độ cuối cùng:", points)

Các sự kiện chuột hay dùng
Sự kiện	Mô tả
cv2.EVENT_LBUTTONDOWN	Nhấn chuột trái
cv2.EVENT_LBUTTONUP	Nhả chuột trái
cv2.EVENT_MOUSEMOVE	Di chuyển chuột
cv2.EVENT_RBUTTONDOWN	Nhấn chuột phải
ấy tọa độ khi di chuột (không cần click)
def mouse_callback(event, x, y, flags, param):
    if event == cv2.EVENT_MOUSEMOVE:
        print(x, y)
