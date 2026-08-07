- [Accuracy Optimization (Tối ưu độ chính xác cho các bài toán computer vision)](#accuracy-optimization-tối-ưu-độ-chính-xác-cho-các-bài-toán-computer-vision)
- [IoU](#iou)
- [mAP50](#map50)
---
# Accuracy Optimization (Tối ưu độ chính xác cho các bài toán computer vision)
[Tối ưu độ chính xác nói chung cho AI](../../../04-Evaluate-Optimize/Accuracy_Optimization.md)

# IoU
**Ex**
```bash
Giả sử ảnh có một con mèo.
    Ground Truth (đáp án đúng):
        +-------------+
        |             |
        |   Con mèo   |
        |             |
        +-------------+

    Model dự đoán
        +-------------+
        |             |
        |   Con mèo   |
        |             |
        +-------------+

    Hai hình không khớp hoàn toàn.

    Ta đo mức chồng nhau bằng IoU (Intersection over Union).
        Công thức: IoU = Phần giao nhau / Phần hợp lại
```
# mAP50
```bash
Số 50 nghĩa là IoU = 0.50
    Quy định:
        Nếu IoU >= 0.5 -> thì dự đoán được xem là đúng.

    Ví dụ
        Ground truth
            ##########
            ##########
            ##########

        Prediction
            #########
            #########
            #########

        IoU = 0.72. Do 0.72 > 0.5 -> nên được tính là đúng.

Giả sử model phát hiện 100 đối tượng.
    Có 80 đối tượng đạt vì IoU >= 0.5 -> thì mAP50 sẽ rất cao.
```
**AP (Average Precision) là gì?**
```bash
Thay vì chỉ kiểm tra một ngưỡng confidence, người ta thay đổi confidence từ
    1.0 -> 0.9 -> 0.8 -> ... -> 0

Mỗi lần sẽ có: Precision, Recall Khác nhau.

Sau đó vẽ đồ thị.
    Precision
    1.0 |\
        | \
    0.8 |  \
        |   \
    0.6 |    \____
        |
        +----------------
    
         Recall

Diện tích dưới đường cong chính là AP.

mAP là gì?

m = mean

Nghĩa là trung bình.

Ví dụ có

3 class

Cat

Dog

Person

AP

Cat     92%

Dog     88%

Person  96%

mAP

(92+88+96)/3

=92%
mAP50-95 là gì?

Đây là chỉ số khó hơn nhiều.

Không chỉ tính ở

IoU=0.5

mà tính ở

0.50

0.55

0.60

0.65

0.70

0.75

0.80

0.85

0.90

0.95

Tổng cộng

10 mức.

Ví dụ

Model đạt

IoU	AP
0.50	96
0.55	95
0.60	94
0.65	92
0.70	90
0.75	87
0.80	84
0.85	80
0.90	73
0.95	60

Lấy trung bình

=85.1%

Đó chính là

mAP50-95
Tại sao mAP50 luôn lớn hơn?

Ví dụ

Prediction

Ground Truth

+----------+
|          |
|          |
+----------+

Prediction

 +---------+
 |         |
 |         |
 +---------+

IoU

0.63

Khi đó

Ở

IoU=0.5

Đúng.

Ở

IoU=0.75

Sai.

Ở

IoU=0.95

Càng sai.

Cho nên

mAP50

>

mAP50-95

gần như luôn đúng.

Ví dụ kết quả YOLO
Precision      0.97

Recall         0.94

mAP50          0.98

mAP50-95       0.81

Nghĩa là

Nếu chỉ cần box trùng khoảng 50%

→ model gần như hoàn hảo.

Nhưng

Nếu yêu cầu box cực kỳ chính xác

→ còn sai khá nhiều.

Vì sao cuộc thi AI hay dùng mAP50-95?

Vì nếu chỉ dùng mAP50 thì một box lệch khá nhiều nhưng vẫn đạt IoU ≥ 0.5 có thể vẫn được tính là đúng. Điều này chưa phản ánh tốt chất lượng định vị.

mAP50-95 đánh giá trên nhiều ngưỡng IoU từ 0.50 đến 0.95, nên mô hình muốn đạt điểm cao phải vừa phát hiện đúng đối tượng, vừa đặt hộp bao (bounding box) thật sát với đối tượng. Do đó đây là thước đo khắt khe và toàn diện hơn, đặc biệt trong các bộ dữ liệu và cuộc thi như COCO.

Tóm tắt
Chỉ số	Ý nghĩa	Dễ hay khó
IoU	Đo mức chồng lấp giữa box dự đoán và box thật	Cơ bản
AP	Điểm của một lớp (ví dụ chỉ lớp "cat") ở một ngưỡng IoU	Trung bình
mAP	Trung bình AP của tất cả các lớp	Trung bình
mAP50	mAP khi chỉ yêu cầu IoU ≥ 0.50	Dễ hơn
mAP50-95	Trung bình mAP trên các ngưỡng IoU từ 0.50 đến 0.95	Khắt khe hơn

Vì vậy, khi xem kết quả huấn luyện YOLO, nếu thấy mAP50 = 98% nhưng mAP50-95 = 82%, điều đó không có nghĩa mô hình nhận diện kém. Nó cho thấy mô hình phát hiện đúng đối tượng rất tốt, nhưng vị trí của một số bounding box vẫn có thể được tinh chỉnh để sát với đối tượng hơn.