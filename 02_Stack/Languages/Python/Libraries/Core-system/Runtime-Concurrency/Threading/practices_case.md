Xử lý đa luồng & đa tiến trình
Bài tập
Demo threading với đọc và hiển thị camera
import cv2
import threading
import time

cap = cv2.VideoCapture(0)
frame = None
running = True

def read_camera():
    global frame
    while running:
        time.sleep(0.1)          # giả lập camera chậm
        ret, f = cap.read()
        if ret:
            frame = f

t = threading.Thread(target=read_camera, daemon=True)
t.start()

while True:
    if frame is not None:
        cv2.imshow("Demo", frame)

    if cv2.waitKey(1) & 0xFF == ord('q'):
        running = False
        break

cap.release()
cv2.destroyAllWindows()

