# XSLT Introduction
**Hãy hình dung**
```bash
XML
 │
 │  XSLT + XPath
 ▼
HTML / XML / Text
```
**Ex**
*XML*
```xml
<employees>
    <employee>
        <id>1</id>
        <name>Nguyen Van A</name>
        <salary>1500</salary>
    </employee>
    <employee>
        <id>2</id>
        <name>Tran Van B</name>
        <salary>2000</salary>
    </employee>
</employees>
-> XSLT sẽ đọc XML này và biến nó thành thứ khác, ví dụ HTML:
-> XSLT không hoạt động một mình. Bạn cần hiểu XPath vì XPath chính là cách XSLT “chỉ đường” tới dữ liệu trong XML.
```
# XPath
/

//

.

..

@

*

[]

and

or

=

!=

>

<

contains()

starts-with()

string()

number()

count()

sum()

position()

last()
Được. Mình giải thích ngắn gọn, đúng trọng tâm 3 phần bạn hỏi: stylesheet, output, template.
# xsl:stylesheet (khung của file XSLT)
**Syn**
```xslt
<xsl:stylesheet
    version="1.0"
    xmlns:xsl="http://www.w3.org/1999/XSL/Transform">

    <!-- các lệnh XSLT -->

</xsl:stylesheet>

- Input:
  + version="1.0": File này sử dụng XSLT 1.0.
  + xmlns:xsl="http://www.w3.org/1999/XSL/Transform": Khai báo rằng prefix xsl là namespace của XSLT.
```
## Ask
### msxsl là gì?
```bash
xmlns:msxsl="urn:schemas-microsoft-com:xslt"

Đây là namespace dành cho Microsoft XSLT extensions, thường thấy trong các file XSLT chạy với môi trường Microsoft.

Ví dụ dự án cũ có thể dùng:
  <msxsl:script> hoặc: <msxsl:node-set>
```
# xsl:output (quy định đầu ra)
```bash
Nó nói cho XSLT biết: Sau khi transform XML, tôi muốn tạo kết quả theo kiểu gì?
```
**Syn**
```bash
<xsl:output method="html" indent="yes"/>

- Input:
  + method="html": Xuất HTML.
    - method="xml": Xuất XML.
    - method="text": Xuất text.
  + indent="yes": Format output cho dễ đọc, có thụt dòng.
```
# xsl:template (nơi xử lý dữ liệu)
```bash
Hiểu đơn giản: XML -> XSLT tìm node phù hợp -> template xử lý node đó -> tạo output
```
**Syn**
```bash
<xsl:template match="XPath">
    <!-- các lệnh xử lý -->
</xsl:template>
```
**Ex**
```xml
<employees>
    <employee>
        <name>Nguyen Van A</name>
    </employee>
</employees>
```
*XSLT*
```xslt
<xsl:stylesheet
    version="1.0"
    xmlns:xsl="http://www.w3.org/1999/XSL/Transform">

    <xsl:output method="html" indent="yes"/>

    <xsl:template match="/">
        <html>
            <body>
                <h1>Employee List</h1>

                <p>
                    Hello
                </p>
            </body>
        </html>
    </xsl:template>
</xsl:stylesheet>

Kết quả:

<html>
    <body>
        <h1>Employee List</h1>
        <p>Hello</p>
    </body>
</html>

Luồng chạy:

employees.xml
      ↓
xsl:stylesheet
      ↓
xsl:output
      ↓
xsl:template match="/"
      ↓
<html>
   <body>
      ...
   </body>
</html>
      ↓
HTML output

6. Demo lấy dữ liệu XML
Bây giờ thêm:

<xsl:value-of select="/employees/employee/name"/>

XSLT:

<xsl:stylesheet
    version="1.0"
    xmlns:xsl="http://www.w3.org/1999/XSL/Transform">

    <xsl:output method="html" indent="yes"/>

    <xsl:template match="/">

        <html>
            <body>

                <h1>Employee</h1>

                <p>
                    <xsl:value-of select="/employees/employee/name"/>
                </p>

            </body>
        </html>

    </xsl:template>

</xsl:stylesheet>

XML:

<employees>
    <employee>
        <name>Nguyen Van A</name>
    </employee>
</employees>

Kết quả:

<h1>Employee</h1>
<p>Nguyen Van A</p>

Ở đây:

<xsl:value-of select="/employees/employee/name"/>

có nghĩa:

/               → từ document root
employees       → tìm employees
employee        → tìm employee
name            → lấy name
```

xsl:for-each
<xsl:for-each select="/employees/employee">

Nghĩ đơn giản:

for mỗi employee
    làm việc này

Ví dụ:

<xsl:for-each select="/employees/employee">
    <xsl:value-of select="name"/>
</xsl:for-each>

Kết quả:

Nguyen Van A
Tran Van B
Le Van C

