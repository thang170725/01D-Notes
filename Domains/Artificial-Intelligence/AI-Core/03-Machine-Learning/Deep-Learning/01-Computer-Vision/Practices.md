Cách tạo và sử dụng file data.yaml
    • File data.yaml là file cấu hình bắt buộc khi bạn muốn huấn luyện mô hình YOLOv8 trên bộ dữ liệu tùy chỉnh của mình.
    • File này có nhiệm vụ thông báo cho mô hình YOLO biết:
        ◦ Vị trí của dữ liệu: Đường dẫn đến các tập tin ảnh và nhãn (labels) cho huấn luyện, đánh giá và kiểm thử.
        ◦ Số lượng lớp (classes): Tổng số loại đối tượng mà mô hình cần học cách nhận diện.
        ◦ Tên của các lớp: Tên dễ đọc của từng loại đối tượng (ví dụ: person, car, dog).
    • File data.yaml là một file văn bản thuần túy và phải tuân theo cú pháp YAML.
Ví dụ:
Giả sử bạn có một thư mục chứa dữ liệu có tên là my_custom_dataset. Cấu trúc file mẫu sẽ trông như sau:
# data.yaml cho bộ dữ liệu tùy chỉnh

# Đường dẫn gốc (tùy chọn, nếu không có, các đường dẫn dưới đây là tuyệt đối hoặc tương đối với thư mục hiện tại)
path: /path/to/my_custom_dataset 

# Đường dẫn tương đối đến thư mục ảnh huấn luyện (Training images)
train: images/train 

# Đường dẫn tương đối đến thư mục ảnh đánh giá (Validation images)
val: images/val 

# Đường dẫn tương đối đến thư mục ảnh kiểm thử (Test images) - Tùy chọn
# test: images/test 

# Số lượng lớp (classes)
nc: 2 

# Tên của các lớp, phải theo thứ tự từ 0 đến nc-1
names: ['cat', 'dog']

Cú pháp:
from ultralytics import YOLO

# 1. Tải mô hình cơ sở (base model)
model = YOLO('yolov8n.pt')  # Sử dụng mô hình nano (n)

# 2. Định nghĩa đường dẫn đến file data.yaml của bạn
data_config_file = 'my_custom_dataset/data.yaml' 

# 3. Bắt đầu quá trình huấn luyện
# Tham số 'data' chỉ định vị trí của file cấu hình dữ liệu
# Tham số 'epochs' chỉ định số lần lặp lại huấn luyện
# Tham số 'imgsz' chỉ định kích thước ảnh đầu vào
print(f"Bắt đầu huấn luyện mô hình với cấu hình dữ liệu: {data_config_file}")

results = model.train(
    data=data_config_file, 
    epochs=100, 
    imgsz=640
)

print("Quá trình huấn luyện đã hoàn thành.")

