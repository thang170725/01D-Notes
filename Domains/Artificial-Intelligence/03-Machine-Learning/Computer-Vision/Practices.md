Cách tạo và sử dụng file data.yaml
    • File data.yaml là file cấu hình bắt buộc khi bạn muốn huấn luyện mô hình YOLOv8 trên bộ dữ liệu tùy chỉnh của mình.
    • File này có nhiệm vụ thông báo cho mô hình YOLO biết:
        ◦ Vị trí của dữ liệu: Đường dẫn đến các tập tin ảnh và nhãn (labels) cho huấn luyện, đánh giá và kiểm thử.
        ◦ Số lượng lớp (classes): Tổng số loại đối tượng mà mô hình cần học cách nhận diện.
        ◦ Tên của các lớp: Tên dễ đọc của từng loại đối tượng (ví dụ: person, car, dog).
    • File data.yaml là một file văn bản thuần túy và phải tuân theo cú pháp YAML.
Ví dụ:
Giả sử bạn có một thư mục chứa dữ liệu có tên là my_custom_dataset. Cấu trúc file mẫu sẽ trông như sau:
# data.yaml cho bộ dữ liệu tùy chỉnh

# Đường dẫn gốc (tùy chọn, nếu không có, các đường dẫn dưới đây là tuyệt đối hoặc tương đối với thư mục hiện tại)
path: /path/to/my_custom_dataset 

# Đường dẫn tương đối đến thư mục ảnh huấn luyện (Training images)
train: images/train 

# Đường dẫn tương đối đến thư mục ảnh đánh giá (Validation images)
val: images/val 

# Đường dẫn tương đối đến thư mục ảnh kiểm thử (Test images) - Tùy chọn
# test: images/test 

# Số lượng lớp (classes)
nc: 2 

# Tên của các lớp, phải theo thứ tự từ 0 đến nc-1
names: ['cat', 'dog']

Cú pháp:
from ultralytics import YOLO

# 1. Tải mô hình cơ sở (base model)
model = YOLO('yolov8n.pt')  # Sử dụng mô hình nano (n)

# 2. Định nghĩa đường dẫn đến file data.yaml của bạn
data_config_file = 'my_custom_dataset/data.yaml' 

# 3. Bắt đầu quá trình huấn luyện
# Tham số 'data' chỉ định vị trí của file cấu hình dữ liệu
# Tham số 'epochs' chỉ định số lần lặp lại huấn luyện
# Tham số 'imgsz' chỉ định kích thước ảnh đầu vào
print(f"Bắt đầu huấn luyện mô hình với cấu hình dữ liệu: {data_config_file}")

results = model.train(
    data=data_config_file, 
    epochs=100, 
    imgsz=640
)

print("Quá trình huấn luyện đã hoàn thành.")

# --- Hoặc sử dụng nó để đánh giá mô hình đã huấn luyện ---
# metrics = model.val(data=data_config_file)