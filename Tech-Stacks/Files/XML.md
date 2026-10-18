- [XML introduction](#xml-introduction)
- [xml-stylesheet (liên kết file XML với một file XSLT giúp trình duyệt có thể chuyển đổi dữ liệu XML thành nội dung dễ đọc và hiển thị theo định dạng mong muốn)](#xml-stylesheet-liên-kết-file-xml-với-một-file-xslt-giúp-trình-duyệt-có-thể-chuyển-đổi-dữ-liệu-xml-thành-nội-dung-dễ-đọc-và-hiển-thị-theo-định-dạng-mong-muốn)
---
# XML introduction 
**Ex**
```xml
<?xml version="1.0" encoding="utf-8" ?>

<library>

    <book id="1">
        <title>Python</title>
        <author>John</author>
        <price>100</price>
    </book>

    <book id="2">
        <title>Java</title>
        <author>David</author>
        <price>120</price>
    </book>

</library>

<!-- Cấu trúc cây
library
│
├── book
│     ├── title
│     ├── author
│     └── price
│
└── book
      ├── title
      ├── author
      └── price -->
```
# xml-stylesheet (liên kết file XML với một file XSLT giúp trình duyệt có thể chuyển đổi dữ liệu XML thành nội dung dễ đọc và hiển thị theo định dạng mong muốn)
**Syn**
```bash
<?xml-stylesheet type="text/xsl" href="ten_file.xslt"?>

- Input:
    + <?xml-stylesheet ... ?>: Khai báo liên kết stylesheet cho XML. Đây là một processing instruction (chỉ thị xử lý).
    + type="text/xsl"	Cho biết file stylesheet sử dụng XSL/XSLT.
    + href="CongTy.xslt"	Đường dẫn đến file XSLT cần sử dụng.
    + ?>	Kết thúc chỉ thị xử lý.
```
Lưu ý: CongTy.xslt là tên file được liên kết. File này thường chứa các quy tắc chuyển đổi XML sang HTML hoặc một định dạng khác.
1. Ví dụ cụ thể
Giả sử bạn có hai file trong cùng một thư mục:
CongTy.xml

CongTy.xslt


File 1: CongTy.xml
<?xml version="1.0" encoding="UTF-8"?>
<?xml-stylesheet type="text/xsl" href="CongTy.xslt"?>

<CongTy>
    <NhanVien>
        <MaNV>NV01</MaNV>
        <HoTen>Nguyen Van An</HoTen>
        <Luong>15000000</Luong>
    </NhanVien>

    <NhanVien>
        <MaNV>NV02</MaNV>
        <HoTen>Tran Thi Binh</HoTen>
        <Luong>18000000</Luong>
    </NhanVien>
</CongTy>


Trong file trên, dòng:
<?xml-stylesheet type="text/xsl" href="CongTy.xslt"?>


báo cho trình xử lý XML biết cần sử dụng file CongTy.xslt để định dạng hoặc chuyển đổi dữ liệu.
File 2: CongTy.xslt
<?xml version="1.0" encoding="UTF-8"?>
<xsl:stylesheet
    version="1.0"
    xmlns:xsl="http://www.w3.org/1999/XSL/Transform">

    <xsl:template match="/">
        <html>
            <body>
                <h2>Danh sach nhan vien</h2>

                <table border="1">
                    <tr>
                        <th>Ma NV</th>
                        <th>Ho ten</th>
                        <th>Luong</th>
                    </tr>

                    <xsl:for-each select="CongTy/NhanVien">
                        <tr>
                            <td><xsl:value-of select="MaNV"/></td>
                            <td><xsl:value-of select="HoTen"/></td>
                            <td><xsl:value-of select="Luong"/></td>
                        </tr>
                    </xsl:for-each>
                </table>
            </body>
        </html>
    </xsl:template>

</xsl:stylesheet>


File XSLT này quy định cách lấy dữ liệu từ XML và tạo ra một bảng HTML.
Kết quả mong muốn
Danh sach nhan vien
Ma NV	Ho ten	Luong
NV01	Nguyen Van An	15000000
NV02	Tran Thi Binh	18000000
Minh họa kết quả HTML sau khi XML được chuyển đổi bằng XSLT.

3. Phân biệt XML, XSLT và XSD
Công nghệ	Công dụng
XML	Lưu trữ dữ liệu có cấu trúc.
XSLT	Chuyển đổi dữ liệu XML sang HTML, XML khác hoặc định dạng khác.
XSD	Quy định cấu trúc và kiểm tra tính hợp lệ của dữ liệu XML.
xml-stylesheet	Liên kết XML với stylesheet như XSLT để xử lý hoặc hiển thị.
Cần nhớ: Dòng xml-stylesheet không trực tiếp tạo ra bảng hay thay đổi dữ liệu XML. Nó chỉ khai báo file stylesheet được liên kết. Việc chuyển đổi thực tế do bộ xử lý XSLT thực hiện; trình duyệt hiện đại cũng có thể không hỗ trợ hiển thị XSLT trực tiếp như trước.