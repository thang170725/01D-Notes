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
MinHash trong datasketch có thể khó hiểu lúc đầu vì bên trong nó dùng nhiều hàm băm (hash functions). Nhưng ý tưởng cốt lõi lại rất đơn giản.

Ý tưởng của MinHash

Giả sử có 2 văn bản.

Text A:
I love machine learning

Text B:
I love deep learning

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

A = {
    "i lov",
    " love",
    "love ",
    " mach",
    "chine",
    "learn"
}
Text B
B = {
    "i lov",
    " love",
    "love ",
    " deep",
    "learn"
}

Ta thấy

A

i lov
 love
love
 mach
chine
learn
B

i lov
 love
love
 deep
learn

Có khá nhiều phần giống nhau.

Nếu dùng Jaccard

Jaccard là

intersection / union

Intersection

i lov
 love
love
learn

= 4

Union

i lov
 love
love
 mach
chine
 deep
learn

= 7

Nên

Jaccard = 4 / 7
= 0.57
Vấn đề

Nếu mỗi trang OCR có

50.000

5-gram

thì

Muốn tính

intersection
union

rất tốn RAM và CPU.

MinHash làm gì?

Thay vì lưu

{
    "i lov",
    " love",
    "love ",
    ...
    50.000 gram
}

MinHash chỉ lưu

[1523,
9812,
352,
991,
7812,
...]

Ví dụ khoảng 128 số nguyên.

Tập 50.000 gram

↓

128 số

Đây gọi là signature.

Ví dụ cực dễ hiểu

Giả sử có tập

A = {
    "apple",
    "banana",
    "cat",
    "dog"
}

Ta tạo MinHash

from datasketch import MinHash

m = MinHash(num_perm=8)

for word in A:
    m.update(word.encode("utf8"))

Giả sử (ví dụ minh họa)

m.hashvalues

ra

[
    1834,
    912,
    7612,
    443,
    9101,
    81,
    291,
    5002
]

Đây chính là chữ ký (signature).

Bây giờ

B = {
    "apple",
    "banana",
    "dog",
    "fish"
}

Làm tương tự

m2 = MinHash(num_perm=8)

for word in B:
    m2.update(word.encode("utf8"))

Giả sử

[
    1834,
    912,
    7612,
    501,
    9200,
    81,
    315,
    4880
]

Nhìn hai signature

A

1834
912
7612
443
9101
81
291
5002

B

1834
912
7612
501
9200
81
315
4880

Có

1834
912
7612
81

giống nhau.

4/8

=

0.5

Rất gần với Jaccard thật.

Demo bằng datasketch
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

print(m1.jaccard(m2))

Ví dụ kết quả

0.7421875

Đây không phải Jaccard chính xác mà là ước lượng từ MinHash.

Jaccard thật
jaccard = len(text1 & text2) / len(text1 | text2)

print(jaccard)

Kết quả

0.6

Có thể thấy MinHash không cho kết quả đúng tuyệt đối, nhưng khá gần. Khi tăng num_perm (ví dụ 256 hoặc 512), kết quả thường sẽ tiến gần hơn tới Jaccard thật.

Tại sao gọi là MinHash?

Giả sử ta có một hàm hash đơn giản (chỉ để minh họa):

Từ	Hash
apple	45
banana	12
cat	81
dog	27

Với tập:

{
    "apple",
    "banana",
    "cat",
    "dog"
}

Các giá trị hash là:

45
12
81
27

MinHash đầu tiên sẽ lấy giá trị nhỏ nhất:

min = 12

Nếu dùng một hàm hash khác:

Từ	Hash #2
apple	300
banana	100
cat	50
dog	70

Giá trị nhỏ nhất là:

50

Tiếp tục với nhiều hàm hash khác, ta thu được:

[12, 50, 91, 7, 130, 42, ...]

Đó chính là MinHash signature.

Thực tế, datasketch không dùng các bảng hash như trên mà mô phỏng hàng trăm phép hoán vị (permutations), nhưng ý tưởng vẫn là: mỗi phép hoán vị chỉ giữ lại giá trị hash nhỏ nhất.

Tóm tắt luồng hoạt động
Text
      ↓
Character 5-gram
      ↓
Set các 5-gram
      ↓
