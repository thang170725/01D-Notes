```bash
- OpenCV để xử lý hình ảnh và nó hỗ trợ vô số các thuật toán liên quan đến lĩnh vực thị giác máy tính và lĩnh vực học máy. Nó có thể sử dụng card đồ họa (GPU) để xử lý nhằm tăng tốc độ xử lý.
- Cần pip install opencv-python, import cv2
```



Computer Vision
Kênh  màu
    • Mặc định Opencv sử dụng kênh màu BGR.
    • Vì OpenCV ban đầu đưuọc viết bằng C/C++ và theo chuẩn xử lý ảnh của Windows Bitmap (BMP) - vốn lưu pixel theo thứ tự BGR. Để tăng hiệu suất và tránh chuyển đổi không cần thiết, OpenCV giữ nguyên thứ tự này.
    • Khi đọc ảnh từ file, OpenCV đọc pixel theo thứ tự BGR để tránh tốn tài nguyên chuyển đổi qua lại nếu bạn xử lý nhiều ảnh ở cấp hệ thống.
Segmentation mask là gì?
    • Là một ảnh đen trắng (hoặc đa kênh) dùng để biểu diện phân vùng (vật thể hoặc khu vực) trong ảnh gốc
        ◦ Mỗi pixel trong mask cho biết vật thể nào (hoặc lớp nào) nó thuộc về.
        ◦ Có 2 loại phổ biến:
            ▪ binary mask: pixel=1 nếu thuộc vật thể, 0 nếu là nền.
            ▪ multi-class mask: pixel =0,1,2,… tương ứng với các lớp khác nhau (mèo, chó, người, …).
    • Không phụ thuộc vào màu sắc, mà phụ thuộc vào nhãn mà bạn gán khi huấn luyện mô hình.
Multi-channel image
Là ảnh có nhiều kênh màu.
Depth - Độ sâu
    • Là số lớp (layers) trong mô hình.
    • Tăng depth → mô hình học được tính chất phức tạp hơn.
Width - Độ rộng
    • Là số lương filters (kernels) mỗi lớp convolution.
    • Tăng width → mỗi lớp trích xuất ddwuocj nhiều đặc trưng hơn.
    • Ví dụ: Có nhiều người cùng quan sát vào một ảnh → mỗi người chú ý vào đặc điểm khác nhau.
Resolution - Độ phân giải ảnh
    • Là kích thước ảnh đầu vào (224x224 → 380x380).
    • Tăng resolution → mô hình nhìn thấy chi tiết nhỏ hơn.
    • Ví dụ: Cùng một bức tranh, nếu ảnh lớn hơn thì nhìn rõ mắt, mũi, lông mi, ...
Kernel
    • Phần lớn các bộ lọc đều dựa trên khái niệm convolution (tích chập) – tức là áp một ma trận (kernel) lên từng vùng nhỏ của ảnh để tính toán giá trị mới cho pixel trung tâm. Cách áp dụng kernel này có một quy tắc chuẩn:
    • Duyệt từng pixel trong ảnh gốc.
    • Với mỗi pixel, lấy vùng lân cận (theo kích thước kernel), nhân chéo với kernel.
    • Tính tổng và gán giá trị kết quả vào pixel tương ứng trong ảnh mới.
Ví dụ:
Với bộ lọc làm mờ trung bình (mean blur), kernel là ma trận các số bằng nhau, cộng lại rồi chia trung bình.
 Sự khác nhau của các bộ lọc:
Tùy loại bộ lọc mà kernel hoặc cách áp dụng sẽ khác nhau:
Bộ lọc
Cách hoạt động đặc trưng
Làm mờ (blur)
Tính trung bình vùng lân cận – làm giảm chi tiết, nhiễu.
Gaussian Blur
Dùng kernel theo phân phối Gauss – làm mờ mịn, tự nhiên hơn.
Median Blur
Lấy giá trị trung vị trong vùng lân cận – khử nhiễu muối tiêu.
Sharpen (làm sắc nét)
Dùng kernel làm nổi bật cạnh, tăng tương phản cục bộ.
Sobel, Laplacian
Dùng để phát hiện biên cạnh – áp kernel đạo hàm.
Bộ lọc tùy chỉnh
Người dùng định nghĩa kernel riêng và áp dụng tương tự.
Bài tập
Cho một ma trận ảnh 5×5 và một kernel 3×3, hãy tính kết quả tích chập (convolution)
import numpy as np

