- [Directory Structure](#directory-structure)
  - [Bài toán phát hiện \& định vị (Detection \& Localization)](#bài-toán-phát-hiện--định-vị-detection--localization)
  - [Bài toán phân vùng (Segmentation)](#bài-toán-phân-vùng-segmentation)
  - [Bài toán nhận dạng (Recognition)](#bài-toán-nhận-dạng-recognition)
  - [Bài toán theo dõi (Tracking)](#bài-toán-theo-dõi-tracking)
  - [Bài toán 3D Vision](#bài-toán-3d-vision)
  - [Bài toán về chuyển động](#bài-toán-về-chuyển-động)
  - [Bài toán tạo sinh (Generative Vision)](#bài-toán-tạo-sinh-generative-vision)
  - [Bài toán hiểu cảnh (Scene Understanding)](#bài-toán-hiểu-cảnh-scene-understanding)
  - [Bài toán đa phương thức (Multimodal)](#bài-toán-đa-phương-thức-multimodal)
  - [Bài toán chuyên biệt](#bài-toán-chuyên-biệt)
  - [Bài toán nền tảng](#bài-toán-nền-tảng)
- [Kênh  màu](#kênh--màu)
- [Segmentation mask](#segmentation-mask)
---
# Directory Structure
```bash
Computer-Vision           # mình dùng thư mục này để xem kiến thức về CV
├── Base.md               # mình dùng file này để xem kiến thức cơ bản và tiện ích
├── Dataset.md      # mình dùng file này đểthao tác liên quan đến tập dữ liệu mẫu
├── Architecture/   # mình dùng file này để xem các kiến trúc model
├── Fields/               # mình dùng thư mục này để xem các lĩnh vực
├── Models.md             # mình dùng thư mục này để xem các model cụ thể
├── Process_IMG.md        # mình dùng thư mục này để xử lý ảnh
└── Practices.md          # mình dùng file này để xem code mẫu, bài tập
# Fields
## Bài toán mức thấp (Low-level Vision)
```bash
Xử lý tín hiệu ảnh, chưa cần hiểu nội dung.
```
```bash
1. Image Classification (Phân loại ảnh)
    - Giải quyết: Ảnh này thuộc lớp nào?
    - Ví dụ: mèo/chó, ung thư/không ung thư.
2. Image Denoising (Khử nhiễu)
    - Giải quyết: Làm sạch ảnh bị nhiễu.
3. Image Deblurring (Khử mờ)
    - Giải quyết: Phục hồi ảnh bị rung hoặc out-focus.
4. Super Resolution
    - Giải quyết: Tăng độ phân giải ảnh.
5. Image Enhancement
- Giải quyết: Cải thiện độ sáng, tương phản, màu sắc.
6. Inpainting
- Giải quyết: Điền phần ảnh bị mất.
7. Colorization
- Giải quyết: Tô màu ảnh đen trắng.
```
## Bài toán phát hiện & định vị (Detection & Localization)
```bash
1. Object Detection
    - Giải quyết: Ảnh có vật thể nào và chúng ở đâu?
    - Output: bounding box + label.
2. Face Detection
    - Giải quyết: Phát hiện khuôn mặt trong ảnh.
3. Object Localization
    - Giải quyết: Vị trí của một vật thể cụ thể trong ảnh.
4. Text Detection
    - Giải quyết: Xác định vị trí chữ trong ảnh.
```
## Bài toán phân vùng (Segmentation)
```bash
1. Semantic Segmentation
    - Giải quyết: Mỗi pixel thuộc lớp nào?
2. Instance Segmentation
    - Giải quyết: Phân biệt từng cá thể riêng biệt.
3. Panoptic Segmentation
    - Giải quyết: Kết hợp semantic + instance.
```
## Bài toán nhận dạng (Recognition)
```bash
3. Action Recognition
    - Giải quyết: Người trong video đang làm gì?
4. Gesture Recognition
    - Giải quyết: Nhận dạng cử chỉ tay.
```
## Bài toán theo dõi (Tracking)
```bash
1. Object Tracking
    - Giải quyết: Theo dõi vật thể qua các frame video.
2. Multi-object Tracking (MOT)
    - Giải quyết: Theo dõi nhiều đối tượng cùng lúc.
```
## Bài toán 3D Vision
```bash
1. Depth Estimation
    - Giải quyết: Ước lượng khoảng cách từ camera.
2. Stereo Matching
    - Giải quyết: Tính depth từ 2 camera.
3. 3D Reconstruction
    - Giải quyết: Xây dựng mô hình 3D từ ảnh.
4. SLAM
    - Giải quyết: Robot vừa xây bản đồ vừa định vị.
5. Pose Estimation (3D Pose)
    - Giải quyết: Tư thế cơ thể trong không gian 3D.
```
## Bài toán về chuyển động
```bash
1. Optical Flow
    - Giải quyết: Pixel di chuyển như thế nào giữa 2 frame?
2. Motion Estimation
    - Giải quyết: Ước lượng chuyển động trong video.
```
## Bài toán tạo sinh (Generative Vision)
```bash
1. Image Generation
    - Giải quyết: Sinh ảnh mới từ noise/text.
2. Image-to-Image Translation
    - Giải quyết: Chuyển đổi phong cách ảnh.
3. Style Transfer
    - Giải quyết: Chuyển phong cách nghệ thuật.
4. Deepfake / Face Swap
    - Giải quyết: Thay đổi khuôn mặt.
```
## Bài toán hiểu cảnh (Scene Understanding)
```bash
1. Scene Classification
    - Giải quyết: Đây là cảnh gì?
2. Scene Graph Generation
    - Giải quyết: Mối quan hệ giữa các vật thể.
3. Visual Question Answering (VQA)
    - Giải quyết: Trả lời câu hỏi về ảnh.
```
## Bài toán đa phương thức (Multimodal)
```bash
1. Image Captioning
    - Giải quyết: Mô tả nội dung ảnh bằng ngôn ngữ.
2. Text-to-Image
    - Giải quyết: Tạo ảnh từ mô tả văn bản.
3. Image Retrieval
    - Giải quyết: Tìm ảnh tương tự.
```
## Bài toán chuyên biệt
```bash
1. Medical Image Analysis
    - Phát hiện khối u, phân đoạn cơ quan.
2. Autonomous Driving Vision
    - Phát hiện lane, xe, người đi bộ.
3. Anomaly Detection
    - Phát hiện bất thường trong sản xuất.
4. Document Layout Analysis
    - Phân tích cấu trúc tài liệu.
5. Remote Sensing Analysis
    - Phân tích ảnh vệ tinh.
```
## Bài toán nền tảng
```bash
1. Feature Extraction
    - Trích đặc trưng từ ảnh.
2. Keypoint Detection
    - Phát hiện điểm đặc trưng.
3. Matching / Registration
    - Ghép ảnh.
```
# Kênh  màu
```bash
- Mặc định Opencv sử dụng kênh màu BGR.
- Vì OpenCV ban đầu đưuọc viết bằng C/C++ và theo chuẩn xử lý ảnh của Windows Bitmap (BMP) - vốn lưu pixel theo thứ tự BGR. Để tăng hiệu suất và tránh chuyển đổi không cần thiết, OpenCV giữ nguyên thứ tự này.
- Khi đọc ảnh từ file, OpenCV đọc pixel theo thứ tự BGR để tránh tốn tài nguyên chuyển đổi qua lại nếu bạn xử lý nhiều ảnh ở cấp hệ thống.
```
# Segmentation mask
```bash
- Là một ảnh đen trắng (hoặc đa kênh) dùng để biểu diện phân vùng (vật thể hoặc khu vực) trong ảnh gốc
- Mỗi pixel trong mask cho biết vật thể nào (hoặc lớp nào) nó thuộc về.
- Có 2 loại phổ biến:
    + binary mask: pixel=1 nếu thuộc vật thể, 0 nếu là nền.
    + multi-class mask: pixel =0,1,2,… tương ứng với các lớp khác nhau (mèo, chó, người, …).
    + Không phụ thuộc vào màu sắc, mà phụ thuộc vào nhãn mà bạn gán khi huấn luyện mô hình.
```