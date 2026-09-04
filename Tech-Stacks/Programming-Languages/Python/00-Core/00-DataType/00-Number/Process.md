- [bin()](#bin)
- [Operator (Toán tử)](#operator-toán-tử)
  - [^ (XOR)](#-xor)
  - [\>\> (dịch phải)](#-dịch-phải)
  - [\<\< (dịch trái)](#-dịch-trái)
  - [| (OR)](#-or)
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
Kết quả 
  - ĐÚNG (1) khi 2 toán hạng KHÁC nhau
  - SAI (0) khi 2 toán hạng GIỐNG nhau
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
## >> (dịch phải) 
**Ex1: dịch phải 1 bit**
```python
a = 3
res = a >> 1 # 011 -> 01
print(res, type(res)) # 1 <class 'int'>
```
## << (dịch trái)
**Ex**
```python
a = 8
res = 2 << a # 10 -> 1000000000 nghĩa là dịch số 2 sang a bit
print(res, type(res)) # 512 <class 'int'>
```
## | (OR)
**Formula**
```bash
| Bit A | Bit B | A OR B |
| ----- | ----- | ------ |
| 0     | 0     | 0      |
| 0     | 1     | 1      |
| 1     | 0     | 1      |
| 1     | 1     | 1      |
```
**Ex**
```python
a = 4 # 100
b = 5 # 101
res = a|b # 100 OR 101 -> 101 (không nhớ)
print(res, type(res))
```