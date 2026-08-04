- [YOLO HBB Introduction (thực hiện tác vụ phát hiện vật thể (Object Detection) trong thời gian thực)](#yolo-hbb-introduction-thực-hiện-tác-vụ-phát-hiện-vật-thể-object-detection-trong-thời-gian-thực)
  - [C2f (Cross-Stage Partial Bottleneck với hai kênh đặc trưng)](#c2f-cross-stage-partial-bottleneck-với-hai-kênh-đặc-trưng)
- [Architecture (Kiến Trúc Mô Hình YOLO - Workflow)](#architecture-kiến-trúc-mô-hình-yolo---workflow)
- [file yaml (Đây là file YAML mô tả dataset)](#file-yaml-đây-là-file-yaml-mô-tả-dataset)
  - [Ask (Các câu hỏi về kiến trúc mô hình YOLO)](#ask-các-câu-hỏi-về-kiến-trúc-mô-hình-yolo)
- [Workflow khi đưa một ảnh vào YOLOv8 để detect object](#workflow-khi-đưa-một-ảnh-vào-yolov8-để-detect-object)
---
# YOLO HBB Introduction (thực hiện tác vụ phát hiện vật thể (Object Detection) trong thời gian thực)
**Thư viện sử dụng YOLO**
[Ultralytics](../../../../../../../Tech-Stacks/Programming-Languages/Python/Core/01-Libraries/AI-Libraries/00-CV/Detection/Ultralytics/Process.md)
```bash
Cái tên "You Only Look Once" nói lên điểm cốt lõi: nó xử lý toàn bộ hình ảnh chỉ trong một lần duy nhất.
    Các version YOLOv1 -> YOLOv8 là các model cụ thể.
```
**Nhãn**
```bash
Đối với YOLO Bounding Box thông thường (HBB), mỗi object được biểu diễn bởi 5 giá trị:
    class_id x_center y_center width height
        Ví dụ: 2 0.625 0.4375 0.25 0.3125

        - class_id	ID của lớp đối tượng (0, 1, 2, ...)
        - x_center	Tọa độ x của tâm bounding box (đã chuẩn hóa từ 0 đến 1)
        - y_center	Tọa độ y của tâm bounding box (đã chuẩn hóa từ 0 đến 1)
        - width	    Chiều rộng của bounding box (đã chuẩn hóa)
        - height	Chiều cao của bounding box (đã chuẩn hóa)
```
**Ex**
```bash
Giả sử ảnh có kích thước:
    - Width = 640 pixel
    - Height = 480 pixel

Trong ảnh có một con chó.
    Bounding box của nó là:
        - Góc trái trên: (160, 120)
        - Góc phải dưới: (320, 280)

Bước 1. Tính chiều rộng và chiều cao
    - width = 320 - 160 = 160 pixel
    - height = 280 - 120 = 160 pixel

Bước 2. Tính tâm
    - x_center = (160 + 320) / 2 = 240
    - y_center = (120 + 280) / 2 = 200

Bước 3. Chuẩn hóa về khoảng [0,1]
    YOLO không lưu pixel, mà lưu theo tỷ lệ so với kích thước ảnh.
        - x_center = 240 / 640 = 0.375
        - y_center = 200 / 480 = 0.4167
        - width = 160 / 640 = 0.25
        - height = 160 / 480 = 0.3333

Nếu con chó có class_id = 0, file nhãn sẽ là:
    0 0.375 0.4167 0.25 0.3333

Minh họa: Ảnh 640 × 480
(0,0)
+--------------------------------------------------+
|                                                  |
|         +--------------------+                   |
|         |                    |                   |
|         |       DOG          |                   |
|         |         ●          | ← tâm             |
|         |                    |                   |
|         +--------------------+                   |
|                                                  |
+--------------------------------------------------+

YOLO chỉ lưu:
    - class_id
    - x_center
    - y_center
    - width
    - height

Nếu có nhiều đối tượng
    Ví dụ ảnh có:
        - chó (class = 0)
        - mèo (class = 1)
        - người (class = 2)

File 0001.txt sẽ có dạng:
0 0.32 0.48 0.21 0.30
1 0.74 0.40 0.15 0.22
2 0.52 0.65 0.18 0.42
-> Mỗi dòng tương ứng với một đối tượng trong ảnh.
```
**Tại sao YOLO dùng tọa độ chuẩn hóa?**
```bash
Thay vì lưu pixel như: 240 200 160 160
    YOLO lưu: 0.375 0.4167 0.25 0.3333
        Nhờ vậy: 
            - Cùng một nhãn có thể dùng cho ảnh ở nhiều độ phân giải khác nhau (640×480, 1280×960, 1920×1440, ...).
            - Mô hình dễ học hơn vì các giá trị luôn nằm trong khoảng 0 đến 1.
            - Không cần sửa lại nhãn nếu ảnh được resize trong quá trình huấn luyện.

Lưu ý: Với YOLO OBB (Oriented Bounding Box) thì định dạng nhãn sẽ khác. Thay vì 5 giá trị (class x_center y_center width height), thường sẽ lưu thêm góc xoay hoặc 4 đỉnh của hình chữ nhật xoay, tùy theo phiên bản YOLO và công cụ gán nhãn bạn sử dụng.
```
## C2f (Cross-Stage Partial Bottleneck với hai kênh đặc trưng)
**Tại sao YOLO lại cần C2f?**
```bash
- Giảm nghẽn cổ chai gradient (Gradient Vanishing): 
    Nhờ có nhánh đi tắt (shortcut), các tín hiệu lỗi khi lan truyền ngược (backpropagation) có thể truyền thẳng về các tầng trước mà không bị tiêu biến khi đi qua quá nhiều lớp tích chập sâu.
- Tốc độ cực nhanh: Việc chia đôi kênh (Split) giúp giảm một nửa khối lượng tham số toán học cần tính toán trong các lớp tích chập của Bottleneck, giúp GPU/NPU chạy mượt mà, đạt FPS cao khi deploy thực tế.
```
**Cơ chế hoạt động của C2f**
```bash
Cột mốc tư duy của C2f dựa trên kiến trúc CSP (Cross-Stage Partial Network). Thay vì bắt toàn bộ các kênh dữ liệu đi qua một chuỗi lớp tích chập nặng nề, C2f chia dòng chảy dữ liệu ra làm hai phần:
    - Nhánh đi tắt (Shortcut/Identity): Một nửa số kênh đặc trưng được giữ nguyên và dẫn thẳng tới cuối khối.
    - Nhánh xử lý sâu: Nửa còn lại được đưa qua một chuỗi các khối Bottleneck (các lớp tích chập nhỏ) để trích xuất các đặc trưng phức tạp.

Điểm cải tiến "đắt giá" của C2f so với C3 là tính năng phân tách dòng chảy đa tầng (Split & Rich Gradient flow). Trong C2f, đầu ra của từng khối Bottleneck nhỏ đều được thu thập lại và ép (Concat) chung với nhau, thay vì chỉ lấy đầu ra của khối cuối cùng.
```
**Quy trình xử lý dữ liệu bên trong C2f**
```bash
Dữ liệu đầu vào (Input) với X kênh màu
          │
          ▼
    [ Lớp Conv 1x1 ] ──► (Giảm hoặc giữ nguyên số kênh để tối ưu tính toán)
          │
          ▼
      [ Split ] ──► Chia làm 2 nửa bằng nhau: Nửa_A và Nửa_B
          │
          ├─────────────────────────────────────────┐ (Nhánh đi tắt)
          ▼                                         │
     ( Nửa_B )                                      │
          │                                         │
          ├─► [ Bottleneck 1 ] ──► Lấy Output_1 ──┐ │
          │                            │          │ │
          ▼                            ▼          ▼ ▼
     ( Đặc trưng tiếp theo ) ──► [ Bottleneck 2 ] ──► Lấy Output_2
          │                                           │
          ▼                                           ▼
      [ Concat ] ◄────────────────────────────────────┘
   (Gộp tất cả lại: Nửa_A + Nửa_B + Output_1 + Output_2 + ...)
          │
          ▼
    [ Lớp Conv 1x1 ] ──► (Hợp nhất và trả về số kênh đầu ra theo cấu hình)
          │
          ▼
      Đầu ra (Output)
```
**Ví dụ số học trực quan (Trình diễn Shape)**
```bash
Giả sử tại một tầng trong Backbone của YOLOv8, dòng dữ liệu đi vào khối C2f có kích thước là [Batch_size, 64, 64, 256] (tức là ảnh có độ phân giải 64×64 và chứa 256 kênh đặc trưng). Khối C2f này được cấu hình có 2 khối Bottleneck bên trong.
```
```bash
Quá trình biến đổi Shape sẽ diễn ra như sau:

Bước 1 (Qua Conv 1x1 đầu tiên): Giả sử cấu hình giữ nguyên kênh, tensor vẫn là [64, 64, 256].

Bước 2 (Split): Tách 256 kênh này thành 2 nhánh bằng nhau theo chiều sâu:
    - Nhánh A: [64, 64, 128] (Đi thẳng xuống hàng chờ Concat).
    - Nhánh B: [64, 64, 128] (Chuẩn bị đi qua chuỗi Bottleneck).

Bước 3 (Xử lý qua các Bottleneck):
    - Nhánh B [64, 64, 128] đi vào Bottleneck 1 → Tạo ra Output_1 có kích thước [64, 64, 128].
    - Lấy Output_1 tiếp tục đưa vào Bottleneck 2 → Tạo ra Output_2 có kích thước [64, 64, 128].

Bước 4 (Hợp nhất - Concat): Mô hình tiến hành gom tất cả các đầu ra lại theo chiều kênh:
    Shape = Nhánh A + Nhánh B + Output_1 + Output_2
    Số kênh tổng = 128+128+128+128 = 512 kênh 
    => Kích thước lúc này phóng lên thành [64, 64, 512].

Bước 5 (Conv 1x1 cuối cùng): 
    Để tránh bùng nổ kích thước ở các tầng sau, lớp tích chập cuối cùng sẽ "nén" 512 kênh này về lại kích thước tiêu chuẩn ban đầu (ví dụ: 256 kênh).

Kết quả cuối cùng: Tensor ra khỏi khối C2f quay về kích thước lý tưởng [64, 64, 256] nhưng đã "giàu" thông tin học được hơn rất nhiều.
```
# Architecture (Kiến Trúc Mô Hình YOLO - Workflow)
```bash
Ảnh đầu vào gốc (Original Image) ──► [1024 x 1024 x 3]
      │
      ▼
┌───────────────────────────────────────────────────────────────────────────────────────────────────┐
│ 1. BACKBONE - TRÍCH XUẤT ĐẶC TRƯNG TỪNG LỚP (Lớp 0 -> Lớp 9)                                      │
│                                                                                                   │
│  ├── [Lớp 0] Conv2d (k=3, s=2, p=1) ──► [1024x1024x3] ──► [512 x 512 x 16]    (Mốc P1)            │
│  │                                                                                                │
│  ├── [Lớp 1] Conv2d (k=3, s=2, p=1) ──► [512x512x16]  ──► [256 x 256 x 32]                        │
│  │                                                                                                │
│  ├── [Lớp 2] Khối C2f (2 Bottlenecks) ──► Xử lý sâu trên mốc P2                                   │
│  │    └─ Split [256x256x32] ──► Nhánh A [16 kênh] (Shortcut) ─────────────────────────┐           │
│  │                          ──► Nhánh B [16 kênh] ──► Bottleneck x2 ──► Out [16 kênh] ┼─► Concat  │
│  │    └─ Kết quả Concat (Nhánh A + B + Các Out trung gian) ──► Conv1x1 nén về ──► [256 x 256 x 32]│
│  │                                                                                                │
│  ├── [Lớp 3] Conv2d (k=3, s=2, p=1) ──► [256x256x32]  ──► [128 x 128 x 64]                        │
│  │                                                                                                │
│  ├── [Lớp 4] Khối C2f (4 Bottlenecks) ──► TẠO RA TẦNG P3 (Đặc trưng vật thể nhỏ)                  │
│  │    └─ Split [128x128x64] ──► Nhánh A [32 kênh] ────────────────────────────────────┐           │
│  │                          ──► Nhánh B [32 kênh] ──► Bottleneck x4 ──► Out [32 kênh] ┼─► Concat  │
│  │    └─ Hợp nhất tất cả các đầu ra lại bằng Concat ──► Conv1x1 nén về ──► [128 x 128 x 128]      │
│  │         │                                                                                      │
│  │         └─► [Gửi Nhánh P3 này sang Lớp 14 ở phần Neck] ──────────────────────────────────────────────────┐
│  │                                                                                                │         │
│  ├── [Lớp 5] Conv2d (k=3, s=2, p=1) ──► [128x128x128] ──► [64 x 64 x 256]                         │         │
│  │                                                                                                │         │
│  ├── [Lớp 6] Khối C2f (4 Bottlenecks) ──► TẠO RA TẦNG P4 (Đặc trưng vật thể vừa)                  │         │
│  │    └─ Split [64x64x256] ──► Nhánh A [128 kênh] ────────────────────────────────────┐           │         │
│  │                         ──► Nhánh B [128 kênh] ──► Bottleneck x4 ──► Out [32 kênh] ┼─► Concat  │         │
│  │    └─ Hợp nhất tất cả các đầu ra lại bằng Concat ──► Conv1x1 nén về ──► [64 x 64 x 256]        │         │
│  │         │                                                                                      │         │
│  │         └─► [Gửi Nhánh P4 này sang Lớp 11 ở phần Neck] ────────────────────────────────────────────────┐ │
│  │                                                                                                │       │ │
│  ├── [Lớp 7] Conv2d (k=3, s=2, p=1) ──► [64x64x256]   ──► [32 x 32 x 512]                         │       │ │
│  │                                                                                                │       │ │
│  ├── [Lớp 8] Khối C2f (2 Bottlenecks) ──► TẠO RA TẦNG P5 (Đặc trưng ngữ cảnh sâu)                 │       │ │
│  │    └─ Chia đôi 512 kênh thành 256 kênh ──► Chạy qua 2 khối Bottleneck nối tiếp                 │       │ │
│  │    └─ Hợp nhất tất cả các đầu ra lại bằng Concat ──► Conv1x1 nén về ──► [32 x 32 x 512]        │       │ │
│  │                                                                                                │       │ │
│  └── [Lớp 9] Khối SPPF (Spatial Pyramid Pooling Fast)                                             │       │ │
│       ├─ Nhận đầu vào [32 x 32 x 512] từ Lớp 8                                                    │       │ │
│       ├─ Chia luồng: Nhánh 1 (Giữ nguyên) ──────────────────────────────────────────┐             │       │ │
│       ├─ Nhánh 2: Qua Pool1 (5x5) ──► Qua Pool2 (5x5) ──► Qua Pool3 (5x5)           │             │       │ │
│       │             [32x32x512]        [32x32x512]        [32x32x512]               ├─►Concat     │       │ │
│       └─ Concat 4 luồng (Gốc + 3 Pool) ──► 2048 kênh ──► Conv1x1 nén lại ──► [32 x 32 x 512] ───────┐     │ │
└───────────────────────────────────────────────────────────────────────────────────────────────────┘ │     │ │
                                                                                                      │     │ │
                                                                                                      │     │ │
┌──────────────────────────────────────────────────────────────────────────────────────────────────┐  │     │ │
│ 2. NECK - PHẦN HỢP NHẤT ĐẶC TRƯNG FPN / PAN (Lớp 10 -> Lớp 21)                                   │  │     │ │
│                                                                                                  │  │     │ │
│  🌐 GIAI ĐOẠN 1: Top-Down                                                                        │  │     │ │
│  │   (Lan truyền từ sâu xuống nông để giữ thông tin ngữ cảnh)                                    │  │     │ │
│  │   Phương pháp được sử dụng ở đây là Nearesr Neighbor Interpolation                            │  │     │ │
│  │   [Link phương pháp Nearesr Neighbor Interpolation]()                                         │  │     │ │
│  │                                               ┌──────────────────────────────────────────────────┘     │ │
│  │                                               ▼                                               │        │ │
│  ├── [Lớp 10] Upsample (Nội suy gần nhất) ────────────► Nhận từ Lớp 9 [32x32x512] ─► [64x64x512] │        │ │
│  │                                                                                               │        │ │
│  ├── [Lớp 11] Concat ──► Ghép Lớp 10 [64x64x512] ➕ Lớp 6 (P4 Backbone) [64x64x256] <─────────────────────┘ │
│  │    └─ Cộng số lượng kênh đặc trưng lại với nhau ─────────────────────► [64 x 64 x 768]        │          │
│  │                                                                                               │          │
│  ├── [Lớp 12] Khối C2f (2 Bottlenecks, không shortcut)                                           │          │
│  │    └─ Xử lý tổ hợp thông tin hỗn hợp vừa tạo ra ở lớp 11 ────────────► [64 x 64 x 256]        │          │
│  │                                                                                               │          │
│  ├── [Lớp 13] Upsample (Nội suy gần nhất) ──► Nhận từ Lớp 12 [64x64x256] ──► [128 x 128 x 256]   │          │
│  │                                                                                               │          │
│  ├── [Lớp 14] Concat ──► Ghép Lớp 13 [128x128x256] ➕ Lớp 4 (P3 Backbone) [128x128x128] <───────────────────┘
│  │    └─ Cộng số lượng kênh đặc trưng lại với nhau ─────────────────────► [128 x 128 x 384]      │
│  │                                                                                               │
│  ├── [Lớp 15] Khối C2f (2 Bottlenecks, không shortcut)                                           │
│  │    └─ Đầu ra hoàn chỉnh tích hợp thông tin vật thể nhỏ ──────────────► [128 x 128 x 128] ──┐  │
│  │                                                                                            │  │
│  🌐 GIAI ĐOẠN 2: Bottom-Up (Lan truyền từ nông lên sâu để giữ thông tin vị trí chính xác)     │  │
│  ├── [Lớp 16] Conv2d (k=3, s=2, p=1) ──► Hạ size dữ liệu từ Lớp 15 ──────► [64 x 64 x 128]    │  │
│  │                                                                                            │  │
│  ├── [Lớp 17] Concat ──► Ghép Lớp 16 [64x64x128] ➕ Lớp 12 (P4 trung gian) [64x64x256]        │  │
│  │    └─ Cộng số lượng kênh đặc trưng lại với nhau ─────────────────────► [64 x 64 x 384]     │  │
│  │                                                                                            │  │
│  ├── [Lớp 18] Khối C2f (2 Bottlenecks, không shortcut)                                        │  │
│  │    └─ Đầu ra hoàn chỉnh tích hợp thông tin vật thể vừa ──────────────► [64 x 64 x 256] ────┼┐ │
│  │                                                                                            ││ │
│  ├── [Lớp 19] Conv2d (k=3, s=2, p=1) ──► Hạ size dữ liệu từ Lớp 18 ──────► [32 x 32 x 256]    ││ │
│  │                                                                                            ││ │
│  ├── [Lớp 20] Concat ──► Ghép Lớp 19 [32x32x256] ➕ Lớp 9 (P5 SPPF gốc) [32x32x512]           ││ │
│  │    └─ Cộng số lượng kênh đặc trưng lại với nhau ─────────────────────► [32 x 32 x 768]     ││ │
│  │                                                                                            ││ │
│  └── [Lớp 21] Khối C2f (2 Bottlenecks, không shortcut)                                        ││ │
│       └─ Đầu ra hoàn chỉnh tích hợp thông tin vật thể lớn ──────────────► [32 x 32 x 512] ────┼┼┐│
└───────────────────────────────────────────────────────────────────────────────────────────────┼┼┼┘
                                                                                                │││
                                                                         ▼▼▼────────────────────┘┘┘
┌─────────────────────────────────────────────────────────────────────────────┐
│                       LỚP 22: LỚP ĐUÔI DỰ ĐOÁN (DETECT HEAD)                │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  3 Đầu vào song song từ phần Neck:                                          │
│  ┌──────────────────────┐ ┌──────────────────────┐ ┌──────────────────────┐ │
│  │ Nhánh 1 (Quét Nhỏ)   │ │ Nhánh 2 (Quét Vừa)   │ │ Nhánh 3 (Quét Lớn)   │ │
│  │ Size: [128 x 128x128]│ │ Size: [64 x 64 x256] │ │ Size: [32 x 32 x512] │ │
│  └──────────┬───────────┘ └──────────┬───────────┘ └──────────┬───────────┘ │
│             │                        │                        │             │
│             ▼                        ▼                        ▼             │
│  ┌────────────────────────────────────────────────────────────────────────┐ │
│  │ BƯỚC 1: TÁCH ĐÔI NHIỆM VỤ (Xử lý song song cho từng nhánh)             │ │
│  │                                                                        │ │
│  │                       [Ma trận đầu vào từ Neck]                        │ │
│  │                                   │                                    │ │
│  │                 ┌─────────────────┴─────────────────┐                  │ │
│  │                 ▼ (Dùng Conv2D 1x1)                 ▼ (Dùng Conv2D 1x1)│ │
│  │           [ Nhánh CLS - Nhãn ]                [ Nhánh REG - Khung ]    │ │
│  │          Đổi kênh về: [Số_Lớp]              Đổi kênh về cố định: [64]  │ │
│  └─────────────────┬───────────────────────────────────┬──────────────────┘ │
│                    │                                   │                    │
│                    ▼                                   ▼                    │
│  ┌────────────────────────────────────────────────────────────────────────┐ │
│  │ BƯỚC 2: TRẢI PHẲNG MA TRẬN (FLATTEN)                                   │ │
│  │ Duỗi ma trận 2D (H x W) thành 1 đường thẳng chứa tổng số vị trí        │ │
│  │                                                                        │ │
│  │  - Nhánh 1: Duỗi 128x128 ──────────────────────────► 16.384 vị trí     │ │
│  │  - Nhánh 2: Duỗi 64x64   ──────────────────────────►  4.096 vị trí     │ │
│  │  - Nhánh 3: Duỗi 32x32   ──────────────────────────►  1.024 vị trí     │ │
│  └─────────────────┬───────────────────────────────────┬──────────────────┘ │
│                    │                                   │                    │
│                    ▼                                   ▼                    │
│  ┌────────────────────────────────────────────────────────────────────────┐ │
│  │ BƯỚC 3: GIẢI MÃ TOẠ ĐỘ (DFL) & GHÉP KÊNH (CONCAT CHANNEL)              │ │
│  │                                                                        │ │
│  │   [Ma trận Nhãn]                                 [Ma trận Khung]       │ │
│  │   Size: [Vị_trí x Số_Lớp]                         Size: [Vị_trí x 64]  │ │
│  │         │                                               │              │ │
│  │         │                                               ▼ (Phép toán DFL)│
│  │         │                                        Tính ra 4 cạnh thực tế│ │
│  │         │                                         Size: [Vị_trí x 4]   │ │
│  │         │                                               │              │ │
│  │         └───────────────────────┬───────────────────────┘              │ │
│  │                                 ▼ (Ghép ngang)                         │ │
│  │                     Bảng kết quả riêng của từng nhánh                  │ │
│  │                         Size: [Vị_trí x (4 + Số_Lớp)]                  │ │
│  └─────────────────────────────────┬──────────────────────────────────────┘ │
│                                    │                                        │
│                                    ▼                                        │
│  ┌────────────────────────────────────────────────────────────────────────┐ │
│  │ BƯỚC 4: XẾP CHỒNG DỌC CẢ 3 NHÁNH (CONCAT SPATIAL)                      │ │
│  │                                                                        │ │
│  │ ┌────────────────────────────────────────────────────────────────────┐ │ │
│  │ │  Nhánh 1 (Quét Nhỏ)  : 16.384 dòng  x  [4 Tọa độ + Số_Lớp Nhãn]    │ │ │
│  │ ├────────────────────────────────────────────────────────────────────┤ │ │
│  │ │  Nhánh 2 (Quét Vừa)  :  4.096 dòng  x  [4 Tọa độ + Số_Lớp Nhãn]    │ │ │
│  │ ├────────────────────────────────────────────────────────────────────┤ │ │
│  │ │  Nhánh 3 (Quét Lớn)  :  1.024 dòng  x  [4 Tọa độ + Số_Lớp Nhãn]    │ │ │
│  │ └────────────────────────────────────────────────────────────────────┘ │ │
│  └─────────────────────────────────┬──────────────────────────────────────┘ │
│                                    │                                        │
└────────────────────────────────────┼────────────────────────────────────────┘
                                     ▼
                  ┌─────────────────────────────────────┐
                  │      MA TRẬN ĐẦU RA TỐI HẬU         │
                  │    Kích thước: [21.504 x 84]        │
                  │ (Ví dụ với tập dữ liệu COCO 80 lớp) │
                  └─────────────────────────────────────┘
                    (Sẵn sàng gửi sang thuật toán NMS 
                     để lọc bớt các khung trùng nhau)
```
# file yaml (Đây là file YAML mô tả dataset)
**Ex**
```bash
train: dataset/train/images
val: dataset/val/images

nc: 2

names:
  0: cat
  1: dog

# YOLO sẽ đọc file này để biết
# train ở đâu, validation ở đâu, có bao nhiêu class, tên class
# Nếu sai đường dẫn thì sẽ báo lỗi ngay.
```
## Ask (Các câu hỏi về kiến trúc mô hình YOLO)
**khi downsample từ 640x640x3 -> 20x20x256, thì 640x640x3 đúng là ảnh nhưng 20x20x256 có phải là ảnh đó nữa đâu, nó là lưu các vector đặc trưng về cạnh góc chứ thì liên quan gì đến object to nhỏ**
```bash
Đúng là khi xuống: 20×20×256 => thì nó KHÔNG còn là “ảnh” theo nghĩa thông thường nữa.

Nó là:
    semantic feature map
        tức: tensor đặc trưng
    
    chứa thông tin đã được encode

“vậy tại sao còn liên quan tới object to/nhỏ?”
    Câu trả lời nằm ở:
        Spatial correspondence vẫn còn tồn tại
        
        Dù không còn là ảnh RGB, nhưng:
            20×20 vẫn đại diện cho:
                vị trí không gian trong ảnh gốc.

        Cực kỳ quan trọng
            Ví dụ:
                Ảnh gốc: 640×640
                
                Sau 5 lần downsample: 20×20
                    thì: 1 pixel ở feature map 20×20 ≈ đại diện cho một vùng lớn trong ảnh gốc.
                    
                    Ví dụ: 1 cell ≈ 32×32 pixels
                        vì: 640 / 20 = 32
```
**tại sao lớp 2 dùng 2 bottlenecks mà lớp 4 dùng 4**
```bash
Sự khác biệt về số lượng khối Bottleneck (lớp 2 dùng 2, lớp 4 dùng 4) chính là nghệ thuật phân bổ tài nguyên tính toán trong thiết kế mạng mạng thần kinh (Neural Network Topology).

Trong kiến trúc YOLOv8, các nhà nghiên cứu không chia đều số lượng Bottleneck cho mọi tầng mà tuân theo một nguyên lý cốt lõi: Tập trung sức mạnh tính toán vào nơi chứa nhiều thông tin giá trị nhất.

Dưới đây là 3 lý do giải thích tại sao lớp 4 lại cần nhiều Bottleneck gấp đôi lớp 2:
    1. Bản đồ đặc trưng ở Lớp 4 chứa "Điểm Vàng" của thông tin
        Mỗi tầng phân giải trong Backbone đảm nhận một nhiệm vụ nhận diện phân cấp khác nhau:
            Lớp 2 (Tầng P2 - Kích thước 256×256): Đây là tầng rất nông. Bản đồ đặc trưng lúc này chủ yếu chứa các thông tin thô như cạnh, góc, kết cấu bề mặt, hoặc các đốm màu. Những thông tin này mang tính chất hình học sơ cấp, rất dễ trích xuất nên chỉ cần 2 khối Bottleneck là đã đủ để mô hình ghi nhớ và xử lý.

            Lớp 4 (Tầng P3 - Kích thước 128×128): Đây là "điểm vàng" nơi các cạnh và góc bắt đầu tổ hợp lại để hình thành nên bộ phận của vật thể (ví dụ: bánh xe, mắt, mũi, tay áo). Tầng này chứa lượng thông tin hình học và ngữ cảnh cực kỳ dồi dào, đóng vai trò then chốt để nhận diện các vật thể có kích thước nhỏ và vừa. Do cấu trúc thông tin ở đây phức tạp hơn rất nhiều, mô hình bắt buộc phải cần tới 4 khối Bottleneck để có thể học được các mối quan hệ phi tuyến sâu hơn.

    2. Chiến lược "Nặng ở Giữa" để tối ưu tốc độ (FPS)
        Nếu chúng ta tăng số lượng Bottleneck ở tất cả các lớp lên bằng nhau (ví dụ lớp nào cũng dùng 4 hoặc 6), mô hình sẽ bị chậm đi rất nhiều và không thể chạy thời gian thực (real-time) được nữa.

    Tại sao lại như vậy? Hãy nhìn vào kích thước không gian (Height x Width):
        Nếu tăng Bottleneck ở lớp 2, mô hình phải thực hiện các phép tính tích chập trên ma trận kích thước lớn lên tới 256×256. Chi phí tính toán (FLOPs) sẽ cực kỳ khổng lồ.

        Ở lớp 4, kích thước ma trận đã co lại còn 128×128 (nhỏ hơn 4 lần về mặt diện tích so với lớp 2). Việc tăng thêm Bottleneck ở đây giúp mô hình học sâu hơn rất nhiều nhưng lại tốn ít tài nguyên hơn so với việc tăng ở các tầng nông phía trên.

        Do đó, cấu trúc của YOLO thường được thiết kế theo dạng hình thoi hoặc phân tầng tăng dần ở giữa Backbone để tối ưu hóa giữa độ chính xác (Accuracy) và tốc độ xử lý (Speed).

    3. Sự tiến hóa qua các phiên bản YOLO
        Để bạn thấy rõ hơn xu hướng thiết kế này, hãy nhìn vào số lượng Bottleneck quy định trong file cấu hình gốc (.yaml) của YOLOv8 qua các tầng Backbone:

    Lớp trong mạng	Tên tầng đặc trưng	Số lượng Bottleneck (C2f)	Vai trò trích xuất
    Lớp 2	Tầng P2 (Nông)	2	Đặc trưng hình học thô (Cạnh, góc, màu sắc)
    Lớp 4	Tầng P3 (Trung cấp)	4	Cấu trúc vật thể nhỏ & vừa (Bộ phận vật thể)
    Lớp 6	Tầng P4 (Cao cấp)	4	Vật thể kích thước vừa & lớn
    Lớp 8	Tầng P5 (Sâu nhất)	2	Ngữ cảnh toàn cục (Mối quan hệ không gian lớn)

    Tóm lại: Lớp 4 cần 4 Bottleneck vì nó xử lý thông tin phức tạp hơn lớp 2 (bắt đầu hình thành hình dáng vật thể thay vì chỉ là các đường nét thô), đồng thời kích thước ảnh lúc này đã đủ nhỏ để mạng có thể "chồng" thêm nhiều lớp học sâu mà không làm sụt giảm FPS của mô hình khi chạy thực tế.
```
**nhìn có vẻ cặp lớp 1-2 và 3-4 có cấu trúc giống nhau. Tại sao Lớp 2 giữ nguyên 32 kênh từ Lớp 1, mà Lớp 4 lại tự ý tăng từ 64 lên 128 kênh?**
```bash
Câu trả lời nằm ở một bí mật thiết kế trong file cấu hình gốc: Thực chất Lớp 3 không phải là bản sao tỷ lệ của Lớp 1. Lớp 3 đã bị "ép" cắt bớt số kênh để tiết kiệm bộ nhớ, và Lớp 4 bắt buộc phải tăng kênh lên để bù lại.

Hãy cùng bóc tách bản chất toán học ở đây để thấy rõ sự khác biệt:

1. Bản chất: Lớp 3 là một lớp Conv "thiếu kênh" có chủ đích
Nếu thiết kế theo kiểu lặp lại đối xứng hoàn hảo (giống cặp Lớp 1-2):

Lớp 1 nhân đôi số kênh từ 16 lên 32.

Thì đúng ra, Lớp 3 phải nhân đôi số kênh từ 32 lên 128 ngay từ đầu. Khi đó Output của Lớp 3 đáng lẽ phải là [128 x 128 x 128].

Tuy nhiên, các tác giả YOLO không làm vậy. Nếu Lớp 3 tạo ra 128 kênh ngay, thì khi đi vào khối C2f ở Lớp 4, quá trình Split và Concat 4 khối Bottleneck liên tiếp trên 128 kênh sẽ làm bùng nổ số lượng tham số tính toán lên một mức khổng lồ, gây nghẽn cổ chai (Bottleneck) hệ thống.

Vì vậy, họ dùng một chiến thuật:

Ép Lớp 3 chỉ sinh ra 64 kênh thôi ([128 x 128 x 64]) để giảm tải cho các lớp tính chập đầu vào của Lớp 4.

Sau khi Lớp 4 thực hiện chia nhỏ và học sâu qua 4 Bottleneck, nó sẽ dùng lớp Conv1x1 cuối cùng để phóng số kênh lên 128 nhằm đạt đúng độ sâu tiêu chuẩn của mốc P3.

2. Hãy nhìn vào "Đích đến" của tầng P2 và tầng P3
Mục tiêu tối hậu của Backbone là chuẩn bị các tầng đặc trưng P3, P4, P5 có độ dày (số kênh) đủ tốt để nạp cho phần Neck và Head làm nhiệm vụ dự đoán.

Tiêu chuẩn số kênh quy định cho các mốc tại Backbone của phiên bản này là:

Mốc P2 (Lớp 2): Cần đạt 32 kênh.

Mốc P3 (Lớp 4): Cần đạt 128 kênh.

Mốc P4 (Lớp 6): Cần đạt 256 kênh.

Bây giờ chúng ta hãy so sánh hành trình đạt chỉ tiêu của Lớp 2 và Lớp 4:

Tiêu chí	Cặp Lớp 1 & 2 (Mốc P2)	Cặp Lớp 3 & 4 (Mốc P3)
Đầu vào	Nhận 16 kênh từ Lớp 0.	Nhận 32 kênh từ Lớp 2.
Lớp Conv đứng trước	Lớp 1 nâng một phát từ 16 lên 32 kênh → Đạt luôn chỉ tiêu của mốc P2.	Lớp 3 nâng từ 32 lên 64 kênh → Chưa đạt chỉ tiêu (Mốc P3 cần 128).
Khối C2f đứng sau	Lớp 2 chỉ việc học đặc trưng và giữ nguyên 32 kênh vì chỉ tiêu đã đạt xong.	Lớp 4 vừa phải học đặc trưng, vừa phải gánh nhiệm vụ nâng từ 64 lên 128 kênh để hoàn thành chỉ tiêu.

3. Chuyện gì xảy ra nếu Lớp 4 giữ nguyên 64 kênh?
Nếu lớp 4 ích kỷ "giữ nguyên 64 kênh giống như cách lớp 2 giữ nguyên 32 kênh", mô hình YOLO sẽ gặp 2 lỗi hệ thống nghiêm trọng ở các tầng phía sau:

Lỗi không khớp kích thước (Shape Mismatch) ở phần Neck:
Lát nữa ở phần Neck, Lớp 14 (Concat) sẽ lấy đầu ra của Lớp 4 để trộn với dữ liệu từ tầng sâu đổ về. Cấu trúc mạng yêu cầu vị trí đó Lớp 4 phải có đúng 128 kênh để thực hiện phép toán ghép nối. Nếu Lớp 4 chỉ có 64 kênh, mạng sẽ bị lỗi và không thể biên dịch (compile) được.

Nghèo nàn thông tin:
Tầng P3 (Lớp 4) đảm nhận nhiệm vụ cực kỳ nặng nề là phát hiện toàn bộ vật thể nhỏ trong ảnh. Vật thể nhỏ rất dễ bị lẫn vào nền. Nếu chỉ cho nó 64 kênh đặc trưng, mô hình sẽ không có đủ "dung lượng bộ nhớ" để ghi nhớ các chi tiết tinh vi của vật thể nhỏ, dẫn đến việc bỏ sót rất nhiều mục tiêu khi nhận diện.

Tóm lại: Lớp 1-2 và Lớp 3-4 trông thì giống như đang lặp lại bước đi của nhau, nhưng thực chất Lớp 3 đã "giấu bớt" số kênh đi để giảm tải tính toán, buộc Lớp 4 phải làm nhiệm vụ tăng kênh để bù lại cho đúng thiết kế của mạng.
```
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
YOLO OBB (Oriented Bounding Box) và YOLO thông thường (Horizontal Bounding Box - HBB) khác nhau chủ yếu ở cách biểu diễn khung bao của vật thể.

1. YOLO bình thường (HBB)

YOLO thông thường dự đoán hộp chữ nhật song song với trục ảnh.

Thông tin mỗi bounding box thường là:

x_center
y_center
width
height

Ví dụ:

      +----------------+
      |                |
      |      Car       |
      |                |
      +----------------+

Hộp luôn thẳng đứng hoặc nằm ngang, không được xoay.

2. YOLO OBB

YOLO OBB dự đoán bounding box có thể xoay theo góc của vật thể.

Ngoài 4 thông số trên còn có:

x_center
y_center
width
height
angle (góc xoay)

Ví dụ:

     /--------------/
    /              /
   /     Ship     /
  /              /
 /--------------/

Bounding box nghiêng theo vật thể.

So sánh
YOLO thường	YOLO OBB
Bounding box thẳng	Bounding box có thể xoay
4 tham số (x, y, w, h)	5 tham số (x, y, w, h, θ)
Đơn giản, nhanh	Phức tạp hơn một chút
Phù hợp người, xe, động vật...	Phù hợp vật thể có hướng rõ ràng
Khi nào dùng OBB?

OBB rất hữu ích khi vật thể bị nghiêng hoặc có hướng rõ ràng, ví dụ:

🚢 Tàu trên ảnh vệ tinh
✈ Máy bay
📦 Container
📄 Văn bản bị nghiêng
🏠 Nhà trong ảnh vệ tinh
🪵 Gỗ, thép trên dây chuyền sản xuất

Nếu dùng YOLO thường, hộp bao sẽ chứa nhiều khoảng trống:

+----------------------+
|                      |
|     /--------/       |
|    /  Ship  /        |
|   /--------/         |
|                      |
+----------------------+

Trong khi YOLO OBB ôm sát vật thể:

     /--------/
    /  Ship  /
   /--------/
Khác nhau về dữ liệu huấn luyện

YOLO thường:

class x_center y_center width height

Ví dụ:

0 0.52 0.48 0.30 0.20

YOLO OBB thường thêm thông tin góc hoặc biểu diễn bằng 4 đỉnh (tùy phiên bản và framework).

Ví dụ với góc:

class x_center y_center width height angle

Hoặc dạng 4 góc:

class x1 y1 x2 y2 x3 y3 x4 y4
Độ chính xác
Nếu vật thể luôn thẳng, YOLO thường là đủ.
Nếu vật thể thường xuyên bị xoay, YOLO OBB thường cho:
IoU cao hơn.
Ít chồng lấn giữa các vật thể.
Định vị chính xác hơn.

Đổi lại, YOLO OBB yêu cầu dữ liệu gán nhãn theo hướng và mô hình cũng phải học thêm thông tin về góc, nên việc huấn luyện và gán nhãn phức tạp hơn.

Tóm lại: YOLO thường chỉ dự đoán hộp chữ nhật song song với trục ảnh, còn YOLO OBB dự đoán hộp chữ nhật có thể xoay theo góc của vật thể. OBB đặc biệt phù hợp cho ảnh vệ tinh, tài liệu, hoặc các vật thể có hướng rõ ràng, trong khi YOLO thường phù hợp với đa số bài toán phát hiện đối tượng thông dụng.