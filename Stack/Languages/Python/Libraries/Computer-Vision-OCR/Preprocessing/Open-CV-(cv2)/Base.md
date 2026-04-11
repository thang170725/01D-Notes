- [Directory Structure](#directory-structure)
- [Introduction](#introduction)
- [Installation](#installation)
- [__version__](#version)
---
# Directory Structure
```bash
Open-CV             # mình dùng thư mục này để xem kiến thức
├── Base.md         # mình dùng file này để xem kiến thức về, tiện ích của OpenCV
├── Create_IO.md    # mình dùng file này để thao tác (IO), khởi tạo
├── Process_IMG.md  # mình dùng file này để xem các thông số và thao tác xử lý trên ảnh    
└── Practices.md    # mình dùng file này để xem code mẫu, bài tập
```
# Introduction
```bash
- OpenCV để xử lý hình ảnh và nó hỗ trợ vô số các thuật toán liên quan đến lĩnh vực thị giác máy tính và lĩnh vực học máy. Nó có thể sử dụng card đồ họa (GPU) để xử lý nhằm tăng tốc độ xử lý.
```
# Installation
```bash
1. pip install opencv-python
```
# __version__
```bash
- Trả về version đang sử dụng.
```
```python
import cv2
print(cv2.__version__) # 4.11.0
```