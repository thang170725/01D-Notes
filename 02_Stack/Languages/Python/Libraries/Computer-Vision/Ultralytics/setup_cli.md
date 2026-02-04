- [YOLO()](#yolo)
- [nó sẽ in ra cấu trúc nơ ron của YOLO](#nó-sẽ-in-ra-cấu-trúc-nơ-ron-của-yolo)
---
# YOLO() 
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