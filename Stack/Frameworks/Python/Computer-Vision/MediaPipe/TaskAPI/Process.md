- [BaseOptions()](#baseoptions)
  - [PoseLandmarkerOptions](#poselandmarkeroptions)
- [HandLandmarkerOptions](#handlandmarkeroptions)
- [PoseLandmarker](#poselandmarker)
  - [.create\_from\_options()](#create_from_options)
    - [.detect()](#detect)
      - [result.hand\_landmarks](#resulthand_landmarks)
      - [result.handedness](#resulthandedness)
      - [result.hand\_world\_landmarks](#resulthand_world_landmarks)
- [mp.Image](#mpimage)
---
# BaseOptions()
```bash
Dùng để load model
```
**Syn**
```bash
python.BaseOptions(
    model_asset_path="model.task"
)
```
**Ex**
```bash
base_options = python.BaseOptions(
    model_asset_path="pose_landmarker.task"
)
```
## PoseLandmarkerOptions
```bash
Cấu hình cho pose detection task.
```
**Syn**
```bash
vision.PoseLandmarkerOptions(
    base_options=...,
    running_mode=...
)

- runing_mode: 
    + vision.RunningMode.IMAGE          : xử lý ảnh
    + vision.RunningMode.VIDEO          : video offline
    + vision.RunningMode.LIVE_STREAM    : webcam realtime
```
**Ex**
```python
options = vision.PoseLandmarkerOptions(
    base_options=base_options,
    running_mode=vision.RunningMode.IMAGE
)
```
# HandLandmarkerOptions
**Syn**
```bash
HandLandmarkerOptions(
    base_options=base_options,
    running_mode=vision.RunningMode.IMAGE
)
```
# PoseLandmarker
```bash
Đây là AI model cho pose detection.
```
## .create_from_options()
```bash
- Dùng để:
    + khởi tạo model
    + load neural network
    + apply config
```
**Syn**
```bash
PoseLandmarker.create_from_options(options)
```
### .detect()
**Syn**
```bash
detect(image: mp.Image) -> ResultObject

- Input: mp.Image
- Output: Một Result object tùy model.
    + HandLandmarker	: HandLandmarkerResult
    + PoseLandmarker	: PoseLandmarkerResult
    + FaceLandmarker	: FaceLandmarkerResult
```
#### result.hand_landmarks
```bash
- có dạng list chứa các điểm dect được trên bàn tay nhưng nó chứa tọa độ đã normalized (0 -> 1)
```
#### result.handedness
#### result.hand_world_landmarks
# mp.Image
```bash
- Tasks API không dùng numpy trực tiếp như Solutions.
- Bạn phải convert sang: mp.Image
```
**Syn**
```bash
mp.Image(
    image_format=mp.ImageFormat.SRGB,
    data=numpy_array
)

- image_format: kiểu màu của ảnh
    + SRGB	: RGB image
    + SRGBA	: RGB + alpha
    + GRAY8	: grayscale
```