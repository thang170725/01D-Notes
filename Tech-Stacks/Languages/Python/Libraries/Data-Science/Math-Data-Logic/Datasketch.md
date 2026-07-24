# Datasketch Introduction 
```bash
datasketch dùng để làm gì?
    Nó cài sẵn rất nhiều thuật toán để xử lý dữ liệu lớn như:
        - MinHash
        - MinHashLSH
        - HyperLogLog
        - HyperLogLog++
        - LeanMinHash
        - WeightedMinHash

Trong thực tế, 90% mọi người dùng datasketch chỉ vì MinHash và LSH.
...
**Ex**
```bash
Bạn có: 10 triệu file txt
    Muốn tìm các file giống nhau.

Nếu dùng Jaccard trực tiếp
    10 triệu²
=> không khả thi.

Datasketch giúp giảm thời gian xuống cực nhiều.
```
# Installation
```bash
pip install datasketch
```
# MinHash (MinHash là bản tóm tắt (signature) của một tập dữ liệu)
**Syn**
```bash
from datasketch import MinHash

m = MinHash(num_perm)

- Input:
    + num_perm=128: tức là 128 hash function
```
## update()
```bash
Mỗi phần tử phải truyền vào dạng bytes
```
**Ex**
```python
from datasketch import MinHash

m = MinHash()

words = [
    "hello",
    "python",
    "chatgpt"
]

for w in words:
    m.update(w.encode())
# Lúc này m đã chứa chữ ký của tập dữ liệu.
```
# MinHashLSH
```bash
Giả sử có 1 triệu tài liệu
    Nếu dùng
        for a in docs:
            for b in docs:

    sẽ có: 1 triệu² => khoảng 10^12 lần so sánh không thể chạy.

LSH nghĩa là Locality Sensitive Hashing

Ý tưởng
    Những tài liệu giống nhau sẽ được đưa vào cùng một bucket.

Ví dụ
    Doc1 - bucket 7
    Doc2 - bucket 7
    Doc3 - bucket 15
    Doc4 - bucket 20
=> Nếu tìm tài liệu giống Doc1 LSH chỉ kiểm tra bucket 7 không cần xem 15, 20, ...
```
**Syn**
```bash
from datasketch import MinHashLSH

lsh = MinHashLSH(
    threshold=0.8,
    num_perm=128
)

- Input:
    + threshold=0.8: chỉ lưu những tài liệu có độ giống khoảng >=0.8
```
## insert() (Đưa tài liệu vào LSH)
## query() (Muốn tìm tài liệu giống)
**Ex**
```python
from datasketch import MinHash, MinHashLSH

doc1 = ["apple", "banana", "orange"]
doc2 = ["apple", "banana", "grape"]

m1 = MinHash()
m2 = MinHash()

for w in doc1:
    m1.update(w.encode())

for w in doc2:
    m2.update(w.encode())

lsh = MinHashLSH(threshold=0.5)

lsh.insert("Document A", m1)

result = lsh.query(m2)

print(result) # ['Document A']
# vì Document A đủ giống. 
```