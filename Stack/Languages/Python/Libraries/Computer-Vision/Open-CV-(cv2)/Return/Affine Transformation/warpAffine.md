warpAffine() là gì & cú pháp chuẩn
2.1 warpAffine làm gì?

👉 Áp dụng ma trận Affine lên ảnh

Input: ảnh + ma trận

Output: ảnh mới đã biến đổi

📌 Nó làm việc pixel → pixel

2.2 Cú pháp đầy đủ (chuẩn OpenCV)
dst = cv2.warpAffine(
    src,        # ảnh đầu vào
    M,          # ma trận Affine (2x3)
    dsize,      # (width, height)
    flags=cv2.INTER_LINEAR,
    borderMode=cv2.BORDER_CONSTANT,
    borderValue=0
)

2.3 Giải thích từng tham số (rất quan trọng)
src

Ảnh gốc

M

Ma trận Affine 2×3:

[a b tx]
[c d ty]

dsize
(width, height)


📌 KHÔNG phải (height, width)
📌 Quyết định canvas đầu ra

flags (nội suy)
Giá trị	Ý nghĩa
INTER_LINEAR	mặc định, tốt
INTER_NEAREST	nhanh, răng cưa
INTER_CUBIC	đẹp, chậm
borderMode

Xử lý vùng ngoài ảnh

Mode	Ý nghĩa
BORDER_CONSTANT	tô màu
BORDER_REFLECT	phản chiếu
BORDER_REPLICATE	lặp pixel biên
borderValue

Màu nền khi dùng BORDER_CONSTANT

borderValue=(255,255,255)  # nền trắng

2.4 Demo “đỡ khó chịu” hơn (không nền đen)
affine_img = cv2.warpAffine(
    img,
    M,
    (w + 200, h + 200),
    borderMode=cv2.BORDER_CONSTANT,
    borderValue=(255, 255, 255)
)


👉 Canvas to hơn + nền trắng

3️⃣ Tư duy đúng khi dùng Affine (chốt lại)

❌ “Affine làm ảnh xấu đi”
✔️ “Affine đưa ảnh về hệ tọa độ tôi cần”

Ví dụ tư duy chuẩn:

OCR: “Tôi không cần nền đẹp, tôi cần chữ thẳng”

Face recognition: “Mắt phải nằm đúng vị trí”

Tracking: “Vật phải ổn định”

Nếu bạn muốn, mình có thể:

Demo Affine để căn mặt người

So sánh Affine vs Homography trên cùng ảnh

Dạy cách chọn 3 điểm cho đúng

Hoặc vẽ lại hệ tọa độ trước/sau biến đổi

👉 Bạn muốn tiếp theo theo hướng toán, thực tế, hay trực quan vẽ hình?