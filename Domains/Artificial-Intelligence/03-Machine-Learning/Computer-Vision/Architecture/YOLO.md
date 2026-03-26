- [Introduction](#introduction)
- [Architecture](#architecture)
---
# Introduction
```bash
- YOLO là một mô hình mạng nơ-ron tích chập (CNN) được thiết kế để thực hiện tác vụ phát hiện vật thể (Object Detection) trong thời gian thực. Cái tên "You Only Look Once" nói lên điểm cốt lõi: nó xử lý toàn bộ hình ảnh chỉ trong một lần duy nhất.
```
# Architecture
```bash
A. Ba phần chính của kiến trúc. Mô hình YOLO có cấu trúc tương tự như một dòng chảy dữ liệu qua 3 phần chính, hoạt động tuần tự:
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