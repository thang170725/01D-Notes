- [Directory structure](#directory-structure)
- [Introduction](#introduction)
- [Installation](#installation)
- [dz/dW = (dz/dy).(dy/dW)](#dzdw--dzdydydw)
- [dy/dW = a = \[1.0, 2.0, 3.0\]](#dydw--a--10-20-30)
- [dz/db = (dz/dy).(dy/db) = 1. + 1. + 1. = 3.](#dzdb--dzdydydb--1--1--1--3)
- [Tạo 1 tensor 2x3 gồm các giá trị ngẫu nhiên ~ N(0, 1)](#tạo-1-tensor-2x3-gồm-các-giá-trị-ngẫu-nhiên--n0-1)
- [tensor đầu ra của mô hình](#tensor-đầu-ra-của-mô-hình)
---
# Directory structure
```bash
PyTorch/
    ├── 01_Tensors.md         # Khởi tạo, Thao tác mảng, tính toán GPU
    ├── 02_Autograd.md        # Đạo hàm tự động (Backpropagation)
    ├── 03_NN_Modules.md      # Xây dựng Layer, Model (nn.Module)
    ├── 04_Data_Pipeline.md   # Xử lý dữ liệu
    └── 05_Optimization.md    # Loss functions, Optimizers (SGD, Adam)Torch
```
# Introduction
```bash
- PyTorch là một thư viện của python nhưng nhiều người gọi nó là framework vì đầy đủ sức mạnh của một framework (end-to-end)
- PyTorch dùng để xây dựng và huấn luyện mô hình học sâu (deep learning).
```
# Installation
```bash
pip install torch
```