# --- Hoặc sử dụng nó để đánh giá mô hình đã huấn luyện ---
# metrics = model.val(data=data_config_file)
# Demo Canny
```python
import sys
import cv2
import numpy as np

class Canny:
    def __init__(self, img):


# ----- 1) Làm mượt: Gaussian hoặc Median -----
def denoise(img, use_median=False, ksize=5, sigma=1.4):
    if use_median:
        # Giữ biên tốt, hợp với nhiễu muối tiêu
        return cv2.medianBlur(img, ksize)
    else:
        # Chuẩn của Canny (ổn định, hợp với nhiễu Gaussian)
        return cv2.GaussianBlur(img, (ksize, ksize), sigma)

# ----- 2) Tính gradient bằng Sobel -----
def sobel_gradients(img):
    gx = cv2.Sobel(img, cv2.CV_64F, 1, 0, ksize=3)
    gy = cv2.Sobel(img, cv2.CV_64F, 0, 1, ksize=3)
    mag = np.hypot(gx, gy)  # sqrt(gx^2 + gy^2)
    mag = mag / (mag.max() + 1e-8) * 255.0  # scale về [0,255]
    angle = np.degrees(np.arctan2(gy, gx))
    angle[angle < 0] += 180.0  # về [0,180)
    return mag.astype(np.float32), angle.astype(np.float32)

# ----- 3) Non-maximum Suppression (làm mảnh cạnh) -----
def non_max_suppression(mag, angle):
    H, W = mag.shape
    Z = np.zeros((H, W), dtype=np.float32)
    # Quy tròn hướng về 4 hướng: 0, 45, 90, 135
    for i in range(1, H-1):
        for j in range(1, W-1):
            q = 255
            r = 255
            a = angle[i, j]

            # 0 độ
            if (0 <= a < 22.5) or (157.5 <= a <= 180):
                q = mag[i, j+1]
                r = mag[i, j-1]
            # 45 độ
            elif (22.5 <= a < 67.5):
                q = mag[i+1, j-1]
                r = mag[i-1, j+1]
            # 90 độ
            elif (67.5 <= a < 112.5):
                q = mag[i+1, j]
                r = mag[i-1, j]
            # 135 độ
            elif (112.5 <= a < 157.5):
                q = mag[i-1, j-1]
                r = mag[i+1, j+1]

            if (mag[i, j] >= q) and (mag[i, j] >= r):
                Z[i, j] = mag[i, j]
            else:
                Z[i, j] = 0.0
    return Z

# ----- 4) Double Threshold -----
def double_threshold(img, low, high, weak_val=75, strong_val=255):
    res = np.zeros_like(img, dtype=np.uint8)
    strong = img >= high
    weak = (img >= low) & (img < high)
    res[strong] = strong_val
    res[weak] = weak_val
    return res, weak_val, strong_val

# ----- 5) Hysteresis (nối cạnh yếu có liên thông với cạnh mạnh) -----
def hysteresis(img, weak_val=75, strong_val=255):
    H, W = img.shape
    out = img.copy()
    # Duyệt 8-láng giềng
    changed = True
    while changed:
        changed = False
        for i in range(1, H-1):
            for j in range(1, W-1):
                if out[i, j] == weak_val:
                    if np.any(out[i-1:i+2, j-1:j+2] == strong_val):
                        out[i, j] = strong_val
                        changed = True
    # Weak còn lại coi là 0
    out[out != strong_val] = 0
    return out

def main():
    if len(sys.argv) < 2:
        print("Usage: python canny_demo.py <image_path>")
        return

    path = sys.argv[1]
    gray = cv2.imread(path, cv2.IMREAD_GRAYSCALE)
    if gray is None:
        print("Không đọc được ảnh:", path)
        return

    # Chọn True để thử Median thay Gaussian
    USE_MEDIAN = False

    # 1) Denoise
    blur = denoise(gray, use_median=USE_MEDIAN, ksize=5, sigma=1.4)

    # 2) Sobel
    mag, angle = sobel_gradients(blur)

    # 3) NMS
    nms = non_max_suppression(mag, angle)

    # 4) Double threshold (chỉnh low/high theo ảnh)
    dt, WEAK, STRONG = double_threshold(nms, low=50, high=100)

    # 5) Hysteresis
    edges_custom = hysteresis(dt, weak_val=WEAK, strong_val=STRONG)

    # So sánh với Canny của OpenCV
    edges_cv = cv2.Canny(blur, 100, 200)

    # Hiển thị
    cv2.imshow("0. Input (Grayscale)", gray)
    cv2.imshow("1. Blur (Gaussian/Median)", blur)
    cv2.imshow("2. Gradient Magnitude (Sobel)", mag.astype(np.uint8))
    cv2.imshow("3. Non-Max Suppression", nms.astype(np.uint8))
    cv2.imshow("4. Double Threshold (weak=75,strong=255)", dt)
    cv2.imshow("5. Hysteresis (Final Edges)", edges_custom)
    cv2.imshow("Canny (OpenCV)", edges_cv)

    print("Bấm phím bất kỳ để thoát…")
    cv2.waitKey(0)
    cv2.destroyAllWindows()

if __name__ == "__main__":
    main()
```