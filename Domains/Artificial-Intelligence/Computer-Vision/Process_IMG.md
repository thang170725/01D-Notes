- [Kỹ thuật xử lý ảnh](#kỹ-thuật-xử-lý-ảnh)
  - [Normalization \& Formatting (chuẩn hóa dữ liệu)](#normalization--formatting-chuẩn-hóa-dữ-liệu)
    - [Resize (Thay đổi kích thước)](#resize-thay-đổi-kích-thước)
    - [Cropping (Cắt ảnh)](#cropping-cắt-ảnh)
    - [ROI (Region Of Interest)](#roi-region-of-interest)
    - [Center Crop / Random Crop](#center-crop--random-crop)
    - [Padding](#padding)
    - [Normalization (Chuẩn hóa pixel)](#normalization-chuẩn-hóa-pixel)
    - [Standardization (Chuẩn hóa theo mean/std)](#standardization-chuẩn-hóa-theo-meanstd)
    - [Color Space Conversion (RGB ↔ Gray ↔ HSV ↔ LAB)](#color-space-conversion-rgb--gray--hsv--lab)
    - [Channel Reordering (RGB ↔ BGR)](#channel-reordering-rgb--bgr)
  - [Tăng cường dữ liệu (Data Augmentation)](#tăng-cường-dữ-liệu-data-augmentation)
  - [Lọc \& cải thiện chất lượng ảnh](#lọc--cải-thiện-chất-lượng-ảnh)
  - [Biến đổi hình học (Geometric Transform)](#biến-đổi-hình-học-geometric-transform)
  - [Trích xuất đặc trưng truyền thống (Feature Engineering)](#trích-xuất-đặc-trưng-truyền-thống-feature-engineering)
  - [Chuẩn bị cho Deep Learning nâng cao](#chuẩn-bị-cho-deep-learning-nâng-cao)
- [data.yaml cho bộ dữ liệu tùy chỉnh](#datayaml-cho-bộ-dữ-liệu-tùy-chỉnh)
- [Đường dẫn gốc (tùy chọn, nếu không có, các đường dẫn dưới đây là tuyệt đối hoặc tương đối với thư mục hiện tại)](#đường-dẫn-gốc-tùy-chọn-nếu-không-có-các-đường-dẫn-dưới-đây-là-tuyệt-đối-hoặc-tương-đối-với-thư-mục-hiện-tại)
- [Đường dẫn tương đối đến thư mục ảnh huấn luyện (Training images)](#đường-dẫn-tương-đối-đến-thư-mục-ảnh-huấn-luyện-training-images)
- [Đường dẫn tương đối đến thư mục ảnh đánh giá (Validation images)](#đường-dẫn-tương-đối-đến-thư-mục-ảnh-đánh-giá-validation-images)
- [Đường dẫn tương đối đến thư mục ảnh kiểm thử (Test images) - Tùy chọn](#đường-dẫn-tương-đối-đến-thư-mục-ảnh-kiểm-thử-test-images---tùy-chọn)
- [test: images/test](#test-imagestest)
- [Số lượng lớp (classes)](#số-lượng-lớp-classes)
- [Tên của các lớp, phải theo thứ tự từ 0 đến nc-1](#tên-của-các-lớp-phải-theo-thứ-tự-từ-0-đến-nc-1)
- [1. Tải mô hình cơ sở (base model)](#1-tải-mô-hình-cơ-sở-base-model)
- [2. Định nghĩa đường dẫn đến file data.yaml của bạn](#2-định-nghĩa-đường-dẫn-đến-file-datayaml-của-bạn)
- [3. Bắt đầu quá trình huấn luyện](#3-bắt-đầu-quá-trình-huấn-luyện)
- [Tham số 'data' chỉ định vị trí của file cấu hình dữ liệu](#tham-số-data-chỉ-định-vị-trí-của-file-cấu-hình-dữ-liệu)
- [Tham số 'epochs' chỉ định số lần lặp lại huấn luyện](#tham-số-epochs-chỉ-định-số-lần-lặp-lại-huấn-luyện)
- [Tham số 'imgsz' chỉ định kích thước ảnh đầu vào](#tham-số-imgsz-chỉ-định-kích-thước-ảnh-đầu-vào)
- [--- Hoặc sử dụng nó để đánh giá mô hình đã huấn luyện ---](#----hoặc-sử-dụng-nó-để-đánh-giá-mô-hình-đã-huấn-luyện----)
- [metrics = model.val(data=data\_config\_file)](#metrics--modelvaldatadata_config_file)
---
# Kỹ thuật xử lý ảnh
## Normalization & Formatting (chuẩn hóa dữ liệu)
### Resize (Thay đổi kích thước)
```bash
Đưa ảnh về kích thước cố định (vd: 224x224)
```
### Cropping (Cắt ảnh)
```bash
Lấy vùng quan tâm (ROI)
```
### ROI (Region Of Interest)
```bash
- Trong cả bức ảnh / frame, mình chỉ quan tâm một vùng nào đó, còn lại thì kệ.
- Ví dụ:
    + Camera giao thông → chỉ quan tâm phần đường, không quan tâm bầu trời
    + Camera lớp học → chỉ quan tâm khu vực bảng
    + Camera an ninh → chỉ quan tâm cửa ra vào
- ROI không phải AI, nó là xử lý ảnh thuần.
```
### Center Crop / Random Crop
```bash
Tăng tính đa dạng dữ liệu
```
### Padding
```bash
Thêm viền để giữ tỉ lệ
```
### Normalization (Chuẩn hóa pixel)
```bash
- Đưa pixel về [0–1] hoặc [-1–1]
- Ứng dụng hầu hết Deep Learning model
```
### Standardization (Chuẩn hóa theo mean/std)
```bash
Giúp model hội tụ nhanh
```
### Color Space Conversion (RGB ↔ Gray ↔ HSV ↔ LAB)
```bash 
Thay đổi không gian màu để dễ trích đặc trưng
```
### Channel Reordering (RGB ↔ BGR)
```bash 
Phù hợp framework (OpenCV dùng BGR)
```
## Tăng cường dữ liệu (Data Augmentation)
9. Flip (Lật ảnh)

👉 Tăng dữ liệu
🎯 Classification

10. Rotation (Xoay)

👉 Giúp model không phụ thuộc góc
🎯 OCR, traffic sign

11. Translation (Dịch chuyển)

👉 Tăng tính robust
🎯 Object detection

12. Scaling (Phóng to/thu nhỏ)

👉 Tăng đa dạng kích thước
🎯 Detection

13. Shear (Biến dạng nghiêng)

👉 Tăng khả năng nhận diện biến dạng
🎯 OCR

14. Perspective Transform

👉 Giả lập góc nhìn
🎯 Nhận diện tài liệu

15. Random Erasing / Cutout

👉 Tăng khả năng chống che khuất
🎯 Classification

16. Mixup

👉 Trộn 2 ảnh
🎯 Giảm overfitting

17. CutMix

👉 Cắt ghép 2 ảnh
🎯 Object detection

18. Color Jitter

👉 Thay đổi sáng/tối/màu
🎯 Outdoor vision

19. Gaussian Noise

👉 Thêm nhiễu
🎯 Robust training

20. Blur (Gaussian / Motion)

👉 Giả lập ảnh mờ
🎯 Camera system

## Lọc & cải thiện chất lượng ảnh
1.  Gaussian Blur

👉 Giảm nhiễu
🎯 Preprocessing

22. Median Filter

👉 Loại bỏ salt-pepper noise
🎯 Medical image

23. Bilateral Filter

👉 Giữ cạnh khi làm mịn
🎯 Segmentation

24. Histogram Equalization

👉 Tăng tương phản
🎯 Ảnh tối

25. CLAHE

👉 Cân bằng tương phản cục bộ
🎯 X-quang

26. Sharpening

👉 Làm rõ cạnh
🎯 OCR

27. Denoising (Non-local means)

👉 Giảm nhiễu nâng cao
🎯 Low-light image

## Biến đổi hình học (Geometric Transform)
28. Affine Transform

👉 Xoay, scale, translate
🎯 Data augmentation

29. Homography

👉 Biến đổi mặt phẳng
🎯 AR, tài liệu

30. Warp Transform

👉 Biến dạng tự do
🎯 Face alignment

## Trích xuất đặc trưng truyền thống (Feature Engineering)
31. Edge Detection (Canny, Sobel)

👉 Phát hiện cạnh
🎯 Lane detection

32. HOG (Histogram of Oriented Gradients)

👉 Trích đặc trưng hình dạng
🎯 People detection

33. SIFT

👉 Keypoint matching
🎯 Image stitching

34. SURF

👉 Tương tự SIFT nhưng nhanh hơn
🎯 Object matching

35. ORB

👉 Keypoint nhanh, miễn phí
🎯 SLAM

36. LBP (Local Binary Pattern)

👉 Texture analysis
🎯 Face recognition

37. Gabor Filter

👉 Phân tích texture
🎯 Vân tay

VI. Phân đoạn & xử lý vùng
38. Thresholding

👉 Chuyển sang ảnh nhị phân
🎯 OCR

39. Adaptive Threshold

👉 Tách nền không đồng đều
🎯 Tài liệu scan

40. Otsu Threshold

👉 Tự động tìm ngưỡng
🎯 Segmentation

41. Morphology (Erode/Dilate)

👉 Làm sạch mask
🎯 Binary image

42. Opening/Closing

👉 Loại bỏ nhiễu nhỏ
🎯 Segmentation

## Chuẩn bị cho Deep Learning nâng cao
43. Image to Tensor

👉 Chuyển sang tensor
🎯 PyTorch, TensorFlow

44. Patch Extraction

👉 Cắt thành nhiều patch
🎯 Vision Transformer

45. Sliding Window

👉 Quét ảnh
🎯 Detection cổ điển

46. Multi-scale Input

👉 Cho nhiều kích thước
🎯 FPN, YOLO

47. Anchor Generation

👉 Tạo khung dự đoán
🎯 Object detection

VIII. Xử lý chuyên biệt
48. Face Alignment

👉 Căn chỉnh khuôn mặt
🎯 Face recognition

49. Background Removal

👉 Tách nền
🎯 E-commerce

50. Super Resolution

👉 Tăng độ phân giải
🎯 Ảnh vệ tinh

51. Depth Estimation Preprocess

👉 Chuẩn hóa stereo
🎯 3D vision

52. Optical Flow

👉 Tính chuyển động
🎯 Video AI

IX. Biến đổi miền tần số
53. FFT

👉 Phân tích tần số
🎯 Khử nhiễu

54. DCT

👉 Nén ảnh
🎯 JPEG

55. Wavelet Transform

👉 Phân tích đa tỉ lệ
🎯 Medical imaging

X. Tiền xử lý cho Transformer & LLM-Vision
56. Positional Encoding for Image

👉 Thêm thông tin vị trí
🎯 ViT

57. Tokenization ảnh (Patch Embedding)

👉 Biến ảnh thành chuỗi
🎯 Multimodal model

XI. Chuẩn bị dữ liệu nhãn
58. Bounding Box Normalization

👉 Chuẩn hóa tọa độ
🎯 YOLO

59. Mask Encoding (RLE)

👉 Mã hóa segmentation
🎯 COCO dataset

XII. Xử lý ảnh nâng cao AI hiện đại
60. Image Embedding Extraction

👉 Trích vector đặc trưng
🎯 CLIP search

61. Contrastive Preprocessing

👉 Chuẩn hóa cho contrastive learning
🎯 Self-supervised learning
Detection
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
YOLO ((You Only Look Once))
    • YOLO là một mô hình mạng nơ-ron tích chập (CNN) được thiết kế để thực hiện tác vụ phát hiện vật thể (Object Detection) trong thời gian thực. Cái tên "You Only Look Once" nói lên điểm cốt lõi: nó xử lý toàn bộ hình ảnh chỉ trong một lần duy nhất.
    • A. Ba phần chính của kiến trúc. Mô hình YOLO có cấu trúc tương tự như một dòng chảy dữ liệu qua 3 phần chính, hoạt động tuần tự:
        1. Backbone (Phần Trích xuất Đặc trưng)
            ▪ Mục đích: Hút các đặc trưng cơ bản từ ảnh (các cạnh, góc, hình dạng).
            ▪ Vị trí trong code: Các lớp từ (0) đến (9):
            ▪ Conv (Convolution): Lớp tích chập cơ bản, dùng để trích xuất đặc trưng.
            ▪ Conv2d(3, 16, kernel_size=(3, 3), stride=(2, 2)): Khởi đầu với ảnh 3 kênh màu (RGB), tạo ra 16 kênh đặc trưng, giảm kích thước ảnh (stride=2).
            ▪ C2f (Cross-Stage Partial Network): Là một khối kiến trúc quan trọng trong YOLO hiện đại (như YOLOv8). Nó giúp tăng hiệu suất bằng cách tách luồng đặc trưng ra hai nhánh và hợp nhất lại. Nó giúp mô hình học sâu hơn mà vẫn giữ được tốc độ.
            ▪ SPPF (Spatial Pyramid Pooling Fast): Lớp (9). Nó tổng hợp thông tin từ nhiều kích thước khác nhau của cùng một đặc trưng. Điều này giúp mô hình nhận diện vật thể bất kể kích thước của chúng (ví dụ: một chiếc xe ô tô to hay nhỏ trong ảnh).
       2. Neck (Phần Hợp nhất Đặc trưng)
            ▪ Mục đích: Kết hợp các đặc trưng đã học được từ các cấp độ sâu khác nhau của Backbone.
            ▪ Các lớp nông (gần đầu) có đặc trưng về chi tiết, vị trí chính xác.
            ▪ Các lớp sâu (gần cuối) có đặc trưng về ngữ cảnh, phân loại vật thể.
            ▪ Vị trí trong code: Các lớp từ (10) đến (21):
            ▪ Upsample (10, 13): Phóng to bản đồ đặc trưng từ lớp sâu lên.
            ▪ Concat (11, 14, 17, 20): Nối (ghép) bản đồ đặc trưng đã được phóng to với bản đồ đặc trưng tương ứng từ Backbone.
            ▪ Mô hình này sử dụng kiến trúc kiểu FPN/PAN: giúp các lớp dự đoán (Head) có được thông tin chi tiết lẫn thông tin ngữ cảnh.
        3. Head (Phần Dự đoán)
            ▪ Mục đích: Lấy các đặc trưng đã được hợp nhất từ Neck và chuyển chúng thành kết quả dự đoán cuối cùng.
            ▪ Vị trí trong code: Lớp (22) Detect(...).
            ▪ Đầu ra của Head:
            ▪ Hộp bao (Bounding Box): Toạ độ (x,y,w,h) của vật thể.
            ▪ Độ tin cậy vật thể (Objectness Score): Xác suất có vật thể trong hộp đó.
            ▪ Xác suất lớp (Class Probability): Xác suất vật thể đó thuộc về mỗi loại lớp (người, chó, xe hơi...).
            ▪ DFL (Distribution Focal Loss): Được sử dụng trong YOLOv8 để cải thiện độ chính xác của hộp bao bằng cách học cách phân phối khoảng cách tới các cạnh của hộp.

Segmentation
Không những detect nó sẽ tô màu lên vùng vật thể được detection.
Bài tập
Demo segmentation yolov8-seg
from ultralytics import YOLO
model = YOLO('model_detect/yolov8n-seg.pt')
res = model("img/predict_1.jpg")
for r in res:
    r.show()
Pose estimation
    • Là kỹ thuật dự đoán tọa độ các keypoints (điểm chính) trên đối tượng, ví dụ: Người: đầu, vai, khuỷu tay, cổ tay, hông, đầu gối, mắt cá chân… Vật thể: góc hộp, chân bàn, cánh tay robot…
    • Pose estimation thường chia thành:
        ◦ 2D Pose Estimation: Keypoints trong không gian 2D (x, y)
        ◦ 3D Pose Estimation: Keypoints có thêm độ sâu (x, y, z)
    • Nhận diện hành động người, phân tích thể thao, ứng dụng thể dục, làm phim, game, vfx, hệ thống giám sát & an ninh, robot, tương tác ảo, y học

Preprocessing (Các kỹ thuật tiền xử lý ảnh)
CLAHE (Contrast Limited Adaptive Histogram Equalization)
    • Mục đích chính của kỹ thuật này là tăng cường độ tương phản (contrast) cục bộ của hình ảnh.
    • Nó giúp làm nổi bật các chi tiết trong các vùng ảnh quá tối hoặc quá sáng mà các phương pháp tăng cường độ tương phản toàn cục (như Histogram Equalization truyền thống) không xử lý tốt, thậm chí còn gây ra nhiễu hoặc làm mất chi tiết.
    • Bạn nên sử dụng kỹ thuật CLAHE khi bạn có những bức ảnh gặp vấn đề về độ tương phản, đặc biệt là khi sự chênh lệch độ sáng (dynamic range) trong ảnh lớn hoặc có những vùng bị tối/sáng cục bộ.
    • Các trường hợp cụ thể thường áp dụng CLAHE bao gồm:
        ◦ Xử lý Ảnh Y học (Medical Imaging): Ảnh chụp X-quang, MRI, CT, ảnh soi đáy mắt (như trong chẩn đoán bệnh lý về mắt) thường có độ tương phản thấp hoặc có các vùng chi tiết cần làm nổi bật. CLAHE giúp tăng khả năng hiển thị các cấu trúc sinh học.
        ◦ Ảnh trong Điều kiện Ánh sáng Kém: Ảnh chụp trong điều kiện thiếu sáng hoặc có ánh sáng nền mạnh (backlit), nơi chi tiết bị "chìm" trong bóng tối hoặc bị "cháy" sáng.
        ◦ Hệ thống Thị giác Máy (Machine Vision) và Xử lý Ảnh: Khi cần tiền xử lý ảnh (preprocessing) để chuẩn hóa hoặc tăng cường chất lượng ảnh đầu vào trước khi đưa vào các thuật toán nhận dạng, phân loại, hoặc học sâu (Deep Learning/CNN). Việc này giúp thuật toán trích xuất đặc trưng (feature extraction) chính xác hơn.
        ◦ Ảnh Thiên văn hoặc Viễn thám: Ảnh vệ tinh hoặc ảnh chụp từ kính thiên văn thường cần CLAHE để làm rõ các cấu trúc và đặc điểm bề mặt.
    • Ưu điểm của CLAHE so với HE truyền thống
        ◦ CLAHE là một cải tiến của phương pháp Cân bằng Biểu đồ màu (Histogram Equalization - HE) truyền thống:
        ◦ Adaptive (Thích nghi): Thay vì áp dụng sự cân bằng độ tương phản cho toàn bộ ảnh, CLAHE chia ảnh thành nhiều ô (tiles/regions) nhỏ và áp dụng HE cho từng ô riêng biệt. Điều này giúp tăng cường độ tương phản cục bộ mà không làm ảnh hưởng đến các vùng khác.
        ◦ Contrast Limited (Giới hạn Độ tương phản): CLAHE có một tham số giới hạn (clip limit) để ngăn chặn việc độ tương phản bị tăng quá mức ở các vùng nhiễu (noise) hoặc các vùng có độ tương phản rất thấp, giúp tránh tình trạng nhiễu bị khuếch đại (over-amplification).
