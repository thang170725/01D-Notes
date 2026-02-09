OCR (Optical Character Recognition)
    • Là công nghệ nhận dạng ký tự quang học. Nó là một quá trình chuyển đổi hình ảnh chứa văn bản (chẳng hạn như tài liệu đã quét, ảnh chụp hoặc tệp PDF) thành văn bản mà máy tính có thể đọc, tìm kiếm và chỉnh sửa được.
    • Quy trình OCR thường bao gồm các bước sau:
    1. Thu nhận hình ảnh: Tài liệu được quét hoặc chụp ảnh. Phần mềm OCR sẽ phân tích hình ảnh này, xác định các vùng sáng (nền) và vùng tối (văn bản).
    2. Tiền xử lý: Hình ảnh được làm sạch và tối ưu hóa để cải thiện độ chính xác nhận dạng. Các bước này có thể bao gồm: 
        a) Chỉnh sửa độ nghiêng: Điều chỉnh lại hình ảnh nếu nó bị lệch khi quét.
        b) Loại bỏ nhiễu: Xóa các điểm hoặc vệt không mong muốn trên hình ảnh.
        c) Làm rõ nét: Tăng độ tương phản và làm sắc nét các ký tự.
        d) Phân đoạn: Chia hình ảnh thành các dòng, từ và ký tự riêng lẻ.
    3. Nhận dạng ký tự: Phần mềm OCR sử dụng các thuật toán và mô hình để so sánh từng ký tự đã phân đoạn với các mẫu ký tự đã được lưu trữ. Có hai phương pháp chính: 
        a) So khớp mẫu (Pattern Matching): So sánh trực tiếp hình dạng của ký tự với các mẫu có sẵn.
        b) Nhận dạng đặc trưng (Feature Recognition): Phân tích các đặc điểm độc đáo của ký tự (ví dụ: đường cong, góc) và so sánh chúng với các đặc trưng đã biết.
    4. Hậu xử lý: Văn bản đã nhận dạng có thể được kiểm tra lỗi chính tả, ngữ pháp và định dạng lại cho phù hợp.
    • Các ứng dụng phổ biến của OCR:
        ◦ Chuyển đổi tài liệu giấy sang định dạng kỹ thuật số: Giúp dễ dàng lưu trữ, tìm kiếm và chỉnh sửa.
        ◦ Trích xuất dữ liệu từ hóa đơn, biên lai, và các tài liệu khác: Tự động hóa việc nhập liệu.
        ◦ Nhận dạng biển số xe: Sử dụng trong hệ thống giao thông thông minh.
        ◦ Hỗ trợ người khiếm thị: Chuyển văn bản thành giọng nói.
        ◦ Dịch thuật: Nhận dạng văn bản trong ảnh để dịch sang ngôn ngữ khác.
        ◦ Tìm kiếm văn bản trong ảnh hoặc tệp PDF không tìm kiếm được.
Tóm lại, OCR là một công nghệ quan trọng giúp chuyển đổi thông tin từ dạng hình ảnh sang dạng văn bản có thể xử lý được bằng máy tính, mang lại nhiều lợi ích trong việc quản lý dữ liệu và tự động hóa quy trình.
Model (Mô hình)
CNN (Convolutional Neural network)
    • Được thiết kế để xử lý dữ liệu có cấu trúc dạng lưới, ví dụ như hình ảnh.
    • Convolutional: Thay vì kết nối mọi input với mọi nơ ron như MLP, CNN sử dụng một bộ lọc nhỏ (filter hoặc kernel) trượt trên ảnh đầu vào để lấy ra những đặc trưng nhỏ như cạnh, góc, hay các mẫu đơn giản. Bộ lọc này sẽ quét khắp ảnh. Phát hiện các đặc điểm quan trọng tại nhiều vị trí. Mỗi kernel học một đặc trưng khác nhau
    • Pooling: Giúp giảm kích thước dữ liệu sau khi tích chấp, làm cho mạng nhẹ hơn, giảm tính toán, đồng thời giữ lại đặc trưng quan trọng. Ví dụ, max pooling chọn giá trị lớn nhất trong một vùng nhỏ.
    • Fully connected: Sau các lớp convolutional và pooling, dữ liệu đặc trưng được dàn phẳng và dựa vào các lớp MLP để phân loại hay dự đoán.
