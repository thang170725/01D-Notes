- [Create \& Config (khởi tạo)](#create--config-khởi-tạo)
  - [FaceAnalysis](#faceanalysis)
- [Analyze (phân tích khuôn mặt)](#analyze-phân-tích-khuôn-mặt)
  - [.get()](#get)
---
# Create & Config (khởi tạo)
## FaceAnalysis
```bash
from insightface.app import FaceAnalysis

app = FaceAnalysis(name="buffalo_l")  # model phổ biến
app.prepare(ctx_id=0)  # 0 = GPU, -1 = CPU

- name: model (buffalo_l, buffalo_m,...)
- ctx_id:
    + 0 → GPU
    + -1 → CPU
```
# Analyze (phân tích khuôn mặt)
## .get()
```bash
faces = app.get(img)

- Output mỗi face gồm:
    + face.bbox        # bounding box
    + face.kps         # keypoints (mắt, mũi,...)
    + face.embedding   # vector 512 chiều
    + face.age         # tuổi
    + face.gender      # giới tính
5.3 So sánh khuôn mặt (core của backend bạn)
import numpy as np

sim = np.dot(f1.embedding, f2.embedding)

👉 Hoặc dùng cosine similarity:

from numpy.linalg import norm

sim = np.dot(f1.embedding, f2.embedding) / (norm(f1.embedding) * norm(f2.embedding))

📌 Threshold thường:

0.3 ~ 0.5 → cùng người (tùy model)

5.4 Load ảnh

InsightFace không có hàm riêng, dùng OpenCV:

import cv2
img = cv2.imread("face.jpg")
5.5 Lấy embedding riêng (thực tế vẫn dùng get)

Không có API riêng nữa → embedding lấy từ face.embedding

1. Pipeline chuẩn (theo best practice)

Flow chuẩn (backend):

img = cv2.imread("input.jpg")
faces = app.get(img)

if len(faces) == 0:
    return "No face"

embedding = faces[0].embedding

So sánh với DB:

for db_embedding in database:
    sim = cosine(embedding, db_embedding)
7. Model phổ biến
buffalo_l (🔥 recommend)
buffalo_m
antelope

👉 buffalo_l = accuracy tốt + stable

8. Tóm lại (rất ngắn gọn)
InsightFace = thư viện
Dùng cho: nhận diện khuôn mặt
API mới:
FaceAnalysis()
app.prepare()
app.get()
Output chính: embedding để so sánh
9. Gợi ý riêng cho case của bạn

Với system bạn đang làm:

Frontend:

gửi ảnh raw là đủ (đừng gửi bbox)

Backend:

dùng app.get()
lấy embedding
so sánh cosine

Nếu bạn muốn, mình có thể:

viết luôn API FastAPI backend chuẩn production
hoặc thiết kế DB lưu embedding tối ưu (scale lớn)