deep_sort_realtime
deepsort_tracker
DeepSort()
    • Dùng để cấu hình đối tượng
    • DeepSORT không tự tìm đối tượng; nó nhận các tọa độ (Bounding Boxes) từ YOLO, sau đó mới thực hiện gán ID và theo dõi qua các khung hình.
Cú pháp:
from deep_sort_realtime.deepsort_tracker import DeepSort

tracker = DeepSort(
    max_age=50,
    n_init=3,
    nn_budget=None, # Lưu trữ tất cả features
   embedder='default',
   max_cosine_distance=0.3, 
   use_cuda=True
)

    • max_age: Số frame tối đa mà một track bị mất có thể tồn tại (mặc định là 30)
    • n_init: Số lần phát hiện liên tiếp để khởi tạo một track mới (mặc định là 3)
    • nn_budget: Số lượng appearance features tối đa để lưu trữ cho mỗi track.
    • override_track_class: Có thể định nghĩa một lớp Track tùy chỉnh nếu cần.
    • embedder: Tên của mô hình Re-ID. 'default' sử dụng mô hình ResNet50 được train sẵn.
    • max_cosine_distance: Đây là giá trị tối đa mà bạn cho phép để hệ thống chấp nhận hai vật thể là một. (mặc định 0.2)
    • use_cuda=True: Tham số quyết định dùng GPU
update_tracks()
Đây là hàm nhận các phát hiện từ mô hình Detector và thực hiện toàn bộ quy trình gán ghép, dự đoán, và cập nhật trạng thái theo dõi.
Cú pháp:
import numpy as np

# Giả lập Khung hình (Frame)
img_height, img_width = 480, 640
frame = np.random.randint(0, 256, (img_height, img_width, 3), dtype=np.uint8)

# Giả lập Dữ liệu Phát hiện (Detections)
# Định dạng: ([x1, y1, x2, y2], confidence, class_name)
detections = [
    ([100, 150, 200, 350], 0.95, 'person'),  # Đối tượng 1
    ([450, 200, 550, 400], 0.88, 'car'),     # Đối tượng 2
    # Thêm một phát hiện mới gần phát hiện 1 (để kiểm tra gán ghép)
    ([105, 145, 205, 345], 0.90, 'person')
]

# Gọi hàm update_tracks
tracks = tracker.update_tracks(detections, frame=frame)

print("\nKết quả Theo dõi (Active Tracks):")
if tracks:
    for track in tracks:
        # Nếu track đang được theo dõi và không phải là track tạm thời
        if not track.is_confirmed():
            continue

        track_id = track.track_id
        # Lấy BBox dưới định dạng xyxy
        bbox_xyxy = track.to_tlbr()
        class_id = track.get_det_class()
        
        print(f"ID: {track_id}, BBox (xyxy): {bbox_xyxy.astype(int)}, Class: {class_id}")
else:
    print("Không có track đang hoạt động (chưa đủ n_init hoặc không có phát hiện).")
track.is_confirmed()	Trả về True nếu track đã được theo dõi đủ n_init frame và đang hoạt động.
.track_id
Lấy ID duy nhất của đối tượng.


.to_ltrb()
Lấy hộp giới hạn (Bounding Box) dưới định dạng [left, top, right, bottom]


track.get_det_class()	Lấy tên lớp (class name) của phát hiện gần nhất.
track.time_since_update	Số frame kể từ lần cập nhật gần nhất.