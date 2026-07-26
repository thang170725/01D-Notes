Nếu datasketch giúp bạn lọc nhanh các ứng viên có khả năng giống nhau, thì RapidFuzz giúp bạn đánh giá chính xác hai chuỗi giống nhau bao nhiêu.
Đúng, nhưng RapidFuzz không phải là một thuật toán, mà là một thư viện (library).

Bên trong RapidFuzz có nhiều thuật toán để đo độ giống nhau của chuỗi.

Có thể hình dung:

datasketch là một thư viện
MinHash là một thuật toán
MinHashLSH là một thuật toán
rapidfuzz là một thư viện
ratio() là một thuật toán
partial_ratio() là một thuật toán
token_sort_ratio() là một thuật toán
token_set_ratio() là một thuật toán
...
Tại sao sau MinHash còn cần RapidFuzz?

Vì MinHash làm việc trên 5-gram (set).

RapidFuzz làm việc trên chuỗi gốc.

Ví dụ

Trang A

Nguyen Van A

Trang B

Nguyen Van A

RapidFuzz

from rapidfuzz import fuzz

fuzz.ratio(
    "Nguyen Van A",
    "Nguyen Van A"
)

Kết quả

100

Ví dụ 2

Nguyen Van A

và

Nguyen Van B

RapidFuzz

fuzz.ratio(...)

Ví dụ

91.6

Tức là

Hai chuỗi giống khoảng 91%.

MinHash thì sao?

MinHash cũng thấy

Nguyen Van A

Nguyen Van B

rất giống.

Ví dụ

0.95

Nhưng MinHash không biết chính xác ký tự nào khác.

RapidFuzz thì biết.

Ví dụ OCR

Trang A

So CCCD:
012345678

Trang B

So CCCD:
012345679

Chỉ khác

8
↓

9

RapidFuzz

99.x

Rất dễ phát hiện.

Nhưng nếu
Hello World

và

World Hello

RapidFuzz ratio()

có thể chỉ

50

vì thứ tự khác.

Trong khi

fuzz.token_sort_ratio(...)

sẽ

100

vì nó sắp xếp từ trước khi so sánh.

Đó là lý do RapidFuzz có nhiều thuật toán.

Các thuật toán phổ biến
1. ratio()

So sánh toàn bộ chuỗi.

fuzz.ratio(a, b)

Ví dụ

apple

apple

↓

100
2. partial_ratio()

Tìm xem chuỗi nhỏ có nằm trong chuỗi lớn không.

Hello World

với

World

ratio

≈62

partial_ratio

100
3. token_sort_ratio()

Đổi thứ tự từ rồi so.

John Smith
Smith John

↓

100
4. token_set_ratio()

Bỏ các từ trùng.

Ví dụ

Apple Apple Banana

với

Apple Banana

↓

100
Trong pipeline OCR của bạn

Hiện tại bạn đang làm

OCR
    ↓
Normalize
    ↓
Character 5-gram
    ↓
MinHash
    ↓
LSH
    ↓
RapidFuzz

Vai trò của từng bước là:

Thành phần	Vai trò
Character 5-gram	Chuyển văn bản thành tập đặc trưng.
MinHash	Tạo signature để ước lượng Jaccard nhanh.
MinHashLSH	Tìm nhanh các trang có khả năng giống nhau.
RapidFuzz	So sánh trực tiếp chuỗi văn bản để xác nhận kết quả cuối cùng.
Vì sao RapidFuzz thường đặt ở cuối?

Giả sử bạn có 100.000 trang.

So sánh RapidFuzz giữa mọi cặp sẽ rất tốn thời gian (O(n²) cặp).
MinHashLSH có thể lọc xuống chỉ còn vài trăm hoặc vài nghìn candidate.
Lúc đó mới dùng RapidFuzz để kiểm tra kỹ từng candidate.

Đây chính là lý do pipeline của bạn vừa nhanh vừa có độ chính xác cao:

100.000 trang
        │
        ▼
MinHashLSH
        │
        ▼
Chỉ còn vài trăm candidate
        │
        ▼
RapidFuzz xác nhận lần cuối

RapidFuzz đóng vai trò như bộ kiểm tra cuối cùng (verification step), còn MinHashLSH đóng vai trò bộ lọc ứng viên (candidate generation). Chúng bổ sung cho nhau chứ không thay thế nhau.
Trong pipeline của bạn:

OCR
↓
Normalize
↓
Character 5-gram
↓
MinHash
↓
LSH
↓
Candidate
↓
RapidFuzz
↓
Duplicate chắc chắn

RapidFuzz thường là bước cuối để xác nhận hai văn bản có thực sự giống nhau hay không.

1. RapidFuzz là gì?

RapidFuzz là thư viện bên thứ ba dùng để so khớp chuỗi (fuzzy string matching).

Cài đặt:

pip install rapidfuzz

Import:

from rapidfuzz import fuzz

hoặc

from rapidfuzz import process
2. Fuzzy Matching là gì?

Giả sử có hai chuỗi

hello world

và

helo world

Hai chuỗi này không giống hệt nhau.

Nếu dùng

s1 == s2

kết quả

False

Nhưng con người vẫn thấy chúng rất giống.

RapidFuzz sẽ trả về

95%

độ giống.

Đó gọi là Fuzzy Matching.

3. fuzz dùng để làm gì?

