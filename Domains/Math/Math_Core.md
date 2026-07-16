phương pháp Fenwick Tree là gì, lấy ví dụ bằng python cho tôi
Fenwick Tree (Binary Indexed Tree) là gì?

Fenwick Tree (BIT - Binary Indexed Tree) là một cấu trúc dữ liệu dùng để:

Cập nhật giá trị của một phần tử trong mảng.
Tính tổng tiền tố (Prefix Sum) rất nhanh.

Thay vì:

Update: O(1)
Query tổng từ 0 -> i: O(n)

thì Fenwick Tree cho phép:

Update: O(log n)
Query Prefix Sum: O(log n)

Đây là cấu trúc dữ liệu rất phổ biến trong các bài toán Competitive Programming và phỏng vấn.

Ý tưởng

Giả sử có mảng

Index: 1 2 3 4 5 6 7 8

Value:
      2 1 3 5 4 6 7 8

Fenwick Tree sẽ không lưu trực tiếp từng phần tử, mà lưu tổng của các đoạn.

Ví dụ:

tree[1] = sum(1)

tree[2] = sum(1..2)

tree[3] = sum(3)

tree[4] = sum(1..4)

tree[5] = sum(5)

tree[6] = sum(5..6)

tree[7] = sum(7)

tree[8] = sum(1..8)

Nhờ vậy mỗi lần cộng hoặc truy vấn chỉ cần đi qua khoảng log n node.

Điều kỳ diệu: lowbit

Fenwick Tree hoạt động nhờ:

x & (-x)

Đây gọi là lowbit.

Ví dụ

x	Binary	lowbit
1	0001	1
2	0010	2
3	0011	1
4	0100	4
5	0101	1
6	0110	2
7	0111	1
8	1000	8

Ví dụ

