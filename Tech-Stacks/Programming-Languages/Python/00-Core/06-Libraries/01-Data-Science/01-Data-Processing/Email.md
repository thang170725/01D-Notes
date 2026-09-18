- [Email Introduction (dùng để tạo, đọc, phân tích và xử lý email theo chuẩn MIME/email)](#email-introduction-dùng-để-tạo-đọc-phân-tích-và-xử-lý-email-theo-chuẩn-mimeemail)
- [mime](#mime)
  - [text](#text)
    - [MIMETEXT()](#mimetext)
  - [multipart](#multipart)
    - [MIMEMulipart (đối tượng đại diện cho một email hoàn chỉnh)](#mimemulipart-đối-tượng-đại-diện-cho-một-email-hoàn-chỉnh)
      - [.attach (thêm nội dung vào email)](#attach-thêm-nội-dung-vào-email)
- [policy (tập hợp các cấu hình quy tắc quy định cách python xử lý email)](#policy-tập-hợp-các-cấu-hình-quy-tắc-quy-định-cách-python-xử-lý-email)
  - [.default](#default)
- [parser](#parser)
  - [Parser (class dùng để parse email dạng text thành một email message object)](#parser-class-dùng-để-parse-email-dạng-text-thành-một-email-message-object)
- [parsestr() (dùng để parse email dạng string)](#parsestr-dùng-để-parse-email-dạng-string)
- ["Nguyen Van A"](#nguyen-van-a)
- ["nguyenvana@gmail.com"](#nguyenvanagmailcom)
---
# Email Introduction (dùng để tạo, đọc, phân tích và xử lý email theo chuẩn MIME/email)
```bash
Đây là thư viện chuẩn không cần tải.
Nếu không có thư viện này thì server không biết email gồm:
    - Tiêu đề
    - Người gửi
    - Người nhận
    - Nội dung
```
Nó làm được những gì?

Có thể chia thành vài nhóm chính:

Chức năng	Mục đích
Parse email	Đọc email dạng raw text/bytes thành cấu trúc có thể truy cập
Đọc headers	Lấy From, To, Subject, Date, CC, Message-ID,...
Đọc body	Xử lý text/plain, text/html
Xử lý MIME	Xử lý email multipart
Xử lý attachment	Đọc file đính kèm, filename, content type, dữ liệu binary
Decode	Xử lý encoding của nội dung/header
Tạo email	Xây dựng email mới để gửi
Serialize	Chuyển email object trở lại thành text/bytes
# mime
## text
### MIMETEXT()
**Syn**
```bash
MIMEText(body, "plain")

- "plain"   : là văn bản thuần (plain text)
- "html"    : là văn bản html
```
**Ex**
```python
from email.mime.text import MIMEText

msg = MIMEText("Xin chào")
```
## multipart
### MIMEMulipart (đối tượng đại diện cho một email hoàn chỉnh)
```bash
Có thể chứa:
    - nội dung text
    - HTML
    - hình ảnh
    - file đính kèm
```
**Ex**
```python
from email.mime.multipart import MIMEMultipart
from email.mime.text import MIMEText

EMAIL = "shop@gmail.com"

msg = MIMEMultipart()
msg["From"] = EMAIL
msg["To"] = "abc@gmail.com"
msg["Subject"] = "OTP Reset Password"

body = "Your OTP is: 123456"
msg.attach(MIMEText(body, "plain"))

print(msg)
# Content-Type: multipart/mixed; boundary="===============123456789=="
# MIME-Version: 1.0
# From: shop@gmail.com
# To: abc@gmail.com
# Subject: OTP Reset Password

# --===============123456789==
# Content-Type: text/plain; charset="us-ascii"
# MIME-Version: 1.0
# Content-Transfer-Encoding: 7bit

# Your OTP is: 123456
# --===============123456789==--
```
#### .attach (thêm nội dung vào email)
**Syn**
```bash
msg.attach(MIMEText(body, "plain"))
```
# policy (tập hợp các cấu hình quy tắc quy định cách python xử lý email)
## .default
**Syn**
```bash
from email import policy

p = policy.default

- Output: EmailPolicy()
```
# parser
## Parser (class dùng để parse email dạng text thành một email message object)
**Syn**
```bash
Parser(policy=policy.default)

- Input:
  + policy=policy.default: cho Parser biết quy tắc xử lý email
```
# parsestr() (dùng để parse email dạng string)
**Syn**
```bash
Parser.parsestr(text, headersonly=False)

- Input: Một str chứa raw email:
- Output: Một email message object.
```
**Ex**
```python
raw_email = """\
From: Alice <alice@gmail.com>
To: Bob <bob@gmail.com>
Subject: Meeting

Hello Bob,
Let's meet tomorrow.
"""
parser = Parser(policy=policy.default)

msg = parser.parsestr(raw_email)

print(msg["From"]) # Alice <alice@gmail.com>
print(msg["Subject"]) # Meeting
print(msg.get_content()) # Hello Bob, Let's meet tomorrow.
```
**Ex**
```python
raw_email = """\
From: alice@example.com
To: bob@example.com
Subject: Hello

Hello Bob!
"""

from email import policy
from email.parser import Parser

msg = Parser(policy=policy.default).parsestr(raw_email)

print(type(msg)) # <class 'email.message.EmailMessage'>
```
parseaddr()

Import:

from email.utils import parseaddr

Hàm này dùng để tách tên và email address từ một chuỗi địa chỉ email.

Ví dụ:

"Nguyen Van A" <nguyenvana@gmail.com>

thành:

(
    "Nguyen Van A",
    "nguyenvana@gmail.com"
)
Cú pháp
parseaddr(address)
Input
address: str
Output
(name, email)
Ví dụ 1
Input
parseaddr('"Nguyen Van A" <nguyenvana@gmail.com>')
Output
(
    "Nguyen Van A",
    "nguyenvana@gmail.com"
)

Có thể unpack:

name, email = parseaddr(
    '"Nguyen Van A" <nguyenvana@gmail.com>'
)

Kết quả:

name
# "Nguyen Van A"

email
# "nguyenvana@gmail.com"

Đây chính là đoạn code của bạn:

from_name, from_email = parseaddr(msg.get("From", ""))

Nếu:

msg.get("From", "")

trả về:

"Nguyen Van A" <nguyenvana@gmail.com>

thì:

from_name

là:

Nguyen Van A

và:

from_email

là:

nguyenvana@gmail.com
Ví dụ 2: chỉ có email
Input
parseaddr("nguyenvana@gmail.com")
Output
("", "nguyenvana@gmail.com")
5. getaddresses()

Import:

from email.utils import getaddresses

getaddresses() dùng khi bạn có nhiều email address.

Đây là điểm khác quan trọng giữa:

parseaddr()

và:

getaddresses()
parseaddr()

Phù hợp với một địa chỉ.

Alice <alice@gmail.com>
getaddresses()

Phù hợp với nhiều địa chỉ.

Alice <alice@gmail.com>, Bob <bob@gmail.com>
Cú pháp
getaddresses(fieldvalues)

fieldvalues thường là list các chuỗi address.

Input
[
    "Alice <alice@gmail.com>, Bob <bob@gmail.com>"
]
Output
[
    ("Alice", "alice@gmail.com"),
    ("Bob", "bob@gmail.com")
]
Ví dụ
addresses = getaddresses([
    "Alice <alice@gmail.com>, Bob <bob@gmail.com>"
])

print(addresses)

Output:

[
    ("Alice", "alice@gmail.com"),
    ("Bob", "bob@gmail.com")
]
6. msg.get()

Đây là method của email message object.

Trong code:

msg.get("From", "")

hoặc:

msg.get("Subject")
Mục đích

Lấy giá trị của một email header.

Ví dụ email:

From: Alice <alice@gmail.com>
To: Bob <bob@gmail.com>
Subject: Hello
Date: Fri, 18 Sep 2026 09:30:00 +0700

thì:

msg.get("Subject")

→

Hello
Cú pháp
msg.get(name, failobj=None)
name

Tên header cần lấy:

"From"
"To"
"Subject"
"Date"
"Cc"
"Message-ID"
failobj

Giá trị trả về nếu header không tồn tại.

Ví dụ:

msg.get("Cc", [])

Nếu không có Cc:

[]
Ví dụ
subject = msg.get("Subject")

Input:

Subject: Hello

Output:

Hello
Nếu không tồn tại
msg.get("Reply-To")

Output:

None

Nếu:

msg.get("Reply-To", "")

Output:

""
7. msg.get_all()

Khác với get(), get_all() lấy tất cả giá trị của một header.

Cú pháp
msg.get_all(name, failobj=None)
Tại sao cần get_all()?

Một header có thể xuất hiện nhiều lần.

Ví dụ:

To: alice@gmail.com
To: bob@gmail.com
To: charlie@gmail.com

Nếu:

msg.get("To")

thì bạn không nên dựa vào nó để xử lý toàn bộ danh sách recipient.

Dùng:

msg.get_all("To", [])

Output:

[
    "alice@gmail.com",
    "bob@gmail.com",
    "charlie@gmail.com"
]
Trong code của bạn
getaddresses(msg.get_all("To", []))

Có thể đọc từ trong ra ngoài:

msg.get_all("To", [])
        ↓
lấy tất cả To
        ↓
getaddresses(...)
        ↓
tách name + email
8. msg.get_content_type()

Đây là method rất quan trọng khi xử lý MIME.

Mục đích

Cho biết kiểu nội dung của một email part.

Ví dụ:

Content-Type: text/html

thì:

msg.get_content_type()

→

text/html
Cú pháp
msg.get_content_type()

Không có tham số.

Ví dụ 1

Email:

Content-Type: text/plain; charset="utf-8"

Code:

msg.get_content_type()

Output:

text/plain

Chú ý:

text/plain; charset="utf-8"

được rút gọn thành:

text/plain
Ví dụ 2

Input:

Content-Type: text/html; charset="utf-8"

Output:

text/html
Ví dụ 3

Attachment:

Content-Type: application/pdf

Output:

application/pdf
9. msg.get_content_disposition()

Dùng để xác định một MIME part được sử dụng như:

attachment

hay:

inline

hoặc không có disposition.

Cú pháp
msg.get_content_disposition()
Ví dụ 1

Email attachment:

Content-Disposition: attachment;
 filename="invoice.pdf"

Code:

part.get_content_disposition()

Output:

attachment
Ví dụ 2

Inline:

Content-Disposition: inline;
 filename="logo.png"

Output:

inline
Ví dụ 3

Không có:

Content-Disposition:

Output:

None

Trong code:

if disposition == "attachment":

có nghĩa:

Nếu MIME part này thực sự là file attachment thì xử lý nó như attachment.

10. msg.get_filename()

Dùng để lấy tên file của attachment.

Cú pháp
msg.get_filename(failobj=None)
Input

Ví dụ MIME:

Content-Disposition: attachment;
 filename="invoice.pdf"

Code:

part.get_filename()

Output:

invoice.pdf
Ví dụ
filename = part.get_filename()

print(filename)

Output:

invoice.pdf

Nếu không có filename:

part.get_filename()

có thể trả về:

None
11. msg.get_payload()

Đây là method hơi quan trọng và dễ nhầm.

Nó lấy payload/content thô của message part.

Cú pháp
msg.get_payload(
    i=None,
    decode=False
)

Hai tham số đáng chú ý:

i

Index của part nếu message chứa nhiều part.

decode

Có decode transfer encoding hay không.

Ví dụ đơn giản

Email:

Content-Type: text/plain

Hello World
part.get_payload()

Output có thể là:

Hello World
Với attachment

Ví dụ PDF được encode trong email.

data = part.get_payload(decode=True)

Output:

b'%PDF-1.7...'

Đây là:

bytes

chứ không phải str.

Vì sao code dùng:
part.get_payload(decode=True)

?

Vì attachment thường là binary.

Ví dụ:

PDF
PNG
JPG
DOCX
XLSX

không nên xử lý như text.

decode=True giúp lấy dữ liệu đã được decode từ MIME transfer encoding thành bytes.

12. msg.get_content()

Đây là method rất tiện khi bạn muốn lấy nội dung đã được decode và chuyển thành Python object phù hợp.

Cú pháp
msg.get_content(*args, **kwargs)

Thông thường bạn chỉ cần:

msg.get_content()
Ví dụ text/plain

Email:

Content-Type: text/plain; charset="utf-8"

Hello World

Code:

content = msg.get_content()

Output:

"Hello World\n"

Kiểu:

str
Ví dụ text/html

Email:

Content-Type: text/html; charset="utf-8"

<html>
    <body>
        <h1>Hello</h1>
    </body>
</html>

Code:

content = msg.get_content()

Output:

<html>
    <body>
        <h1>Hello</h1>
    </body>
</html>

Kiểu:

str
13. msg.is_multipart()

Dùng để kiểm tra email có phải multipart email hay không.

Cú pháp
msg.is_multipart()

Output:

True

hoặc:

False
Multipart là gì?

Ví dụ một email có:

Body text
+
Body HTML
+
PDF attachment

thì email có thể có cấu trúc:

multipart/mixed
│
├── multipart/alternative
│   ├── text/plain
│   └── text/html
│
└── application/pdf

Đây là multipart.

Ví dụ

Nếu email:

Content-Type: text/plain

thì:

msg.is_multipart()

→

False

Nếu:

Content-Type: multipart/mixed

thì:

msg.is_multipart()

→

True
14. msg.walk()

Đây là method rất quan trọng để duyệt toàn bộ cây MIME của email.

Cú pháp
msg.walk()

Nó trả về một iterator.

Thường dùng:

for part in msg.walk():
    ...
Ví dụ

Giả sử email:

multipart/mixed
│
├── text/plain
├── text/html
└── application/pdf

Code:

for part in msg.walk():
    print(part.get_content_type())

Output:

multipart/mixed
text/plain
text/html
application/pdf

Bạn có thể hình dung:

msg
 ↓
walk()
 ↓
part 1 → multipart/mixed
part 2 → text/plain
part 3 → text/html
part 4 → application/pdf
15. Hiểu toàn bộ đoạn xử lý multipart

Bây giờ quay lại đoạn:

if msg.is_multipart():

    for part in msg.walk():

        content_type = part.get_content_type()
        disposition = part.get_content_disposition()

        if disposition == "attachment":

            filename = part.get_filename()

            attachments.append({
                "filename": filename,
                "content_type": content_type,
                "size": len(
                    part.get_payload(decode=True) or b""
                ),
            })

            continue

        if content_type == "text/plain":
            body_text = part.get_content()

        elif content_type == "text/html":
            body_html = part.get_content()

Có thể đọc theo flow:

                 msg
                  │
                  ▼
        is_multipart()?
             /          \
           True         False
            │             │
            ▼             ▼
        walk()       xử lý trực tiếp
            │
            ▼
         từng part
            │
     ┌──────┴─────────┐
     │                │
     ▼                ▼
attachment?        body?
     │                │
    Yes               │
     │                │
     ▼                ▼
get_filename()   get_content_type()
get_payload()         │
                      ├── text/plain
                      │       ↓
                      │  get_content()
                      │
                      └── text/html
                              ↓
                         get_content()
16. Một ví dụ hoàn chỉnh

Giả sử raw email:

From: "Alice" <alice@gmail.com>
To: Bob <bob@gmail.com>, Charlie <charlie@gmail.com>
Subject: Invoice
Date: Fri, 18 Sep 2026 09:30:00 +0700
Content-Type: multipart/mixed; boundary="abc"

--abc
Content-Type: text/plain; charset="utf-8"

Hello,
Please find invoice attached.

--abc
Content-Type: application/pdf
Content-Disposition: attachment; filename="invoice.pdf"

...binary data...

--abc--
Bước 1 — Parse
msg = Parser(
    policy=policy.default
).parsestr(raw_email)

Ta có:

raw string
   ↓
EmailMessage
Bước 2 — Header
msg.get("Subject")

Output:

Invoice
Bước 3 — From
parseaddr(msg.get("From", ""))

Output:

("Alice", "alice@gmail.com")
Bước 4 — To
getaddresses(
    msg.get_all("To", [])
)

Output:

[
    ("Bob", "bob@gmail.com"),
    ("Charlie", "charlie@gmail.com")
]
Bước 5 — Multipart
msg.is_multipart()

Output:

True
Bước 6 — Walk
for part in msg.walk():
    print(part.get_content_type())

Output:

multipart/mixed
text/plain
application/pdf
Bước 7 — Body

Với part:

text/plain

thì:

part.get_content_type()

→

text/plain

Sau đó:

part.get_content()

→

Hello,
Please find invoice attached.
Bước 8 — Attachment

Với PDF:

part.get_content_disposition()

→

attachment

Sau đó:

part.get_filename()

→

invoice.pdf

Và:

part.get_payload(decode=True)

→

b'%PDF-...'
17. Tóm tắt API trong code của bạn
API	Input chính	Output	Mục đích
policy.default	—	Policy object	Cấu hình cách xử lý email
Parser()	policy	Parser	Tạo parser
.parsestr()	str	EmailMessage	Parse raw email text
parseaddr()	str	(name, email)	Tách 1 địa chỉ
getaddresses()	list[str]	list[tuple]	Tách nhiều địa chỉ
.get()	header name	str/None	Lấy 1 header
.get_all()	header name	list	Lấy tất cả giá trị header
.get_content_type()	—	str	Lấy MIME type
.get_content_disposition()	—	str/None	Xác định attachment/inline
.get_filename()	—	str/None	Lấy tên file
.get_payload()	index/decode	payload	Lấy dữ liệu thô
.get_content()	—	content	Lấy nội dung đã decode
.is_multipart()	—	bool	Kiểm tra multipart
.walk()	—	iterator	Duyệt toàn bộ MIME parts
Một điểm rất quan trọng cần nhớ

Bạn có thể chia các API này thành 3 tầng:

TẦNG 1 — PARSE
Parser
└── parsestr()
        ↓
   EmailMessage


TẦNG 2 — ĐỌC CẤU TRÚC
EmailMessage
├── get()
├── get_all()
├── is_multipart()
└── walk()


TẦNG 3 — ĐỌC NỘI DUNG
EmailMessage / MIME part
├── get_content_type()
├── get_content_disposition()
├── get_filename()
├── get_content()
└── get_payload()

Còn:

parseaddr()
getaddresses()

là các utility functions trong email.utils, chủ yếu phục vụ việc xử lý địa chỉ email.