- [Albumentations Introduction](#albumentations-introduction)
- [Installation](#installation)
- [Compose() (Ghép nhiều phép biến đổi (transform) lại thành một pipeline và thực hiện chúng theo đúng thứ tự)](#compose-ghép-nhiều-phép-biến-đổi-transform-lại-thành-một-pipeline-và-thực-hiện-chúng-theo-đúng-thứ-tự)
  - [transform()](#transform)
- [ShiftScaleRotate (Dùng để dịch chuyển, phóng to/thu nhỏ, và xoay ảnh)](#shiftscalerotate-dùng-để-dịch-chuyển-phóng-tothu-nhỏ-và-xoay-ảnh)
- [HorizontalFlip() (Lật ngang)](#horizontalflip-lật-ngang)
- [RandomBrightnessContrast() (Thay đổi độ sáng và độ tương phản)](#randombrightnesscontrast-thay-đổi-độ-sáng-và-độ-tương-phản)
- [HueSaturationValue() (Đổi màu)](#huesaturationvalue-đổi-màu)
- [OneOf() (Chỉ chọn một augmentation trong danh sách)](#oneof-chỉ-chọn-một-augmentation-trong-danh-sách)
- [GaussianBlur() (Làm mờ ảnh)](#gaussianblur-làm-mờ-ảnh)
- [GaussNoise() (Thêm nhiễu Gaussian)](#gaussnoise-thêm-nhiễu-gaussian)
- [BboxParams (hướng dẫn Albumentations xử lý bounding box)](#bboxparams-hướng-dẫn-albumentations-xử-lý-bounding-box)
---
# Albumentations Introduction 
```bash
là thư viện data augmentation rất phổ biến trong Computer Vision. Ý tưởng là bạn tạo một "pipeline" gồm nhiều phép biến đổi rồi áp dụng lên ảnh.
```
# Installation
```bash
pip install albumentations
```
# Compose() (Ghép nhiều phép biến đổi (transform) lại thành một pipeline và thực hiện chúng theo đúng thứ tự)
**Syn**
```bash
transform = A.Compose(
    [
        transform_1,
        transform_2,
        transform_3,
        ...
    ]
)

- Output: function
```
## transform()
**Ex1: Compose chỉ có 1 transform lật ngang ảnh**
```python
import albumentations as A

transform = A.Compose([
    A.HorizontalFlip(p=1)
])

result = transform(image=image) # result["image"] là ảnh đã lật.
```
**Ex2: Compose nhiều transform**
```python
import albumentations as A

transform = A.Compose([
    A.HorizontalFlip(p=1),

    A.RandomBrightnessContrast(
        brightness_limit=0.2,
        contrast_limit=0.2,
        p=1
    ),

    A.GaussianBlur(
        blur_limit=(3,5),
        p=1
    )
])
```
# ShiftScaleRotate (Dùng để dịch chuyển, phóng to/thu nhỏ, và xoay ảnh)
**Syn**
```bash
A.ShiftScaleRotate(
    shift_limit=0.0625,
    scale_limit=0.1,
    rotate_limit=45,
    interpolation=cv2.INTER_LINEAR,
    border_mode=cv2.BORDER_CONSTANT,
    p=0.5
)

- Input:
    + shift_limit	: dịch ảnh theo x,y. Tự sinh ngẫu nhiên giá trị dịch chuyển (Ví dụ: 0.1 -> shift_x ∈ [-0.1, 0.1], shift_y ∈ [-0.1, 0.1])
    + scale_limit	: phóng to hoặc thu nhỏ
    + rotate_limit	: góc xoay
    + p	            : xác suất áp dụng
```
**Ex**
```python
A.ShiftScaleRotate(
    shift_limit=0.1,
    scale_limit=0.2,
    rotate_limit=20,
    p=1
)

# giả sử ảnh 
# +----------------+
# |                |
# |      Stamp     |
# |                |
# +----------------+

# Sau augmentation có thể thành
# +----------------+
# |          Stamp |
# |                |
# |                |
# +----------------+
```
# HorizontalFlip() (Lật ngang)
**Syn**
```bash
A.HorizontalFlip(p=0.5)

- Output:
    + Ví dụ: 
        - Ảnh gốc ABC. Sau CBA
        - Đối với chữ ký: Ký tên sẽ thành nêt ýK
```
# RandomBrightnessContrast() (Thay đổi độ sáng và độ tương phản)
**syn**
```bash
A.RandomBrightnessContrast(
    brightness_limit=0.2,
    contrast_limit=0.2,
    p=0.5
)

- Input:
    + brightness: 
        - -0.2 → tối hơn
        - +0.2 → sáng hơn
    + contrast
        - -0.2 → nhạt
        - +0.2 → đậm
- Output:
    + Ví dụ: Ảnh gốc ████ Sau ▓▓▓▓ (tối hơn) hoặc ██████ (sáng hơn)
```
# HueSaturationValue() (Đổi màu)
**Syn**
```bash
A.HueSaturationValue(
    hue_shift_limit=20,
    sat_shift_limit=30,
    val_shift_limit=20,
    p=0.5
)

- Input:
    + hue_shift_limit: đổi màu. đỏ -> xanh -> vàng
    + sat_shift_limit: ít màu -> nhiều màu
    + val: tối -> sáng
- Output:
    - Con dấu đỏ 🔴 có thể thành 🟠🟣🟢 # Nếu dữ liệu chỉ là ảnh scan đen trắng thì phép này thường không cần thiết.
```
# OneOf() (Chỉ chọn một augmentation trong danh sách)
**Syn**
```bash
A.OneOf([
    A.GaussianBlur(),
    A.MotionBlur(),
    A.GaussNoise()
], p=0.5)

- Output:
    + Nếu OneOf được áp dụng nó chỉ chọn GaussianBlur hoặc MotionBlur hoặc GaussNoise không bao giờ cả ba.
```
# GaussianBlur() (Làm mờ ảnh)
**Syn**
```bash
A.GaussianBlur(
    blur_limit=(3,7),
    p=0.5
)

- Input:
    + blur_limit: kernel 3x3, 5x5, 7x7 # Ví dụ Ảnh gốc ######## Sau ▒▒▒▒▒▒▒ -> Viền mềm hơn.
```
A.GaussianBlur(
    blur_limit=7,
    p=1
)
# GaussNoise() (Thêm nhiễu Gaussian)
**Syn**
```bash
A.GaussNoise(
    std_range=(0.02, 0.08),
    p=0.5
)

- Output:
    + Ví dụ Ảnh gốc ██████ Sau ██▓█▒█ Có các điểm sáng tối ngẫu nhiên. Rất hữu ích khi dữ liệu thực tế bị nhiễu từ máy scan hoặc camera.
```
# BboxParams (hướng dẫn Albumentations xử lý bounding box)
**Syn**
```bash
bbox_params=A.BboxParams(
    format="yolo",
    label_fields=["class_labels"]
)

- Input:
    + format: Có nhiều kiểu
        - pascal_voc
        - coco
        - yolo

YOLO sử dụng

x_center
y_center
width
height

đã được chuẩn hóa về khoảng [0, 1].

Ví dụ

0.5
0.5
0.2
0.1
label_fields

Ví dụ

class_labels=[0,1]

thì

bbox 1

↓

label 0
bbox 2

↓

label 1

Nếu không khai báo

Albumentations chỉ biến đổi box

không biết box nào thuộc class nào.


2. HorizontalFlip()

Lật ngang.

transform = A.Compose([
    A.HorizontalFlip(p=1)
])

Ảnh

😀➡

Sau

⬅😀

p

p=1

→ luôn thực hiện

p=0.5

→ 50% lật

3. VerticalFlip()

Lật dọc

A.VerticalFlip(p=1)

Ví dụ

😀
⬇

thành

⬆
😀
4. Rotate()

Xoay

A.Rotate(limit=30, p=1)

Nghĩa là

-30°
đến
30°

ngẫu nhiên.

5. Resize()

Đổi kích thước

A.Resize(640,640)

hoặc

A.Resize(
    height=640,
    width=640
)

Ví dụ

transform = A.Compose([
    A.Resize(224,224)
])
6. RandomCrop()

Cắt ngẫu nhiên

A.RandomCrop(
    width=300,
    height=300
)

Ví dụ

Ảnh

1000x1000

↓

300x300
7. CenterCrop()

Cắt giữa ảnh

A.CenterCrop(
    width=200,
    height=200
)

Không ngẫu nhiên.



11. Normalize()

Chuẩn hóa

A.Normalize(
    mean=(0.485,0.456,0.406),
    std=(0.229,0.224,0.225)
)

Hay dùng trước khi đưa vào CNN.

12. RandomGamma()

Đổi Gamma

A.RandomGamma(
    p=1
)

Ảnh sáng hoặc tối theo gamma.
14. RGBShift()

Dịch từng kênh màu

A.RGBShift(
    r_shift_limit=20,
    g_shift_limit=20,
    b_shift_limit=20,
    p=1
)
15. CLAHE()

Tăng tương phản

A.CLAHE(
    p=1
)

Hay dùng trong ảnh X-ray.



17. ToTensorV2()

Nếu dùng PyTorch

from albumentations.pytorch import ToTensorV2

transform = A.Compose([
    A.Resize(224,224),
    ToTensorV2()
])

Chuyển

numpy

↓

torch.Tensor
Ví dụ hoàn chỉnh
import albumentations as A
import cv2

image = cv2.imread("cat.jpg")
image = cv2.cvtColor(image, cv2.COLOR_BGR2RGB)

transform = A.Compose([
    A.Resize(224,224),
    A.HorizontalFlip(p=0.5),
    A.Rotate(limit=15,p=0.5),
    A.RandomBrightnessContrast(p=0.5)
])

result = transform(image=image)

new_image = result["image"]

Pipeline trên sẽ:

Resize về 224×224.
Có 50% khả năng lật ngang.
Có 50% khả năng xoay trong khoảng ±15°.
Có 50% khả năng thay đổi độ sáng và độ tương phản.
Các hàm quan trọng nhất cần nhớ
Hàm	Công dụng
A.Compose()	Ghép nhiều phép biến đổi thành một pipeline
A.Resize()	Đổi kích thước ảnh

A.VerticalFlip()	Lật dọc
A.Rotate()	Xoay ảnh
A.RandomCrop()	Cắt ngẫu nhiên
A.CenterCrop()	Cắt ở giữa
A.RandomBrightnessContrast()	Thay đổi độ sáng và tương phản
A.GaussianBlur()	Làm mờ
A.GaussNoise()	Thêm nhiễu
A.Normalize()	Chuẩn hóa ảnh
A.HueSaturationValue()	Thay đổi màu sắc
A.RGBShift()	Dịch các kênh màu RGB
A.CLAHE()	Tăng tương phản cục bộ
A.OneOf()	Chọn ngẫu nhiên một phép biến đổi
ToTensorV2()	Chuyển ảnh NumPy sang torch.Tensor để dùng với PyTorch

Đây là những phép biến đổi bạn sẽ gặp thường xuyên trong các bài toán phân loại ảnh, phát hiện đối tượng (YOLO), phân đoạn ảnh và OCR.
category_ids không phải là một từ khóa đặc biệt của Albumentations. Nó chỉ là tên của danh sách chứa nhãn (class) của từng bounding box mà bạn tự đặt.

Ví dụ:

bbox_params=A.BboxParams(
    format="yolo",
    label_fields=["category_ids"]
)

Nghĩa là Albumentations hiểu rằng:

"Ngoài bboxes, còn có một biến tên category_ids. Mỗi bbox sẽ có một phần tử tương ứng trong danh sách này."

Ví dụ đơn giản

Giả sử ảnh có:

1 con dấu (stamp)
1 chữ ký (signature)

Theo data.yaml

names:
  0: stamp
  1: signature

Ta có

bboxes = [
    [0.50, 0.45, 0.20, 0.18],   # stamp
    [0.30, 0.75, 0.15, 0.08]    # signature
]

category_ids = [
    0,
    1
]

Có thể hình dung như bảng:

BBox	Class
[0.50,0.45,0.20,0.18]	0 (stamp)
[0.30,0.75,0.15,0.08]	1 (signature)
Khi augment

Ví dụ ảnh bị xoay.

Trước

+------------------------+
|                        |
|      Stamp             |
|                        |
|              Signature |
+------------------------+

Sau

+------------------------+
| Stamp                  |
|                        |
|     Signature          |
+------------------------+

Albumentations sẽ tự động cập nhật:

result = transform(
    image=image,
    bboxes=bboxes,
    category_ids=category_ids
)

Kết quả

result["bboxes"]

có thể thành

[
    [0.42,0.31,0.20,0.18],
    [0.55,0.68,0.15,0.08]
]

và

result["category_ids"]

vẫn là

[0,1]

Nó biết bbox đầu vẫn là stamp, bbox sau vẫn là signature.

Tại sao cần label_fields

Giả sử có

bboxes = [
    bbox1,
    bbox2,
    bbox3
]

category_ids = [
    0,
    1,
    1
]

Nếu một bbox bị cắt mất sau augmentation và bị xóa thì:

Ban đầu

BBox	Class
bbox1	0
bbox2	1
bbox3	1

Sau augmentation

bbox2

bị mất.

Albumentations sẽ tự động trả về

bboxes = [
    bbox1,
    bbox3
]

category_ids = [
    0,
    1
]

Nếu không khai báo:

label_fields=["category_ids"]

thì Albumentations chỉ biết xóa bbox, không biết phải xóa class tương ứng, dẫn đến số lượng bbox và nhãn không khớp.

min_visibility=0.3
bbox_params=A.BboxParams(
    format="yolo",
    label_fields=["category_ids"],
    min_visibility=0.3,
)

Giả sử bbox ban đầu:

██████████

Sau khi dịch ảnh, chỉ còn:

███

Tức là chỉ còn khoảng 30% diện tích ban đầu.

Nếu min_visibility=0.3 → bbox được giữ lại.
Nếu chỉ còn 20% → bbox bị loại bỏ.

Mục đích là tránh đưa vào dữ liệu huấn luyện những đối tượng chỉ còn một phần rất nhỏ, vì chúng thường không còn đủ thông tin để mô hình học.

Có nhất thiết phải tên là category_ids không?

Không. Bạn có thể đặt tên bất kỳ, miễn là thống nhất:

bbox_params=A.BboxParams(
    format="yolo",
    label_fields=["labels"]
)

transform(
    image=image,
    bboxes=bboxes,
    labels=[0, 1, 1]
)

hoặc

bbox_params=A.BboxParams(
    format="yolo",
    label_fields=["classes"]
)

transform(
    image=image,
    bboxes=bboxes,
    classes=[0, 1, 1]
)

Trong nhiều ví dụ và tài liệu, người ta dùng category_ids vì đây là tên quen thuộc trong các bộ dữ liệu như COCO, nhưng về bản chất đó chỉ là tên của danh sách chứa ID lớp (class ID) tương ứng với từng bounding box.

nhưng bộ dữ liệu của tôi tự làm tự gán nhã làm gì có cái nào là category_id\
Đúng rồi. Bộ dữ liệu của bạn không cần có cột hay file nào tên category_id cả.

Có một điểm dễ nhầm là:

YOLO dataset lưu nhãn trong file .txt.
Albumentations làm việc với dữ liệu trong bộ nhớ (Python), không đọc trực tiếp file .txt.
Dataset YOLO của bạn

Ví dụ image1.txt

0 0.45 0.52 0.20 0.15
1 0.70 0.35 0.12 0.08

Trong đó:

0 = stamp
1 = signature

Bạn đọc file này vào Python:

bboxes = [
    [0.45, 0.52, 0.20, 0.15],
    [0.70, 0.35, 0.12, 0.08]
]

category_ids = [
    0,
    1
]

category_ids chính là cột đầu tiên của file YOLO được tách ra thành một list.

Vì sao phải tách?

Albumentations yêu cầu:

transform(
    image=image,
    bboxes=bboxes,
    category_ids=category_ids
)

chứ không yêu cầu

transform(
    image=image,
    bboxes=[
        [0,0.45,0.52,0.20,0.15],
        [1,0.70,0.35,0.12,0.08]
    ]
)

Nó muốn:

bbox riêng
label riêng
Ví dụ đầy đủ

File YOLO

0 0.50 0.40 0.20 0.10
1 0.30 0.60 0.15 0.08

Đọc file:

bboxes = []
category_ids = []

for line in lines:
    cls, x, y, w, h = map(float, line.split())

    category_ids.append(int(cls))
    bboxes.append([x, y, w, h])

Sau đó

augmented = transform(
    image=image,
    bboxes=bboxes,
    category_ids=category_ids
)
Có thể đổi tên không?

Được.

Bạn hoàn toàn có thể viết

bbox_params=A.BboxParams(
    format="yolo",
    label_fields=["labels"]
)

và

augmented = transform(
    image=image,
    bboxes=bboxes,
    labels=[0,1]
)

hoặc

label_fields=["classes"]

và

classes=[0,1]

Tên nào cũng được, miễn là trùng nhau.

Với dự án của bạn

Vì bạn đang tự augment dữ liệu YOLO (stamp và signature), mình khuyên nên dùng:

bbox_params=A.BboxParams(
    format="yolo",
    label_fields=["labels"],
    min_visibility=0.3,
)

và trong code:

transform(
    image=image,
    bboxes=bboxes,
    labels=labels
)

Tên labels sẽ trực quan hơn category_ids, nhưng về chức năng thì hoàn toàn giống nhau.