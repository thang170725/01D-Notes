- [PaddleOCR (class chính để chạy OCR)](#paddleocr-class-chính-để-chạy-ocr)
  - [Display (Nhóm cung cấp thông tin)](#display-nhóm-cung-cấp-thông-tin)
    - [.predict()](#predict)
---
# PaddleOCR (class chính để chạy OCR)
```bash
- Dùng để khởi tạo, load các model cần thiết.
- Tùy config, pipeline sẽ gồm:
    + Text Detection (det) → tìm vùng có chữ
    + Text Recognition (rec) → đọc chữ
    + (optional) Orientation / preprocessing
```
**Syn**
```bash
ocr = PaddleOCR(
    use_doc_orientation_classify=False,
    use_doc_unwarping=False,
    use_textline_orientation=False
)

- Input:
    + use_doc_orientation_classify: phát hiện ảnh bị xoay (90°, 180°…). True là bật, False là tắt
    + use_doc_unwarping: sửa ảnh bị cong (scan sách). True là bật, False là tắt
    + use_textline_orientation: detect hướng từng dòng chữ. True là bật, False là tắt
```
## Display (Nhóm cung cấp thông tin)
### .predict()
**Syn**
```bash
ocr.predict("img.jpg")

- Output:
# [
#     res1,   # ảnh 1
#     res2,   # ảnh 2
# ]
```
**Ex: Lưu tất cả dữ liệu trả về của .predict**
```python
from paddleocr import PaddleOCR

ocr = PaddleOCR(
    use_doc_orientation_classify=False, 
    use_doc_unwarping=False, 
    use_textline_orientation=False) # text detection + text recognition
# ocr = PaddleOCR(use_doc_orientation_classify=True, use_doc_unwarping=True) # text image preprocessing + text detection + textline orientation classification + text recognition
# ocr = PaddleOCR(use_doc_orientation_classify=False, use_doc_unwarping=False) # text detection + textline orientation classification + text recognition
# ocr = PaddleOCR(
#     text_detection_model_name="PP-OCRv5_mobile_det",
#     text_recognition_model_name="PP-OCRv5_mobile_rec",
#     use_doc_orientation_classify=False,
#     use_doc_unwarping=False,
#     use_textline_orientation=False) # Switch to PP-OCRv5_mobile models
result = ocr.predict("./general_ocr_002.png")
for res in result:
    res.print()
    res.save_to_img("output")
    res.save_to_json("output")
```
