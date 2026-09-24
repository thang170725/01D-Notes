deepface
9.3.1 Kiến thức cơ sở
    • Là một thư viện mã nguồn mở được sử dụng để nhận diện khuôn mặt và phân tích khuôn mặt bằng cách sử dụng các mô hình học sâu (deep learning).
    • Đây là một thư viện cấp cao, đơn giản hóa việc tích hợp các chức năng như:
        ◦ Xác thực khuôn mặt (face verification)
        ◦ Nhận diện khuôn mặt (face recognition)
        ◦ Phân tích cảm xúc (emotion analysis)
        ◦ Dự đoán tuổi (age prediction)
        ◦ Ước tính giới tính (gender prediction)
        ◦ Ước tính chủng tộc (race/ethnicity prediction)
DeepFace dùng để làm gì?
    • So sánh 2 khuôn mặt để kiểm tra xem có phải là một người không
    • Nhận dạng khuôn mặt bằng cách so sánh với cơ sở dữ liệu
    • Phân tích các đặc điểm khuôn mặt như cảm xúc, tuổi, giới tính, chủng tộc.
Cài đặt DeepFace
pip install deepface
9.3.2 
extract_faces()
Để test xem DeepFace có phát hiện khuôn mặt hay không. Nếu không tìm thấy khuôn mặt nó sẽ ném ra một lỗi.
from deepface import DeepFace
import os
# Đảm bảo rằng đường dẫn là đúng
# kết quả trả về là một đường dẫn
img1 = os.path.join(".", "anh1.jpg")
img2 = os.path.join(".", "anh2.jpg")
img3 = os.path.join(".", "anh3.jpg")
DeepFace.extract_faces(img_path=img2, enforce_detection=True)
# code này bị lỗi nhưng khi thay bằng img1, img3 thì code chạy bình thường, chứng tỏ ảnh 2 không phát hiện được khuôn mặt
verify()
So sánh 2 hình ảnh xem có cùng một người hay không.
Cú pháp: DeepFace.verify(img1, img2, model_name)
    • Img1: Đường dẫn đến ảnh đầu tiên.
    • Img2: Đường dẫn đến ảnh thứ 2.
    • model_name: Tùy chọn. Tên mô hình để nhận diện “VGG-Face”, “Facenet”, “Facenet512”, “OpenFace”, “DeepFace”, “DeepID”, “Dlib”, “ArcFace”
    • detector_backend: Tùy chọn. Cách phát hiện khuôn mặt “opencv”, “retinaface”, “mtcnn”, “ssd”, “dlib”, …
    • enforce_detection: Tùy chọn. Nếu True – mặc định, sẽ báo lỗi nếu không phát hiện được khuôn mặt.
    • distance_metric: Tùy chọn. Cách đo sự khác nhau giữa đặc trưng 2 khuôn mặt “cosine”, “eucliden”, “euclideean_12”
from deepface import DeepFace
import os
# Đảm bảo rằng đường dẫn là đúng
# kết quả trả về là một đường dẫn
img1 = os.path.join(".", "anh1.jpg")
img2 = os.path.join(".", "anh3.jpg")

res = DeepFace.verify(
    img1_path=img1,
    img2_path=img2,
    # Xử ngay cả khi deepface không phát hiện khuôn mặt
    enforce_detection=False
    )

if res["verified"] == True:
    print("Đây là cùng một người")
else:
    print("Đây không phải cùng một người")
Đây là cùng một người
Lưu ý: 
    • Ảnh chỉ nên tập trung vào khuôn mặt, khuôn mặt không bị che, quay đi, …
    • Nên sử dụng retinaface hoặc mtcnn ở detector_backend có khả năng xử lý các trường hợp khó tốt hơn opencv. Opencv dễ bị nhầm và bỏ qua khuôn mặt.
    • 
