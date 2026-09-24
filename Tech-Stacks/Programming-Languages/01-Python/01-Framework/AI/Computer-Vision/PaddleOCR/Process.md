- [PaddleOCR (class chính để chạy OCR - Dùng để khởi tạo, load các model cần thiết)](#paddleocr-class-chính-để-chạy-ocr---dùng-để-khởi-tạo-load-các-model-cần-thiết)
  - [Display (Nhóm cung cấp thông tin)](#display-nhóm-cung-cấp-thông-tin)
    - [.predict()](#predict)
      - [rec\_texts](#rec_texts)
      - [rec\_score() (độ tự tin của mô hình đối với chuỗi mà nó đã chọn)](#rec_score-độ-tự-tin-của-mô-hình-đối-với-chuỗi-mà-nó-đã-chọn)
---
# PaddleOCR (class chính để chạy OCR - Dùng để khởi tạo, load các model cần thiết)
```bash
Tùy config, pipeline sẽ gồm:
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
```bash
Khi bạn gọi
    result = ocr.predict("images/bao_hiem_tai_nan.jpg")
    
    PaddleOCR thực hiện
        Ảnh
         ↓
        Detector
         ↓
        Recognizer
         ↓
        CTC Decoder
         ↓
        Greedy Search
         ↓
        Text cuối cùng
```
**Syn**
```bash
ocr.predict("img.jpg")

- Output:
# [
#   {
#       'input_path': str, 'page_index': , 
#       'doc_preprocessor_res': {
#           'output_img': list,
#           'model_settings': {
#               'use_doc_preprocessor': bool,
#               'use_textline_orientation': bool
#           }
#           'text_det_params': {
#               'limit_side_len': int,
#               'limit_type': str,
#               'thresh': float,
#               'max_side_limit': int,
#               'box_thresh': float,
#               'unclip_ratio': float
#           }
#           'text_type': str,
#           'text_rec_score_thresh': float,
#           'return_word_box': bool,
#           'rec_texts': list,
#           'rec_score': list
#           'rec_polys': list,
#           'vis_fonts': list,
#           'textline_orientation_angles': list,
#           'rec_boxes': list
#       }
#   },
#   ...
# ]
```
#### rec_texts
**Ex**
```python
from paddleocr import PaddleOCR

ocr = PaddleOCR(
    use_doc_orientation_classify=False,
    use_doc_unwarping=False,
    use_textline_orientation=False
)

result = ocr.predict("images/bao_hiem_tai_nan.jpg")

for page in result:
    for text in page['rec_texts']:
        print(text)

# NHÜNG DIÈU CÀN LUU Ý
# BAOVIET
# Insurance

# ...

# Tur.1.0.... già00... ngày18.../04../ 20.1.8
# Dén ..gi 0 ngay 18../..04/.2019
```
#### rec_score() (độ tự tin của mô hình đối với chuỗi mà nó đã chọn)
```python
from paddleocr import PaddleOCR

ocr = PaddleOCR(
    use_doc_orientation_classify=False,
    use_doc_unwarping=False,
    use_textline_orientation=False
)

result = ocr.predict("images/bao_hiem_tai_nan.jpg")

for page in result:
    texts = page["rec_texts"]
    scores = page["rec_scores"]

    for text, score in zip(texts, scores):
        print(f"{score:.4f}  {text}")

# 0.9415  NHÜNG DIÈU CÀN LUU Ý
# 1.0000  BAOVIET

# ...

# 0.8603  Tur.1.0.... già00... ngày18.../04../ 20.1.8
# 0.7408  Dén ..gi 0 ngay 18../..04/.2019
```
**Ex: Lưu tất cả dữ liệu trả về của .predict**
```python
from paddleocr import PaddleOCR

ocr = PaddleOCR(
    use_doc_orientation_classify=False, 
    use_doc_unwarping=False, 
    use_textline_orientation=False) # text detection + text recognition

result = ocr.predict("./general_ocr_002.png")
for res in result:
    res.print()
    res.save_to_img("output")
    res.save_to_json("output")
```