img = np.array([
    [1,2,3,4,5], 
    [6,7,8,9,10],
    [11,12,13,14,15],
    [16,17,18,19,20],
    [21,22,23,24,25]
])
kernel = np.array([
    [2,4,6],
    [1,2,3],
    [3,4,5]
])

h, w = img.shape
kh, kw = kernel.shape
out_h = h - kh + 1
out_w = w - kw + 1

# ✅ Tạo mảng kết quả có kích thước sẵn
out = np.zeros((out_h, out_w))

for i in range(out_h):
    for j in range(out_w):
        out[i, j] = np.sum(img[i:i+kh, j:j+kw] * kernel)

print(out)
[[178. 202. 226.]
 [298. 322. 346.]
 [418. 442. 466.]]
Chuẩn hóa
Bài tập
Chuẩn hóa ảnh về [0,1]
x_train = x_train.astype('float32') / 255.0
x_test  = x_test.astype('float32') / 255.0


ResizeWindow()
Dùng để thay đổi kích thước cửa sổ hiển thị 
Cú pháp:
import cv2

img = cv2.imread("image.jpg")

cv2.namedWindow("window", cv2.WINDOW_NORMAL)   # cho phép resize
cv2.resizeWindow("window", 800, 600)           # set kích thước cửa sổ

cv2.imshow("window", img)
cv2.waitKey(0)
cv2.destroyAllWindows()


Rectangle()
Dùng để vẽ hình chữ nhật
Cú pháp:
cv2.rectangle(
    frame,
    pt1=(x1, y1),
    pt2=(x2, y2),
    color=(0, 255, 0),
    thickness=2
)

Dùng để vẽ đa giác
Cú pháp:
pts = np.array([
    [300, 700],
    [600, 400],
    [1200, 400],
    [1600, 700]
], np.int32)

cv2.polylines(frame, [pts], True, (255, 0, 0), 2)
FillPoly()
Dùng để tạo mask

mask = np.zeros(frame.shape[:2], dtype=np.uint8)
cv2.fillPoly(mask, [pts], 255)
bitwise_and()
Dùng để áp mask ROI

roi = cv2.bitwise_and(frame, frame, mask=mask)
PointPolygonTest()
Kiểm tra điểm có nằm trong ROI không. Dùng để: Check bbox center có trong ROI khôn

cx, cy = 500, 600
inside = cv2.pointPolygonTest(pts, (cx, cy), False)

if inside >= 0:
    print("Object inside ROI")
InRange()
ROI theo màu (nâng cao) Thường dùng cho:

Làn đường

Biển báo

Vạch kẻ

mask = cv2.inRange(hsv, lower, upper)
FindContours()
ROI dựa trên hình dạngDùng khi:

ROI không cố định

ROI sinh ra từ segmentation

contours, _ = cv2.findContours(mask, cv2.RETR_EXTERNAL, cv2.CHAIN_APPROX_SIMPLE)
BoundingRect()
chuyển contour → ROI rectangle

