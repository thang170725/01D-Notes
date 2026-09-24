- [YOLO() (dùng để load mô hình YOLO)](#yolo-dùng-để-load-mô-hình-yolo)
  - [model()](#model)
  - [.train() (dùng để huấn luyện (train) mô hình trên tập dữ liệu của bạn)](#train-dùng-để-huấn-luyện-train-mô-hình-trên-tập-dữ-liệu-của-bạn)
  - [.show() (dự đoán ảnh)](#show-dự-đoán-ảnh)
  - [.plot()](#plot)
  - [.boxes (nó chứa tất cả các hộp giới hạn (bounding boxes) và thông tin liên quan)](#boxes-nó-chứa-tất-cả-các-hộp-giới-hạn-bounding-boxes-và-thông-tin-liên-quan)
  - [.cls (Trả về id của lớp. ví dụ {0: ‘person’} thì nếu giá trị cls là 0 thì lớp đó là person)](#cls-trả-về-id-của-lớp-ví-dụ-0-person-thì-nếu-giá-trị-cls-là-0-thì-lớp-đó-là-person)
  - [.conf (tensor chứa điểm tin cậy (confidence score) của phát hiện)](#conf-tensor-chứa-điểm-tin-cậy-confidence-score-của-phát-hiện)
  - [.xyxy (là tensor chứa tọa độ (x\_min, y\_min, x\_max, y\_max))](#xyxy-là-tensor-chứa-tọa-độ-x_min-y_min-x_max-y_max)
  - [.names \& .names\[\] (Là một từ điển (dictionary) tích hợp sẵn trong mô hình, ánh xạ ID lớp (class ID) sang tên lớp)](#names--names-là-một-từ-điển-dictionary-tích-hợp-sẵn-trong-mô-hình-ánh-xạ-id-lớp-class-id-sang-tên-lớp)
  - [predict() (dùng để thực hiện suy luận (inference) trên ảnh, video, webcam hoặc cả thư mục)](#predict-dùng-để-thực-hiện-suy-luận-inference-trên-ảnh-video-webcam-hoặc-cả-thư-mục)
---
# YOLO() (dùng để load mô hình YOLO)
[Kiến thức cơ bản về YOLO](../../../../../../../../../Domains/Artificial-Intelligence/AI-Core/03-Machine-Learning/04-Deep-Learning/01-Computer-Vision/02-Architectures-Models/YOLO.md)
**Syn**
```bash
from ultralytics import YOLO

model = YOLO("yolov8n.pt")   # tải model YOLOv8 nano (nhẹ nhất)

- "yolov8s.pt" (small)
- "yolov8m.pt" (medium)
- "yolov10n.pt" (YOLOv10)
- "yolov8n-seg.pt" (segmentation)
- "yolov8n-pose.pt" (pose estimation)
```
**Ex**
```python
from ultralytics import YOLO

model = YOLO('weights/yolov8n.pt')

print(model)

# nó sẽ in ra cấu trúc nơ ron của YOLO
```
## model()
**Syn**
```bash
results = model(source="image.jpg", save=True, stream=True, device=) # đường dẫn có thể là ảnh hoặc video

- model    
    + tên biến được đặt cho mô hình (Ex: model = YOLO(...))
    + model(0)  : sử dụng webcam
- source    : đường dẫn ảnh
- save      : True là Lưu ảnh, False là không lưu
- device    : chỉ định chạy cpu hoặc gpu
```
**Ex**
```python
res = model('image.jpg')

print(res)

# boxes: ultralytics.engine.results.Boxes object
# keypoints: ultralytics.engine.results.Keypoints object
# masks: None
# names: {0: 'person'}
# obb: None
# orig_img: array(...)
# orig_shape: (443, 665)
# path: '/home/thang/projects/nhan_dien/img/predict_1.jpg'
# probs: None
# save_dir: 'runs/pose/predict'
# speed: {'preprocess': 3.722213999935775, 'inference': 140.20678599990788, 'postprocess': 245.47614899984183}]
```
## .train() (dùng để huấn luyện (train) mô hình trên tập dữ liệu của bạn)
**Syn**
```bash
results = model.train(
    data=...,
    epochs=...,
    imgsz=...,
    batch=...,
    workers=...,
    project=...,
    name=...,
    exist_ok=...
)

- Input:
    + model         : mô hình YOLO đã được tạo.
    + data=str      : đường dẫn tới file .yaml
    + epochs=int    : số vòng lặp cần train
    + imgsz=int     : Thường là 640. Là kích thước ảnh đưa vào mạng.
        - Ví dụ: Ảnh gốc 1920×1080 -> YOLO resize 640×640
            + Nếu: imgsz=320 Train nhanh hơn nhưng độ chính xác có thể giảm.
            + Nếu: imgsz=1280 Train chậm hơn tốn VRAM hơn nhưng đôi khi chính xác hơn.
    + batch=int     : Là số ảnh xử lý trong một lần cập nhật trọng số
        - Ví dụ: Dataset 100 ảnh. Batch=25
            + Mỗi lần GPU nhận 4 ảnh
            + Batch càng lớn GPU càng tốn RAM nhưng train nhanh hơn.
    + workers=int   : Đây là số tiến trình đọc dữ liệu. 
        - Linux: thường dùng workers=8
        - Windows: nhiều khi lỗi nên hay để workers=0 để ổn định.
    + projects=str  : Là thư mục chứa kết quả. Thường là runs
    + name=str      : Tên thư mục của lần train
    + exist_ok=bool : Nếu thư mục đã tồn tại. 
        - True -> ghi đè.
        - False -> YOLO sẽ tạo
- Output: 
    + results: kết quả sau khi train.
```
**Ex**
```python
from ultralytics import YOLO

model = YOLO("yolo11n.pt")

results = model.train(
    data="dataset.yaml",
    epochs=100,
    imgsz=640,
    batch=16
)
```
## .show() (dự đoán ảnh)
```bash
- Hiển thị ngay ảnh bằng GUI tích hợp. show() hiển thị trực tiếp (bằng cv2 hoặc thư viện mặc định). Không trả về dữ liệu hình ảnh.
- Chỉ phù hợp khi:
    + Bạn muốn xem nhanh
    + Debug khi đang phát triển
- Nhược điểm:
    + Không lưu được ảnh (phải screenshot)
    + Không linh hoạt
    + Không dùng được trong server (không có GUI), Linux headless, notebook…
```
**Ex**
```python
results = model("image.jpg", save=True)

for r in results: # vì results là một list kết quả nên phải dùng vòng lặp
    r.show()   # hiện ảnh có bounding box
```
## .plot()
```bash
- Trả về ảnh đã được vẽ kết quả (recommended trong code). plot() không hiển thị luôn. Nó trả về một numpy array chứa ảnh gốc + keypoints/box đã vẽ.
- Dùng để:-
    + Lưu ảnh-
    + Gửi ảnh vào pipeline khác-
    + Hiển thị bằng thư viện bạn muốn (cv2, PIL…)-
    + Tối ưu trong ứng dụng thực tế
```
**Ex**
```python
from ultralytics import YOLO

model = YOLO("yolov8n-pose.pt")
results = model("person.jpg")

results[0].plot()  # hiện ảnh với keypoint
```
## .boxes (nó chứa tất cả các hộp giới hạn (bounding boxes) và thông tin liên quan)
**Ex**
```python
from ultralytics import YOLO

model = YOLO('weights/yolov8n.pt')

results = model(
    source='data/images/many-objects.jpeg',
    save=False,
    device='cuda'
)

all_boxes = results[0].boxes
print(f"Tổng số đối tượng được phát hiện trong ảnh: **{len(all_boxes)}**")
Tổng số đối tượng được phát hiện trong ảnh: **8**
```
## .cls (Trả về id của lớp. ví dụ {0: ‘person’} thì nếu giá trị cls là 0 thì lớp đó là person)
**Ex**
```python
from ultralytics import YOLO

model = YOLO('weights/yolov8n.pt')

results = model(
    source='data/images/many-objects.jpeg',
    save=False,
    device='cuda'
)

all_boxes = results[0].boxes

for i, box in enumerate(all_boxes):   
    print(box.cls[0])
tensor(41., device='cuda:0')
tensor(66., device='cuda:0')
tensor(67., device='cuda:0')
tensor(62., device='cuda:0')
tensor(63., device='cuda:0')
tensor(67., device='cuda:0')
tensor(67., device='cuda:0')
tensor(67., device='cuda:0')
from ultralytics import YOLO

model = YOLO('weights/yolov8n.pt')

results = model(
    source='data/images/many-objects.jpeg',
    save=False,
    device='cuda'
)

all_boxes = results[0].boxes

for box in all_boxes:   
    print(box.cls.item())
41.0
66.0
67.0
62.0
63.0
67.0
67.0
67.0
```
## .conf (tensor chứa điểm tin cậy (confidence score) của phát hiện)
**Ex**
```python
from ultralytics import YOLO

model = YOLO('weights/yolov8n.pt')

results = model(
    source='data/images/many-objects.jpeg',
    save=False,
    device='cuda'
)

all_boxes = results[0].boxes

for i, box in enumerate(all_boxes):   
    print(box.conf[0])
tensor(0.9537, device='cuda:0')
tensor(0.9295, device='cuda:0')
tensor(0.9042, device='cuda:0')
tensor(0.8160, device='cuda:0')
tensor(0.5819, device='cuda:0')
tensor(0.4090, device='cuda:0')
tensor(0.3846, device='cuda:0')
tensor(0.2900, device='cuda:0')
from ultralytics import YOLO

model = YOLO('weights/yolov8n.pt')

results = model(
    source='data/images/many-objects.jpeg',
    save=False,
    device='cuda'
)

for b in results[0].boxes:
    print(b.conf.shape)
torch.Size([1])
torch.Size([1])
torch.Size([1])
torch.Size([1])
torch.Size([1])
torch.Size([1])
torch.Size([1])
torch.Size([1])
```
## .xyxy (là tensor chứa tọa độ (x_min, y_min, x_max, y_max))
**Ex**
```python
from ultralytics import YOLO

model = YOLO('weights/yolov8n.pt')

results = model(
    source='data/images/many-objects.jpeg',
    save=False,
    device='cuda'
)

xyxy = results[0].boxes.xyxy

for i, coord in enumerate(xyxy):   
    print(coord)
tensor([ 80.7958, 314.5251, 213.7577, 432.0266], device='cuda:0')
tensor([1.2202e-01, 2.4386e+02, 2.2782e+02, 3.7741e+02], device='cuda:0')
tensor([185.8370, 287.1443, 301.3015, 346.3632], device='cuda:0')
tensor([  0.3699,   0.3549, 354.3244, 227.1534], device='cuda:0')
tensor([598.0267, 170.3140, 795.4203, 272.7632], device='cuda:0')
tensor([748.8848, 210.8769, 851.9120, 291.7232], device='cuda:0')
tensor([334.5608, 342.5161, 445.7292, 422.4576], device='cuda:0')
tensor([761.8676, 211.8118, 851.4373, 275.6527], device='cuda:0')
from ultralytics import YOLO

model = YOLO('weights/yolov8n.pt')

results = model(
    source='data/images/many-objects.jpeg',
    save=False,
    device='cuda'
)

for b in results[0].boxes:
    print(b.xyxy.shape)
torch.Size([1, 4])
torch.Size([1, 4])
torch.Size([1, 4])
torch.Size([1, 4])
torch.Size([1, 4])
torch.Size([1, 4])
torch.Size([1, 4])
torch.Size([1, 4])
```
## .names & .names[] (Là một từ điển (dictionary) tích hợp sẵn trong mô hình, ánh xạ ID lớp (class ID) sang tên lớp)
**Syn**
```python
from ultralytics import YOLO

model = YOLO('weights/yolov8n.pt')

results = model(
    source='data/images/many-objects.jpeg',
    save=False,
    device='cuda'
)

print(f'tổng số lớp mô hình nhận diện {len(model.names)}')
print(f'các lớp mô hình: {model.names}')
for i in range(len(results)):
    print(f'tên lớp có id {i} là: {model.names[i]}')

# tổng số lớp mô hình nhận diện 80
# các lớp mô hình: {0: 'person', 1: 'bicycle', 2: 'car', 3: 'motorcycle', 4: 'airplane', 5: 'bus', 6: 'train', 7: 'truck', 8: 'boat', 9: 'traffic light', 10: 'fire hydrant', 11: 'stop sign', 12: 'parking meter', 13: 'bench', 14: 'bird', 15: 'cat', 16: 'dog', 17: 'horse', 18: 'sheep', 19: 'cow', 20: 'elephant', 21: 'bear', 22: 'zebra', 23: 'giraffe', 24: 'backpack', 25: 'umbrella', 26: 'handbag', 27: 'tie', 28: 'suitcase', 29: 'frisbee', 30: 'skis', 31: 'snowboard', 32: 'sports ball', 33: 'kite', 34: 'baseball bat', 35: 'baseball glove', 36: 'skateboard', 37: 'surfboard', 38: 'tennis racket', 39: 'bottle', 40: 'wine glass', 41: 'cup', 42: 'fork', 43: 'knife', 44: 'spoon', 45: 'bowl', 46: 'banana', 47: 'apple', 48: 'sandwich', 49: 'orange', 50: 'broccoli', 51: 'carrot', 52: 'hot dog', 53: 'pizza', 54: 'donut', 55: 'cake', 56: 'chair', 57: 'couch', 58: 'potted plant', 59: 'bed', 60: 'dining table', 61: 'toilet', 62: 'tv', 63: 'laptop', 64: 'mouse', 65: 'remote', 66: 'keyboard', 67: 'cell phone', 68: 'microwave', 69: 'oven', 70: 'toaster', 71: 'sink', 72: 'refrigerator', 73: 'book', 74: 'clock', 75: 'vase', 76: 'scissors', 77: 'teddy bear', 78: 'hair drier', 79: 'toothbrush'}
# tên lớp có id 0 là: person
```
## predict() (dùng để thực hiện suy luận (inference) trên ảnh, video, webcam hoặc cả thư mục)

Cú pháp cơ bản
from ultralytics import YOLO

model = YOLO("best.pt")

results = model.predict(
    source="images/",
    conf=0.25,
    imgsz=640
)

Hoặc ngắn gọn:

results = model("images/")

Thực chất dòng trên tương đương:

results = model.predict(source="images/")
Các tham số quan trọng
1. source

Nguồn dữ liệu cần detect.

source="image.jpg"

Có thể là

source="folder/"
source="video.mp4"
source=0       # webcam
source="https://..."

Đây là tham số bắt buộc nhất.

2. conf

Confidence threshold.

conf=0.25

YOLO chỉ giữ các object có confidence ≥ giá trị này.

Ví dụ

Nếu model trả về

Object	Confidence
Stamp	0.92
Stamp	0.53
Stamp	0.18

Nếu

conf=0.25

thì kết quả còn

0.92
0.53

Nếu

conf=0.6

thì chỉ còn

0.92

Giá trị thường dùng:

0.1 : detect nhiều hơn nhưng dễ sai.
0.25 : mặc định.
0.5 : khá chính xác.
0.7 : rất chặt.

3. iou

Ngưỡng IoU cho Non-Maximum Suppression (NMS).

iou=0.7

Nếu có nhiều box chồng lên nhau thì YOLO sẽ loại bớt.

Ví dụ

Box A (0.95)
Box B (0.90)

Nếu overlap quá lớn (> iou)

↓

Giữ

Box A

Loại

Box B

Giá trị nhỏ

iou=0.3

→ loại mạnh.

Giá trị lớn

iou=0.8

→ giữ nhiều box hơn.

4. imgsz

Kích thước ảnh đưa vào model.

imgsz=640

YOLO resize ảnh trước khi suy luận.

Ví dụ

Ảnh gốc

3000×2200

↓

640×640

Nếu

imgsz=320

→ nhanh hơn nhưng có thể giảm độ chính xác.

Nếu

imgsz=1280

→ chính xác hơn nhưng chậm hơn.

Có thể truyền:

imgsz=640

hoặc

imgsz=(640, 960)

5. save

Có lưu ảnh kết quả không.

save=True

YOLO sẽ sinh

runs/detect/predict/

chứa ảnh đã vẽ bounding box.

Nếu

save=False

chỉ trả về results.

6. project

Thư mục lưu kết quả.

project="runs"

Ví dụ

runs/
    predict/

hoặc

my_output/
7. name

Tên phiên detect.

name="test1"

Kết quả

runs/
    test1/
8. exist_ok

Nếu thư mục đã tồn tại.

exist_ok=True

→ ghi tiếp.

Nếu

False

YOLO sẽ tạo

predict2
predict3
predict4
...
9. device

Thiết bị chạy.

CPU

device="cpu"

GPU đầu tiên

device=0

GPU thứ hai

device=1
10. classes

Chỉ detect một số class.

Ví dụ

Dataset

0 stamp
1 signature
2 logo

Chỉ detect stamp

classes=[0]

Stamp + logo

classes=[0,2]

11. verbose

Hiển thị log.

verbose=True

In

image 1/15 ...
640x640
2 stamps
120ms

Nếu

False

→ chạy im lặng.

12. stream

Dùng generator thay vì tải toàn bộ kết quả vào RAM.

stream=True

Rất hữu ích khi xử lý video dài hoặc hàng nghìn ảnh vì tiết kiệm bộ nhớ.

13. show

Hiển thị cửa sổ ảnh.

show=True
14. max_det

Giới hạn số object.

max_det=300

Ví dụ

max_det=5

→ mỗi ảnh chỉ giữ tối đa 5 object.

15. agnostic_nms

Có phân biệt class khi NMS hay không.

agnostic_nms=True

Nếu hai class khác nhau nhưng box chồng lên nhau vẫn có thể bị loại.

Ví dụ đầy đủ
results = model.predict(
    source="images",
    imgsz=640,
    conf=0.3,
    iou=0.7,
    device="cpu",
    save=False,
    verbose=True,
    project="runs",
    name="predict_test",
    exist_ok=True,
    classes=[0]
)

Ý nghĩa:

Đọc toàn bộ ảnh trong images/
Resize về 640×640
Chỉ giữ box có confidence ≥ 0.3
Dùng IoU = 0.7 cho NMS
Chạy trên CPU
Không lưu ảnh kết quả
Hiển thị log trên terminal
Lưu (nếu bật save) vào runs/predict_test
Ghi đè thư mục nếu đã tồn tại
Chỉ detect class có ID 0
Các tham số bạn sẽ dùng nhiều nhất
Tham số	Công dụng
source	Nguồn ảnh/video/thư mục
conf	Ngưỡng confidence
iou	Ngưỡng NMS
imgsz	Kích thước ảnh đầu vào
device	CPU hoặc GPU
save	Lưu ảnh kết quả
project	Thư mục lưu
name	Tên phiên chạy
exist_ok	Cho phép ghi đè thư mục
classes	Lọc theo class
stream	Tiết kiệm RAM khi xử lý nhiều dữ liệu
verbose	Hiển thị log

Các tham số trên là những tùy chọn quan trọng và được sử dụng phổ biến nhất trong model.predict() của Ultralytics.