- [XML introduction](#xml-introduction)
- [sax (Nó đọc từng dòng, từng thẻ và báo sự kiện (event) cho chương trình của bạn)](#sax-nó-đọc-từng-dòng-từng-thẻ-và-báo-sự-kiện-event-cho-chương-trình-của-bạn)
  - [ContentHandler](#contenthandler)
  - [make\_parser()](#make_parser)
    - [setContentHandler()](#setcontenthandler)
    - [parse()](#parse)
- [dom (đọc toàn bộ XML vào bộ nhớ, sau đó bạn muốn xem chỗ nào cũng được)](#dom-đọc-toàn-bộ-xml-vào-bộ-nhớ-sau-đó-bạn-muốn-xem-chỗ-nào-cũng-được)
  - [minidom](#minidom)
    - [parse (Đọc file XML)](#parse-đọc-file-xml)
      - [documentElement (Lấy node gốc)](#documentelement-lấy-node-gốc)
        - [tagName](#tagname)
      - [getElementsByTagName()](#getelementsbytagname)
        - [.getAttribute()](#getattribute)
        - [.firstChild.data](#firstchilddata)
      - [.createElement()](#createelement)
        - [.setAttribute()](#setattribute)
      - [createTextNode()](#createtextnode)
        - [.appendChild(text)](#appendchildtext)
      - [removeChild() (Xóa node con)](#removechild-xóa-node-con)
      - [toprettyxml() (Xuất XML ra chuỗi có định dạng đẹp)](#toprettyxml-xuất-xml-ra-chuỗi-có-định-dạng-đẹp)
- [Practices](#practices)
  - [Đọc tất cả thông tin bằng dom](#đọc-tất-cả-thông-tin-bằng-dom)
---
# XML introduction 
**Ex**
```xml
<?xml version="1.0"?>

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
# sax (Nó đọc từng dòng, từng thẻ và báo sự kiện (event) cho chương trình của bạn)
**SAX hoạt động như thế nào?**
```bash
Giả sử parser đọc từ trên xuống.

Đọc đến
    <library> => gọi startElement("library")

Đọc đến
    <book id="1"> => gọi startElement("book")

Đọc đến
    <title> => gọi startElement("title")

Đọc đến
    Python => gọi characters("Python")

Đọc đến
    </title> => gọi endElement("title")

Cứ thế cho tới hết file.

Nói cách khác luồng hoạt động của SAX:
    books.xml
    ↓
    Parser
    ↓
    <book>
    ↓
    startElement()
    ↓
    <title>
    ↓
    startElement()
    ↓
    Python
    ↓
    characters()
    ↓
    </title>
    ↓
    endElement()
    ↓
    ...
    ↓
    Kết thúc XML
Đây là ba hàm quan trọng nhất của SAX.
```
**Muốn dùng SAX cần những gì?**
```bash
Luôn có 2 phần.
    - Parser
        import xml.sax

        parser = xml.sax.make_parser() # Parser chỉ có nhiệm vụ đọc file.

    - Handler # Handler là nơi bạn viết code xử lý.
```
## ContentHandler
**Ex1: Lưu thành object. Đây mới là cách dùng phổ biến**
```bash
class MyHandler(xml.sax.ContentHandler):

    def __init__(self):
        self.book = {}
        self.books = []

    def startElement(self, name, attrs):
        self.current = name

        if name == "book":
            self.book = {
                "id": attrs["id"]
            }

    def characters(self, content):
        text = content.strip()

        if not text:
            return

        self.book[self.current] = text

    def endElement(self, name):
        if name == "book":
            self.books.append(self.book)

handler = MyHandler()
parser.setContentHandler(handler)
parser.parse("books.xml")

print(handler.books)
# [
#     {
#         "id": "1",
#         "title": "Python",
#         "author": "John",
#         "price": "100"
#     },
#     {
#         "id": "2",
#         "title": "Java",
#         "author": "David",
#         "price": "120"
#     }
# ]
```
## make_parser()
### setContentHandler()
### parse()
**Ex**
```xml
<!-- file example -->
<?xml version="1.0"?>

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
```
```python
import xml.sax

class MyHandler(xml.sax.ContentHandler):

    def startElement(self, name, attrs):
        print("Start:", name)

    def endElement(self, name):
        print("End:", name)

parser = xml.sax.make_parser()
parser.setContentHandler(MyHandler())
parser.parse("books.xml")
# Start: library
# Start: book
# Start: title
# End: title
# Start: author
# End: author
# Start: price
# End: price
# End: book
# ...
```
# dom (đọc toàn bộ XML vào bộ nhớ, sau đó bạn muốn xem chỗ nào cũng được)
```bash
Với người mới học, DOM thường dễ học hơn SAX vì cách làm việc rất trực quan.
```
**Ex**
```xml
<?xml version="1.0"?>

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

<!-- DOM sẽ đọc toàn bộ file và tạo thành một cây (Tree) trong bộ nhớ.
Document
│
└── library
      │
      ├── book(id=1)
      │      │
      │      ├── title
      │      ├── author
      │      └── price
      │
      └── book(id=2)
             │
             ├── title
             ├── author
             └── price -->
```
## minidom
### parse (Đọc file XML)
```bash
from xml.dom import minidom

doc = minidom.parse("books.xml")

- Output: doc chính là toàn bộ cây XML.
```
#### documentElement (Lấy node gốc)
##### tagName
**Ex**
```python
root = doc.documentElement

print(root.tagName) # library
```
#### getElementsByTagName()
##### .getAttribute()
##### .firstChild.data
**Ex**
```bash
Document
│
└── library
      │
      ├── book
      │      │
      │      ├── title
      │      ├── author
      │      └── price
      │
      └── book
```
```python
books = doc.getElementsByTagName("book")
# nó sẽ tìm toàn bộ node tên book Sau đó trả về
#  [
#   book1,
#   book2
#  ]

title = books[0].getElementsByTagName("title")[0]

title.firstChild.data = "Python Advanced" # DOM cho phép sửa trực tiếp cây XML trong bộ nhớ.

with open("new.xml", "w") as f: # Ghi lại file
    f.write(doc.toprettyxml())

# <library>
#     <book id="1">
#         <title>Python Advanced</title>
...
```
#### .createElement()
##### .setAttribute()
#### createTextNode()
##### .appendChild(text)
#### removeChild() (Xóa node con)
#### toprettyxml() (Xuất XML ra chuỗi có định dạng đẹp)
# Practices
## Đọc tất cả thông tin bằng dom
```python
from xml.dom import minidom

doc = minidom.parse("books.xml")

books = doc.getElementsByTagName("book")

for book in books:

    id = book.getAttribute("id")

    title = book.getElementsByTagName("title")[0].firstChild.data

    author = book.getElementsByTagName("author")[0].firstChild.data

    price = book.getElementsByTagName("price")[0].firstChild.data

    print(id, title, author, price)

# 1 Python John 100
# 2 Java David 120
```