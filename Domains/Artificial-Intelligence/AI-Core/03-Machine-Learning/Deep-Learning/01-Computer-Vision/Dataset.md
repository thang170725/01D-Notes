# COCO
COCO là:

Một tập hợp ảnh thực tế + nhiều loại annotation chi tiết + chuẩn định dạng dùng chung

Không chỉ “gán nhãn” đơn giản:

Ngoài việc biết “ảnh này có con mèo”, COCO còn cung cấp:

📦 Bounding box → vị trí chính xác của từng object
🎯 Segmentation mask → từng pixel thuộc object nào
🧍 Keypoints → vị trí khớp cơ thể (vai, tay, chân…)
📝 Caption → mô tả ảnh bằng ngôn ngữ tự nhiên
🔢 ID, category, metadata → chuẩn hóa để train dễ dàng
Điểm quan trọng:
Một ảnh có thể chứa nhiều object chồng lên nhau
Object nằm trong bối cảnh thật (đường phố, nhà cửa…), không phải ảnh nền sạch
Có format JSON chuẩn mà hầu hết framework (Detectron2, YOLO, MMDetection…) đều hỗ trợ
Tóm lại:

👉 COCO =
Không chỉ là “ảnh có nhãn”
mà là
một bộ dữ liệu chuẩn hóa + annotation chi tiết + dùng làm benchmark chung
## cấu trúc JSON của coco

Cấu trúc JSON của COCO được thiết kế rất rõ ràng để các framework trong Computer Vision có thể đọc thống nhất.

Dưới đây là cấu trúc chuẩn (rút gọn + dễ hiểu):

1. Tổng thể file JSON
{
  "info": {...},
  "licenses": [...],
  "images": [...],
  "annotations": [...],
  "categories": [...]
}
2. images – danh sách ảnh

Mỗi ảnh là một object:

{
  "id": 397133,
  "file_name": "000000397133.jpg",
  "width": 640,
  "height": 427
}

👉 Ý nghĩa:

id: định danh ảnh (rất quan trọng để liên kết)
file_name: tên file
width, height: kích thước
3. annotations – nhãn (quan trọng nhất)

Mỗi object trong ảnh = 1 annotation:

{
  "id": 1768,
  "image_id": 397133,
  "category_id": 18,
  "bbox": [x, y, width, height],
  "area": 702.105,
  "iscrowd": 0,
  "segmentation": [...]
}

👉 Ý nghĩa:

image_id: liên kết tới ảnh
category_id: object thuộc class nào
bbox: khung bao [x, y, w, h]
segmentation: polygon (dùng cho segmentation)
iscrowd: object dạng “đám đông” (ví dụ nhiều người)
4. categories – danh sách class
{
  "id": 18,
  "name": "dog",
  "supercategory": "animal"
}

👉 Ý nghĩa:

id: dùng trong annotation
name: tên class
supercategory: nhóm lớn hơn
5. info – thông tin dataset
{
  "description": "COCO 2017 Dataset",
  "version": "1.0",
  "year": 2017
}
6. licenses – thông tin bản quyền ảnh
{
  "id": 1,
  "name": "Attribution-NonCommercial",
  "url": "http://..."
}
Cách liên kết dữ liệu (rất quan trọng)
images.id ⟶ nối với ⟶ annotations.image_id
categories.id ⟶ nối với ⟶ annotations.category_id

👉 Tức là:

1 ảnh có nhiều annotation
1 annotation là 1 object trong ảnh
Tóm tắt dễ nhớ

COCO JSON =

images → ảnh
annotations → object trong ảnh
categories → loại object

Nếu bạn đang dùng Detectron2, mình có thể giải thích luôn:

cách nó load JSON này
hoặc map sang dataset dict nội bộ 👍