# xsl:value-of (lấy giá trị của node)
**Ex**
```xml
<name>Nguyen Van A</name>
```
*XSLT*
```xslt
<xsl:value-of select="name"/>
Nguyen Van A
```
# xsl:if
**Ex: Ví dụ chỉ hiển thị nhân viên IT**
```xsl
<xsl:for-each select="/employees/employee">
    <xsl:if test="department = 'IT'">
        <p>
            <xsl:value-of select="name"/>
        </p>
    </xsl:if>
</xsl:for-each>

Kết quả:
Nguyen Van A
Le Van C
```
# xsl:choose (tương đương if/else if/else)
**Ex: Ví dụ phân loại lương**
```xslt
<xsl:choose>
    <xsl:when test="salary >= 2500">
        Senior
    </xsl:when>

    <xsl:when test="salary >= 1800">
        Mid
    </xsl:when>

    <xsl:otherwise>
        Junior
    </xsl:otherwise>

</xsl:choose>

Tư duy:
if salary >= 2500
    Senior
else if salary >= 1800
    Mid
else
    Junior
-> Đây là một trong những cấu trúc bạn sẽ dùng rất nhiều.
```
9. xsl:sort — cực kỳ hữu ích
Muốn sort nhân viên theo salary:

<xsl:for-each select="/employees/employee">

    <xsl:sort select="salary" data-type="number" order="descending"/>

    <p>
        <xsl:value-of select="name"/>
        -
        <xsl:value-of select="salary"/>
    </p>

</xsl:for-each>

Kết quả:

Le Van C - 2500
Tran Van B - 1800
Nguyen Van A - 1500

Tăng dần:

<xsl:sort
    select="salary"
    data-type="number"
    order="ascending"/>

10. Điều cực kỳ quan trọng: .
Trong XSLT bạn sẽ gặp:

.

Nó nghĩa gần như:

context hiện tại

Ví dụ:

<xsl:for-each select="/employees/employee">

    <xsl:value-of select="name"/>

</xsl:for-each>

Khi đang ở:

<employee>

thì:

name

nghĩa là:

name của employee hiện tại

Còn:

.

là chính employee hiện tại.

Ví dụ:

<xsl:value-of select="."/>

sẽ lấy text của context hiện tại.

11. @ — lấy Attribute
XML:

<employee id="1001" department="IT">
    <name>Nguyen Van A</name>
</employee>

Lấy id:

@id

Lấy department:

@department

Trong XSLT:

<xsl:value-of select="@id"/>

Đây là điểm người mới học XSLT rất hay nhầm:

name

là element

còn:

@name

là attribute.

12. Một bảng “cheat sheet” XSLT
Bạn muốn	XSLT/XPath
Lặp	xsl:for-each
Lấy giá trị	xsl:value-of
Điều kiện	xsl:if
If/else	xsl:choose
Sắp xếp	xsl:sort
Template	xsl:template
Gọi template	xsl:call-template
Apply template	xsl:apply-templates
# xsl:variable
**Ex**
```xslt
<?xml version="1.0" encoding="utf-8"?>
<xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform"
    xmlns:msxsl="urn:schemas-microsoft-com:xslt" exclude-result-prefixes="msxsl"
>
    <xsl:output method="html" indent="yes"/>

    <xsl:template match="/">
		<html>
			<body>
				<xsl:variable name="a" select="/GOC/SO[1]" />
				<xsl:variable name="b" select="/GOC/SO[2]" />
				
				<xsl:value-of select="$a"/>+<xsl:value-of select="$b"/>=<xsl:value-of select="$a+$b"/>
			</body>
		</html>
    </xsl:template>
</xsl:stylesheet>
```
Parameter	xsl:param
Truyền parameter	xsl:with-param
Copy node	xsl:copy
Copy cả cây	xsl:copy-of
Tạo attribute	xsl:attribute
Tạo element	xsl:element
Text cố định	xsl:text
Output	xsl:output
Import XSLT	xsl:import
Include XSLT	xsl:include
Key	xsl:key
Message/debug	xsl:message

14. Nhưng đừng học thuộc tất cả
Có một điều mình muốn bạn nhớ:

XSLT không phải là ngôn ngữ mà bạn cần thuộc 50–100 câu lệnh.

Để làm việc nhanh, bạn cần thành thạo khoảng:

XPath
   ↓
template
   ↓
apply-templates
   ↓
for-each
   ↓
value-of
   ↓
if / choose
   ↓
sort
   ↓
variable / param
   ↓
copy / copy-of
   ↓
namespace

Sau đó bạn sẽ đọc được phần lớn file XSLT trong dự án.

14. Cách học với Visual Studio
Mình khuyên bạn tạo một project học riêng:

XSLT-Learning
│
├── 01-basic
│   ├── employees.xml
│   └── employees.xsl
│
├── 02-xpath
│   ├── employees.xml
│   └── test.xsl
│
├── 03-condition
│   ├── employees.xml
│   └── condition.xsl
│
├── 04-sort
│   ├── employees.xml
│   └── sort.xsl
│
├── 05-template
│   ├── employees.xml
│   └── template.xsl
│
└── ...

