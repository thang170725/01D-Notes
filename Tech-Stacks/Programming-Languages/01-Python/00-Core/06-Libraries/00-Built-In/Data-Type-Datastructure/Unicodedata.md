- [unicodedata là thư viện có sẵn (built-in) của Python, dùng để xử lý và chuẩn hóa ký tự Unicode.](#unicodedata-là-thư-viện-có-sẵn-built-in-của-python-dùng-để-xử-lý-và-chuẩn-hóa-ký-tự-unicode)
---
# Unicodedata Introduction (dùng để xử lý và chuẩn hóa ký tự Unicode)
```bash
là thư viện có sẵn (built-in) của Python không cần tải.
Mục đích là chuẩn hóa chuỗi trước khi mapping nhãn, tránh trường hợp hai chuỗi nhìn giống nhau nhưng Python lại coi là khác nhau.
```
## Unicode là gì? Tại sao cần unicodedata?
```bash
Bạn nhìn hai chuỗi sau:
    - s1 = "ế"
    - s2 = "ế"
-> Trên màn hình, chúng trông giống hệt nhau. Nhưng bên trong máy tính, chúng có thể được biểu diễn khác nhau:
    - s1: Một ký tự ế duy nhất.
    - s2: Ký tự e + dấu mũ + dấu sắc.

Python có thể coi hai chuỗi này là khác nhau:
    print(s1 == s2) # False (nếu chúng được mã hóa theo hai dạng khác nhau)

-> Đây chính là lý do cần Unicode normalization.
```
# normalize() (Chuẩn hóa Unicode)
**Syn**
```bash
unicodedata.normalize(form, text)

- Input:
    + form: Kiểu chuẩn hóa Unicode.
        - NFC: Ghép ký tự thành dạng chuẩn dựng sẵn nếu có
        - NFD: Tách ký tự thành ký tự cơ sở và dấu kết hợp
        - NFKC: Chuẩn hóa tương thích và ghép ký tự
        - NFKD: Chuẩn hóa tương thích và tách ký tự
    + text: Chuỗi cần chuẩn hóa.
```
**Ex1: NFC**
```python
import unicodedata

s = "e\u0302\u0301"
result = unicodedata.normalize("NFC", s)
print(result) # ế

# Ở đây:
# - e: Chữ e.
# - \u0302: Dấu mũ.
# - \u0301: Dấu sắc.
# NFC cố gắng ghép chúng thành ký tự ế.
```
# category() (Xác định loại ký tự)
**Syn**
```bash
unicodedata.category(character)
```
**Ex**
```python
import unicodedata

print(unicodedata.category("A")) # Lu: Chữ cái viết hoa
print(unicodedata.category("a")) # Ll: Chữ cái viết thường
print(unicodedata.category("1") ) # Nd: Chữ số thập phân 
print(unicodedata.category(" ")) # Zs: Khoảng trắng
print(unicodedata.category("!")) # Po: Dấu câu
```
# combining() (Kiểm tra dấu kết hợp)
**Syn**
```bash
unicodedata.combining(character)

- Output: Hàm trả về giá trị số thể hiện combining class của ký tự.
```
**Ex**
```python
import unicodedata

print(unicodedata.combining("e")) # 0
print(unicodedata.combining("\u0301")) # 230
```
# name() (Lấy tên Unicode của ký tự)
**Syn**
```bash
unicodedata.name(character)



Ví dụ:
import unicodedataprint(unicodedata.name("A"))# LATIN CAPITAL LETTER Aprint(unicodedata.name("ế"))# LATIN SMALL LETTER E WITH CIRCUMFLEX AND ACUTEprint(unicodedata.name("中"))# CJK UNIFIED IDEOGRAPH-4E2D



Ứng dụng: Debug các ký tự lạ trong dữ liệu, tìm hiểu ký tự nào đang xuất hiện trong chuỗi.
2.5. lookup() – Tìm ký tự theo tên Unicode
Đây là hàm ngược với name().

Cú pháp:
unicodedata.lookup(name)



Ví dụ:
import unicodedataresult = unicodedata.lookup("LATIN SMALL LETTER A")print(result)# a



Một ví dụ khác:
result = unicodedata.lookup("EURO SIGN")print(result)# €



Ứng dụng: Tạo ký tự đặc biệt dựa trên tên Unicode.
2.6. decimal() – Lấy giá trị số của chữ số
Cú pháp:
unicodedata.decimal(character)



Ví dụ:
import unicodedataprint(unicodedata.decimal("5"))# 5print(unicodedata.decimal("٣"))# 3



Hàm này hỗ trợ các chữ số thập phân thuộc nhiều hệ chữ viết khác nhau.

Ngoài ra còn có:
unicodedata.digit(character)unicodedata.numeric(character)



- digit(): Lấy giá trị chữ số, bao gồm một số ký hiệu số đặc biệt.
- numeric(): Lấy giá trị số rộng hơn, ví dụ phân số.
Ví dụ:
print(unicodedata.digit("²"))# 2print(unicodedata.numeric("½"))# 0.5



3. Bảng tổng hợp các hàm
Hàm	Chức năng	Mức độ cần biết
normalize()	Chuẩn hóa Unicode	Rất quan trọng
category()	Xác định loại ký tự	Quan trọng
combining()	Kiểm tra dấu kết hợp	Nâng cao
name()	Lấy tên Unicode	Hữu ích khi debug
lookup()	Tìm ký tự theo tên	Hữu ích
decimal()	Lấy giá trị chữ số	Thường dùng
digit()	Lấy giá trị chữ số/ký hiệu số	Ít dùng
numeric()	Lấy giá trị số tổng quát	Ít dùng
east_asian_width()	Xác định độ rộng ký tự Đông Á	Chuyên biệt
bidirectional()	Xác định hướng hiển thị ký tự	Chuyên biệt

4. Áp dụng trực tiếp vào code xử lý email của bạn
Quay lại đoạn code ban đầu:
def _norm(s) -> str:    """Chuẩn hóa để so khớp: NFC, bỏ khoảng trắng thừa, lowercase."""    s = unicodedata.normalize("NFC", str(s or ""))    return " ".join(s.split()).casefold()



Hàm này thực hiện 3 bước:
Bước 1: Chuẩn hóa Unicode bằng NFC
s = unicodedata.normalize("NFC", str(s or ""))



Đưa các cách biểu diễn Unicode tương đương về cùng một dạng.


Bước 2: Xử lý khoảng trắng
s = " ".join(s.split())



Xóa khoảng trắng đầu cuối và gộp nhiều khoảng trắng liên tiếp thành một.


Bước 3: Chuẩn hóa chữ hoa/thường
s = s.casefold()



Chuyển chữ về dạng phù hợp để so sánh không phân biệt hoa thường.


Ví dụ thực tế:
s1 = "  KHIẾU NẠI   DỊCH VỤ "s2 = "khiếu nại dịch vụ"print(_norm(s1))# khiếu nại dịch vụprint(_norm(s2))# khiếu nại dịch vụprint(_norm(s1) == _norm(s2))# True



Nhờ vậy, khi mapping:
key = (    _norm(row.get("loai_yeu_cau")),    _norm(row.get("yeu_cau")))label = mapping.get(key, "")



Bạn không bị mapping thất bại chỉ vì dữ liệu có khoảng trắng thừa hoặc khác kiểu viết hoa/thường.

Một lưu ý quan trọng: NFC không xóa dấu tiếng Việt. Ví dụ ế vẫn là ế, chứ không chuyển thành e. Đây là điều tốt vì khi phân loại yêu cầu, bạn thường cần phân biệt chính xác nội dung tiếng Việt.

5. Bài tập nhỏ để bạn tự hiểu
Thử chạy đoạn code này và dự đoán kết quả trước khi chạy:
Kiểm tra kiến thức
0/4 câu

Câu 1. Hàm nào dùng để chuẩn hóa Unicode về dạng NFC?

category()

normalize()

combining()



Câu 2. unicodedata.category('A') trả về gì?

Lu

Ll

Nd



Câu 3. NFC có tự động xóa dấu tiếng Việt không?

Có

Không



Câu 4. Hàm nào giúp lấy tên Unicode của một ký tự?

lookup()

name()

decimal()


Kiểm tra đáp án
Mình khuyên bạn trước mắt chỉ cần nắm thật chắc normalize(), đặc biệt là 4 dạng NFC, NFD, NFKC, NFKD. Đây là phần quan trọng nhất khi xử lý dữ liệu tiếng Việt và xây dựng pipeline làm sạch email.