6 = 110
-6 = 010 (two's complement)

110
010
---
010 = 2

Vậy

lowbit(6)=2
Update hoạt động như nào?

Muốn cộng thêm delta tại vị trí i

while i <= n:
    tree[i] += delta
    i += i & -i

Ví dụ update index = 5

5
↓

5 + lowbit(5)=6

↓

6 + lowbit(6)=8

↓

8 + lowbit(8)=16

Ta cập nhật

5
6
8
16
Query Prefix Sum

Muốn tính

sum(1...i)

Ta làm

while i > 0:
    ans += tree[i]
    i -= i & -i

Ví dụ

sum(7)

↓

tree[7]

↓

tree[6]

↓

tree[4]

↓

0
Cài đặt Python
class FenwickTree:
    def __init__(self, n):
        self.n = n
        self.tree = [0] * (n + 1)

    def update(self, index, delta):
        while index <= self.n:
            self.tree[index] += delta
            index += index & -index

    def query(self, index):
        s = 0
        while index > 0:
            s += self.tree[index]
            index -= index & -index
        return s

    def range_query(self, left, right):
        return self.query(right) - self.query(left - 1)
Ví dụ

Giả sử

A = [2,1,3,5,4]

Ta xây dựng Fenwick Tree

arr = [2,1,3,5,4]

ft = FenwickTree(len(arr))

for i, x in enumerate(arr, start=1):
    ft.update(i, x)
Tổng từ 1 → 5
print(ft.query(5))

Kết quả

15

vì

2+1+3+5+4=15
Tổng từ 2 → 4
print(ft.range_query(2,4))

Kết quả

9

vì

1+3+5=9
Update

Giả sử

A[3] += 10
ft.update(3, 10)

Mảng trở thành

2 1 13 5 4

Bây giờ

print(ft.query(5))

Kết quả

25
Minh họa trực quan

Giả sử có 8 phần tử.

Index:

1 2 3 4 5 6 7 8

Mỗi node lưu:

tree[1] = [1]

tree[2] = [1 2]

tree[3] = [3]

tree[4] = [1 2 3 4]

tree[5] = [5]

tree[6] = [5 6]

tree[7] = [7]

tree[8] = [1 2 3 4 5 6 7 8]

Nếu cần

sum(7)

thì chỉ cần lấy

tree[7]
+
tree[6]
+
tree[4]

thay vì cộng cả 7 phần tử.

Khi nào nên dùng Fenwick Tree?

Fenwick Tree phù hợp khi cần xử lý nhiều thao tác trên mảng:

✅ Cập nhật một phần tử (Point Update)
✅ Tính tổng tiền tố (Prefix Sum)
✅ Tính tổng trên đoạn [L, R] (thông qua prefix(R) - prefix(L-1))
✅ Đếm số lượng, tần suất (frequency counting)
✅ Đếm số nghịch thế (Inversion Count)
✅ Coordinate Compression kết hợp Fenwick Tree
Fenwick Tree vs Segment Tree
Tiêu chí	Fenwick Tree	Segment Tree
Cài đặt	Rất đơn giản	Phức tạp hơn
Bộ nhớ	O(n)	O(4n)
Prefix Sum	O(log n)	O(log n)
Range Sum	O(log n)	O(log n)
Point Update	O(log n)	O(log n)
Range Update	Khó (cần biến thể)	Dễ với Lazy Propagation
Hỗ trợ nhiều phép toán (min, max, gcd, ...)	Hạn chế	Linh hoạt

Kết luận: Nếu bài toán chỉ cần cập nhật một phần tử và truy vấn tổng trên đoạn, Fenwick Tree thường là lựa chọn tối ưu vì mã ngắn gọn, ít tốn bộ nhớ và dễ triển khai. Nếu cần các phép toán phức tạp hơn hoặc cập nhật trên cả một đoạn, Segment Tree sẽ phù hợp hơn.
không hiểu nói dễ hiểu hơn cho tôi, bị nhiều thông tin quá
Được, mình sẽ giải thích theo cách trực quan nhất, bỏ hết các công thức phức tạp.

Bài toán

Giả sử bạn có mảng:

Index:  1  2  3  4  5
Value:  2  1  3  5  4

Bạn cần thực hiện rất nhiều câu hỏi kiểu:

Tổng từ phần tử 1 đến phần tử i là bao nhiêu?

Ví dụ:

sum(3)

= 2 + 1 + 3
= 6

hay

sum(5)

= 2 + 1 + 3 + 5 + 4
= 15
Cách bình thường

Mỗi lần hỏi:

sum(5)

bạn sẽ cộng

2
+
1
+
3
+
5
+
4

=> phải đi qua 5 số.

Nếu có 100.000 số thì phải cộng 100.000 lần.

Rất chậm.

Ý tưởng của Fenwick Tree

Thay vì mỗi lần cộng lại từ đầu...

Ta lưu sẵn một số tổng.

Ví dụ:

tree[1] = 2

tree[2] = 2+1 = 3

tree[4] = 2+1+3+5 = 11

Nó giống như bạn ghi nhớ sẵn các tổng để sau này dùng lại.

Ví dụ dễ hiểu

Giả sử cần tính

sum(4)

Thay vì

2
+
1
+
3
+
5

Fenwick Tree biết rằng

tree[4]

đã bằng

11

=> lấy luôn.

Ví dụ khác

Muốn tính

sum(6)

Giả sử mảng là

2 1 3 5 4 6

Fenwick Tree không cộng

2+1+3+5+4+6

Nó lấy

tree[6]
+
tree[4]

vì

tree[6]

đã chứa

4+6

và

tree[4]

đã chứa

2+1+3+5

=> Tổng là

(4+6)
+
(2+1+3+5)

Không cần cộng từng số nữa.

Nhưng tại sao biết lấy tree[6] rồi tree[4]?

Đây là phần duy nhất cần nhớ.

Fenwick Tree dùng quy tắc:

i -= i & -i

Ví dụ

i = 6

↓

6

↓

4

↓

0

Nghĩa là

sum(6)

=

tree[6]
+
tree[4]

Nếu

i = 7

thì

7

↓

6

↓

4

↓

0

nên

sum(7)

=

tree[7]
+
tree[6]
+
tree[4]
Khi cập nhật thì sao?

Giả sử

A[3] = 3

đổi thành

A[3] = 13

tức tăng thêm

+10

Fenwick Tree chỉ cập nhật các ô bị ảnh hưởng:

3

↓

4

↓

8

↓

16

Nếu mảng chỉ có 5 phần tử thì chỉ cần cập nhật:

tree[3]

tree[4]

Không phải tính lại toàn bộ cây.

Bạn chỉ cần nhớ 2 hàm
Cập nhật
while i <= n:
    tree[i] += delta
    i += i & -i

Đi lên trên.

Tính tổng
while i > 0:
    ans += tree[i]
    i -= i & -i

Đi lùi về gốc.

Có thể hình dung như thế này

Fenwick Tree giống như một kế toán.

Thay vì mỗi lần sếp hỏi:

"Doanh thu từ đầu tháng đến hôm nay là bao nhiêu?"

Kế toán không cộng lại từng hóa đơn.

Họ đã ghi sẵn:

Tổng tuần 1
Tổng tuần 2
Tổng vài ngày cuối

Rồi ghép các tổng đó lại để trả lời rất nhanh.

👉 Mình có thể vẽ hình minh họa (ASCII) cho thấy tree[] lưu những đoạn nào (ví dụ tree[6] vì sao lại lưu tổng của phần tử 5 và 6), đây là cách mà hầu hết mọi người sẽ "ngộ" Fenwick Tree chỉ sau 5 phút.
Đây chính là chỗ khiến hầu hết mọi người lần đầu học Fenwick Tree bị nhầm. Thực ra tree[i] KHÔNG phải là tổng từ 1 đến i.

Nếu tree[i] là tổng từ 1 đến i thì đã không cần Fenwick Tree nữa.

Ta lấy ví dụ
Index: 1 2 3 4 5 6 7 8

Value: 2 1 3 5 4 6 7 8

Fenwick Tree lưu như sau:

tree[i]	Lưu những phần tử nào
tree[1]	1
tree[2]	1 2
tree[3]	3
tree[4]	1 2 3 4
tree[5]	5
tree[6]	5 6
tree[7]	7
tree[8]	1 2 3 4 5 6 7 8

Nếu thay bằng giá trị thật:

tree[1] = 2

tree[2] = 2+1 = 3

tree[3] = 3

tree[4] = 2+1+3+5 = 11

tree[5] = 4

tree[6] = 4+6 = 10

tree[7] = 7

tree[8] = 2+1+3+5+4+6+7+8
Tại sao tree[6] chỉ chứa phần tử 5 và 6?

Đây là quy tắc của Fenwick Tree.

Nó dựa vào:

lowbit(i) = i & -i

Ví dụ

6 = 110
lowbit(6)=2

Nghĩa là

tree[6]

luôn lưu 2 phần tử cuối kết thúc tại vị trí 6

5 6

Ví dụ khác

4 = 100
lowbit(4)=4

nên

tree[4]

lưu 4 phần tử cuối kết thúc tại vị trí 4

1 2 3 4

Ví dụ

5 = 101
lowbit(5)=1

nên

tree[5]

chỉ lưu

5

Ví dụ

8 = 1000
lowbit(8)=8

nên

tree[8]

lưu

1 2 3 4 5 6 7 8
Có công thức tổng quát

tree[i] lưu đoạn:

[i - lowbit(i) + 1 ... i]

Ví dụ

tree[6]
lowbit(6)=2

6-2+1=5

nên

tree[6]
=
5..6
tree[4]
lowbit(4)=4

4-4+1=1

nên

tree[4]
=
1..4
tree[12]
12 = 1100

lowbit(12)=4
12-4+1=9

nên

tree[12]

=

9..12
Vì sao cộng tree[6] + tree[4] lại ra tổng 1..6?

Muốn tính:

1 2 3 4 5 6

Fenwick Tree chia thành các đoạn không bị chồng lặp:

tree[6]
=
5 6

tree[4]
=
1 2 3 4

Ghép lại:

1 2 3 4
+
5 6

đúng bằng

1 2 3 4 5 6
Hình minh họa
Mảng

1 2 3 4 5 6
|-----| |--|
tree4   tree6

Hai đoạn này ghép lại đúng thành:

1 2 3 4 5 6

Mẹo nhớ quan trọng nhất về Fenwick Tree:

❌ Sai: tree[i] là tổng từ 1..i.

✅ Đúng: tree[i] là tổng của một đoạn kết thúc tại i, và độ dài đoạn đó bằng lowbit(i).

Khi bạn hiểu được câu này, khoảng 80% Fenwick Tree đã trở nên dễ hiểu. Bước tiếp theo chỉ còn là hiểu vì sao khi truy vấn lại dùng i -= lowbit(i) và khi cập nhật lại dùng i += lowbit(i).
tại sao lại thế, không hiểu lắm, sao phải lưu như thế tôi thấy không có quy luật nào cả
Đây là câu hỏi rất hay. Thực ra Fenwick Tree không phải là một ý tưởng "tự nhiên", mà là một mẹo toán học rất thông minh. Nếu chỉ nhìn bảng tree[] thì đúng là trông rất "ngẫu nhiên".

Đừng học thuộc bảng đó. Hãy hiểu vì sao người ta thiết kế như vậy.

Hãy tưởng tượng bạn là người thiết kế

Bạn có mảng:

2 1 3 5 4 6 7 8

Bạn muốn trả lời nhanh câu hỏi:

Tổng từ 1 đến i là bao nhiêu?

Cách 1: Không lưu gì

Muốn tính sum(6) thì:

2+1+3+5+4+6

=> Cộng 6 lần.

Cách 2: Lưu tổng từ đầu

Bạn nghĩ:

prefix[1] = 2
prefix[2] = 3
prefix[3] = 6
prefix[4] = 11
prefix[5] = 15
prefix[6] = 21

Quá tuyệt!

Muốn tính sum(6) chỉ cần

prefix[6]
Nhưng có vấn đề

Giả sử

A[3] += 10

Mọi tổng phía sau đều sai.

prefix[3]
prefix[4]
prefix[5]
prefix[6]
prefix[7]
prefix[8]

đều phải tính lại.

Nếu có 1 triệu phần tử thì sao?

👉 Rất chậm.

Fenwick Tree ra đời để giải quyết điều này

Người ta nghĩ:

"Đừng lưu tổng từ đầu nữa."

"Hãy chia thành nhiều đoạn nhỏ."

Ví dụ

1
12
3
1234
5
56
7
12345678

Bạn thấy hơi kỳ đúng không?

Nhưng hãy nhìn theo đoạn.

tree[1] = đoạn 1

tree[2] = đoạn 1-2

tree[3] = đoạn 3

tree[4] = đoạn 1-4

tree[5] = đoạn 5

tree[6] = đoạn 5-6

tree[7] = đoạn 7

tree[8] = đoạn 1-8
Vì sao lại chia như vậy?

Hãy nhìn số nhị phân.

1 = 001
2 = 010
4 = 100
8 =1000

Đây đều là lũy thừa của 2.

Fenwick Tree thích chia đoạn có kích thước

1
2
4
8
16

vì máy tính xử lý rất nhanh.

Ví dụ

tree[6]

số 6 có

110

bit cuối là

10

tức bằng

2

nên

tree[6]

lưu 2 phần tử cuối

5 6

Ví dụ

tree[12]

12

1100

bit cuối

100

=

4

nên lưu

9 10 11 12
Tại sao phải là 1,2,4,8?

Đây mới là điều quan trọng.

Nếu mỗi node đều lưu đoạn có độ dài là lũy thừa của 2 thì:

Khi update, chỉ vài đoạn bị ảnh hưởng.
Khi query, chỉ cần ghép vài đoạn là đủ.

Ví dụ muốn lấy

1..13

Fenwick tự chia thành

13
+
9..12
+
1..8

Không bị trùng.

Không bị thiếu.

Hình dung như xếp Lego

Giả sử bạn có thanh Lego

□□□□□□□□

Thay vì luôn lấy từng viên

■
■
■
■

bạn chuẩn bị sẵn

1 ô

2 ô

4 ô

8 ô

Khi cần ghép thành 13 ô

8
+
4
+
1

là xong.

Fenwick Tree cũng làm đúng điều đó.

Nó chia thành các "khối" kích thước

1

2

4

8

16

rồi ghép lại.

Điều bạn đang thắc mắc nhất

"Tại sao tree[6] phải là 5..6 mà không phải 1..6?"

Câu trả lời là:

Không có lý do toán học bắt buộc. Đây là cách thiết kế để đảm bảo rằng:

mọi vị trí chỉ ảnh hưởng đến khoảng log(n) node khi cập nhật;
mọi truy vấn tổng tiền tố có thể ghép từ khoảng log(n) đoạn;
các đoạn không chồng lặp và luôn phủ kín phần cần tính.

Nếu lưu 1..6, thì khi cập nhật phần tử thứ 2, bạn phải sửa gần như tất cả các tổng phía sau. Fenwick Tree tránh điều đó bằng cách chia thành các đoạn có kích thước là lũy thừa của 2.

👉 Theo mình, cách dễ "vỡ ra" nhất là tự xây dựng Fenwick Tree từ đầu trên mảng 8 phần tử. Mình sẽ không dùng công thức lowbit ngay, mà sẽ chỉ cho bạn tại sao tree[6] buộc phải là 5..6 nếu muốn việc cập nhật và truy vấn đều chỉ mất O(log n). Khi nhìn từng bước, quy luật sẽ trở nên rất tự nhiên.
đấy là bạn đang lấy ví dụ mảng 8 số nếu khác giả sử mảng dài hơn thi như thế nào quy luật như nào, tree như nào
Đúng! Bạn đang hỏi đúng chỗ cốt lõi của Fenwick Tree.

Nếu mảng không phải 8 phần tử mà là 100, 1000 hay 1 triệu phần tử thì quy luật là gì?

Câu trả lời là:

Quy luật hoàn toàn không phụ thuộc vào độ dài mảng.

Nó chỉ phụ thuộc vào chỉ số i.

Quy luật duy nhất

Mỗi tree[i] lưu một đoạn có độ dài:

lowbit(i)

hay

i & -i

Đoạn đó luôn kết thúc tại i.

Công thức:

tree[i]

lưu

[i-lowbit(i)+1 ... i]

Đây là quy luật của mọi Fenwick Tree.

Ví dụ với mảng 16 phần tử

Ta tính từng cái.

tree[1]
lowbit(1)=1

=> lưu

1
tree[2]
lowbit(2)=2

=> lưu

1 2
tree[3]
lowbit(3)=1

=> lưu

3
tree[4]
lowbit(4)=4

=> lưu

1 2 3 4
tree[5]
lowbit(5)=1

=>

5
tree[6]
lowbit(6)=2

=>

5 6
tree[7]
lowbit(7)=1

=>

7
tree[8]
lowbit(8)=8

=>

1 2 3 4 5 6 7 8
tree[9]
lowbit(9)=1

=>

9
tree[10]
lowbit(10)=2

=>

9 10
tree[11]
lowbit(11)=1

=>

11
tree[12]
lowbit(12)=4

=>

9 10 11 12
tree[13]
lowbit(13)=1

=>

13
tree[14]
lowbit(14)=2

=>

13 14
tree[15]
lowbit(15)=1

=>

15
tree[16]
lowbit(16)=16

=>

1 ... 16
Bạn sẽ thấy quy luật
tree[1]  -> 1

tree[2]  -> 1 2

tree[3]  -> 3

tree[4]  -> 1 2 3 4

tree[5]  -> 5

tree[6]  -> 5 6

tree[7]  -> 7

tree[8]  -> 1..8

tree[9]  -> 9

tree[10] -> 9 10

tree[11] -> 11

tree[12] -> 9..12

tree[13] -> 13

tree[14] -> 13 14

tree[15] -> 15

tree[16] -> 1..16

Có thấy giống gì không?

Nó giống các khối:

1

12

3

1234

5

56

7

12345678

9

910

11

9-12

13

13-14

15

1-16
Nếu có 1000 phần tử thì sao?

Ví dụ

tree[1000]

Ta không cần biết mảng dài bao nhiêu.

Chỉ cần tính

lowbit(1000)

1000 ở hệ nhị phân là

1111101000

bit 1 cuối cùng là

1000

=

8

Nên

tree[1000]

luôn lưu

993...1000

vì

1000-8+1=993
Ví dụ nữa
tree[100]

100

1100100

lowbit

100

=

4

nên

tree[100]

lưu

97 98 99 100
Điều quan trọng nhất

Bạn không bao giờ tạo thủ công những đoạn này.

Trong code, chỉ có đúng một dòng:

lowbit = i & -i

Sau đó tính:

left = i - lowbit + 1
right = i

Là biết tree[i] đại diện cho đoạn nào.

Mình nghĩ bạn còn đang thiếu một mảnh ghép

Có lẽ bạn đang thắc mắc:

"Tại sao i & -i lại đúng là độ dài đoạn?"

Đó là nguồn gốc của toàn bộ Fenwick Tree. Nếu hiểu được vì sao phép toán bit này sinh ra các đoạn 1, 2, 4, 8, ..., thì bạn sẽ không cần học thuộc bất kỳ bảng nào nữa.

Mình có thể giải thích i & -i bằng hình nhị phân từng bước (không cần kiến thức bit nâng cao), và thường sau phần đó thì Fenwick Tree sẽ trở nên rất dễ hiểu.
# số chẵn và số lẻ
**Công thức tổng n số lẻ đầu tiên**
```bash
s = n**2

chứng minh:
    S=(2⋅1−1)+(2⋅2−1)+⋯+(2⋅n−1)
    S=2(1+2+⋯+n)−n
    S=2*(n(n+1))/2 − n
     =n(n+1)−n
     =n**2
```
**Công thức tổng n số chẵn đầu tiên**
```bash
s = n*(n+1)

chứng minh:
    s = 2 + 4 + 6 + ... + 2n
      = 2*(1+2+...+n) = 2*(n(n+1))/2 = n*(n+1)
```
# DFS
```python
from collections import defaultdict

class DFS:
    def __init__(self):
        self.data = defaultdict(list)
        self.tree_data()

    def tree_data(self):
        # Khởi tạo dữ liệu cây dạng dictionary (adjacency list)
        self.data['A'] = ['B', 'C', 'D']
        self.data['B'] = ['M', 'N']
        self.data['C'] = ['L']
        self.data['D'] = ['O', 'P']
        self.data['M'] = ['X', 'Y']
        self.data['N'] = ['U', 'V']
        self.data['O'] = ['I', 'J']
        self.data['Y'] = ['R', 'S']
        self.data['V'] = ['G', 'H']
        return self.data

    def dfs_path(self, start, end, path=None):
        """
        Tìm một đường từ start đến end bằng DFS (đệ quy).
        Trả về list các nút theo đường tìm được hoặc None nếu không tìm thấy.
        """
        if path is None:
            path = []

        # tạo bản sao đường đi hiện tại + thêm nút start
        path = path + [start]

        if start == end:
            return path

        # Nếu start không tồn tại trong đồ thị (không có kề) -> None
        if start not in self.data:
            return None

        for neighbor in self.data[start]:
            if neighbor not in path:  # tránh vòng lặp
                new_path = self.dfs_path(neighbor, end, path)
                print(neighbor, new_path)
                if new_path:
                    return new_path

        return None
    
if __name__ == '__main__':
    dfs = DFS()

    p = dfs.dfs_path('A', 'R')
    print("DFS path:", " -> ".join(p) if p else "No path")
```
# LeetCode 1038 - Medium
```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def bstToGst(self, root):
        """
        :type root: Optional[TreeNode]
        :rtype: Optional[TreeNode]
        """
        self.sum = 0

        def dfs(node):
            if not node:
                return

            # đi sang phải
            dfs(node.right)

            # xử lý node
            self.sum += node.val
            node.val = self.sum

            # di sang trái
            dfs(node.left)
        
        dfs(root)
        return root
```
- [Leetcode - 2181](#leetcode---2181)
---
# Leetcode - 2181
**Ex1**
```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution(object):
    def mergeNodes(self, head):
        """
        :type head: Optional[ListNode]
        :rtype: Optional[ListNode]
        """
        new_head = ListNode(0)
        tail = new_head
        temp = head.next
        s = 0
        while temp:
            if temp.val == 0:
                new_node = ListNode(val=s)
                tail.next = new_node
                tail = new_node
                s = 0
            else:
                s += temp.val
            temp = temp.next
        
        return new_head.next
```
**Ex2**
```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution(object):
    def mergeNodes(self, head):
        """
        :type head: Optional[ListNode]
        :rtype: Optional[ListNode]
        """
        cur = head
        temp = head.next
        s = 0

        while temp:
            if temp.val == 0:
                cur = cur.next
                cur.val = s
                s = 0
            else:
                s += temp.val
            temp = temp.next
        
        cur.next = None
        return head.next
```