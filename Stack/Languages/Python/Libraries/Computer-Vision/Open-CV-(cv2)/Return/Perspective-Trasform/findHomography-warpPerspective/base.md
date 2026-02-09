# cv2.findHomography()
```bash
- Tìm ma trận Homography (3×3) biến đổi tập điểm src → dst
- Dùng khi:
    + Sửa méo ảnh
    + Bird-eye view
    + Ghép ảnh (stitching)
    + Chuyển mặt phẳng (mặt đường, biển báo, giấy A4…)
```
**Bản chất toán học**
```bash
```
**Syn**
```bash
H, mask = cv2.findHomography(src, dst, method=cv2.RANSAC, ransacReprojThreshold=3.0)

- src	    : Nx2 điểm nguồn
- dst	    : Nx2 điểm đích
- method	: 0, RANSAC, LMEDS
- mask	    : 0/1 cho biết điểm nào hợp lệ

Kết quả trả về
H (numpy array)
[[ h11  h12  h13 ]
 [ h21  h22  h23 ]
 [ h31  h32  h33 ]]
Ma trận biến đổi phối cảnh
```

# cv2.warpPerspective()
```bash
- Áp dụng ma trận Homography để biến đổi ảnh
```
**Syn**
```bash
warped = cv2.warpPerspective(
    src_image,
    H,
    dsize=(width, height)
)

- src_image	    : Ảnh gốc
- H	            : Ma trận Homography
- dsize	        : Kích thước ảnh output
```