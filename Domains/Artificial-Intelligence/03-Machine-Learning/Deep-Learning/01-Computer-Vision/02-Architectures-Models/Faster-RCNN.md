- [Faster R-CNN](#faster-r-cnn)
---
# Faster R-CNN
```bash
Faster R-CNN là một mô hình Object Detection (phát hiện đối tượng) rất nổi tiếng, được giới thiệu năm 2015. Khác với bài toán Classification chỉ trả về tên ảnh, Faster R-CNN vừa:
    - Xác định đối tượng là gì (classification).
    - Xác định đối tượng nằm ở đâu (bounding box).

Dùng để:
    - Phát hiện vật thể chính xác cao nhưng chậm hơn YOLO.
    - Gồm 2 bước: Xác định vùng → nhận diện vật thể.
    - Dùng khi cần độ chính xác cao, ít quan trọng tốc độ.
```
**Ex: Ảnh có một con mèo và một con chó**
```bash
Classification:
    Input Image
          │
          ▼
      CNN (ResNet)
          │
          ▼
    Output: "Cat"
=> Chỉ biết trong ảnh có mèo

Object Detection (Faster R-CNN)
    +--------------------------------+
    |        ______                  |
    |       | Cat |                  |
    |       |_____|                  |
    |                    ________    |
    |                   | Dog   |    |
    |                   |_______|    |
    +--------------------------------+

    Output:
        Cat : (x1,y1,x2,y2)
        Dog : (x1,y1,x2,y2)
```
**Kiến trúc Faster R-CNN**
```bash
                Input Image
                     │
                     ▼
            Backbone CNN
         (VGG / ResNet ...)
                     │
                     ▼
               Feature Map
                /         \
               /           \
              ▼             ▼
           RPN         RoI Pooling
              │              │
              └──────┬───────┘
                     ▼
              Fully Connected
                 /       \
                ▼         ▼
         Classification  Bounding Box
```
**Workflow: luồng hoạt động**
```bash
Bước 1: Backbone CNN
    Ví dụ ảnh: 800x600

    Qua CNN:
        Input: 800 x 600 x 3
            ↓
        ResNet
            ↓
        50 x 38 x 1024
        => Đây gọi là Feature Map
            - Không còn pixel.
            - Mỗi điểm biểu diễn đặc trưng.

Bước 2: Region Proposal Network (RPN)

Đây là phần quan trọng nhất.

RPN nhìn vào Feature Map và trả lời:

"Ở đây có object không?"

Ví dụ

Feature Map

□□□□□□□□□□□□□□


RPN trượt một cửa sổ nhỏ (sliding window) qua từng vị trí.

□■□□□□□□□□□□□□


Sau đó

□□■□□□□□□□□□□□


Cứ như vậy cho toàn bộ ảnh.

Anchor Box

Tại mỗi vị trí,

RPN sinh nhiều Anchor.

Ví dụ:

      □

   ▭▭▭▭

  ██████


Hay

Anchor 1

40x40

Anchor 2

80x40

Anchor 3

40x80

Thông thường

3 scale

×

3 ratio

=

9 anchor

Mỗi điểm trên feature map có 9 anchor.

RPN dự đoán gì?

Cho mỗi anchor:

Anchor

↓

Objectness Score

↓

Bounding Box Offset

Ví dụ

Anchor

↓

0.98

↓

(+3,-2,+5,+1)

Nghĩa là

Có khả năng là object.
Dịch box một chút.
Non-Maximum Suppression (NMS)

RPN sẽ sinh rất nhiều box.

Ví dụ

□□□□□

 □□□□□

  □□□□□


Ba box gần như giống nhau.

NMS sẽ giữ box có điểm cao nhất.

█████

Các box trùng lặp bị loại.

Bước 3: RoI Pooling

Sau RPN ta có khoảng vài trăm proposal.

Mỗi proposal kích thước khác nhau.

Ví dụ

Cat

100x60

Dog

220x180

Neural Network cần đầu vào cùng kích thước.

RoI Pooling chuyển tất cả thành:

7 x 7

Ví dụ

100x60

↓

7x7

220x180

↓

7x7

Nhờ vậy Fully Connected xử lý được.

Bước 4: Classification

Sau RoI Pooling:

Proposal

↓

FC

↓

Cat

Ví dụ

Cat

0.98

Dog

0.01

Car

0.01
Bước 5: Bounding Box Regression

Ngoài class,

Network còn tinh chỉnh box.

Ví dụ

Proposal

────────────


Ground Truth

 ───────────

Network học

Δx
Δy
Δw
Δh

để box khớp hơn.

Toàn bộ Pipeline
Image
   │
   ▼
CNN Backbone
   │
   ▼
Feature Map
   │
   ├──────────────┐
   ▼              │
RPN               │
   │              │
Proposal          │
   ▼              │
RoI Pooling ◄─────┘
   │
   ▼
Fully Connected
   │
   ├──────────────┐
   ▼              ▼
Classification   Box Regression
Hàm Loss

Faster R-CNN học đồng thời hai nhiệm vụ:

1. Classification Loss

Dự đoán đúng nhãn.

Ví dụ

Cat

↓

Cross Entropy
2. Regression Loss

Điều chỉnh bounding box.

Thường dùng

Smooth L1 Loss

Tổng:

Loss=L
cls
	​

+λL
bbox
	​


Trong đó:

L
cls
	​

: mất mát phân loại.
L
bbox
	​

: mất mát hồi quy tọa độ hộp giới hạn.
λ: hệ số cân bằng giữa hai thành phần.
Ưu điểm

✅ Độ chính xác cao.

✅ Proposal được học tự động (không cần Selective Search).

✅ Backbone được chia sẻ giữa RPN và Detection Head nên nhanh hơn các phiên bản trước.

✅ Hoạt động tốt với nhiều loại đối tượng có kích thước khác nhau.

Nhược điểm

❌ Là mô hình two-stage detector (hai giai đoạn: tạo proposal rồi mới phân loại), nên chậm hơn các mô hình one-stage như YOLO hay SSD.

❌ Khó triển khai trên thiết bị có tài nguyên hạn chế hoặc yêu cầu thời gian thực.

❌ Kiến trúc phức tạp hơn các mô hình one-stage.

Tóm tắt trực quan
                   Input Image
                        │
                        ▼
                Backbone CNN
                        │
                 Feature Map
                        │
          ┌─────────────┴─────────────┐
          ▼                           ▼
 Region Proposal Network (RPN)    (chia sẻ feature)
          │
      Candidate Boxes
          │
          ▼
       RoI Pooling
          │
          ▼
    Detection Head
     ┌───────────────┬────────────────┐
     ▼               ▼
 Classification   Bounding Box
      (Cat)        (x, y, w, h)

Ý tưởng cốt lõi của Faster R-CNN có thể gói gọn trong một câu:

Thay vì dùng thuật toán bên ngoài để tìm các vùng nghi ngờ chứa vật thể, Faster R-CNN dùng Region Proposal Network (RPN) để học cách sinh các vùng đề xuất ngay trên feature map, sau đó phân loại và tinh chỉnh các vùng này. Việc chia sẻ cùng một backbone CNN giữa RPN và bộ phát hiện giúp mô hình vừa nhanh hơn đáng kể so với R-CNN/Fast R-CNN, vừa giữ được độ chính xác rất cao.