Conv2D:
Lớp Conv sâu hơn thường học đã trưng trừu tượng hơn (edge → shape → object)
RetinaNet
    • Là một mô hình deep learning dùng để phát hiện và phân loại nhiều vật thể trong ảnh (object detection), ví dụ tìm xe, người, mèo, chó trong cùng một ảnh.
    • retinaNet giả quyết một vấn đề cuecj lớn trong object detection gọi là imbalance (mất cân bằng) giữa các vùng có vật thể và vùng không có vật thể.
    • RetinaNet sử dụng một kỹ thuật tên là Focal Loss => nhờ đó mô hình tập trung học tốt hơn ở những vùng khó, không bị lười học ở các vùng dễ.
        ◦ Nếu mô hình đoán đúng và tự tin → loss rất nhỏ.
        ◦ Nếu mô hình đoán sai → loss rất lớn.
        ◦ Nhưng nếu mô hình đoán đúng mà không tự tin → loss vẫn tương đối cao → khuyến khích cải thiện.
    • Cấu trúc:
        ◦ Backbone (ResNet50, ResNet101): Trích xuất đặc trưng.
        ◦ Feature Pyramid Network (FPN): Giúp phát hiện vật thể ở nhiều kích cỡ.
        ◦ Two Subnets:
            ▪ Classification subnet: phân loại mỗi anchor box.
            ▪ Regression subnet: dự đoán bounding box cho từng object.
    • Dùng RetinaNet khi cần độ chính xác tốt hơn YOLO, làm việc với ảnh có nhiều vật thể nhỏ hoặc nhiều lớp khác nhau, muốn thử nghiệm focal loss cho bài toán mất cân bằng.
Inception
    • Là một kiến trúc mạng nơ-ron tích chập (CNN), nó kết hợp nhiều kernel khác nhau chạy song song và sau đó gộp kết quả lại, nhằm giúp mô hình vừa học được chi tiết nhỏ, vừa nhìn được tổng thể.
    • Cách hoạt động:
        ◦ Tạo nhiều nhánh song song.
        ◦ Mooic nhánh xử lý cùng một input - tức sao chép ảnh gốc cho nhiều nhánh.
        ◦ Mỗi nhánh áp dụng một loại xử lý khác nhau, ví dụ:
            ▪ Nhánh 1: Convolution 1x1
            ▪ Nhánh 2: Convolution 1x1 → 3x3
            ▪ Nhánh 3: Convolution 1x1 → 5x5
            ▪ Nhánh 4: MaxPooling 3x3 → Convolution 1x1
        ◦ Gộp kết quả từ tất cả các nhanh theo chiều channel.
MobileNet - Mạng nhẹ cho di động
    • Mô hình VGG hay ResNet rất mạnh nhwung quá nặng, không chạy nổi trên điện thoại hoặc thiết bị trên IoT.
    • Mô hình sử dụng kỹ thuật Depthwise Separable Convolution, thay vì dùng Convolution thường.
        ◦ Depthwise Separable tách ra làm 2 bước → Nhệ hơn 8-9 lần so với Conv chuẩn mà vẫn giữ được độ chính xác.
            ▪ Depthwise Convolution - Xử lý từng kênh riêng biệt (nhẹ hơn rất nhiều).
            ▪ Pointwise Convolution - Dùng Conv 1x1 để kết hợp các kênh lại.
EfficientNet - Mạng cân bằng cả tốc độ và độ chính xác
    • Dùng MobileNet thì nhẹ nhwung độ chính xác hơi kém so với ResNet. Dùng ResNet thì chính xác nhưng chậm.
    • EfficientNet dùng kỹ thuật Compound Scaling để cân bằng giữa độ sâu, độ rộng, và độ phân giải đầu vào.
    • Cấu trúc:
        ◦ Dùng khối MBConv (Mobile Inverted Bottleneck) giống MobileNetV2.
        ◦ Thêm SE Block (Squeeze-and-Excitation) để học kênh nào quan trọng.
        ◦ Dùng Swish hoạc SiLU activation thay cho ReLU để tăng độ mượt.
SSD - Single Shot Detector
    • Phát hiện vật thể trong 1 lần quét ảnh (sigle shot).
    • Nhanh, nhẹ, dùng tốt cho real-time (ảnh từ wwebcam, robot, …)
Faster R-CNN
    • Phát hiện vật thể chính xác cao nhưng chậm hơn YOLO.
    • Gồm 2 bước: Xác định vùng → nhận diện vật thể.
    • Dùng khi cần độ chính xác cao, ít quan trọng tốc độ.
U-Net
    • Phân đoạn ảnh y tế (VD: Tách khối u khỏi ảnh chụp CT).
    • Inout là ảnh, output là mặt nạ (mask) có cùng kích thước.
    • Cực kỳ hiệu quả với ảnh nhỏ, ít dữ liệu.
Mask R-CNN
    • Phát hiện + phân đoạn vật thể (VD: viền rõ từng người, từng con mèo, …).
    • Nâng cấp từ Fastẻ R-CNN + thêm mặt nạ phân đoạn.
    • Output: Bounding box + Class + Mask.