fuzz là module chứa các hàm tính độ giống giữa hai chuỗi.

Ví dụ

from rapidfuzz import fuzz

Sau đó dùng

fuzz.ratio(...)

hoặc

fuzz.partial_ratio(...)

...

4. fuzz.ratio()

Đây là hàm đơn giản và dùng nhiều nhất.

Cú pháp

score = fuzz.ratio(s1, s2)

Trả về

0 → 100
100 = giống hoàn toàn
0 = khác hoàn toàn
Ví dụ 1
from rapidfuzz import fuzz

s1 = "hello world"
s2 = "hello world"

print(fuzz.ratio(s1, s2))

Kết quả

100.0
Ví dụ 2
from rapidfuzz import fuzz

s1 = "hello world"
s2 = "helo world"

print(fuzz.ratio(s1, s2))

Giả sử

95.2
Ví dụ 3
from rapidfuzz import fuzz

print(
    fuzz.ratio(
        "apple",
        "banana"
    )
)

Giả sử

18.0
5. fuzz.partial_ratio()

Dùng khi

một chuỗi nằm bên trong chuỗi còn lại.

Ví dụ

Hello World

và

World

ratio

fuzz.ratio(
    "Hello World",
    "World"
)

Giả sử

62

Trong khi

fuzz.partial_ratio(
    "Hello World",
    "World"
)

cho

100

vì

World

xuất hiện nguyên vẹn.

6. fuzz.token_sort_ratio()

Dùng khi

hai câu có cùng từ

nhưng khác thứ tự.

Ví dụ

apple banana orange

và

orange apple banana

Nếu dùng

ratio()

có thể chỉ được

70

Nhưng

token_sort_ratio()

sẽ

tách từ
sắp xếp
so sánh

Ví dụ

from rapidfuzz import fuzz

s1 = "apple banana orange"
s2 = "orange apple banana"

print(fuzz.token_sort_ratio(s1, s2))

Kết quả

100
7. fuzz.token_set_ratio()

Đây là hàm rất hay.

Ví dụ

apple banana orange

và

banana orange

Chuỗi thứ hai chỉ thiếu một từ.

from rapidfuzz import fuzz

print(
    fuzz.token_set_ratio(
        "apple banana orange",
        "banana orange"
    )
)

Kết quả

100

vì

banana orange

đều có trong chuỗi đầu.

8. So sánh các hàm
Hàm	Dùng khi
ratio()	So sánh toàn bộ chuỗi
partial_ratio()	Một chuỗi là một phần của chuỗi kia
token_sort_ratio()	Khác thứ tự từ
token_set_ratio()	Thiếu hoặc dư một vài từ
9. process.extractOne()

RapidFuzz còn có module

from rapidfuzz import process

Giả sử

choices = [
    "apple",
    "banana",
    "orange",
    "pineapple"
]

Muốn tìm chuỗi giống nhất với

aple

Code

from rapidfuzz import process

choices = [
    "apple",
    "banana",
    "orange",
    "pineapple"
]

result = process.extractOne(
    "aple",
    choices
)

print(result)

Kết quả giả định

('apple', 88.5, 0)

Ý nghĩa

Chuỗi giống nhất

apple

Điểm

88.5

Index

0
10. Ví dụ trực quan

Giả sử OCR đọc ra

Trang 1

The quick brown fox jumps over the lazy dog

Trang 2

The quick brown fox jump over the lazy dog

So sánh

from rapidfuzz import fuzz

text1 = "The quick brown fox jumps over the lazy dog"

text2 = "The quick brown fox jump over the lazy dog"

print(fuzz.ratio(text1, text2))

Giả sử

98.7

=> Có thể coi là duplicate.

11. Ví dụ gần với bài toán của bạn

Sau khi OCR + normalize

Trang A

contract number 123456 customer nguyen van a

Trang B

contract number 123456 customer nguyen van a
score = fuzz.ratio(textA, textB)

Kết quả

100

Trang C

contract number 123456 customer nguyen van an

Kết quả

97

Trang D

invoice number 999999 company abc

Kết quả

25
12. RapidFuzz khác MinHash như thế nào?
MinHash	RapidFuzz
So sánh tập hợp token/shingle	So sánh chuỗi ký tự
Là thuật toán xấp xỉ Jaccard	Tính điểm giống chuỗi trực tiếp
Rất nhanh với dữ liệu lớn	Chậm hơn nếu phải so sánh mọi cặp
Kết hợp với LSH để tìm ứng viên	Dùng để xác nhận ứng viên

Ví dụ bạn có 100.000 trang OCR:

Nếu dùng RapidFuzz để so sánh tất cả các cặp, bạn sẽ phải thực hiện khoảng 5 tỷ phép so sánh (100000 × 99999 / 2), rất tốn thời gian.
Nếu dùng MinHash + LSH trước, bạn có thể chỉ còn vài nghìn hoặc vài chục nghìn cặp ứng viên cần kiểm tra.
Sau đó mới áp dụng RapidFuzz cho các ứng viên này để xác nhận.

Đó cũng chính là lý do pipeline MinHashLSH → RapidFuzz được sử dụng rất phổ biến trong các hệ thống phát hiện near-duplicate documents: MinHashLSH giúp lọc nhanh, còn RapidFuzz giúp đánh giá chính xác độ giống giữa các chuỗi văn bản.