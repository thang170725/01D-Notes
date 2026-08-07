- [id()](#id)
- [isinstance()](#isinstance)
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