- [Introduction](#introduction)
- [Architecture](#architecture)
- [Workflow khi đưa một ảnh vào YOLOv8 để detect object](#workflow-khi-đưa-một-ảnh-vào-yolov8-để-detect-object)
---
# Introduction
```bash
- YOLO là một kiến trúc được thiết kế để thực hiện tác vụ phát hiện vật thể (Object Detection) trong thời gian thực. Cái tên "You Only Look Once" nói lên điểm cốt lõi: nó xử lý toàn bộ hình ảnh chỉ trong một lần duy nhất.
- Các version YOLOv1 -> YOLOv8 là các model cụ thể.
```
# Architecture
```bash
Mô hình YOLO có cấu trúc tương tự như một dòng chảy dữ liệu qua 3 phần chính, hoạt động tuần tự:
    1. Backbone (Phần Trích xuất Đặc trưng)
        - Mục đích: Hút các đặc trưng cơ bản từ ảnh (các cạnh, góc, hình dạng).
        - Vị trí trong code: Các lớp từ (0) đến (9):
        - Conv (Convolution): Lớp tích chập cơ bản, dùng để trích xuất đặc trưng.
        - Conv2d(3, 16, kernel_size=(3, 3), stride=(2, 2)): Khởi đầu với ảnh 3 kênh màu (RGB), tạo ra 16 kênh đặc trưng, giảm kích thước ảnh (stride=2).
        - C2f (Cross-Stage Partial Network): Là một khối kiến trúc quan trọng trong YOLO hiện đại (như YOLOv8). Nó giúp tăng hiệu suất bằng cách tách luồng đặc trưng ra hai nhánh và hợp nhất lại. Nó giúp mô hình học sâu hơn mà vẫn giữ được tốc độ.
        - SPPF (Spatial Pyramid Pooling Fast): Lớp (9). Nó tổng hợp thông tin từ nhiều kích thước khác nhau của cùng một đặc trưng. Điều này giúp mô hình nhận diện vật thể bất kể kích thước của chúng (ví dụ: một chiếc xe ô tô to hay nhỏ trong ảnh).
    2. Neck (Phần Hợp nhất Đặc trưng)
        - Mục đích: Kết hợp các đặc trưng đã học được từ các cấp độ sâu khác nhau của Backbone.
        - Các lớp nông (gần đầu) có đặc trưng về chi tiết, vị trí chính xác.
        - Các lớp sâu (gần cuối) có đặc trưng về ngữ cảnh, phân loại vật thể.
        - Vị trí trong code: Các lớp từ (10) đến (21):
        - Upsample (10, 13): Phóng to bản đồ đặc trưng từ lớp sâu lên.
        - Concat (11, 14, 17, 20): Nối (ghép) bản đồ đặc trưng đã được phóng to với bản đồ đặc trưng tương ứng từ Backbone.
        - Mô hình này sử dụng kiến trúc kiểu FPN/PAN: giúp các lớp dự đoán (Head) có được thông tin chi tiết lẫn thông tin ngữ cảnh.
    3. Head (Phần Dự đoán)
        - Mục đích: Lấy các đặc trưng đã được hợp nhất từ Neck và chuyển chúng thành kết quả dự đoán cuối cùng.
        - Vị trí trong code: Lớp (22) Detect(...).
        - Đầu ra của Head:
        - Hộp bao (Bounding Box): Toạ độ (x,y,w,h) của vật thể.
        - Độ tin cậy vật thể (Objectness Score): Xác suất có vật thể trong hộp đó.
        - Xác suất lớp (Class Probability): Xác suất vật thể đó thuộc về mỗi loại lớp (người, chó, xe hơi...).
        - DFL (Distribution Focal Loss): Được sử dụng trong YOLOv8 để cải thiện độ chính xác của hộp bao bằng cách học cách phân phối khoảng cách tới các cạnh của hộp.
```
# Workflow khi đưa một ảnh vào YOLOv8 để detect object
```bash
Bước 1: Resize
    - ảnh gốc       : 1920x1080x3 (RGB)
    - ảnh resize    : 640x640x3 (vì model cần input fix size)
Bước 2: Preprocessing
    - scale
Bước 3: Tensor hóa ảnh
    1. (640x640x3) -> (3x640x640)
    2. Batch dimension: (1,3,640,640)
Bước 4: Backbone CNN feature extraction
    - YOLOv8 dùng CNN backbone (C2f blocks)
    - Ảnh đi qua nhiều convolution layers
    - Ví dụ:
        + Input         : 640x640x3
        + Kernel        : 3x3
        + Filter count  : 32
        + Output        : 640x640x32
Bước 5: Downsampling
    - CNN sẽ giảm spatial dimension
    - Ví dụ:
        Input (640,640) -> Conv1 (320, 320)
        -> Conv2 (160, 160)
        -> Conv3 (80, 80)
        -> Conv4 (40, 40)
        -> Conv5 (20, 20)
        Nhưng số chanel tăng (3 -> 32 -> 64 -> 128 -> 256 -> ...)
Bước 6: Feature Pyramid / Neck
    - Vấn đề của object detection là object có nhiều kích thước:
        + người xa -> nhỏ
        + xe gần -> to
    - Nếu chỉ dùng feature map cuối 20x20 thì:
        + object lớn -> OK
        + object nhỏ -> mất hết chi tiết
```

ở 7, khi downsample từ 640x640x3 -> 20x20x256, thì 640x640x3 đúng là ảnh nhưng 20x20x256 có phải là ảnh đó nữa đâu, nó là lưu các vector đặc trưng về cạnh góc chứ thì liên quan gì đến object to nhỏ
Đúng rồi — bạn đang chạm đúng “điểm bản chất” của CNN.
Khi xuống:
20×20×256
thì nó KHÔNG còn là “ảnh” theo nghĩa thông thường nữa.
Nó là:
semantic feature map
tức:


tensor đặc trưng


chứa thông tin đã được encode


Bạn hiểu đúng ở chỗ:

“nó là vector đặc trưng cạnh/góc/pattern…”

Đó chính xác là điều CNN đang làm.
Nhưng phần dễ gây nhầm là:

“vậy tại sao còn liên quan tới object to/nhỏ?”

Câu trả lời nằm ở:
Spatial correspondence vẫn còn tồn tại
Dù không còn là ảnh RGB, nhưng:
20×20
vẫn đại diện cho:


vị trí không gian trong ảnh gốc.



Cực kỳ quan trọng
Ví dụ:
Ảnh gốc:
640×640
Sau 5 lần downsample:
20×20
thì:
1 pixel ở feature map 20×20
≈ đại diện cho một vùng lớn trong ảnh gốc.
Ví dụ:
1 cell ≈ 32×32 pixels
vì:
640 / 20 = 32

Ý nghĩa thực sự
Feature map:
20×20×256
có nghĩa:


có 20×20 vị trí spatial


mỗi vị trí có vector 256 chiều


Vector đó encode:
“vùng này có gì?”
Ví dụ tại cell (7,12):
256 values có thể encode:
- cạnh cong- texture kính- bánh xe- metallic pattern
CNN sâu hơn sẽ hiểu:
À vùng này giống CAR

Vậy object lớn/nhỏ liên quan gì?
Do receptive field.

Receptive field
Một neuron sâu trong mạng không nhìn:


1 pixel


Nó nhìn:


một vùng lớn của ảnh gốc.



Ví dụ
Ở layer nông:
80×80
1 cell có thể chỉ nhìn:
8×8 pixels
Ở layer sâu:
20×20
1 cell có thể nhìn:
100×100 pixels
hoặc hơn.

Trực giác cực kỳ quan trọng
Feature map lớn (80×80)


mỗi cell đại diện vùng nhỏ


giữ nhiều detail


=> tốt cho object nhỏ.

Feature map nhỏ (20×20)


mỗi cell đại diện vùng lớn


semantic mạnh hơn


=> tốt cho object lớn.

Ví dụ thực tế
Chim nhỏ
Con chim:
10×10 pixels
Nếu dùng feature map:
20×20
mỗi cell đại diện:
32×32 pixels
thì:


chim bị “nuốt”


không đủ resolution



Nhưng ở 80×80
Mỗi cell chỉ đại diện:
8×8 pixels
=> vẫn còn detail để detect chim.

Còn xe tải lớn?
Xe tải:
200×200 pixels
thì feature map nhỏ vẫn OK.
Vì:


object quá lớn


không cần detail pixel-level nữa


Mà cần:


semantic understanding mạnh hơn.



Tại sao semantic ở layer sâu mạnh hơn?
Do nhiều convolution stacking.
Layer sâu nhìn được:


context lớn


nhiều pattern combine lại


Ví dụ:
Layer đầu:


cạnh


Layer giữa:


bánh xe


Layer sâu:


bánh xe + kính + thân xe


=> “CAR”.

Điều quan trọng nhất
Feature map KHÔNG còn là ảnh.
Nhưng:
nó vẫn giữ spatial structure
Đây là chìa khóa của CNN.

So sánh dễ hiểu
640×640×3
Giống:


ảnh thật



20×20×256
Giống:


bản đồ semantic nén


Mỗi ô:
“vùng này chứa pattern gì?”

CNN không “vứt bỏ không gian”
Nó chỉ:


nén không gian


tăng semantic density



Công thức trực giác
Khi depth tăng:
Spatial detailSemantic meaninggiảmtăng
CNN trade-off:


detail ↓


understanding ↑



Vì vậy YOLO mới cần multi-scale
YOLO combine:


feature map lớn → giữ detail


feature map nhỏ → hiểu semantic mạnh


để detect:


object nhỏ


object lớn
cùng lúc.

