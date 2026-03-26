- [bin()](#bin)
- [Operator (Toán tử)](#operator-toán-tử)
  - [^ (XOR)](#-xor)
---
# bin()
**Ex1**
```python
n = 10
b = bin(n)

print(b)   # 0b1010

n = 10
b = bin(n)[2:]

print(b)   # 1010
```
# Operator (Toán tử)
## ^ (XOR)
```bash
- Kết quả ĐÚNG (1) khi 2 toán hạng KHÁC nhau
- Kết quả SAI (0) khi 2 toán hạng GIỐNG nhau
```
**Formula**
```bash
A	B	A XOR B
0	0	0
0	1	1
1	0	1
1	1	0
```
**Property**
```bash
XOR có 3 tính chất cực quan trọng:
1. Tự triệt tiêu: a ^ a = 0
2. XOR với 0 giữ nguyên: a ^ 0 = a
3. XOR là phép TOÁN NGHỊCH ĐẢO (invertible): a ^ b = c  ⇔  c ^ a = b  ⇔  c ^ b = a
```
**Ex**
```python
print(1 ^ 1)  # 0
print(1 ^ 0)  # 1
print(0 ^ 1)  # 1
print(0 ^ 0)  # 0
```
**
**Ex2: XOR trên số nguyên (bitwise XOR)**
```python
a = 5   # 0101
b = 3   # 0011

print(a ^ b)

# Phân tích
#   0101  (5)
# ^ 0011  (3)
# ------
#   0110  (6)
# Kết quả: 6
```