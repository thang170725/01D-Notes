- [id()](#id)
- [isinstance()](#isinstance)
- [bytes (kiểu dữ liệu bytes)](#bytes-kiểu-dữ-liệu-bytes)
  - [.encode() \& .decode()](#encode--decode)
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
JSON
Là cú pháp để lưu trữ và trao đổi dữ liệu.
JSON là văn bản, được viết bằng ký hiệu đối tượng Javascript.
json.loads()
Để phân tích cú pháp nhằm mục đích chuyển từ JSON sang Python.
Cú pháp:
json.loads(<variable>)
json.dumps()
# bytes (kiểu dữ liệu bytes)
## .encode() & .decode()
**Ex**
```python
a = "hello"
encoded = a.encode()
decoded = encoded.decode()

print(a, encoded, decoded) # hello b'hello' hello
# b"hello" chính là chuỗi nhị phân nhưng python hiển thị dưới dạng dễ đọ
```