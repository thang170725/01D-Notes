- [id()](#id)
- [isinstance()](#isinstance)
- [FP16 (Floating Point 16-bit là mỗi số được lưu bằng 16 bit (2 byte))](#fp16-floating-point-16-bit-là-mỗi-số-được-lưu-bằng-16-bit-2-byte)
- [bytes (kiểu dữ liệu bytes)](#bytes-kiểu-dữ-liệu-bytes)
  - [.encode()](#encode)
  - [.decode()](#decode)
---
# id()
```bash
Để xem địa chỉ id của một biến trong bộ nhớ.
```
**Syn** 
```bash
id(<variable>)
```
# isinstance()
**Ex**
```python
isinstance(object, type)
x = isinstance("Hello", (str, float, int, str, list, dict, tuple))
print(x) # True
```
# FP16 (Floating Point 16-bit là mỗi số được lưu bằng 16 bit (2 byte))
Trong AI, đặc biệt là các model neural network, bạn sẽ gặp:

FP32  → 32 bit → 4 byte
FP16  → 16 bit → 2 byte
BF16  → 16 bit → 2 byte
INT8  → 8 bit  → 1 byte
INT4  → 4 bit  → 0.5 byte
**Tại sao FP16 quan trọng khi chạy LLM?**
```bash
Model có hàng tỷ weight.

Ví dụ model 14B có khoảng: 14,000,000,000 weights
  Nếu mỗi weight dùng FP16: 14B × 2 byte ≈ 28 GB
    - Nên một model 14B ở FP16 cần khoảng 28 GB chỉ riêng cho weights.
    - Chưa tính:
      + KV cache
      + activation
      + framework overhead
      + context
      + các bộ nhớ phụ khác
```
# bytes (kiểu dữ liệu bytes)
## .encode() 
**Ex**
```python
a = "hello"
encoded = a.encode()

print(type(encoded)) # <class 'bytes'>
```
## .decode()
**Ex**
```python
a = "hello"
encoded = a.encode()
decoded = encoded.decode()

print(a, encoded, decoded) # hello b'hello' hello
# b"hello" chính là chuỗi nhị phân nhưng python hiển thị dưới dạng dễ đọ
```