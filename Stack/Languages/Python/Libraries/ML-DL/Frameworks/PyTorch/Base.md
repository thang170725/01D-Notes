- [Directory structure](#directory-structure)
- [Introduction](#introduction)
- [Installation](#installation)
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
process.md

👉 File này nên chứa các thao tác tensor + autograd + device + data
(tức là các thứ dùng trước khi xây dựng model)

# Tensor Processing (các thao tác cơ bản với tensor trong PyTorch)

- [Tensor Creation](#tensor-creation) # tạo tensor
  - [Tensor()](#tensor)
  - [.clone()](#clone)
  - [arange()](#arange)
  - [zeros()](#zeros)
  - [ones()](#ones)
  - [empty()](#empty)

- [Random Tensor](#random-tensor) # tạo tensor ngẫu nhiên
  - [rand()](#rand)
  - [randn()](#randn)
  - [randn_like()](#randn_like)
  - [randint()](#randint)
  - [manual_seed()](#manual_seed)

- [Tensor Structure / Shape](#tensor-structure--shape) # thay đổi cấu trúc tensor
  - [[]](#indexing)
  - [.view()](#view)
  - [.reshape()](#reshape)
  - [.unsqueeze()](#unsqueeze)
  - [.squeeze()](#squeeze)
  - [.stack()](#stack)
  - [.cat()](#cat)
  - [.tolist()](#tolist)

- [Tensor Info](#tensor-info) # xem thông tin tensor
  - [.size()](#size)
  - [.shape](#shape)
  - [.item()](#item)

- [Tensor Math](#tensor-math) # các phép toán tensor
  - [.mean()](#mean)
  - [exp()](#exp)
  - [tanh()](#tanh)
  - [add()](#add)
  - [add_()](#add_)
  - [.argmax()](#argmax)

- [Autograd](#autograd) # hệ thống tính gradient tự động
  - [.backward()](#backward)
  - [.grad](#grad)
  - [.detach()](#detach)
  - [no_grad()](#no_grad)

- [Device (CPU / GPU)](#device-cpu--gpu) # quản lý thiết bị tính toán
  - [device()](#device)
  - [cuda.is_available()](#is_available)
  - [cuda.get_device_name()](#get_device_name)
  - [.to()](#to)

- [Data Pipeline](#data-pipeline) # chuẩn bị dữ liệu cho training
  - [Dataset](#dataset)
  - [DataLoader](#dataloader)

- [Utils](#utils) # tiện ích bổ sung
2️⃣ nn_modules.md

👉 File này chỉ nên chứa xây dựng mạng neural

# Neural Network Modules

# các công cụ trong torch.nn dùng để xây dựng mạng nơ ron

- [NN Core](#nn-core)
  - [Module](#module) # lớp cơ bản để định nghĩa model
  - [Linear()](#linear) # fully connected layer

- [Model Mode](#model-mode) # chuyển trạng thái model
  - [.train()](#train) # bật training mode
  - [.eval()](#eval) # bật inference mode

- [Model Output](#tensor-đầu-ra-của-mô-hình)
  # tensor output của model thường dùng để tính loss hoặc prediction

- [Training Pipeline](#training-pipeline)
  - [TRAIN](#train-process) # quy trình train model
  - [TEST](#test-process) # quy trình đánh giá model
3️⃣ export.md

👉 File này dành cho deployment / xuất model

# Model Export / Deployment

# xuất model sang định dạng khác để deploy hoặc chạy ngoài PyTorch

- [ONNX Export](#onnx-export)
  - [.onnx.export()](#onnxexport) # chuyển model PyTorch sang ONNX
4️⃣ Cấu trúc note hoàn chỉnh của bạn sẽ là
pytorch_notes
│
├── process.md
│   # tensor operations
│   # autograd
│   # device
│   # dataset
│
├── nn_modules.md
│   # xây dựng neural network
│   # layers
│   # model mode
│
└── export.md
    # xuất model
    # deployment

Workflow tương ứng:

process.md
   ↓
nn_modules.md
   ↓
training
   ↓
export.md
5️⃣ Một mẹo cực quan trọng khi viết PyTorch note

Luôn nghĩ theo pipeline:

Data
 ↓
Tensor
 ↓
Model
 ↓
Loss
 ↓
Backward
 ↓
Update
 ↓
Export

Tương ứng:

process.md
nn_modules.md
optimizer.md (sau này nên thêm)
export.md

💡 Nếu bạn muốn, mình có thể giúp bạn tạo luôn một PyTorch Note Structure chuẩn cho Deep Learning (khoảng 10 file markdown) để khi bạn học:

CNN

RNN

Transformer

RAG

thì không cần reorganize lại notes nữa.
Cái này rất đáng làm sớm.