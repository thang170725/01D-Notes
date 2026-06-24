- [Shape (xử lý hình dạng)](#shape-xử-lý-hình-dạng)
  - [Resize (Thay đổi kích thước)](#resize-thay-đổi-kích-thước)
  - [Cropping (Cắt ảnh)](#cropping-cắt-ảnh)
  - [ROI (Region Of Interest)](#roi-region-of-interest)
  - [Center Crop / Random Crop](#center-crop--random-crop)
  - [Padding](#padding)
  - [Normalization (Chuẩn hóa pixel)](#normalization-chuẩn-hóa-pixel)
  - [Standardization (Chuẩn hóa theo mean/std)](#standardization-chuẩn-hóa-theo-meanstd)
  - [Color Space Conversion (RGB ↔ Gray ↔ HSV ↔ LAB)](#color-space-conversion-rgb--gray--hsv--lab)
  - [Channel Reordering (RGB ↔ BGR)](#channel-reordering-rgb--bgr)
  - [Flip (Lật ảnh)](#flip-lật-ảnh)
  - [Rotation (Xoay)](#rotation-xoay)
  - [Translation (Dịch chuyển)](#translation-dịch-chuyển)
  - [Scaling (Phóng to/thu nhỏ)](#scaling-phóng-tothu-nhỏ)
  - [Shear (Biến dạng nghiêng)](#shear-biến-dạng-nghiêng)
  - [Perspective Transform](#perspective-transform)
  - [Random Erasing / Cutout](#random-erasing--cutout)
  - [Mixup](#mixup)
  - [CutMix](#cutmix)
  - [Affine Transform](#affine-transform)
  - [Homography](#homography)
  - [Warp Transform](#warp-transform)
- [Tăng cường dữ liệu (Data Augmentation)](#tăng-cường-dữ-liệu-data-augmentation)
- [Edge (xử lý cạnh)](#edge-xử-lý-cạnh)
  - [Sharpening](#sharpening)
- [Noise (xử lý nhiễu)](#noise-xử-lý-nhiễu)
  - [Denoising (Non-local means)](#denoising-non-local-means)
  - [HOG (Histogram of Oriented Gradients)](#hog-histogram-of-oriented-gradients)
  - [SIFT](#sift)
  - [SURF](#surf)
  - [ORB](#orb)
  - [LBP (Local Binary Pattern)](#lbp-local-binary-pattern)
  - [Gabor Filter](#gabor-filter)
  - [Thresholding](#thresholding)
  - [Adaptive Threshold](#adaptive-threshold)
  - [Otsu Threshold](#otsu-threshold)
  - [Morphology (Erode/Dilate)](#morphology-erodedilate)
  - [Opening/Closing](#openingclosing)
  - [Image to Tensor](#image-to-tensor)
  - [Patch Extraction](#patch-extraction)
  - [Sliding Window](#sliding-window)
  - [Multi-scale Input](#multi-scale-input)
  - [Anchor Generation](#anchor-generation)
  - [Face Alignment](#face-alignment)
  - [Background Removal](#background-removal)
  - [Super Resolution](#super-resolution)
  - [Depth Estimation Preprocess](#depth-estimation-preprocess)
  - [Optical Flow](#optical-flow)
  - [FFT](#fft)
  - [DCT](#dct)
  - [Wavelet Transform](#wavelet-transform)
  - [Positional Encoding for Image](#positional-encoding-for-image)
  - [Tokenization ảnh (Patch Embedding)](#tokenization-ảnh-patch-embedding)
  - [Bounding Box Normalization](#bounding-box-normalization)
  - [Mask Encoding (RLE)](#mask-encoding-rle)
  - [Image Embedding Extraction](#image-embedding-extraction)
  - [Contrastive Preprocessing](#contrastive-preprocessing)
- [Color (xử lý màu sắc)](#color-xử-lý-màu-sắc)
  - [CLAHE](#clahe)
  - [Color Jitter](#color-jitter)
  - [Gaussian Noise](#gaussian-noise)
  - [Gaussian Blur](#gaussian-blur)
  - [Median Filter](#median-filter)
  - [Bilateral Filter](#bilateral-filter)
  - [Histogram Equalization](#histogram-equalization)
---
# Shape (xử lý hình dạng)
## Resize (Thay đổi kích thước)
```bash
Đưa ảnh về kích thước cố định (vd: 224x224)
```
## Cropping (Cắt ảnh)
```bash
Lấy vùng quan tâm (ROI)
```
## ROI (Region Of Interest)
```bash
- Trong cả bức ảnh / frame, mình chỉ quan tâm một vùng nào đó, còn lại thì kệ.
- Ví dụ:
    + Camera giao thông → chỉ quan tâm phần đường, không quan tâm bầu trời
    + Camera lớp học → chỉ quan tâm khu vực bảng
    + Camera an ninh → chỉ quan tâm cửa ra vào
- ROI không phải AI, nó là xử lý ảnh thuần.
```
## Center Crop / Random Crop
```bash
Tăng tính đa dạng dữ liệu
```
## Padding
```bash
Thêm viền để giữ tỉ lệ
```
## Normalization (Chuẩn hóa pixel)
```bash
- Đưa pixel về [0–1] hoặc [-1–1]
- Ứng dụng hầu hết Deep Learning model
```
## Standardization (Chuẩn hóa theo mean/std)
```bash
Giúp model hội tụ nhanh
```
## Color Space Conversion (RGB ↔ Gray ↔ HSV ↔ LAB)
```bash 
Thay đổi không gian màu để dễ trích đặc trưng
```
## Channel Reordering (RGB ↔ BGR)
```bash 
Phù hợp framework (OpenCV dùng BGR)
```
## Flip (Lật ảnh)
```bash
- Dùng để Tăng dữ liệu
- Ứng dụng trong Classification
```
## Rotation (Xoay)
## Translation (Dịch chuyển)
##  Scaling (Phóng to/thu nhỏ)
##  Shear (Biến dạng nghiêng)
##  Perspective Transform
##  Random Erasing / Cutout
##  Mixup
##  CutMix
## Affine Transform
```bash
Xoay, scale, translate
```
## Homography
```bash 
Biến đổi mặt phẳng
```
## Warp Transform
```bash
Biến dạng tự do
```
# Tăng cường dữ liệu (Data Augmentation)
# Edge (xử lý cạnh)
## Sharpening
```bash
Làm rõ cạnh
```
# Noise (xử lý nhiễu)
## Denoising (Non-local means)
```bash
Giảm nhiễu nâng cao
```
## HOG (Histogram of Oriented Gradients)
```bash
Trích đặc trưng hình dạng
```
## SIFT
## SURF
## ORB
## LBP (Local Binary Pattern)
## Gabor Filter
## Thresholding
```bash
- Chuyển sang ảnh nhị phân
```
## Adaptive Threshold
## Otsu Threshold
## Morphology (Erode/Dilate)
## Opening/Closing
## Image to Tensor
## Patch Extraction
## Sliding Window
## Multi-scale Input
## Anchor Generation
## Face Alignment
## Background Removal
## Super Resolution
## Depth Estimation Preprocess
## Optical Flow
## FFT
## DCT
## Wavelet Transform
## Positional Encoding for Image
## Tokenization ảnh (Patch Embedding)
## Bounding Box Normalization
## Mask Encoding (RLE)
## Image Embedding Extraction
## Contrastive Preprocessing
# Color (xử lý màu sắc)
## CLAHE
```bash
- Mục đích chính của kỹ thuật này là tăng cường độ tương phản (contrast) cục bộ của hình ảnh.
- Nó giúp làm nổi bật các chi tiết trong các vùng ảnh quá tối hoặc quá sáng mà các phương pháp tăng cường độ tương phản toàn cục (như Histogram Equalization truyền thống) không xử lý tốt, thậm chí còn gây ra nhiễu hoặc làm mất chi tiết.
- Bạn nên sử dụng kỹ thuật CLAHE khi bạn có những bức ảnh gặp vấn đề về độ tương phản, đặc biệt là khi sự chênh lệch độ sáng (dynamic range) trong ảnh lớn hoặc có những vùng bị tối/sáng cục bộ.
- Các trường hợp cụ thể thường áp dụng CLAHE bao gồm:
- Xử lý Ảnh Y học (Medical Imaging): Ảnh chụp X-quang, MRI, CT, ảnh soi đáy mắt (như trong chẩn đoán bệnh lý về mắt) thường có độ tương phản thấp hoặc có các vùng chi tiết cần làm nổi bật. CLAHE giúp tăng khả năng hiển thị các cấu trúc sinh học.
- Ảnh trong Điều kiện Ánh sáng Kém: Ảnh chụp trong điều kiện thiếu sáng hoặc có ánh sáng nền mạnh (backlit), nơi chi tiết bị "chìm" trong bóng tối hoặc bị "cháy" sáng.
- Hệ thống Thị giác Máy (Machine Vision) và Xử lý Ảnh: Khi cần tiền xử lý ảnh (preprocessing) để chuẩn hóa hoặc tăng cường chất lượng ảnh đầu vào trước khi đưa vào các thuật toán nhận dạng, phân loại, hoặc học sâu (Deep Learning/CNN). Việc này giúp thuật toán trích xuất đặc trưng (feature extraction) chính xác hơn.
- Ảnh Thiên văn hoặc Viễn thám: Ảnh vệ tinh hoặc ảnh chụp từ kính thiên văn thường cần CLAHE để làm rõ các cấu trúc và đặc điểm bề mặt.
- Ưu điểm của CLAHE so với HE truyền thống
- CLAHE là một cải tiến của phương pháp Cân bằng Biểu đồ màu (Histogram Equalization - HE) truyền thống:
- Adaptive (Thích nghi): Thay vì áp dụng sự cân bằng độ tương phản cho toàn bộ ảnh, CLAHE chia ảnh thành nhiều ô (tiles/regions) nhỏ và áp dụng HE cho từng ô riêng biệt. Điều này giúp tăng cường độ tương phản cục bộ mà không làm ảnh hưởng đến các vùng khác.
- Contrast Limited (Giới hạn Độ tương phản): CLAHE có một tham số giới hạn (clip limit) để ngăn chặn việc độ tương phản bị tăng quá mức ở các vùng nhiễu (noise) hoặc các vùng có độ tương phản rất thấp, giúp tránh tình trạng nhiễu bị khuếch đại (over-amplification).
```
## Color Jitter
```bash
 Thay đổi sáng/tối/màu
```
## Gaussian Noise
```bash
Thêm nhiễu
``` 
## Gaussian Blur
## Median Filter
```bash
- Dùng để loại bỏ salt-pepper noise
```
## Bilateral Filter
```bash
Giữ cạnh khi làm mịn
```
## Histogram Equalization
```bash
Tăng tương phản
```