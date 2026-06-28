- [Create (Nhóm khởi tạo MediaPipe modules)](#create-nhóm-khởi-tạo-mediapipe-modules)
  - [mp.solutions.hands.Hands()](#mpsolutionshandshands)
  - [mp.solutions.pose.Pose()](#mpsolutionsposepose)
  - [mp.solutions.face\_mesh.FaceMesh()](#mpsolutionsface_meshfacemesh)
  - [mp.solutions.face\_detection.FaceDetection()](#mpsolutionsface_detectionfacedetection)
- [Process (Thao tác xử lý)](#process-thao-tác-xử-lý)
  - [process()](#process)
- [Access (Nhóm truy cập dữ liệu landmark)](#access-nhóm-truy-cập-dữ-liệu-landmark)
  - [hand\_landmarks.landmark](#hand_landmarkslandmark)
  - [landmark.x](#landmarkx)
  - [landmark.y](#landmarky)
  - [landmark.z](#landmarkz)
- [Draw (Nhóm vẽ landmark)](#draw-nhóm-vẽ-landmark)
  - [draw\_landmarks()](#draw_landmarks)
  - [draw\_detection()](#draw_detection)
- [CONSTANT (Nhóm constant quan trọng)](#constant-nhóm-constant-quan-trọng)
  - [HAND\_CONNECTIONS](#hand_connections)
  - [POSE\_CONNECTIONS](#pose_connections)
  - [FACEMESH\_TESSELATION](#facemesh_tesselation)
- [Result (Nhóm kết quả)](#result-nhóm-kết-quả)
  - [results.multi\_hand\_landmarks](#resultsmulti_hand_landmarks)
  - [results.multi\_face\_landmarks](#resultsmulti_face_landmarks)
  - [results.pose\_landmarks](#resultspose_landmarks)
---
# Create (Nhóm khởi tạo MediaPipe modules)
## mp.solutions.hands.Hands()
```bash
Khởi tạo hand tracking model.
```
**Syn**
```bash
hands = mp.solutions.hands.Hands(
    static_image_mode=False,
    max_num_hands=2,
    model_complexity=1,
    min_detection_confidence=0.5,
    min_tracking_confidence=0.5
)

- static_image_mode	        : True nếu xử lý ảnh tĩnh
- max_num_hands	            : số bàn tay tối đa
- model_complexity	        : độ chính xác model
- min_detection_confidence	: ngưỡng detect
- min_tracking_confidence	: ngưỡng tracking
```
## mp.solutions.pose.Pose()
```bash
Detect skeleton body pose.
```
**Syn**
```bash
mp.solutions.pose.Pose(
    static_image_mode=False,
    model_complexity=1,
    enable_segmentation=False,
    min_detection_confidence=0.5,
    min_tracking_confidence=0.5
)

- Output : 33 body landmarks.
```
## mp.solutions.face_mesh.FaceMesh()
```bash
Detect 468 điểm khuôn mặt.
```
**Syn**
```bash
mp.solutions.face_mesh.FaceMesh(
    static_image_mode=False,
    max_num_faces=1,
    refine_landmarks=True,
    min_detection_confidence=0.5,
    min_tracking_confidence=0.5
)
```
## mp.solutions.face_detection.FaceDetection()
```bash
Detect khuôn mặt (nhanh hơn face mesh).
```
**Syn**
```bash
mp.solutions.face_detection.FaceDetection(
    model_selection=0,
    min_detection_confidence=0.5
)
```
# Process (Thao tác xử lý)
## process()
```bash
Chạy model để detect object.
```
**Syn**
```bash
results = model.process(image)

- Output: object chứa:
    + results.multi_hand_landmarks
    + results.multi_hand_world_landmarks
    + results.multi_handedness
```
# Access (Nhóm truy cập dữ liệu landmark)
```bash
MediaPipe trả về landmark object.
```
## hand_landmarks.landmark
```bash
Truy cập danh sách landmark.
```
**Syn**
```bash
hand_landmarks.landmark[index]
```
## landmark.x
```bash
Tọa độ X. Giá trị 0 → 1
```
## landmark.y
## landmark.z
```bash
Độ sâu.
```
# Draw (Nhóm vẽ landmark)
```bash
- MediaPipe có utility vẽ sẵn.
- Module: mp.solutions.drawing_utils
```
## draw_landmarks()
```bash
Vẽ landmark lên ảnh.
```
**Syn**
```bash
mp_draw.draw_landmarks(
    image,
    landmark_list,
    connections
)
```
**Ex**
```python
mp_draw.draw_landmarks(
    frame,
    hand_landmarks,
    mp_hands.HAND_CONNECTIONS
)
```
## draw_detection()
```bash
Vẽ bounding box.
```
**Syn**
```bash
mp_draw.draw_detection(frame, detection)
```
# CONSTANT (Nhóm constant quan trọng)
## HAND_CONNECTIONS
```bash
Danh sách các đường nối tay.
```
**Ex**
```python
mp_hands.HAND_CONNECTIONS
```
## POSE_CONNECTIONS
```bash
Cho skeleton.
```
**Ex**
```python
mp_pose.POSE_CONNECTIONS
```
## FACEMESH_TESSELATION
```bash
Cho mesh mặt.
```
**Ex**
```python
mp_face_mesh.FACEMESH_TESSELATION
```
# Result (Nhóm kết quả)
## results.multi_hand_landmarks
```bash
Danh sách bàn tay.
```
**Ex**
```python
for hand in results.multi_hand_landmarks:
    results.multi_handedness

# Cho biết tay trái / phải.
```
## results.multi_face_landmarks
```bash
Landmark khuôn mặt.
```
## results.pose_landmarks