DeepLab (V3, V3+)
    • Phân đoạn ảnh toàn cục (sematic segmentation).
    • Biết từng pixel là cái gì (VD: pixel này là người, kia là đường, …).
    • Rất mạnh trong phân đoạn cảnh quan, bản đồ, ảnh vệ tinh.
OpenPose
    • Dự đoán vị trí khớp cơ thể người (pose estimation).
    • Trích ra được: Đầu, vai, tay, chân, … từ ảnh/video.
MediaPipe
    • Thư viện của Google, hỗ trợ real-time:
    • Nhận diện tay, pose, tracking, …
    • Rất nhẹ và chạy được trên điện thoại
HRNet - High Resolution Network
    • Dự đoán khớp người, phân đoạn ảnh với độ chi tiết cao.
    • Giữ ảnh độ phân giải lớn suốt mạng → chính xác hơn OpenPose.
VGG-Face
Facenet
OpenFace
DeepFace
ArcFace
Dlib
Sface
Kỹ thuật xử lý ảnh
ROI (Region Of Interest)
    • Trong cả bức ảnh / frame, mình chỉ quan tâm một vùng nào đó, còn lại thì kệ.
    • Ví dụ đời thường:
        ◦ Camera giao thông → chỉ quan tâm phần đường, không quan tâm bầu trời
        ◦ Camera lớp học → chỉ quan tâm khu vực bảng
        ◦ Camera an ninh → chỉ quan tâm cửa ra vào
    • ROI không phải AI, nó là xử lý ảnh thuần.

Detection
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
YOLO ((You Only Look Once))
    • YOLO là một mô hình mạng nơ-ron tích chập (CNN) được thiết kế để thực hiện tác vụ phát hiện vật thể (Object Detection) trong thời gian thực. Cái tên "You Only Look Once" nói lên điểm cốt lõi: nó xử lý toàn bộ hình ảnh chỉ trong một lần duy nhất.
    • A. Ba phần chính của kiến trúc. Mô hình YOLO có cấu trúc tương tự như một dòng chảy dữ liệu qua 3 phần chính, hoạt động tuần tự:
        1. Backbone (Phần Trích xuất Đặc trưng)
            ▪ Mục đích: Hút các đặc trưng cơ bản từ ảnh (các cạnh, góc, hình dạng).
            ▪ Vị trí trong code: Các lớp từ (0) đến (9):
            ▪ Conv (Convolution): Lớp tích chập cơ bản, dùng để trích xuất đặc trưng.
            ▪ Conv2d(3, 16, kernel_size=(3, 3), stride=(2, 2)): Khởi đầu với ảnh 3 kênh màu (RGB), tạo ra 16 kênh đặc trưng, giảm kích thước ảnh (stride=2).
            ▪ C2f (Cross-Stage Partial Network): Là một khối kiến trúc quan trọng trong YOLO hiện đại (như YOLOv8). Nó giúp tăng hiệu suất bằng cách tách luồng đặc trưng ra hai nhánh và hợp nhất lại. Nó giúp mô hình học sâu hơn mà vẫn giữ được tốc độ.
            ▪ SPPF (Spatial Pyramid Pooling Fast): Lớp (9). Nó tổng hợp thông tin từ nhiều kích thước khác nhau của cùng một đặc trưng. Điều này giúp mô hình nhận diện vật thể bất kể kích thước của chúng (ví dụ: một chiếc xe ô tô to hay nhỏ trong ảnh).
       2. Neck (Phần Hợp nhất Đặc trưng)
            ▪ Mục đích: Kết hợp các đặc trưng đã học được từ các cấp độ sâu khác nhau của Backbone.
            ▪ Các lớp nông (gần đầu) có đặc trưng về chi tiết, vị trí chính xác.
            ▪ Các lớp sâu (gần cuối) có đặc trưng về ngữ cảnh, phân loại vật thể.
            ▪ Vị trí trong code: Các lớp từ (10) đến (21):
            ▪ Upsample (10, 13): Phóng to bản đồ đặc trưng từ lớp sâu lên.
            ▪ Concat (11, 14, 17, 20): Nối (ghép) bản đồ đặc trưng đã được phóng to với bản đồ đặc trưng tương ứng từ Backbone.
            ▪ Mô hình này sử dụng kiến trúc kiểu FPN/PAN: giúp các lớp dự đoán (Head) có được thông tin chi tiết lẫn thông tin ngữ cảnh.
        3. Head (Phần Dự đoán)
            ▪ Mục đích: Lấy các đặc trưng đã được hợp nhất từ Neck và chuyển chúng thành kết quả dự đoán cuối cùng.
            ▪ Vị trí trong code: Lớp (22) Detect(...).
            ▪ Đầu ra của Head:
            ▪ Hộp bao (Bounding Box): Toạ độ (x,y,w,h) của vật thể.
            ▪ Độ tin cậy vật thể (Objectness Score): Xác suất có vật thể trong hộp đó.
            ▪ Xác suất lớp (Class Probability): Xác suất vật thể đó thuộc về mỗi loại lớp (người, chó, xe hơi...).
            ▪ DFL (Distribution Focal Loss): Được sử dụng trong YOLOv8 để cải thiện độ chính xác của hộp bao bằng cách học cách phân phối khoảng cách tới các cạnh của hộp.

