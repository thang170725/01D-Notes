- [XSLT Introduction (chuyển tử xml sang định dạng khác)](#xslt-introduction-chuyển-tử-xml-sang-định-dạng-khác)
- [xsl:stylesheet (khung của file XSLT)](#xslstylesheet-khung-của-file-xslt)
  - [Ask](#ask)
    - [msxsl là gì?](#msxsl-là-gì)
- [xsl:output (quy định đầu ra)](#xsloutput-quy-định-đầu-ra)
- [xsl:template (nơi xử lý dữ liệu)](#xsltemplate-nơi-xử-lý-dữ-liệu)
- [xsl:for-each](#xslfor-each)
- [xsl:value-of (lấy giá trị của node)](#xslvalue-of-lấy-giá-trị-của-node)
- [xsl:if](#xslif)
- [xsl:choose (tương đương if elif else)](#xslchoose-tương-đương-if-elif-else)
- [xsl:sort (sắp xếp)](#xslsort-sắp-xếp)
- [xsl:variable](#xslvariable)
- [xsl:apply-templates (dùng để duyệt các phần tử con trong XML và áp dụng quy tắc xử lý đã định nghĩa bằng xsl:template)](#xslapply-templates-dùng-để-duyệt-các-phần-tử-con-trong-xml-và-áp-dụng-quy-tắc-xử-lý-đã-định-nghĩa-bằng-xsltemplate)
- [practices](#practices)
  - [Cấu trúc của một file XSLT](#cấu-trúc-của-một-file-xslt)
---
# XSLT Introduction (chuyển tử xml sang định dạng khác)
**Hãy hình dung**
```bash
XML --XSLT + XPath--> HTML / XML / Text
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

- Input:
    + match: xác định node nào sẽ được template xử lý.
        - match="/">
        - match="employee"
        - match="employees"
        - match="employee[@status='active']"
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
```xsl
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
```
# xsl:for-each
**Ex**
```xsl
<xsl:for-each select="/employees/employee">
    <xsl:value-of select="name"/>
</xsl:for-each>

<!-- Nguyen Van A
Tran Van B
Le Van C -->
```
# xsl:value-of (lấy giá trị của node)
**Syn**
```bash
<xsl:value-of select="position()"/>

- Input:
    + select:
        - position(): số thứ tự tăng dần
```
**Ex**
```xml
<name>Nguyen Van A</name>
```
*XSLT*
```xslt
<xsl:value-of select="name"/>
<!-- Nguyen Van A -->
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

<!-- Nguyen Van A
Le Van C -->
```
# xsl:choose (tương đương if elif else)
**Ex: Ví dụ phân loại lương**
```xsl
<xsl:choose>
    <xsl:when test="salary &gt;= 2500">
        Senior
    </xsl:when>

    <xsl:when test="salary &gt;= 1800">
        Mid
    </xsl:when>

    <xsl:otherwise>
        Junior
    </xsl:otherwise>

</xsl:choose>

<!-- 
if salary >= 2500
    Senior
else if salary >= 1800
    Mid
else
    Junior
-> Đây là một trong những cấu trúc bạn sẽ dùng rất nhiều. -->
```
# xsl:sort (sắp xếp)
**Syn**
```bash
<xsl:sort select="salary" data-type="number" order="descending"/>
```
*Ex**
```xsl
<xsl:for-each select="/employees/employee">

    <xsl:sort select="salary" data-type="number" order="descending"/>

    <p>
        <xsl:value-of select="name"/>
        -
        <xsl:value-of select="salary"/>
    </p>

</xsl:for-each>

<!-- Le Van C - 2500
Tran Van B - 1800
Nguyen Van A - 1500 -->
```
# xsl:variable
**Ex**
```xsl
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
# xsl:apply-templates (dùng để duyệt các phần tử con trong XML và áp dụng quy tắc xử lý đã định nghĩa bằng xsl:template)
1. Cú pháp cơ bản
<xsl:apply-templates select="biểu_thức_xpath"/>


- xsl:apply-templates: gọi xử lý template cho các node được chọn.
- select: xác định những node nào sẽ được xử lý bằng XPath.
- Nếu bỏ select, XSLT mặc định xử lý các node con của node hiện tại.
2. Ví dụ đơn giản
Giả sử file XML có dữ liệu:
<congty>
    <nhanvien>
        <name>Thắng</name>
        <luong>15000000</luong>
    </nhanvien>
    <nhanvien>
        <name>Hùng</name>
        <luong>12000000</luong>
    </nhanvien>
</congty>


Bạn muốn in tên của tất cả nhân viên.
File XSLT:
<xsl:stylesheet version="1.0"
    xmlns:xsl="http://www.w3.org/1999/XSL/Transform">

    <xsl:template match="/">
        <html>
            <body>
                <h2>Danh sách nhân viên</h2>

                <xsl:apply-templates select="congty/nhanvien"/>
            </body>
        </html>
    </xsl:template>

    <xsl:template match="nhanvien">
        <p>
            <xsl:apply-templates select="name"/>
        </p>
    </xsl:template>

    <xsl:template match="name">
        <xsl:value-of select="."/>
    </xsl:template>

</xsl:stylesheet>


Kết quả HTML:
Danh sách nhân viên
Thắng

Hùng

3. Luồng hoạt động của apply-templates
Template gốc
match="/"

apply-templates select="congty/nhanvien"
Chọn các node nhân viên

Template nhân viên 1
match="nhanvien"


Template nhân viên 2
match="nhanvien"



Mỗi node được xử lý bằng template phù hợp. Template nhân viên tiếp tục gọi template name để lấy tên.

Điểm quan trọng: apply-templates không trực tiếp lấy giá trị của node. Nó chuyển việc xử lý node đó cho template phù hợp. Trong ví dụ trên, xsl:value-of select="." mới là lệnh lấy giá trị văn bản của node name.
4. Những cách dùng thường gặp
Cách 1: Chọn các node con
<xsl:apply-templates select="nhanvien"/>


Áp dụng template cho các phần tử nhanvien là con của node hiện tại.
Cách 2: Chọn tất cả node con
<xsl:apply-templates select="*"/>


Áp dụng template cho tất cả phần tử con trực tiếp.
Cách 3: Chọn theo điều kiện XPath
<xsl:apply-templates select="nhanvien[luong &gt; 10000000]"/>


Chỉ xử lý những nhân viên có lương lớn hơn 10 triệu.
Cách 4: Gọi template theo mode
<xsl:apply-templates select="nhanvien" mode="inLuong"/>

<xsl:template match="nhanvien" mode="inLuong">
    <p>
        <xsl:value-of select="luong"/>
    </p>
</xsl:template>


mode cho phép bạn có nhiều cách xử lý khác nhau cho cùng một loại node.
5. Phân biệt apply-templates, call-template và value-of
Lệnh	Công dụng
xsl:apply-templates	Chọn node và tìm template phù hợp để xử lý
xsl:call-template	Gọi trực tiếp một template theo tên
xsl:value-of	Lấy giá trị của biểu thức XPath và xuất ra kết quả
xsl:for-each	Lặp qua các node được chọn để thực hiện nội dung bên trong
Ví dụ, nếu muốn lấy tên nhân viên ngay tại chỗ thì có thể dùng:
<xsl:value-of select="name"/>


Nhưng nếu muốn mỗi nhân viên được xử lý theo một quy tắc riêng đã định nghĩa trong xsl:template, hãy dùng:
<xsl:apply-templates select="nhanvien"/>


Mẹo nhớ: match định nghĩa template sẽ xử lý node nào; select chọn node cần xử lý; apply-templates kết nối hai việc đó với nhau.
Mình giải thích lại từ đầu nhé. Vấn đề là: tại sao không viết thẳng tên nhân viên ra, mà phải chia thành 3 xsl:template rồi gọi qua xsl:apply-templates?
Thực ra, bạn không bắt buộc phải viết phức tạp như vậy. Ví dụ trước dùng nhiều template để minh họa cách apply-templates hoạt động.
1. Đầu tiên, hãy nhìn vào dữ liệu XML
Giả sử file XML của bạn là:
<congty>
    <nhanvien>
        <name>Thắng</name>
        <luong>15000000</luong>
    </nhanvien>
    <nhanvien>
        <name>Hùng</name>
        <luong>12000000</luong>
    </nhanvien>
</congty>


Hãy tưởng tượng dữ liệu có cấu trúc như sau:
congty

nhanvien thứ nhất

name
Thắng

luong
15000000


nhanvien thứ hai

name
Hùng

luong
12000000



Mục tiêu của chúng ta là biến XML trên thành HTML hiển thị:
- Thắng
- Hùng
2. Cách dễ nhất: Không cần apply-templates
Nếu chỉ cần in tên nhân viên, bạn có thể viết ngắn gọn thế này:
<xsl:stylesheet version="1.0"
    xmlns:xsl="http://www.w3.org/1999/XSL/Transform">

    <xsl:template match="/">
        <html>
            <body>
                <h2>Danh sách nhân viên</h2>

                <xsl:for-each select="congty/nhanvien">
                    <p>
                        <xsl:value-of select="name"/>
                    </p>
                </xsl:for-each>

            </body>
        </html>
    </xsl:template>

</xsl:stylesheet>


Ở đây chỉ cần hiểu 3 việc:
1. match="/": bắt đầu xử lý từ node gốc của tài liệu XML.
2. for-each: duyệt lần lượt từng nhân viên.
3. value-of select="name": lấy tên của nhân viên đang được duyệt.
Kết quả:
Danh sách nhân viên
Thắng
Hùng

Đây là cách dễ hiểu hơn nếu bạn mới học XSLT.

3. Vậy apply-templates dùng để làm gì?
Bây giờ, giả sử mỗi nhân viên cần được xử lý theo một quy tắc riêng. Ví dụ:
- Tên nhân viên được in đậm.
- Lương được hiển thị riêng.
- Mỗi nhân viên được trình bày trong một khối HTML.
- Có thể tái sử dụng cách hiển thị nhân viên ở nhiều nơi.
Lúc này, bạn có thể tách cách xử lý thành những template riêng.
Template 1: Bắt đầu từ node gốc
<xsl:template match="/">
    <html>
        <body>
            <h2>Danh sách nhân viên</h2>
            <xsl:apply-templates select="congty/nhanvien"/>
        </body>
    </html>
</xsl:template>


Dòng quan trọng là:
<xsl:apply-templates select="congty/nhanvien"/>


Nó có nghĩa là:
“Hãy tìm các phần tử nhanvien nằm trong congty, rồi xử lý từng phần tử bằng template phù hợp.”
Nó không có nghĩa là lấy giá trị tên nhân viên. Nó giao việc xử lý các node nhanvien cho template khác.
Template 2: Quy định cách hiển thị một nhân viên
<xsl:template match="nhanvien">
    <p>
        <b>
            <xsl:value-of select="name"/>
        </b>
        -
        <xsl:value-of select="luong"/>
    </p>
</xsl:template>


match="nhanvien" có nghĩa là template này dùng để xử lý các phần tử <nhanvien>.
Khi apply-templates chọn nhân viên Thắng, XSLT sẽ chạy template này với nhân viên Thắng làm node hiện tại. Sau đó nó chạy tiếp với nhân viên Hùng.
Kết quả sẽ là:
Thắng - 15000000


Hùng - 12000000



Lưu ý: Trong ví dụ này, mình dùng value-of trực tiếp để lấy name và luong, nên chưa cần template riêng cho name.
Template 3: Nếu muốn tách riêng cả phần tên
Bạn cũng có thể viết:
<xsl:template match="nhanvien">
    <p>
        <xsl:apply-templates select="name"/>
    </p>
</xsl:template>

<xsl:template match="name">
    <b>
        <xsl:value-of select="."/>
    </b>
</xsl:template>


Lúc này, khi xử lý nhân viên Thắng:
1. Template match="nhanvien" được chạy.
2. apply-templates select="name" yêu cầu xử lý node name của nhân viên đó.
3. XSLT tìm template match="name" và chạy nó.
4. value-of select="." lấy nội dung của node name hiện tại, tức là Thắng.
Luồng xử lý:
match="/"
Bắt đầu

apply-templates select="congty/nhanvien"

match="nhanvien"
Xử lý từng nhân viên

apply-templates select="name"

match="name"
Xuất ra Thắng hoặc Hùng


4. Chốt lại: Khi nào dùng cái nào?
Bạn muốn làm gì?	Nên dùng
Lặp qua nhân viên rồi lấy tên, lương	for-each + value-of
Định nghĩa cách hiển thị nhân viên ở template riêng	apply-templates
Định nghĩa cách xử lý riêng cho node name	apply-templates + template match="name"
Gọi trực tiếp một template có tên cụ thể	call-template
Điều quan trọng nhất cần nhớ: apply-templates giúp bạn tách biệt việc chọn node và việc quy định cách xử lý node đó. Bạn không cần dùng nó cho mọi trường hợp; với tác vụ đơn giản, for-each thường dễ đọc hơn.
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
```

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





