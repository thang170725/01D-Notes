- [Datasketch Introduction (Nó cài sẵn rất nhiều thuật toán để xử lý dữ liệu lớn)](#datasketch-introduction-nó-cài-sẵn-rất-nhiều-thuật-toán-để-xử-lý-dữ-liệu-lớn)
- [Installation](#installation)
- [MinHash (MinHash là bản tóm tắt (signature) của một tập dữ liệu)](#minhash-minhash-là-bản-tóm-tắt-signature-của-một-tập-dữ-liệu)
  - [update() (đưa từng phần tử (shingle/ngram/word) vào để tính chữ ký MinHash)](#update-đưa-từng-phần-tử-shinglengramword-vào-để-tính-chữ-ký-minhash)
  - [.hashvalues](#hashvalues)
  - [.jaccard()](#jaccard)
- [MinHashLSH()](#minhashlsh)
  - [insert() (Đưa tài liệu vào LSH)](#insert-đưa-tài-liệu-vào-lsh)
  - [query() (Muốn tìm tài liệu giống)](#query-muốn-tìm-tài-liệu-giống)
- [Practices](#practices)
  - [so sánh 2 tập có giống nhau hay không bằng jaccard](#so-sánh-2-tập-có-giống-nhau-hay-không-bằng-jaccard)
  - [demo minhashLSH](#demo-minhashlsh)
---
# Datasketch Introduction (Nó cài sẵn rất nhiều thuật toán để xử lý dữ liệu lớn)
```bash
Chứa các thuật toán dùng để xử lý dữ liệu lớn
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
**Ý tưởng**
```bash
Giả sử có 2 văn bản:
    - Text A: I love machine learning
    - Text B: I love deep learning

Ta tạo character 5-gram.
    Text A
    i lov
     love
    love 
    ove m
    ve ma
    e mac
     mach
    ...

Giả sử cuối cùng thu được tập (set)
    - A = {"i lov"," love","love "," mach", "chine", "learn"}
    - B = {"i lov", " love", "love ", " deep", "learn"}

Ta thấy
    A và B có khá nhiều phần giống nhau.
        Nếu dùng Jaccard -> rất tốn RAM và CPU.

MinHash làm gì?
    Thay vì lưu 
        {
            "i lov",
            " love",
            "love ",
            ...
            50.000 gram
        }
    => MinHash chỉ lưu [1523, 9812, 352, 991, 7812, ...]. Ví dụ khoảng 128 số nguyên. Đây gọi là signature.
```
[Giới thiệu về thuật toán Jaccard](../../../../../../Domains/Artificial-Intelligence/00-Math-Core/Base.md#jaccard)
**Syn**
```bash
from datasketch import MinHash

m = MinHash(num_perm)

- Input:
    + num_perm=128: tức là 128 hash function
```
## update() (đưa từng phần tử (shingle/ngram/word) vào để tính chữ ký MinHash)
```bash
Điều quan trọng là:
    - update() không trả về gì (None).
    - Bạn không nhìn thấy chữ ký thay đổi ngay.
    - Muốn xem kết quả, phải in m.hashvalues.
```
**Syn**
```bash
- Input: Mỗi phần tử phải truyền vào dạng bytes
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
## .hashvalues
**Ex**
```python
from datasketch import MinHash

m = MinHash(num_perm=8)

print(m.hashvalues)

m.update(b"hello")

print(m.hashvalues)
# [4294967295 4294967295 4294967295 4294967295
#  4294967295 4294967295 4294967295 4294967295]

# [ 3452345 9876543 1234567 7654321
#  2345678 4567890 1122334 9988776]
```
## .jaccard()
# MinHashLSH()
```bash
Bước 1: Tạo MinHash
    - m1 = MinHash(...)
    - m2 = MinHash(...)
    - m3 = MinHash(...)

    => Lúc này (ví dụ minh họa)
        - Page1: [12, 41, 92, 15, 81, ...]
        - Page2: [12, 41, 92, 16, 81, ...]
        - Page3: [91, 55, 10, 74, 63, ...]
    => Đây là signature.

Bước 2: Đưa vào LSH
    - lsh.insert("page1", m1)
    - lsh.insert("page2", m2)
    - lsh.insert("page3", m3)
```
**LSH làm gì?**
```bash
Giả sử signature có 128 số. -> LSH chia thành nhiều band.

Ví dụ đơn giản chỉ có 8 số: 12 41 | 92 15 | 81 20 | 11 66

Chia thành 4 band
    - Band1: 12 41
    - Band2: 92 15
    - Band3: 81 20
    - Band4: 11 66

Page2
    12 41 | 92 16 | 81 20 | 15 77
    
    Band
        - Band1: 12 41
        - Band2: 92 16
        - Band3: 81 20
        - Band4: 15 77

-> LSH sẽ tạo bảng băm.
```
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
**Syn**
```python
lsh.insert(key, minhash)

- key: tên hoặc ID của tài liệu.
- minhash: đối tượng MinHash đã được tạo.
```
Ví dụ 1: Chỉ có 2 tài liệu
from datasketch import MinHash, MinHashLSH

lsh = MinHashLSH(threshold=0.5, num_perm=128)

m1 = MinHash(num_perm=128)
m2 = MinHash(num_perm=128)

for word in "I love machine learning".split():
    m1.update(word.encode())

for word in "I love machine learning".split():
    m2.update(word.encode())

lsh.insert("doc1", m1)
lsh.insert("doc2", m2)

Ở đây:

lsh.insert("doc1", m1)

có nghĩa là:

"LSH, hãy nhớ rằng tài liệu có ID là doc1 có chữ ký MinHash là m1."

Tiếp theo:

lsh.insert("doc2", m2)

"LSH, hãy nhớ rằng tài liệu doc2 có chữ ký m2."

Ví dụ 2: Thêm nhiều tài liệu

Giả sử

docs = {
    "page_1": "hello world",
    "page_2": "hello world",
    "page_3": "python programming",
}

Ta thường viết

from datasketch import MinHash

for key, text in docs.items():

    m = MinHash(num_perm=128)

    for word in text.split():
        m.update(word.encode())

    lsh.insert(key, m)

Sau vòng lặp, LSH sẽ chứa

page_1
page_2
page_3

nhưng nó không lưu nội dung text, chỉ lưu thông tin cần thiết để tìm kiếm nhanh.

Ví dụ 3: Project OCR của bạn

Giả sử có

pages = [
    Page(1, "..."),
    Page(2, "..."),
    Page(3, "..."),
]

và mỗi Page đã có

page.minhash

thì

lsh = MinHashLSH(threshold=0.9, num_perm=128)

for page in pages:
    lsh.insert(str(page.page), page.minhash)

Sau đó muốn tìm các trang giống trang số 5:

target = pages[4]

result = lsh.query(target.minhash)

print(result)

Ví dụ kết quả

['5', '18', '42']

nghĩa là trang 5 có khả năng giống trang 18 và 42.

insert() có lưu dữ liệu thật không?

Không.

Ví dụ

lsh.insert("doc1", m1)

LSH không biết:

văn bản của doc1
số trang
tên file
nội dung PDF

Nó chỉ biết:

key = "doc1"

↓

MinHash signature

↓

Các bucket mà signature này thuộc về

Nói cách khác, key chỉ là nhãn (label) để sau này query() trả lại cho bạn. Vì vậy trong dự án OCR, nhiều người dùng:

lsh.insert(f"{file_name}:{page_number}", page.minhash)

Ví dụ:

lsh.insert("invoice01.pdf:12", page.minhash)

Khi gọi:

lsh.query(page.minhash)

có thể nhận được:

[
    "invoice01.pdf:12",
    "invoice03.pdf:7",
    "invoice08.pdf:12"
]

LSH chỉ giúp bạn lọc ra các ứng viên có khả năng giống nhau. Sau đó bạn mới dùng Jaccard hoặc RapidFuzz để kiểm tra và xác nhận mức độ giống thực sự.
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
# Practices
## so sánh 2 tập có giống nhau hay không bằng jaccard
**Ex**
```python
from datasketch import MinHash

text1 = {
    "apple",
    "banana",
    "cat",
    "dog"
}

text2 = {
    "apple",
    "banana",
    "dog",
    "fish"
}

m1 = MinHash(num_perm=128)
for word in text1:
    m1.update(word.encode("utf8"))

m2 = MinHash(num_perm=128)
for word in text2:
    m2.update(word.encode("utf8"))

print(m1.jaccard(m2)) # 0.5703125
```
## demo minhashLSH
```python
from datasketch import MinHash, MinHashLSH

docs = {
    "doc1": "I love machine learning",
    "doc2": "I love machine learning",
    "doc3": "I love deep learning",
    "doc4": "Today is sunny",
    "doc5": "Today is sunny",
}

lsh = MinHashLSH(threshold=0.5, num_perm=128)

minhashes = {}

for name, text in docs.items():
    m = MinHash(num_perm=128)

    for word in text.split():
        m.update(word.encode())

    minhashes[name] = m
    lsh.insert(name, m)

for name, m in minhashes.items():
    print(name, "->", lsh.query(m))
# doc1 -> ['doc1', 'doc2', 'doc3']
# doc2 -> ['doc1', 'doc2', 'doc3']
# doc3 -> ['doc1', 'doc2', 'doc3']
# doc4 -> ['doc5', 'doc4']
# doc5 -> ['doc5', 'doc4']
```