Segmentation
Không những detect nó sẽ tô màu lên vùng vật thể được detection.
Bài tập
Demo segmentation yolov8-seg
from ultralytics import YOLO
model = YOLO('model_detect/yolov8n-seg.pt')
res = model("img/predict_1.jpg")
for r in res:
    r.show()
Pose estimation
    • Là kỹ thuật dự đoán tọa độ các keypoints (điểm chính) trên đối tượng, ví dụ: Người: đầu, vai, khuỷu tay, cổ tay, hông, đầu gối, mắt cá chân… Vật thể: góc hộp, chân bàn, cánh tay robot…
    • Pose estimation thường chia thành:
        ◦ 2D Pose Estimation: Keypoints trong không gian 2D (x, y)
        ◦ 3D Pose Estimation: Keypoints có thêm độ sâu (x, y, z)
    • Nhận diện hành động người, phân tích thể thao, ứng dụng thể dục, làm phim, game, vfx, hệ thống giám sát & an ninh, robot, tương tác ảo, y học

Preprocessing (Các kỹ thuật tiền xử lý ảnh)
CLAHE (Contrast Limited Adaptive Histogram Equalization)
    • Mục đích chính của kỹ thuật này là tăng cường độ tương phản (contrast) cục bộ của hình ảnh.
    • Nó giúp làm nổi bật các chi tiết trong các vùng ảnh quá tối hoặc quá sáng mà các phương pháp tăng cường độ tương phản toàn cục (như Histogram Equalization truyền thống) không xử lý tốt, thậm chí còn gây ra nhiễu hoặc làm mất chi tiết.
    • Bạn nên sử dụng kỹ thuật CLAHE khi bạn có những bức ảnh gặp vấn đề về độ tương phản, đặc biệt là khi sự chênh lệch độ sáng (dynamic range) trong ảnh lớn hoặc có những vùng bị tối/sáng cục bộ.
    • Các trường hợp cụ thể thường áp dụng CLAHE bao gồm:
        ◦ Xử lý Ảnh Y học (Medical Imaging): Ảnh chụp X-quang, MRI, CT, ảnh soi đáy mắt (như trong chẩn đoán bệnh lý về mắt) thường có độ tương phản thấp hoặc có các vùng chi tiết cần làm nổi bật. CLAHE giúp tăng khả năng hiển thị các cấu trúc sinh học.
        ◦ Ảnh trong Điều kiện Ánh sáng Kém: Ảnh chụp trong điều kiện thiếu sáng hoặc có ánh sáng nền mạnh (backlit), nơi chi tiết bị "chìm" trong bóng tối hoặc bị "cháy" sáng.
        ◦ Hệ thống Thị giác Máy (Machine Vision) và Xử lý Ảnh: Khi cần tiền xử lý ảnh (preprocessing) để chuẩn hóa hoặc tăng cường chất lượng ảnh đầu vào trước khi đưa vào các thuật toán nhận dạng, phân loại, hoặc học sâu (Deep Learning/CNN). Việc này giúp thuật toán trích xuất đặc trưng (feature extraction) chính xác hơn.
        ◦ Ảnh Thiên văn hoặc Viễn thám: Ảnh vệ tinh hoặc ảnh chụp từ kính thiên văn thường cần CLAHE để làm rõ các cấu trúc và đặc điểm bề mặt.
    • Ưu điểm của CLAHE so với HE truyền thống
        ◦ CLAHE là một cải tiến của phương pháp Cân bằng Biểu đồ màu (Histogram Equalization - HE) truyền thống:
        ◦ Adaptive (Thích nghi): Thay vì áp dụng sự cân bằng độ tương phản cho toàn bộ ảnh, CLAHE chia ảnh thành nhiều ô (tiles/regions) nhỏ và áp dụng HE cho từng ô riêng biệt. Điều này giúp tăng cường độ tương phản cục bộ mà không làm ảnh hưởng đến các vùng khác.
        ◦ Contrast Limited (Giới hạn Độ tương phản): CLAHE có một tham số giới hạn (clip limit) để ngăn chặn việc độ tương phản bị tăng quá mức ở các vùng nhiễu (noise) hoặc các vùng có độ tương phản rất thấp, giúp tránh tình trạng nhiễu bị khuếch đại (over-amplification).
