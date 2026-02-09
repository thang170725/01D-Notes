# Hàm in mã ASCII của phím bấm (dùng OpenCV)
```python
import cv2
import numpy as np

def print_ascii_key():
    img = np.zeros((200, 400, 3), dtype=np.uint8)
    cv2.putText(img, "Press any key (ESC to exit)",
                (20, 100),
                cv2.FONT_HERSHEY_SIMPLEX,
                0.6, (255, 255, 255), 1)

    while True:
        cv2.imshow("Key ASCII Detector", img)
        key = cv2.waitKey(0) & 0xFF   # đợi bấm phím

        print(f"Key pressed: ASCII = {key}, char = {chr(key) if key < 128 else 'N/A'}")

        if key == 27:  # ESC
            break

    cv2.destroyAllWindows()

print_ascii_key()
```