analyze()
Phân tích cảm xúc, tuổi, giới tính, chủng tộc (tức là phân tích khuôn mặt trong ảnh.
Kích hoạt stream camera để nhận diện khuôn mặt theo thời gian thực.
Hàm này trả về một dictionary, mỗi dictionary chứa thông tin cho một khuôn mặt.
Cú pháp: DeepFace.analyze(img_path, actions=[‘emotion’, ‘age’, ‘gender’, ‘race’])
    • img_path: Đường dẫn tới ảnh, URL hoặc mảng ảnh numpy array.
    • actions: Các loại phân tích thực hiện.
    • enforce_detection: Nếu True, sẽ báo lỗi nếu không tìm thấy khuôn mặt.
    • detector_backend: Chọn thuật toán nhận diện khuôn mặt. opencv, retinaface, mtcnn, ssd, mediapipe, yolov8. Mặc định là opencv.
    • silent: Nếu True, ẩn thông báo log. Mặc định là False.
from deepface import DeepFace
import os
# lưu kết quả
res = {}
# Đảm bảo rằng đường dẫn là đúng
# kết quả trả về là một đường dẫn
img3 = os.path.join(".", "anh3.jpg")
# xem deepface có phát hiện khuôn mặt không
face3 = DeepFace.extract_faces(img_path=img3, enforce_detection=False)
# enforce_detection=False để DeepFace không tìm thấy
# khuôn mặt nó sẽ không hiển thị lỗi mà đưa ra một list rỗng
if len(face3)>0:
    res = DeepFace.analyze(img_path=img3, actions=['age', 'gender', 'emotion', 'race'])
    print(res)
else:
    print("không phát hiện khuôn mặt nào")
[{'age': 25, 'region': {'x': 192, 'y': 529, 'w': 506, 'h': 506, 'left_eye': (530, 729), 'right_eye': (359, 711)}, 'face_confidence': 0.91, 'gender': {'Woman': 0.13398927403613925, 'Man': 99.86600875854492}, 'dominant_gender': 'Man', 'emotion': {'angry': 22.14689701795578, 'disgust': 1.8149201252981584e-05, 'fear': 0.9051406756043434, 'happy': 0.0005697631422663108, 'sad': 23.5756516456604, 'surprise': 1.0167737229949125e-05, 'neutral': 53.3717155456543}, 'dominant_emotion': 'neutral', 'race': {'asian': 99.99998807907104, 'indian': 2.204514792936152e-07, 'black': 1.1265895307572757e-11, 'white': 9.731043526528538e-07, 'middle eastern': 1.1882095174854494e-12, 'latino hispanic': 1.4451661911607516e-05}, 'dominant_race': 'asian'}]
# region là vị trí phát hiện khuôn mặt
# face_confidence là mức độ chắc chắn đó cố phải là khuôn mặt hay không

from deepface import DeepFace
import os
import sys  # dùng để dừng chương trình

img_path = os.path.join(".", "anh1.jpg")

try:
    # Nếu không có mặt sẽ ném lỗi (mặc định enforce_detection=True)
    faces = DeepFace.extract_faces(img_path=img_path)
except Exception as e:
    print("❌ Không tìm thấy khuôn mặt trong ảnh.")
    sys.exit()  # Dừng chương trình tại đây

# Nếu không bị lỗi → tiếp tục phân tích
print("✅ Phát hiện khuôn mặt, đang phân tích...")
result = DeepFace.analyze(img_path=img_path, actions=['age', 'gender', 'emotion', 'race'])
print(result)

find()
    • Tìm kiếm khuôn mặt trong thư viện hình ảnh.
    • Hàm này không dùng để kiểm tra gương mặt này có tồn tại trong dataset không, mà nó chỉ đơn giản là tìm ra khuôn mặt trong dataset gần giống nhất với ảnh đầu vào, bất kể có giống thực sự hay không.
        ◦ Ví dụ: Dataset gồm khuôn mặt A, B, C và bạn đựa vào khuôn mặt mới D(chưa có trong dataset) sẽ vẫn trả về sẽ trả về khuôn mặt giống nhất.
Cú pháp:
from deepface import DeepFace

results = DeepFace.find(
    img_path="ảnh_cần_xác_thực.jpg",
    db_path="thư_mục_dataset/",
    model_name="VGG-Face",         # (tùy chọn)
    distance_metric="cosine",      # (tùy chọn)
    enforce_detection=True,        # (default: True)
    detector_backend="opencv"      # (tùy chọn)
)
    • model_name: “VGG-Face”, “Facenet”, “OpenFace”, “DeepFace”, “ArcFace”, “Dlib”.
    • distance_metric: Cách đo độ giống nhau: “cosine” (phổ biến), “euclidean”, “euclidean_12”
    • enforce_detection: Nếu True, sẽ báo lỗi nếu không phát hiện khuôn mặt. Nếu False sẽ bỏ qua ảnh không có mặt.
    • detector_backend: Dùng bộ phát hiện khuôn mặt nào: “opencv”, “ssd”, “mtcnn”, “retinaface”, “mediapipe”, …
Output trả về:
    • Một list chứa pandas Dataframe (thường chỉ có 1 phần tử, tức là result[0], mỗi dataFrame chứa thông tin về những khuôn mặt giống nhất được tìm thấy trong db_path.
result[0] là gì?
    • Là một pandas DataFrame chứa các ảnh trong dataset có độ tương đồng cao nhất với khuôn mặt đầu vào.
    • Các cột trong result[0] thường gồm:
        ◦ identity: đường dẫn tới ảnh giống nhất trong dataset.
        ◦ distance: Khoảng các giữa ảnh đầu vào và ảnh trong dataset (càng nhỏ càng giống).
        ◦ source_x: Nguồn dữ liệu (thường là database)
        ◦ target_x: tên ảnh đầu vào
empty
Trả về True nếu DataFrame rỗng (không có kết quả nào được tìm thấy.
Cú pháp: result[0].empty
iloc[]
Lấy dòng thứ n trong bảng kết quả
Cú pháp: result[0].iloc[0]
Ví dụ: result[0].iloc[0][‘identity’] - Lấy tên ảnh (đường dẫn) tương ứng với dòng đó