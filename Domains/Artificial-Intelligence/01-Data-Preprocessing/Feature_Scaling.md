- [Introduction](#introduction)
- [Technical (các kỹ thuật scaling)](#technical-các-kỹ-thuật-scaling)
  - [Min-Max Scaling](#min-max-scaling)
- [Standardization (Z-score)](#standardization-z-score)
  - [Robust Scaling](#robust-scaling)
---
# Introduction 
```bash
- Scaling trong data preprocessing dùng để đưa các feature về cùng "đơn vị ảnh hưởng" trong model (tức đưa feature về cùng thang đo)
```
**Ex**
```bash
- Giả sử bạn có 2 feature:
    + Chiều cao: 150 → 180 (cm)
    + Lương: 5,000 → 50,000 (USD)
- Nếu không scale: Model sẽ “nghĩ” lương quan trọng hơn nhiều (vì số lớn hơn)
- Sau khi scaling về [0,1]: Cả 2 feature đều nằm cùng range → model học công bằng hơn
```
# Technical (các kỹ thuật scaling)
## Min-Max Scaling
```bash
Đưa dữ liệu về khoảng [0, 1]
```
**Formula**
```bash
x' = (x - x_min) / (x_max - x_min)
```
# Standardization (Z-score)
```bash
Đưa dữ liệu về phân phối có
    - mean = 0
    - std = 1
```
**Formula**
```bash
x' = (x - μ) / σ

- x         : giá trị gốc
- μ (mu)    : mean — trung bình của toàn bộ feature
- σ (sigma) : standard deviation — độ lệch chuẩn (mức độ phân tán dữ liệu)
- x′        : giá trị sau khi scale
```
## Robust Scaling
```bash
- Dùng median + IQR
- Ít bị ảnh hưởng bởi outlier
```
**Formula**
```bash
x' = (x - median) / IQR

- x                         : giá trị gốc
- median                    : giá trị trung vị (ở giữa khi sắp xếp)
- IQR (Interquartile Range) : IQR = Q3 - Q1
    + Q1: 25th percentile
    + Q3: 75th percentile
    + x′: giá trị sau scaling
```