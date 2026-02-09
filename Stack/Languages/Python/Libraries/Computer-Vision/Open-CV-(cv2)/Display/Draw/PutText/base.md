# .putText()
**Syn**
```bash
cv2.putText(img, text, org, fontFace, fontScale, color, thickness, lineType)

    + img	    : Ảnh hoặc khung hình (frame) bạn muốn vẽ lên.
    + text	    : Nội dung chữ (Kiểu String). Lưu ý: OpenCV mặc định không viết được tiếng Việt có dấu.
    + org	    : Tọa độ điểm bắt đầu (góc dưới bên trái của chữ) dạng (x, y).
    + fontFace	: Loại font chữ (Ví dụ: cv2.FONT_HERSHEY_SIMPLEX, cv2.FONT_HERSHEY_COMPLEX).
    + fontScale	: Tỷ lệ kích thước chữ (Số thực, ví dụ: 1.0, 0.5).
    + color	Màu : sắc theo hệ BGR (ví dụ: (0, 255, 0) là màu xanh lá).
    + thickness	: Độ dày nét chữ (Số nguyên).
    + lineType	: Loại đường nét. Nên dùng cv2.LINE_AA (Anti-Aliased) để chữ mịn, không bị răng cưa.
```