Mỗi bài chỉ tập trung vào một kỹ thuật.

Đừng copy nguyên một file XSLT lớn rồi cố hiểu toàn bộ.

15. Lộ trình A → Z mình đề xuất cho bạn
Mình có thể dạy bạn theo dạng “không biết gì → có thể đọc/sửa/viết XSLT thực tế” như sau:

Phần A — Nền tảng
XML là gì

Element / Attribute

XML Tree

Namespace

XPath

Context node

Absolute vs relative XPath

Phần B — XPath thực chiến
/

//

.

..

@

*

[]

and

or

contains()

starts-with()

substring()

string()

number()

count()

sum()

position()

last()

Phần C — XSLT cơ bản


template

value-of

for-each

if

choose

when

otherwise

sort

output

Phần D — XSLT thực tế
apply-templates

match

call-template

param

with-param

variable

copy

copy-of

attribute

element

text

Phần E — Kỹ thuật nâng cao
Namespace trong XSLT

XML có namespace

Grouping

xsl:key

Muenchian grouping

Recursive template

Include

Import

Mode

Priority

XSLT 1.0

XSLT 2.0

XSLT 3.0

Performance

Debugging

XSLT trong Visual Studio

XSLT transform từ C#

XSLT transform từ command line

Đọc và sửa XSLT của dự án thực tế

Và mình muốn dạy bạn theo kiểu thực hành
Thay vì chỉ giải thích lý thuyết, mỗi bài sẽ theo mẫu:

1. Đây là XML
       ↓
2. Tôi hỏi bạn muốn lấy dữ liệu nào
       ↓
3. Viết XPath
       ↓
4. Viết XSLT
       ↓
5. Chạy trong Visual Studio
       ↓
6. Xem kết quả
       ↓
7. Tôi cho bài tập biến thể

Ví dụ sau khi học xsl:for-each, mình sẽ đưa:

<employees>
    ...
</employees>

và yêu cầu:

Chỉ lấy nhân viên IT, sort salary giảm dần, salary > 1800, rồi xuất thành HTML table.

Bạn sẽ tự viết:

/employees/employee[department='IT' and salary > 1800]

sau đó ghép với:

<xsl:for-each>
<xsl:sort>
<xsl:value-of>

Đây là cách nhanh nhất để thực sự đọc được XSLT của người khác và tự sửa XSLT trong công việc.

Nếu bạn muốn, bài tiếp theo mình sẽ bắt đầu từ số 0 với XPath, giải thích cực kỹ ./, /, //, ., .., @, *, [] bằng một file XML duy nhất và khoảng 20 bài tập, vì nắm chắc XPath là bạn đã đi được hơn nửa đường với XSLT.
# practices
## Cấu trúc của một file XSLT
```xslt
<?xml version="1.0" encoding="UTF-8"?>

<xsl:
    version="1.0"
    xmlns:xsl="http://www.w3.org/1999/XSL/Transform">

    <xsl:output method="html" />

    <xsl:template match="/">
        
        <html>
            <body>
                Hello
            </body>
        </html>

    </xsl:template>

</xsl:>

Hãy tách nó thành:

XSLT
│
├── xsl:
│   │
│   ├── xsl:output
│   │
│   ├── xsl:template
│   │   │
│   │   └── HTML/XML output
│   │
│   └── các XSLT instruction khác
│
└── kết quả output
```
Ví dụ:

<xsl:template match="/">
    <html>
        ...
    </html>
</xsl:template>

match
match="/"

match xác định node nào sẽ được template xử lý.

Sau này bạn sẽ gặp:

<xsl:template match="/">

<xsl:template match="employee">

<xsl:template match="employees">

<xsl:template match="employee[@status='active']">

Đây là chỗ XPath bắt đầu kết hợp với XSLT.

select
Ví dụ:

<xsl:value-of select="name"/>

select nói:

Tôi muốn lấy dữ liệu nào?

Ví dụ:

<xsl:value-of select="employee/name"/>

hoặc:

<xsl:for-each select="employees/employee">

match và select là hai thứ bạn sẽ gặp liên tục.

Một quy tắc rất đáng nhớ
Khi đọc XSLT, bạn hãy nhìn các câu này:

match="..."
select="..."
test="..."

và hiểu:

match  → Template này áp dụng cho node nào?

select → Lấy/chọn node nào?

test   → Kiểm tra điều kiện gì?

Ví dụ:

<xsl:for-each select="/employees/employee">
    
    <xsl:if test="salary > 2000">
        
        <xsl:value-of select="name"/>

    </xsl:if>

</xsl:for-each>

Đọc bằng tiếng Việt:

select → chọn các employee
test   → salary có > 2000 không?
select → lấy name

Đây chính là cách mình muốn bạn học XSLT.

Bài tiếp theo mình khuyên bắt đầu ngay với xsl:template, match, select và xsl:value-of, sau đó dùng một XML mẫu để mình chỉ cho bạn từng dòng XSLT chạy như thế nào.