x, y, w, h = cv2.boundingRect(cnt)
roi = frame[y:y+h, x:x+w]
GetPerspectiveTransform()
    • Dùng để tính toán một ma trận chuyển đổi kích thước 3×3 (gọi là ma trận biến đổi phối cảnh). 
    • Ma trận này cho phép bạn chuyển một vùng hình ảnh từ góc nhìn nghiêng (3D perspective) về một góc nhìn thẳng từ trên xuống (2D bird's-eye view).
Cú pháp:
M = cv2.getPerspectiveTransform(
   src, 
   dst
)
    • src: Mảng chứa tọa độ 4 điểm trên hình ảnh gốc (ảnh bị nghiêng). kiểu np.float32
    • dst: Mảng chứa tọa độ 4 điểm tương ứng trên hình ảnh đích (hình chữ nhật chuẩn).
    • M: Kết quả trả về là ma trận 3×3. kiểu np.float32
import cv2
import numpy as np

# 1. Tọa độ 4 điểm góc của sân trên ảnh gốc (ảnh nghiêng)
# Thứ tự: Top-Left, Top-Right, Bottom-Right, Bottom-Left
pts_src = np.array([
    [200, 150], [450, 150], 
    [550, 450], [100, 450]
], dtype="float32")

# 2. Tọa độ 4 điểm tương ứng bạn muốn hiển thị trên ảnh mới (hình chữ nhật)
# Giả sử ta muốn kết quả là ảnh 300x500
width, height = 300, 500
pts_dst = np.array([
    [0, 0], [width, 0], 
    [width, height], [0, height]
], dtype="float32")

# 3. Tính ma trận biến đổi M
M = cv2.getPerspectiveTransform(pts_src, pts_dst)

# 4. Áp dụng ma trận M để biến đổi ảnh (warp)
# Giả sử 'img' là ảnh đầu vào của bạn
# result = cv2.warpPerspective(img, M, (width, height))

print("Ma trận biến đổi M:")
print(M)

PerspectiveTransform()
    • Dùng để tính toán tọa độ mới của các điểm (tập hợp các điểm x, y).
    • Ví dụ: Trong bài toán sân cầu lông, hàm này cực kỳ hữu ích để bạn lấy tọa độ quả cầu hoặc vận động viên trên camera rồi chuyển nó thành tọa độ x,y trên sơ đồ sân 2D.
Cú pháp:
dst_points = cv2.perspectiveTransform(src_points, M)
    • src_points: Mảng các điểm cần chuyển đổi.
        ◦ Lưu ý cực kỳ quan trọng: Mảng này phải có cấu trúc 3 chiều với định dạng (N, 1, 2), trong đó N là số lượng điểm. Kiểu dữ liệu phải là float32.
    • M: Ma trận biến đổi 3×3 (đã tính được từ hàm cv2.getPerspectiveTransform).
    • dst_points: Kết quả trả về là tọa độ các điểm sau khi đã "trải phẳng" về 2D.
import cv2
import numpy as np

# --- Bước 1: Giả lập ma trận M (thực tế bạn lấy từ getPerspectiveTransform) ---
# Tọa độ 4 góc sân trên Camera (ảnh bị nghiêng)
src_corners = np.array([[100, 100], [500, 100], [600, 500], [0, 500]], dtype="float32")
# Tọa độ 4 góc sân trên sơ đồ 2D (hình chữ nhật chuẩn)
dst_corners = np.array([[0, 0], [610, 0], [610, 1340], [0, 1340]], dtype="float32")

M = cv2.getPerspectiveTransform(src_corners, dst_corners)

# --- Bước 2: Tọa độ một điểm cụ thể cần map (ví dụ: Quả cầu) ---
# Giả sử quả cầu đang ở tọa độ (300, 400) trên frame camera
ball_x, ball_y = 300, 400

# Chuyển điểm về định dạng mảng 3 chiều (N, 1, 2)
points_to_map = np.array([[[ball_x, ball_y]]], dtype="float32")

# --- Bước 3: Sử dụng perspectiveTransform ---
mapped_points = cv2.perspectiveTransform(points_to_map, M)

# Lấy kết quả x, y mới
new_x = mapped_points[0][0][0]
new_y = mapped_points[0][0][1]

print(f"Tọa độ gốc trên Camera: ({ball_x}, {ball_y})")
print(f"Tọa độ sau khi map vào sân 2D: ({new_x:.2f}, {new_y:.2f})")

# --- Bonus: Map nhiều điểm cùng lúc ---
# Nếu bạn có cả tọa độ cầu và 2 người chơi
many_points = np.array([
    [[300, 400]], # Quả cầu
    [[150, 450]], # Người chơi A
    [[450, 200]]  # Người chơi B
], dtype="float32")

mapped_many = cv2.perspectiveTransform(many_points, M)
print("\nDanh sách các điểm đã map:")
for i, pt in enumerate(mapped_many):
    print(f"Điểm {i+1}: {pt[0]}")
MinAreaRect()
Hàm này tìm một hình chữ nhật bao quanh có diện tích nhỏ nhất cho một tập hợp điểm. Khác với cv2.boundingRect (luôn thẳng đứng), minAreaRect có thể xoay theo hướng của vật thể.
Cú pháp:

.get()
Lấy kích thước của video
Cú pháp:
cap.get(input)
    • cv2.CAP_PROP_FPS: lấy ra tốc độ của video gốc
    • cv2.CAP_PROP_FRAME_WIDTH: lấy chiều rộng của video
    • cv2.CAP_PROP_FRAME_HEIGHT: Lấy chiều cao của video
import cv2

cap = cv2.VideoCapture('video/output.mp4')

width  = int(cap.get(cv2.CAP_PROP_FRAME_WIDTH))
height = int(cap.get(cv2.CAP_PROP_FRAME_HEIGHT))

print(height, width)

[]

import cv2
def main():
    # Load an image
    image = cv2.imread('night.jpg')
    # Check if the image was loaded successfully
    if image is None:
        print("Error: Could not load image.")
        return
    else:
        # lấy màu ở tọa độ (50, 50)
        b, g, r = image[50, 50]
        print(f"Pixel value at (50, 50): B={b}, G={g}, R={r}")
        return
main()
Pixel value at (50, 50): B=188, G=96, R=83
import cv2
def main():
    # Load an image
    image = cv2.imread('night.jpg')
    # Check if the image was loaded successfully
    if image is None:
        print("Error: Could not load image.")
        return
    else:
        imageCut = image[50:100, 1000:1500]
        cv2.imshow('Image Cut', imageCut)
        cv2.waitKey(0)
        cv2.destroyAllWindows()
        return
main()
# ảnh được lưu dưới dạng mảng numpy 2d
# chiều cao: y2 – y1
# chiều rộng: x2 – x1
red_values = img[0:3, 0:3, 2]
# Lấy ra ma trận 3x3 chữa giá trị cường độ của màu đỏ
Ví dụ
import cv2
def main():
    # Load an image
    image = cv2.imread('night.jpg', cv2.IMREAD_GRAYSCALE)
    # Check if the image was loaded successfully
    if image is None:
        print("Error: Could not load image.")
        return
    # Display the image in a window
    cv2.imshow('Image Ha Long Bay', image)

    while True:
        # Wait for a key press
        key = cv2.waitKey(0) & 0xFF
        # If 'q' is pressed, exit the loop
        if key == ord('n'):
            print("Exiting...")
            cv2.destroyAllWindows()
            break # Exit the loop and close the window
        else: print("you pressed:", chr(key))
main()
# code này để hiển thị hình ảnh và bấm phím n để thoát hình ảnh
# nếu không có vòng lặp while thì chương trình chỉ bắt kết quả đúng một lần từ bàn phím rồi sau đó kết thúc chương trình, hình ảnh sẽ tự động tắt khi hàm main() kết thúc kể cả có bấm đúng phím hay không
# vòng lặp while để giữ cho chương trình luôn chạy đến khi nào bấm đúng phím ‘n’ thì mới thôi.
Lưu ý: imshow() chỉ sử dụng dụng được chữ viết không dấu, không hỗ trợ hiển thị văn bản Unicode (tiếng việt) trực tiếp trong tiêu đề cửa sổ. Hàm imshow() chỉ hỗ trợ chuỗi ASCII. Tuy nhiên, bạn có thể khắc phục bằng cách tạo một cửa sổ riêng bằng thư viện khác như tkiner hoặc vẽ chữ tiếng việt trực tiếp lên ảnh bằng pillow (với font hỗ trợ unicode)
Cách tốt nhất là dùng pillow + cv2 để hiển thị hình ảnh với chữ tiếng việt.
Code thuần làm mờ ảnh
import numpy as np
import cv2
img = cv2.imread('anh3.jpg')
kernel = np.array([
    [1,2,1],
    [2,4,2],
    [1,2,1]
], dtype=np.float32)/16
h, w, c = img.shape
blurred = np.zeros_like(img)

for y in range(1,h-1):
    for x in range(1,w-1):
        for ch in range(3):
            region = img[y-1:y+2, x-1:x+2, ch]
            blurred[y,x,ch] = np.sum(region*kernel)
# Cắt giá trị vượt giới hạn (0-255)
blurred = np.clip(blurred, 0, 255).astype(np.uint8)

# Hiển thị
cv2.imshow('Original', img.astype(np.uint8))
cv2.imshow('Blurred', blurred)
cv2.waitKey(0)
cv2.destroyAllWindows()

# 
Dùng để làm mờ ảnh, cách hoạt động giống với gaussianBlur chỉ khác là ma trận kernel.
# blur() & GaussianBlur()
Đều dùng để làm mờ ảnh nhưng có những cách sử lý làm mờ khác nhau mà tác dụng cũng khác nhau
**GaussianBlur**
**Syn**
```bash
cv2.GaussianBlur(src=, ksize=, sigmaX=0)
- src: ảnh gốc (ảnh đầu vào).
- ksize: bộ lọc (kernel size), dạng (width, height), phải là số lẻ (ví dụ: (5,5)).
- sigmaX: độ lệch chuẩn theo trục X.
```
Cách hoạt động:
Giả sử chúng ta muốn tính giá trị của pixel tại vị trí (1,1), giá trị 60 trong ví dụ. Chúng ta sẽ đặt môt kernel 3x3 lên ma trận ảnh sao cho trung tâm của kernel đó trùng với pixel(1,1).
Các pixel xung quanh pixel (1,1) trong ma trận ảnh gốc sẽ là:

Bây giờ, chúng ta sẽ thực hiện phép tích chập:
Giá trị pixel mới tại (1,1) sẽ là: (10×0.0625)+(20×0.125)+(30×0.0625)+ (50×0.125)+(60×0.25)+(70×0.125)+ (90×0.0625)+(100×0.125)+(110×0.0625)
=0.625+2.5+1.875+ 6.25+15+8.75+ 5.625+12.5+6.875
=65
Vậy, giá trị pixel mới tại vị trí (1,1) trong ma trận kết quả sẽ là 65.
import cv2
anh = cv2.imread('anh1.jpg', -1)
blur = cv2.GaussianBlur(anh, (11,11), 0)
cv2.imshow("anh", blur)
cv2.waitKey(0)
cv2.destroyAllWindows()
# (11,11) là độ mờ, số càng lớn mờ càng nhiều, số này phải là số lẻ
MedianBlur()
    • Median là bộ loc giảm nhiễu, đặc biệt hiệu quả với “salt & pepper noise” nhiễu muối tiêu - tức là các điểm trắng/đen ngẫu nhiên.
Cách hoạt động:
    • Với mỗi pixel trong ảnh, ta lấy một vùng lân cận (3x3, 5x5, …)
    • sắp xếp tất cả cấc giá trị pixel trong vùng đó theo thứ tự.
    • Thay pixel trung tâm bằng giá trị median của vùng đó.
import cv2

img = cv2.imread('anh3.jpg')
cv2.imshow("original", img)

median = cv2.medianBlur(img, 5)
cv2.imshow("test", median)
cv2.waitKey(0)
cv2.destroyAllWindows()
Canny()
Là hàm dùng để phát hiện cạnh trong ảnh, rất phổ biến và hiệu quả.
Cú pháp: edges = cv2.Canny(image, threshold1, threshold2)
    • image: ảnh đầu vào (thường là ảnh xám – grayscale).
    • threshold1, threshold2: ngưỡng dưới và trên để xác định cạnh.
Các bước hoạt động:
    1. Làm mờ ảnh bằng bộ lọc gaussian: Giảm nhiễu, nhiễu có thể gây ra các cạnh giả.
    2. Tính toán gradient cường độ và hướng gradient: Xác định các vùng có sự thay đổi cường độ sáng lớn nhất.
    3. Làm trong hướng
    4. Loại bỏ các điểm không phải là cực đại cục bộ.
    5. Ngưỡng kép.
    6. Theo dõi cạnh bằng độ trễ
import cv2
anh = cv2.imread('anh1.jpg', 0)
edge = cv2.Canny(anh, 100,200)
cv2.imshow("anh", edge)
cv2.waitKey(0)
cv2.destroyAllWindows()

# cvtColor()
Là hàm dùng để chuyển đổi không gian màu của ảnh, ví dụ từ ảnh màu ảnh xám, RGB sang HSV, …
**Syn** 
```bash
dst = cv2.cvtColor(src, code)
- src: ảnh gốc (đầu vào).
- code: mã chuyển đổi màu, ví dụ:
    + cv2.COLOR_BGR2GRAY: chuyển ảnh từ BGR sang ảnh xám.
    + cv2.COLOR_BGR2RGB: chuyển từ BGR (mặc định OpenCV) sang RGB.
    + cv2.COLOR_BGR2HSV: chuyển từ BGR sang HSV.
```
**Ex**
```python
import cv2
anh = cv2.imread('anh1.jpg')
gray = cv2.cvtColor(anh, cv2.COLOR_BGR2GRAY)
cv2.imshow("anh", gray)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

## chuyển ảnh màu sang ảnh đen trắng
```python
import cv2
anh = cv2.imread('anh1.jpg')
gray = cv2.cvtColor(anh, cv2.COLOR_BGR2GRAY)
inv = 255 - gray
cv2.imshow("anh", inv)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

divide()
Dùng để chia từng pixel của 2 ảnh (hoặc ảnh với số) – hay dùng làm ảnh sáng, tạo hiệu ứng ảnh phác thảo (sketch).
Cú pháp: output = cv2.divide(src1, src2[, scale])
    • src1, src2: hai ảnh cùng kích thước.
    • scale (tùy chọn): hệ số nhân sau khi chia (mặc định = 1).
import cv2
gray = cv2.imread('anh1.jpg', 0)
inv = 255 - gray
blur = cv2.GaussianBlur(inv, (21,21), 0)
sketch = cv2.divide(gray, 255-blur, scale=256)
cv2.imshow("anh", sketch)
cv2.waitKey(0)
cv2.destroyAllWindows()
# giống hiệu ứng nét bút chì
filter2D()
Dùng để áp dụng để áp dụng bộ lọc tùy chỉnh lên ảnh – giúp làm mờ, làm sắc nét, phát hiện cạnh, …
Cú pháp: dst = cv2.filter2D(src, depth, kernel)
    • src: ảnh đầu vào.
    • depth: độ sâu ảnh đầu ra (-1 để giữ nguyên độ sâu ảnh gốc).
    • kernel: ma trận lọc (numpy array), ví dụ:
kernel = np.array([[0, -1, 0],
                   [-1, 5, -1],
                   [0, -1, 0]])
import cv2
import numpy as np
img = cv2.imread('anh1.jpg')
kernel = np.array([[0,-1,0],
                  [-1,5,-1],
                  [0,-1,0]])
sharrpend = cv2.filter2D(img, -1, kernel)
cv2.imshow("anh", sharrpend)
cv2.waitKey(0)
cv2.destroyAllWindows()
# làm sắc nét ảnh
bilateralFilter()
    • Bilateral filter (lọc song phương) là một bộ lọc phi tuyến tính, thực hiện làm mịn ảnh bằng cách kết hợp thông tịn không gian và cường độ màu (độ sáng) của điểm ảnh. Nó giữ cạnh rõ ràng vì:
        ◦ Không làm mờ các pixel có giá trị màu khác biệt lớn (ví dụ tại rìa cạnh).
        ◦ Chỉ làm mịn các pixel có màu tương tự và nằm gần nhau.
    • Hiểu đơn giản thì nó dùng một kernel có thể thay đổi giá trị. kernel này chứa
        ◦ Gaussian theo không gian -> đảm bảo các điểm gần được ưu tiên.
        ◦ Gaussian theo độ sáng -> loại bỏ các pixel có độ sáng quá khác biệt.
Cú pháp: cv2.bilateralFilter(src, d, sigmaColor, sigmaSpace)
    • src: Ảnh đầu vào.
    • d: Đường kính của pixel lân cận (cửa sổ) - ma trận kernel  
    • sigmaColor: Độ nhạy với khác biệt màu. Càng lớn thì càng mịn, bỏ qua sự khác biệt màu nhỏ. - kiểm soát mức độ quan tâm đến độ khác biệt màu sắc. 
    • sigmaSpace: Độ nhay với khoảng cách không gian. Càng lớn thì ảnh hưởng pixel xa hơn càng nhiều - Kiểm soát khaongr cách không gian trong kernel.
Dùng để:
    • Làm mịn ảnh mà vẫn giữ được cạnh sắc nét (khác với Gaussian blur).
    • Tiền xử lý cho nhận diện khuôn mặt, OCR, …
    • Trong làm đẹp ảnh (beautify filter).
    • Tách nền / foreground-background segmentation.
    • Trước khi phân đoạn ảnh (image segmentation)
Công thức:
I(filtered)​(i,j)=(1/W)(k,l∑​I(k,l))⋅Gs​(∥(k,l)−(i,j)∥)⋅Gr​(∣I(k,l)−I(i,j)∣)
Bài tập
Mở video từ file
import cv2

cap = cv2.VideoCapture(r'E:\video\Một chút chill.mp4')
if not cap.isOpened():
    print("Không thể mở video")
exit()

while True:
    ret, frame = cap.read()
    if not ret:
        print("Không thể đọc video hoặc đã hết video")
        break
    cv2.imshow(frame)
    if cv2.waitKey(25) & 0xFF == ord('q'):
        print("Bạn đã nhấn 'q', thoát...")
        break
cap.release()
cv2.destroyAllWindows()
