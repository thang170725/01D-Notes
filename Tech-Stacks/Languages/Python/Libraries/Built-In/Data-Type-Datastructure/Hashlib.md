- [Hashlib Introduction](#hashlib-introduction)
- [.md5()](#md5)
  - [.hexdigest()](#hexdigest)
---
# Hashlib Introduction 
```bash
Đúng, hashlib là một thư viện built-in (thư viện chuẩn) của Python. Bạn không cần cài đặt bằng pip.
    Chỉ cần: import hashlib

Hash là quá trình biến một dữ liệu bất kỳ thành một chuỗi ký tự có độ dài cố định.
    Ví dụ
        "Hello"
           │
           ▼
        185f8db32271fe25f561a6fc938b2e264306ec304eda518007d1764826381969

Đầu vào có thể là:
    - chuỗi
    - file
    - ảnh
    - video
    - bytes
-> Đầu ra luôn là một chuỗi hash.
```
**Hash có những đặc điểm gì?**
```bash
Ví dụ dùng MD5
    Hello
    ↓
    8b1a9953c4611296a827abf8c47804d7

Nếu đổi chỉ 1 ký tự
    Hello
    ↓
    hello
-> Hash sẽ thành: 5d41402abc4b2a76b9719d911017c592. Hoàn toàn khác.
```
**hashlib dùng để làm gì?**
```bash
Có rất nhiều ứng dụng.
    1. Kiểm tra hai file có giống nhau không ⭐
        Ví dụ:
            image1.jpg
                ↓
            MD5
                ↓
            7AF319...

            image2.jpg
                ↓
                MD5
                ↓
            7AF319...

            => Hash giống nhau -> Hai file giống nhau. Không cần so từng pixel.

    2. Kiểm tra file có bị sửa không
    3. Lưu mật khẩu
    4. Phát hiện dữ liệu thay đổi
```
**Tại sao phải dùng .encode()?**
```bash
Hash chỉ làm việc với bytes.

Ví dụ
    text = "Hello" là kiểu str -> Ta phải đổi thành bytes
        text.encode()
        ↓
        b'Hello'
        -> mới hash được.

Ví dụ
    import hashlib

    text = "Hello"

    print(type(text)) # <class 'str'>
    print(type(text.encode())) # <class 'bytes'>
```
# .md5()
**Ex**
```python
import hashlib

data = b"hello"

h = hashlib.md5(data)
print(h) # <md5 _hashlib.HASH object @ 0x000002B3886ABC30>
```
## .hexdigest()
**Ex**
```python
import hashlib

data = b"Hello"

h = hashlib.md5(data).hexdigest()
print(h) # 8b1a9953c4611296a827abf8c47804d7
```
