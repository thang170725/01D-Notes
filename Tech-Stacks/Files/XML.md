- [XML introduction](#xml-introduction)
- [XSD (XML Schema Definition là file dùng để quy định XML được phép có cấu trúc và dữ liệu như thế nào)](#xsd-xml-schema-definition-là-file-dùng-để-quy-định-xml-được-phép-có-cấu-trúc-và-dữ-liệu-như-thế-nào)
  - [complexType (Dùng khi một element có cấu trúc bên trong, ví dụ chứa nhiều element con)](#complextype-dùng-khi-một-element-có-cấu-trúc-bên-trong-ví-dụ-chứa-nhiều-element-con)
  - [sequence (Các element phải xuất hiện đúng thứ tự)](#sequence-các-element-phải-xuất-hiện-đúng-thứ-tự)
  - [choice (Chỉ được chọn một trong các element)](#choice-chỉ-được-chọn-một-trong-các-element)
  - [all (Các element có thể xuất hiện theo bất kỳ thứ tự nào)](#all-các-element-có-thể-xuất-hiện-theo-bất-kỳ-thứ-tự-nào)
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
- [xs:attribute](#xsattribute)
- [value](#value)
- [xs:restriction](#xsrestriction)
- [enumeration](#enumeration)
- [simpleType](#simpletype)
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
# XSD (XML Schema Definition là file dùng để quy định XML được phép có cấu trúc và dữ liệu như thế nào)
```bash
Bạn có thể hình dung:
    - XML = Dữ liệu
    - XSD = Luật quy định dữ liệu
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

Nó nói rằng:
    person phải có name
    name phải là string
    age phải là integer
    name phải đứng trước age
```
*Nếu XML viết*
```xml
<person>
    <name>An</name>
    <age>abc</age>
</person>

❌ Sai vì age yêu cầu xs:integer nhưng "abc" không phải số nguyên.
```
**XSD dùng để làm gì?**
```bash
Chủ yếu để kiểm tra (validate) XML có đúng cấu trúc và dữ liệu hay không.

Ví dụ XSD có thể quy định:

age       → số nguyên từ 15 đến 150
tel       → đúng 10 chữ số
gender    → chỉ "male" hoặc "female"
name      → bắt buộc phải có
email     → kiểu string

Đúng với những gì bạn đang học:

<xs:restriction>

dùng để đặt thêm các giới hạn cho dữ liệu.

Nhớ ngắn gọn để đi học/thi
XSD (XML Schema Definition) là ngôn ngữ dùng để định nghĩa cấu trúc, kiểu dữ liệu và các ràng buộc của tài liệu XML, giúp kiểm tra XML có hợp lệ hay không.
```
**Syn: Một file .xsd thường có dạng**
```bash
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
## Datatype (kiểu dữ liệu trong xsd)
### xs:string	
**Ex**
```bash
"Hello"
```
### xs:integer | xs:int
```bash
100
```
### xs:decimal	
```bash
<xs:element name="salary" type="xs:decimal"/>
# 10.5
```
### xs:float	
```bash
10.5
```
### xs:double	
```bash
10.5
```
### xs:boolean	
```bash
<xs:element name="isActive" type="xs:boolean"/>
# true / false
```
### xs:date	
```bash
<xs:element name="birthDate" type="xs:date"/>
# 2026-09-29
```
### xs:dateTime	
```bash
2026-09-29T10:30:00
```
### xs:time	
```bash
10:30:00
```
# xs:attribute
**Ex**
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

# XML:
<person id="100">
    <name>An</name>
</person>

use thường có: use="required" hoặc: use="optional"
```
# value
```bash
Đây là điểm mạnh của XSD: không chỉ nói kiểu dữ liệu, mà còn giới hạn giá trị.
```
**Ex1: Ví dụ tuổi phải từ 18 đến 100**
```bash
<xs:simpleType name="AgeType">
    <xs:restriction base="xs:int">
        <xs:minInclusive value="18"/>
        <xs:maxInclusive value="100"/>
    </xs:restriction>
</xs:simpleType>

Sau đó: <xs:element name="age" type="AgeType"/>
```
**Ex2: Ví dụ mã sản phẩm phải có dạng ABC-123**
```bash
<xs:simpleType name="ProductCodeType">
    <xs:restriction base="xs:string">
        <xs:pattern value="[A-Z]{3}-[0-9]{3}"/>
    </xs:restriction>
</xs:simpleType>
```
# xs:restriction
xs:restriction dùng để giới hạn/ràng buộc giá trị của một kiểu dữ liệu trong XSD.

Hiểu đơn giản:

xs:restriction = "Giá trị này phải thuộc kiểu X, nhưng bị giới hạn thêm theo các điều kiện bên dưới."

Ví dụ ngay trong XSD của bạn
Bạn có:

<xs:element name="age">
    <xs:simpleType>
        <xs:restriction base="xs:integer">
            <xs:minInclusive value="15"/>
            <xs:maxInclusive value="150"/>
        </xs:restriction>
    </xs:simpleType>
</xs:element>

Ở đây:

base="xs:integer"
        ↓
Giá trị phải là số nguyên
        ↓
restriction
        ↓
15 ≤ age ≤ 150

Vì vậy:

<age>20</age>

✅ Hợp lệ.

<age>10</age>

❌ Không hợp lệ vì nhỏ hơn 15.

<age>200</age>

❌ Không hợp lệ vì lớn hơn 150.

<age>abc</age>

❌ Không hợp lệ vì không phải số nguyên.

Một số restriction thường gặp
1. minInclusive / maxInclusive
Giới hạn số và cho phép luôn giá trị biên:

<xs:restriction base="xs:integer">
    <xs:minInclusive value="1"/>
    <xs:maxInclusive value="100"/>
</xs:restriction>

→ 1 và 100 đều hợp lệ.

2. minExclusive / maxExclusive
Giới hạn số nhưng không cho phép giá trị biên:

<xs:restriction base="xs:integer">
    <xs:minExclusive value="0"/>
    <xs:maxExclusive value="100"/>
</xs:restriction>

→ 1 đến 99 hợp lệ.

→ 0, 100 không hợp lệ.

3. pattern
Dùng để bắt giá trị phải khớp biểu thức mẫu (regex).

Ví dụ số điện thoại 10 chữ số:

<xs:restriction base="xs:string">
    <xs:pattern value="[0-9]{10}"/>
</xs:restriction>

0123456789   ✅
0987654321   ✅
12345        ❌
012345678a   ❌

4. enumeration
Giới hạn chỉ được phép một số giá trị nhất định:

<xs:restriction base="xs:string">
    <xs:enumeration value="male"/>
    <xs:enumeration value="female"/>
</xs:restriction>

→ Chỉ được:

male      ✅
female    ✅
other     ❌

5. minLength / maxLength
Giới hạn độ dài chuỗi:

<xs:restriction base="xs:string">
    <xs:minLength value="5"/>
    <xs:maxLength value="20"/>
</xs:restriction>

→ Chuỗi từ 5 đến 20 ký tự.

Tóm lại
Bạn có thể nhớ thế này:

xs:restriction
       │
       ├── minInclusive   → số ≥ ...
       ├── maxInclusive   → số ≤ ...
       ├── minExclusive   → số > ...
       ├── maxExclusive   → số < ...
       ├── pattern        → phải khớp mẫu
       ├── enumeration    → chỉ được chọn các giá trị cho trước
       ├── minLength      → độ dài tối thiểu
       └── maxLength      → độ dài tối đa

base cho biết kiểu dữ liệu gốc mà bạn muốn giới hạn:

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
# enumeration
# simpleType
