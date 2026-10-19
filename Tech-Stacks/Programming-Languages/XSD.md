- [XSD (XML Schema Definition là file dùng để quy định XML được phép có cấu trúc và dữ liệu như thế nào)](#xsd-xml-schema-definition-là-file-dùng-để-quy-định-xml-được-phép-có-cấu-trúc-và-dữ-liệu-như-thế-nào)
  - [Ask](#ask)
    - [Cấu trúc một file xsd](#cấu-trúc-một-file-xsd)
- [Datatype (kiểu dữ liệu trong xsd)](#datatype-kiểu-dữ-liệu-trong-xsd)
  - [xs:string](#xsstring)
  - [xs:integer | xs:int](#xsinteger--xsint)
  - [xs:decimal](#xsdecimal)
  - [xs:float](#xsfloat)
  - [xs:double](#xsdouble)
  - [xs:boolean](#xsboolean)
  - [xs:date](#xsdate)
  - [xs:dateTime](#xsdatetime)
  - [xs:time](#xstime)
- [xs:element](#xselement)
  - [complexType (Dùng khi một element có cấu trúc bên trong, ví dụ chứa nhiều element con)](#complextype-dùng-khi-một-element-có-cấu-trúc-bên-trong-ví-dụ-chứa-nhiều-element-con)
    - [xs:attribute (dùng để khai báo thuộc tính cho một phần tử XML)](#xsattribute-dùng-để-khai-báo-thuộc-tính-cho-một-phần-tử-xml)
  - [sequence (Các element phải xuất hiện đúng thứ tự)](#sequence-các-element-phải-xuất-hiện-đúng-thứ-tự)
  - [choice (Chỉ được chọn một trong các element)](#choice-chỉ-được-chọn-một-trong-các-element)
  - [all (Các element có thể xuất hiện theo bất kỳ thứ tự nào)](#all-các-element-có-thể-xuất-hiện-theo-bất-kỳ-thứ-tự-nào)
- [simpleType (dùng để tạo kiểu dữ liệu đơn giản)](#simpletype-dùng-để-tạo-kiểu-dữ-liệu-đơn-giản)
  - [enumeration (Giới hạn chỉ được phép một số giá trị nhất định)](#enumeration-giới-hạn-chỉ-được-phép-một-số-giá-trị-nhất-định)
- [xs:unique (dùng để đảm bảo giá trị của một trường không bị trùng nhau trong phạm vi các phần tử được chọn)](#xsunique-dùng-để-đảm-bảo-giá-trị-của-một-trường-không-bị-trùng-nhau-trong-phạm-vi-các-phần-tử-được-chọn)
- [xs:key (Tương tự unique, nhưng trường khóa bắt buộc phải có giá )](#xskey-tương-tự-unique-nhưng-trường-khóa-bắt-buộc-phải-có-giá-)
- [xs:keyref	(Kiểm tra giá trị tham chiếu phải tồn tại trong một key hoặc unique đã khai báo)](#xskeyrefkiểm-tra-giá-trị-tham-chiếu-phải-tồn-tại-trong-một-key-hoặc-unique-đã-khai-báo)
- [xs:restriction (giá trị này phải thuộc kiểu X, nhưng bị giới hạn thêm theo các điều kiện bên dưới)](#xsrestriction-giá-trị-này-phải-thuộc-kiểu-x-nhưng-bị-giới-hạn-thêm-theo-các-điều-kiện-bên-dưới)
  - [minInclusive / maxInclusive (Giới hạn số và cho phép luôn giá trị biên)](#mininclusive--maxinclusive-giới-hạn-số-và-cho-phép-luôn-giá-trị-biên)
  - [minExclusive / maxExclusive (Giới hạn số nhưng không cho phép giá trị biên)](#minexclusive--maxexclusive-giới-hạn-số-nhưng-không-cho-phép-giá-trị-biên)
  - [xs:pattern (Dùng để bắt giá trị phải khớp biểu thức chính quy)](#xspattern-dùng-để-bắt-giá-trị-phải-khớp-biểu-thức-chính-quy)
---
# XSD (XML Schema Definition là file dùng để quy định XML được phép có cấu trúc và dữ liệu như thế nào)
```bash
Bạn có thể hình dung:
    - XML = Dữ liệu
    - XSD = Luật quy định dữ liệu
```
**XSD dùng để làm gì?**
```bash
Chủ yếu để kiểm tra (validate) XML có đúng cấu trúc và dữ liệu hay không.

Ví dụ XSD có thể quy định:
    - age   : số nguyên từ 15 đến 150
    - tel   : đúng 10 chữ số
    - gender: chỉ "male" hoặc "female"
    - name  : bắt buộc phải có
    - email : kiểu string
```
## Ask 
### Cấu trúc một file xsd
```xsd
<?xml version="1.0" encoding="UTF-8"?>

<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema">

    <xs:element name="book">
        <xs:complexType>
            <xs:sequence>
                <xs:element name="title" type="xs:string"/>
                <xs:element name="author" type="xs:string"/>
                <xs:element name="price" type="xs:decimal"/>
            </xs:sequence>
        </xs:complexType>
    </xs:element>

</xs:schema>

- Input:
    + <xs:schema>: Là phần tử gốc của XSD
    + <xs:element>: Dùng để khai báo một phần tử XML
        - Một số thuộc tính thường dùng:
            + name="name": tên element
            + type="xs:string": kiểu dữ liệu
            + minOccurs="0": số lần xuất hiện tối thiểu
            + maxOccurs="1": số lần xuất hiện tối đa.
```
**Ex1**
```bash
<xs:element name="phone"
            type="xs:string"
            minOccurs="0"
            maxOccurs="3"/>

# Nghĩa là phone có thể xuất hiện từ 0 đến 3 lần.
```
# Datatype (kiểu dữ liệu trong xsd)
## xs:string	
**Ex**
```bash
"Hello"
```
## xs:integer | xs:int
```bash
100
```
## xs:decimal	
```bash
<xs:element name="salary" type="xs:decimal"/>
# 10.5
```
## xs:float	
```bash
10.5
```
## xs:double	
```bash
10.5
```
## xs:boolean	
```bash
<xs:element name="isActive" type="xs:boolean"/>
# true / false
```
## xs:date	
```bash
<xs:element name="birthDate" type="xs:date"/>
# 2026-09-29
```
## xs:dateTime	
```bash
2026-09-29T10:30:00
```
## xs:time	
```bash
10:30:00
```
# xs:element
**Syn**
```bash
<xs:element
    name="..."
    type="..."
    ref="..."
    minOccurs="..."
    maxOccurs="..."
    default="..."
    fixed="..."
    nillable="..."
    abstract="..."
    form="..."
    substitutionGroup="..."
/>

- Input:
    + name: Tên phần tử XML	name="email"
    + type: Kiểu dữ liệu của phần tử, type="xs:string"
    + minOccurs: Số lần xuất hiện tối thiểu	minOccurs="0"
    + maxOccurs: Số lần xuất hiện tối đa	maxOccurs="3" hoặc "unbounded"
    + default	Giá trị mặc định nếu không cung cấp giá trị	default="Unknown"
    + fixed	Giá trị cố định được phép sử dụng	fixed="VN"
    + nillable	Cho phép phần tử có giá trị nil	nillable="true"
    + abstract	Khai báo phần tử trừu tượng, không được sử dụng trực tiếp theo cách thông thường	abstract="true"
    + form	Quy định phần tử có được qualified bởi namespace hay không	"qualified" hoặc "unqualified"
    + ref	Tham chiếu đến một phần tử đã khai báo	ref="user"
    + substitutionGroup	Khai báo phần tử có thể thay thế phần tử khác	substitutionGroup="baseElement"
```
**Ex**
```xml
<person>
    <name>An</name>
    <age>20</age>
</person>
```
*XSD quy định*
```xsd
<xs:element name="person">
    <xs:complexType>
        <xs:sequence>
            <xs:element name="name" type="xs:string"/>
            <xs:element name="age" type="xs:integer"/>
        </xs:sequence>
    </xs:complexType>
</xs:element>

<!-- Nó nói rằng:
    person phải có name
    name phải là string
    age phải là integer
    name phải đứng trước age -->
```
*Nếu XML viết*
```xml
<person>
    <name>An</name>
    <age>abc</age>
</person>

<!-- ❌ Sai vì age yêu cầu xs:integer nhưng "abc" không phải số nguyên. -->
```
## complexType (Dùng khi một element có cấu trúc bên trong, ví dụ chứa nhiều element con)
**Ex**
```bash
<xs:element name="person">
    <xs:complexType>
        <xs:sequence>
            <xs:element name="name" type="xs:string"/>
            <xs:element name="age" type="xs:int"/>
        </xs:sequence>
    </xs:complexType>
</xs:element>

XML tương ứng:
<person>
    <name>An</name>
    <age>20</age>
</person>
```
### xs:attribute (dùng để khai báo thuộc tính cho một phần tử XML)
```bash
Nó cho phép quy định tên thuộc tính, kiểu dữ liệu, thuộc tính có bắt buộc hay không, giá trị mặc định và nhiều ràng buộc khác.
```
**Syn**
```bash
<xs:attribute
    name="attributeName"
    type="xs:string"
    use="optional"
    default="defaultValue"
    fixed="fixedValue"
    form="qualified"
/>

- Input:
    + name	Tên thuộc tính được khai báo	id, age, status
    + type	Kiểu dữ liệu của thuộc tính	xs:string, xs:integer, xs:boolean
    + use	Quy định thuộc tính có bắt buộc hay không	optional, required, prohibited
        - optional: Không bắt buộc
        - required: Bắt buộc
        - prohibited: Cấm sử dụng
    + default: Giá trị mặc định nếu thuộc tính bị bỏ qua	default="active"
    + fixed: Giá trị cố định mà thuộc tính phải tuân theo	fixed="VN"
    + ref: Tham chiếu đến một thuộc tính được khai báo toàn cục	ref="countryCode"
    + form: Quy định thuộc tính có thuộc namespace hay không	qualified, unqualified
- Lưu ý:
    +  name và ref không được dùng đồng thời.
    +  type và ref không được dùng đồng thời.
    +  default và fixed không được dùng đồng thời.
    +  use mặc định là optional.
    +  default và fixed không thay thế cho nhau: default cho phép giá trị khác, còn fixed không cho phép giá trị khác giá trị cố định đã quy định.
```
**Ex**
```xsd
<?xml version="1.0" encoding="UTF-8"?>

<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema">

    <xs:element name="user">
        <xs:complexType>
            <xs:simpleContent>
                <xs:extension base="xs:string">

                    <xs:attribute
                        name="id"
                        type="xs:string"
                        use="required"/>

                    <xs:attribute
                        name="age"
                        type="xs:integer"
                        use="optional"/>

                </xs:extension>
            </xs:simpleContent>
        </xs:complexType>
    </xs:element>

</xs:schema>
```
*XML hợp lệ*
```xml
<user id="U01" age="20">Nguyen Van A</user>
<user id="U02">Tran Van B</user>
```
*XML không hợp lệ*
```xml
<user age="20">Nguyen Van A</user>
```
**Ex2: Sử dụng default và fixed**
```xsd
<xs:element name="product">
    <xs:complexType>
        <xs:attribute
            name="status"
            type="xs:string"
            default="active"/>

        <xs:attribute
            name="country"
            type="xs:string"
            fixed="VN"/>
    </xs:complexType>
</xs:element>
```
**Ex3: Giới hạn giá trị thuộc tính bằng kiểu dữ liệu tùy chỉnh**
```xsd
<xs:element name="account">
    <xs:complexType>
        <xs:attribute name="status" use="required">
            <xs:simpleType>
                <xs:restriction base="xs:string">
                    <xs:enumeration value="active"/>
                    <xs:enumeration value="inactive"/>
                    <xs:enumeration value="pending"/>
                </xs:restriction>
            </xs:simpleType>
        </xs:attribute>
    </xs:complexType>
</xs:element>
```
*XML*
```xml
<account status="active"/>
```
**XML không hợp lệ**
```xml
<account status="deleted"/>
```
**Ex4**
```bash
<xs:element name="person">
    <xs:complexType>
        <xs:sequence>
            <xs:element name="name" type="xs:string"/>
        </xs:sequence>

        <xs:attribute name="id"
                      type="xs:int"
                      use="required"/>
    </xs:complexType>
</xs:element>
```
*XML*
```xml
<person id="100">
    <name>An</name>
</person>

<!-- use thường có: use="required" hoặc: use="optional" -->
```
## sequence (Các element phải xuất hiện đúng thứ tự)
**Ex**
```bash
<xs:sequence>
    <xs:element name="name" type="xs:string"/>
    <xs:element name="age" type="xs:int"/>
</xs:sequence>

# XML hợp lệ:
# <person>
#    <name>An</name>
#    <age>20</age>
# </person>

# Nhưng:
# <person>
#    <age>20</age>
#    <name>An</name>
# </person>
# không hợp lệ.
```
## choice (Chỉ được chọn một trong các element)
**Ex**
```bash
<xs:choice>
    <xs:element name="email" type="xs:string"/>
    <xs:element name="phone" type="xs:string"/>
</xs:choice>

# Có thể là:
# <contact>
#    <email>a@gmail.com</email>
# </contact>

# hoặc:
# <contact>
#    <phone>0123456789</phone>
# </contact>
```
## all (Các element có thể xuất hiện theo bất kỳ thứ tự nào)
**Ex**
```bash
<xs:all>
    <xs:element name="name" type="xs:string"/>
    <xs:element name="age" type="xs:int"/>
</xs:all>

# Cả hai thứ tự đều được:
# <person>
#    <name>An</name>
#    <age>20</age>
# </person>

# hoặc:
# <person>
#    <age>20</age>
#    <name>An</name>
# </person>
```
# simpleType (dùng để tạo kiểu dữ liệu đơn giản)
**Kiến thức nên học trước**
- [restriction](#xsrestriction-giá-trị-này-phải-thuộc-kiểu-x-nhưng-bị-giới-hạn-thêm-theo-các-điều-kiện-bên-dưới)
```bash
thường dựa trên kiểu có sẵn như xs:string, xs:integer, xs:decimal rồi thêm các điều kiện ràng buộc.
```
**Syn**
```bash
<xs:simpleType name="TenKieu">
    <xs:restriction base="xs:string">
        <!-- Các điều kiện ràng buộc -->
    </xs:restriction>
</xs:simpleType>

- Input:
    + name: tên kiểu dữ liệu do bạn tự đặt.
    + xs:restriction: giới hạn kiểu dữ liệu gốc.
    + base: kiểu dữ liệu gốc, chẳng hạn xs:string, xs:integer, xs:decimal.
    + Các điều kiện bên trong xs:restriction được gọi là facets.
```
**Ex1: Mã hàng tối đa 6 ký tự**
```xsd
<xs:simpleType name="MaHangType">
    <xs:restriction base="xs:string">
        <xs:maxLength value="6"/>
    </xs:restriction>
</xs:simpleType>

<!-- 
Ví dụ hợp lệ: MH01, SP1234.
Ví dụ không hợp lệ: SP12345 vì có 7 ký tự.
-->
```
**Ex2: Đơn giá phải lớn hơn 0**
```xsd
<xs:simpleType name="DonGiaType">
    <xs:restriction base="xs:decimal">
        <xs:minExclusive value="0"/>
    </xs:restriction>
</xs:simpleType>


<!-- 
100: hợp lệ.
0: không hợp lệ.
-10: không hợp lệ.
 -->
```
## enumeration (Giới hạn chỉ được phép một số giá trị nhất định)
**Syn**
```bash
<xs:enumeration value="gói"/>
```
**Ex: Đơn vị tính chỉ được là gói, hộp, chiếc**
```xsd
<xs:simpleType name="DonViTinhType">
    <xs:restriction base="xs:string">
        <xs:enumeration value="gói"/>
        <xs:enumeration value="hộp"/>
        <xs:enumeration value="chiếc"/>
    </xs:restriction>
</xs:simpleType>


<!-- 
Sau khi tạo simpleType, bạn sử dụng nó qua thuộc tính type:
<xs:element name="MaHang" type="MaHangType"/>
<xs:element name="DonGia" type="DonGiaType"/>
<xs:element name="DonViTinh" type="DonViTinhType"/>
-> Như vậy, bạn không phải viết lại các điều kiện ở mọi nơi. -->
```
# xs:unique (dùng để đảm bảo giá trị của một trường không bị trùng nhau trong phạm vi các phần tử được chọn)
**Syn**
```bash
<xs:element name="HangHoa">
    <xs:complexType>
        <!-- Khai báo cấu trúc dữ liệu -->
    </xs:complexType>

    <xs:unique name="MaHangKhongTrung">
        <xs:selector xpath="MatHang"/>
        <xs:field xpath="MaHang"/>
    </xs:unique>
</xs:element>

- Input:
    + xs:unique name="MaHangKhongTrung": đặt tên cho quy tắc duy nhất.
    + xs:selector xpath="MatHang": chọn các phần tử MatHang cần kiểm tra.
    + xs:field xpath="MaHang": chọn trường MaHang trong mỗi phần tử MatHang để so sánh.
```
**Ex**
```xsd
<?xml version="1.0" encoding="UTF-8"?>
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema">

    <xs:element name="HangHoa">
        <xs:complexType>
            <xs:sequence>
                <xs:element name="MatHang"
                            minOccurs="1"
                            maxOccurs="unbounded">
                    <xs:complexType>
                        <xs:sequence>
                            <xs:element name="MaHang" type="xs:string"/>
                            <xs:element name="TenHang" type="xs:string"/>
                        </xs:sequence>
                    </xs:complexType>
                </xs:element>
            </xs:sequence>
        </xs:complexType>

        <xs:unique name="MaHangKhongTrung">
            <xs:selector xpath="MatHang"/>
            <xs:field xpath="MaHang"/>
        </xs:unique>
    </xs:element>

</xs:schema>
```
*XML hợp lệ*
```xml
<HangHoa>
    <MatHang>
        <MaHang>MH01</MaHang>
        <TenHang>Bút bi</TenHang>
    </MatHang>
    <MatHang>
        <MaHang>MH02</MaHang>
        <TenHang>Vở</TenHang>
    </MatHang>
</HangHoa>
```
*XML không hợp lệ*
```xml
<HangHoa>
    <MatHang>
        <MaHang>MH01</MaHang>
        <TenHang>Bút bi</TenHang>
    </MatHang>
    <MatHang>
        <MaHang>MH01</MaHang>
        <TenHang>Vở</TenHang>
    </MatHang>
</HangHoa>

```
# xs:key (Tương tự unique, nhưng trường khóa bắt buộc phải có giá )
# xs:keyref	(Kiểm tra giá trị tham chiếu phải tồn tại trong một key hoặc unique đã khai báo)
# xs:restriction (giá trị này phải thuộc kiểu X, nhưng bị giới hạn thêm theo các điều kiện bên dưới)
**Syn**
```bash
<xs:restriction base="xs:integer">
```
**Ex**
```xsd
<xs:element name="age">
    <xs:simpleType>
        <xs:restriction base="xs:integer"> <!-- Giá trị phải là số nguyên -->
            <!-- 15 ≤ age ≤ 150 -->
            <xs:minInclusive value="15"/>
            <xs:maxInclusive value="150"/>
        </xs:restriction>
    </xs:simpleType>
</xs:element>
```
```xml
<age>20</age> <!-- ✅ Hợp lệ -->
<age>10</age> <!-- ❌ Không hợp lệ vì nhỏ hơn 15 -->
<age>200</age> <!-- ❌ Không hợp lệ vì lớn hơn 150 -->
<age>abc</age> <!-- ❌ Không hợp lệ vì không phải số nguyên -->
```
## minInclusive / maxInclusive (Giới hạn số và cho phép luôn giá trị biên)
```xsd
<xs:restriction base="xs:integer">
    <xs:minInclusive value="1"/>
    <xs:maxInclusive value="100"/>
</xs:restriction>

<!-- → 1 và 100 đều hợp lệ. -->
```
## minExclusive / maxExclusive (Giới hạn số nhưng không cho phép giá trị biên)
```xsd
<xs:restriction base="xs:integer">
    <xs:minExclusive value="0"/>
    <xs:maxExclusive value="100"/>
</xs:restriction>

<!-- → 1 đến 99 hợp lệ.
→ 0, 100 không hợp lệ. -->
```




5. minLength / maxLength
Giới hạn độ dài chuỗi:

<xs:restriction base="xs:string">
    <xs:minLength value="5"/>
    <xs:maxLength value="20"/>
</xs:restriction>

→ Chuỗi từ 5 đến 20 ký tự.


<xs:restriction base="xs:integer">

→ giới hạn một số nguyên

<xs:restriction base="xs:string">

→ giới hạn một chuỗi.

Nếu đang học XSD để thi/thực hành, chỉ cần nắm chắc restriction + base + pattern + enumeration + min/max là đã bao phủ phần rất quan trọng rồi.
```bash
<xs:simpleType name="UsernameType">
    <xs:restriction base="xs:string">
        <xs:minLength value="5"/>
        <xs:maxLength value="20"/>
    </xs:restriction>
</xs:simpleType>
```


Trong XSD, các yêu cầu này dùng những facet và thuộc tính sau:
Yêu cầu	Tham số XSD	Ý nghĩa
Mã hàng duy nhất	xs:unique	Đảm bảo giá trị mã hàng không trùng nhau trong phạm vi được chọn
Mã hàng tối đa 6 ký tự	xs:maxLength value="6"	Giới hạn độ dài tối đa 6 ký tự
Đơn giá lớn hơn 0	xs:minExclusive value="0"	Giá trị phải lớn hơn 0, không bao gồm 0
Tối đa 4 hóa đơn	maxOccurs="4"	Cho phép tối đa 4 phần tử hóa đơn
Tối đa 10 loại hàng	maxOccurs="10"	Cho phép tối đa 10 phần tử loại hàng
Không hạn chế số mặt hàng	maxOccurs="unbounded"	Cho phép số lượng phần tử không giới hạn
Ví dụ XSD
<!-- Mã hàng: tối đa 6 ký tự -->
<xs:simpleType name="MaHangType">
    <xs:restriction base="xs:string">
        <xs:maxLength value="6"/>
    </xs:restriction>
</xs:simpleType>

<!-- Đơn giá: lớn hơn 0 -->
<xs:simpleType name="DonGiaType">
    <xs:restriction base="xs:decimal">
        <xs:minExclusive value="0"/>
    </xs:restriction>
</xs:simpleType>



Khai báo số lượng phần tử:
<xs:element name="HoaDon"
            type="HoaDonType"
            maxOccurs="4"/>

<xs:element name="LoaiHang"
            type="LoaiHangType"
            maxOccurs="10"/>

<xs:element name="MatHang"
            type="MatHangType"
            maxOccurs="unbounded"/>


Lưu ý: xs:unique phải được khai báo ở cấp phần tử chứa các mã hàng cần kiểm tra, thông qua xs:selector và xs:field. Chỉ khai báo kiểu MaHangType không đảm bảo mã hàng duy nhất.
## xs:pattern (Dùng để bắt giá trị phải khớp biểu thức chính quy)
**Ex: Ví dụ mã sản phẩm phải có dạng ABC-123**
```bash
<xs:simpleType name="ProductCodeType">
    <xs:restriction base="xs:string">
        <xs:pattern value="[A-Z]{3}-[0-9]{3}"/>
    </xs:restriction>
</xs:simpleType>
```