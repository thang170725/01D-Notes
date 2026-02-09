# imread()
```bash
- Được sử dụng để đọc một hình ảnh từ ổ đĩa và lưu nó dưới dạng một mảng NumPy để xử lý trong các ứng dụng xử lý ảnh.
```
**Syn**
```bash
cv2.imread(filename, flags)

- Filename: Đường dẫn đến ảnh (có thể là tuyệt đối hoặc tương đối).
- Flags: Chế độ đọc ảnh, mặc định là cv2.IMREAD_COLOR
    + cv2.IMREAD_COLOR (hoặc 1): Đọc ảnh màu bỏ kênh anpha.
    + cv2.IMREAD_GRAYSCALE (hoặc 0): Đọc ảnh ở dạng grayscale (đen trắng).
    + cv2.IMREAD_UNCHANGED (hoặc -1): Giữ nguyên ảnh, kể cả kênh alpha nếu có.
```