MinHash
      ↓
Signature (128 số nguyên)
      ↓
So sánh signature
      ↓
Ước lượng Jaccard

Điểm mạnh của MinHash là bạn không cần lưu hoặc so sánh hàng chục nghìn 5-gram của mỗi tài liệu. Chỉ cần một signature nhỏ (thường 128 hoặc 256 số nguyên) là đã có thể ước lượng độ tương đồng rất nhanh, đặc biệt khi kết hợp với MinHashLSH để tìm các cặp tài liệu giống nhau trong tập dữ liệu lớn.
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
Đây chính là chỗ dễ gây nhầm nhất. Thực ra MinHashLSH không dùng trước MinHash.

Thứ tự đúng là:

Text
   ↓
5-gram
   ↓
MinHash  ← bắt buộc
   ↓
MinHashLSH
   ↓
Candidate
   ↓
MinHash.jaccard()
   ↓
RapidFuzz

LSH không thể hoạt động nếu chưa có MinHash.

Tại sao?

Giả sử có 3 trang

Page1: Nguyễn Văn A

Page2: Nguyễn Văn A

Page3: Hóa đơn điện
Bước 1: Tạo MinHash
m1 = MinHash(...)
m2 = MinHash(...)
m3 = MinHash(...)

Lúc này (ví dụ minh họa)

Page1
[12, 41, 92, 15, 81, ...]

Page2
[12, 41, 92, 16, 81, ...]

Page3
[91, 55, 10, 74, 63, ...]

Đây là signature.

Bước 2: Đưa vào LSH
lsh.insert("page1", m1)
lsh.insert("page2", m2)
lsh.insert("page3", m3)

Điều quan trọng là:

LSH không đọc text.

Nó chỉ đọc

[12,41,92,15,81...]

[12,41,92,16,81...]

[91,55,10,74,63...]
LSH làm gì?

Giả sử signature có 128 số.

LSH chia thành nhiều band.

Ví dụ đơn giản chỉ có 8 số:

12 41 | 92 15 | 81 20 | 11 66

Chia thành 4 band

Band1
12 41

Band2
92 15

Band3
81 20

Band4
11 66

Page2

12 41 | 92 16 | 81 20 | 15 77

Band

Band1
12 41

Band2
92 16

Band3
81 20

Band4
15 77

LSH sẽ tạo bảng băm.

Ví dụ

Band1

12 41
↓

bucket A
Page1
↓

bucket A

Page2

12 41
↓

bucket A

Nó thấy

Ơ

bucket A đã có Page1.

Đánh dấu

Page1
Page2

→ Có khả năng giống

Page3

91 55

↓

bucket X

Không trùng bucket.

LSH bỏ qua.

Tức là LSH không biết "giống"

Nó chỉ biết

Hai signature có nhiều đoạn giống nhau nên có khả năng giống.

Ví dụ

Page1

12 41
92 15
81 20
11 66
Page2

12 41
92 16
81 20
15 77

Có

Band1 giống

Band3 giống

=> Candidate.

Sau đó mới dùng MinHash

LSH trả về

candidate = lsh.query(m1)

print(candidate)

Ví dụ

['page2']

Lúc này mới làm

m1.jaccard(m2)

Ví dụ

0.98

=> Duplicate.

Tại sao phải tách ra?

Vì nếu có

100.000 page

thì:

Không dùng LSH
Page1

↓

so với

99.999 page
Có LSH
Page1

↓

LSH

↓

Page18
Page702
Page19999

Chỉ cần so với 3 trang.

Một câu tóm tắt rất dễ nhớ
MinHash trả lời câu hỏi: "Hai tài liệu này giống nhau bao nhiêu?"
MinHashLSH trả lời câu hỏi: "Trong hàng nghìn tài liệu, tài liệu nào đáng để mang ra so sánh?"

Nói cách khác:

MinHash = thước đo độ giống.
LSH = công cụ tìm kiếm nhanh các ứng viên.

LSH không hề tự tính độ tương đồng từ văn bản; nó chỉ lập chỉ mục trên MinHash signature đã được tạo trước đó. Vì vậy, trong datasketch, bạn luôn phải tạo MinHash trước rồi mới insert() vào MinHashLSH.
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