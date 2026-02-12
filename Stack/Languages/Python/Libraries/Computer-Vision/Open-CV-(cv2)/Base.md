- [Directory Structure](#directory-structure)
- [Introduction](#introduction)
- [Kênh  màu](#kênh--màu)
- [Segmentation mask](#segmentation-mask)
- [__version__](#version)
---
# Directory Structure
```bash
Open-CV             # mình dùng thư mục này để xem kiến thức
├── Base.md         # mình dùng file này để xem kiến thức về, tiện ích của OpenCV
├── Create_IO.md    # mình dùng file này để khởi tạo, cấu hình, đọc, ghi, hiển thị v.v (IO)
├── Process_IMG.md  # mình dùng file này để xem các thông số và thao tác xử lý trên ảnh    
├── Css         # mình dùng thư mục này để xem kiến thức về Css
├── Java        # mình dùng thư mục này để xem kiến thức về Java
└── Practices.md    # mình dùng file này để xem code mẫu, bài tập
```
# Introduction
```bash
- OpenCV để xử lý hình ảnh và nó hỗ trợ vô số các thuật toán liên quan đến lĩnh vực thị giác máy tính và lĩnh vực học máy. Nó có thể sử dụng card đồ họa (GPU) để xử lý nhằm tăng tốc độ xử lý.
- Cần pip install opencv-python, import cv2
```
# Kênh  màu
```bash
- Mặc định Opencv sử dụng kênh màu BGR.
- Vì OpenCV ban đầu đưuọc viết bằng C/C++ và theo chuẩn xử lý ảnh của Windows Bitmap (BMP) - vốn lưu pixel theo thứ tự BGR. Để tăng hiệu suất và tránh chuyển đổi không cần thiết, OpenCV giữ nguyên thứ tự này.
- Khi đọc ảnh từ file, OpenCV đọc pixel theo thứ tự BGR để tránh tốn tài nguyên chuyển đổi qua lại nếu bạn xử lý nhiều ảnh ở cấp hệ thống.
```
# Segmentation mask
```bash
- Là một ảnh đen trắng (hoặc đa kênh) dùng để biểu diện phân vùng (vật thể hoặc khu vực) trong ảnh gốc
- Mỗi pixel trong mask cho biết vật thể nào (hoặc lớp nào) nó thuộc về.
- Có 2 loại phổ biến:
    + binary mask: pixel=1 nếu thuộc vật thể, 0 nếu là nền.
    + multi-class mask: pixel =0,1,2,… tương ứng với các lớp khác nhau (mèo, chó, người, …).
    + Không phụ thuộc vào màu sắc, mà phụ thuộc vào nhãn mà bạn gán khi huấn luyện mô hình.
```
# __version__
```bash
- Trả về version đang sử dụng.
```
```python
import cv2
print(cv2.__version__) # 4.11.0
```