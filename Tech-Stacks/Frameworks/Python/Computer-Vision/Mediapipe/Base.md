- [Introduction](#introduction)
  - [Architecture (kiến trúc)](#architecture-kiến-trúc)
  - [Installation](#installation)
---
# Introduction
```bash
- Đây là framework xử lý pipeline ML realtime của Google 
    + dùng để xử lý vision realtime
    + nhận diện tay, pose, mặt, tracking… từ camera. 

Nó cung cấp các model sẵn như:
    + Hand              : Tracking	nhận diện bàn tay
    + Face Mesh	        : 468 điểm trên khuôn mặt
    + Pose	            : nhận diện skeleton cơ thể
    + Object Detection	: phát hiện vật
    + Gesture	        : nhận diện cử chỉ
```
## Architecture (kiến trúc)
```bash
Camera/Image
     ↓
Convert BGR → RGB
     ↓
MediaPipe model process()
     ↓
Results (landmarks / detection)
     ↓
Draw / xử lý logic
```
## Installation
```bash
1. pip install mediapipe opencv-python | pip install mediapipe==0.10.20      # để cài bản ổn định
```