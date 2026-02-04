- [Cấu trúc thư mục](#cấu-trúc-thư-mục)
- [Installation](#installation)
---
# Cấu trúc thư mục
```bash
Ultralytics/
├── 01_setup_cli.md       # Cài đặt, CLI commands & Model weights
├── 02_data_yaml.md       # Cấu trúc dataset, file config.yaml, Augmentation
├── 03_training_val.md    # Huấn luyện (Train) & Đánh giá (Validation/Metrics)
├── 04_inference_predict.md # Dự đoán & lấy kết quả, giá trị, Export model (ONNX, TensorRT)
└── 05_object_tracking.md # Theo dõi vật thể (ByteTrack, BoT-SORT)Ultralytics
```
# Installation
```bash
pip install ultralytics
```

.train()
from ultralytics import YOLO

model = YOLO("yolov8n.pt")

model.train(
    data="data.yaml",
    epochs=50,
    imgsz=640,
    batch=16
)
train: datasets/images/train
val: datasets/images/val

names:
  0: cat
  1: dog

.data

Predict()
Hàm predict là hàm cốt lõi để chạy suy luận (inference) trên ảnh, video hoặc luồng dữ liệu theo thời gian thực.
Cú pháp:
results = model.predict(source, classes=[] stream=False, conf=0.25, iou=0.7, save=False…)
    • source:"Đầu vào (ảnh, video, thư mục ảnh, URL, luồng webcam, v.v.). str, Path, list, np.ndarray",
    • classes               :Dùng để chỉ định đối tượng nào sẽ được detect. tham số truyền vào là một mảng
    • conf: Ngưỡng độ tin cậy tối thiểu để chấp nhận một phát hiện – float - mặc định là 0.25
    • iou: Ngưỡng IOU (Intersection over Union) cho Non-Maximum Suppression (NMS) – float mặc định là 0.7
    • stream,"Chế độ xử lý luồng dữ liệu (ví dụ: video/webcam). Nếu True, sẽ trả về một trình tạo (generator).",bool,False,Không
    • save: Lưu kết quả suy luận (ảnh/video có hộp giới hạn) vào thư mục runs/detect/predict – bool - mặc định là False
    • show,Hiển thị kết quả trong một cửa sổ Pop-up.,bool,False,Không
    • device=’cuda’: thiết lập chạy trên gpu
from ultralytics import YOLO
import cv2

model = YOLO('weights/yolov8n.pt')

results_list = model.predict(
    source='data/images/many-objects.jpeg',
    conf=0.5,
    save=False
)

result = results_list[0]

total_detections = len(result.boxes)
print(f'tổng detect {total_detections}')

annotated_img = result.plot()

cv2.imshow("Demo", annotated_img)
cv2.waitKey(1)

if total_detections > 0:
        first_box = result.boxes[0]
        cls_id = int(first_box.cls[0].item())
        conf = first_box.conf[0].item()
        obj_name = model.names[cls_id]
        print(f"  -> Phát hiện đầu tiên: **{obj_name}** | Conf: **{conf:.2f}**")
tổng detect 5
  -> Phát hiện đầu tiên: **cup** | Conf: **0.95**
from ultralytics import YOLO
import cv2

model = YOLO('weights/yolov8n.pt')

results = model.predict(
    source='data/images/many-objects.jpeg',
    conf=0.5,
    save=False,
    device='cuda'
)
print(results)
boxes: ultralytics.engine.results.Boxes object
keypoints: None
masks: None
names: {0: 'person', 1: 'bicycle', 2: 'car', 3: 'motorcycle', 4: 'airplane', 5: 'bus', 6: 'train', 7: 'truck', 8: 'boat', 9: 'traffic light', 10: 'fire hydrant', 11: 'stop sign', 12: 'parking meter', 13: 'bench', 14: 'bird', 15: 'cat', 16: 'dog', 17: 'horse', 18: 'sheep', 19: 'cow', 20: 'elephant', 21: 'bear', 22: 'zebra', 23: 'giraffe', 24: 'backpack', 25: 'umbrella', 26: 'handbag', 27: 'tie', 28: 'suitcase', 29: 'frisbee', 30: 'skis', 31: 'snowboard', 32: 'sports ball', 33: 'kite', 34: 'baseball bat', 35: 'baseball glove', 36: 'skateboard', 37: 'surfboard', 38: 'tennis racket', 39: 'bottle', 40: 'wine glass', 41: 'cup', 42: 'fork', 43: 'knife', 44: 'spoon', 45: 'bowl', 46: 'banana', 47: 'apple', 48: 'sandwich', 49: 'orange', 50: 'broccoli', 51: 'carrot', 52: 'hot dog', 53: 'pizza', 54: 'donut', 55: 'cake', 56: 'chair', 57: 'couch', 58: 'potted plant', 59: 'bed', 60: 'dining table', 61: 'toilet', 62: 'tv', 63: 'laptop', 64: 'mouse', 65: 'remote', 66: 'keyboard', 67: 'cell phone', 68: 'microwave', 69: 'oven', 70: 'toaster', 71: 'sink', 72: 'refrigerator', 73: 'book', 74: 'clock', 75: 'vase', 76: 'scissors', 77: 'teddy bear', 78: 'hair drier', 79: 'toothbrush'}
obb: None
orig_img: array([[[ 45,  38,  35],
        [ 45,  38,  35],
        [ 47,  40,  37],
        ...,
        [100,  94,  95],
        [ 99,  93,  94],
        [ 99,  93,  94]]], dtype=uint8)
orig_shape: (482, 860)
path: '/home/thang/projects/Test/data/images/many-objects.jpeg'
probs: None
save_dir: 'runs/detect/predict'
speed: {'preprocess': 3.1937180001477827, 'inference': 126.71867700009898, 'postprocess': 228.35321700040367}]
.tolist()