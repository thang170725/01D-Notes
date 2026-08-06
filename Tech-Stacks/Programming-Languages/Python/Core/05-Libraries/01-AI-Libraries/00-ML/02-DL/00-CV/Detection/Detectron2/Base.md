- [Introduction](#introduction)
- [Installation](#installation)
---
# Introduction
**Documentation**
```bash
1. https://detectron2.readthedocs.io/en/latest/tutorials/install.html
```
```bash
- Detectron2 là một thư viện mã nguồn mở mạnh mẽ dành cho thị giác máy tính (computer vision), được phát triển bởi Meta AI. Nó chủ yếu dùng cho các bài toán như phát hiện đối tượng, phân đoạn ảnh, và nhận dạng keypoint.
- Detectron2 là phiên bản nâng cấp của Detectron (trước đó), được viết lại bằng PyTorch với mục tiêu:
    + Linh hoạt hơn
    + Hiệu năng cao hơn
    + Dễ mở rộng và nghiên cứu
- Detectron2 hỗ trợ nhiều tác vụ quan trọng trong CV:
    1. Object Detection: Xác định vị trí và loại đối tượng trong ảnh. Ví dụ: người, xe, động vật...
    2. Instance Segmentation: Phân đoạn từng đối tượng riêng biệt (pixel-level). Mô hình nổi bật: Mask R-CNN
    3. Semantic Segmentation: Gán nhãn cho từng pixel trong ảnh
    4. Keypoint Detection: Xác định các điểm đặc trưng (ví dụ: khớp xương người)
- Đặc điểm nổi bật
    + Hiệu năng cao: tối ưu GPU, training nhanh
    + Modular (mô-đun hóa): dễ tùy chỉnh từng phần của model
    + Model zoo: nhiều model pretrained sẵn
    + Dễ nghiên cứu: code rõ ràng, phù hợp cho research
    + Kiến trúc cơ bản
```
# Installation
**Requirement**
```bash
1. Python >= 3.7
2. PyTorch >= 1.8 (recommend version 2.1.0)
3. torchvision
```
```bash
python -m pip install 'git+https://github.com/facebookresearch/detectron2.git'
# (add --user if you don't have permission)

# Or, to install it from a local clone:
git clone https://github.com/facebookresearch/detectron2.git
python -m pip install -e detectron2
```