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
# .sax (Nó đọc từng dòng, từng thẻ và báo sự kiện event cho chương trình của bạn)
**SAX hoạt động như thế nào?**
```bash
Giả sử parser đọc từ trên xuống.
  Đọc đến: <library> => gọi startElement("library")
  Đọc đến: <book id="1"> => gọi startElement("book")
  Đọc đến: <title> => gọi startElement("title")
  Nếu thẻ có nội dung => gọi characters("Python")
  Đọc đến: </title> => gọi endElement("title")
  ...
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
## make_parser() (khởi tạo một máy đọc XML) 
```bash
Sau khi có parser, bạn mới gán ContentHandler và yêu cầu parser đọc file XML.
```
**Syn**
```bash
import xml.sax

parser = xml.sax.make_parser() # Lúc này parser là một đối tượng có nhiệm vụ đọc XML
```
**Quy trình sử dụng**
```bash
Thông thường sẽ có 3 bước:
  1. Tạo parser
        ↓
  2. Gán ContentHandler
        ↓
  3. Đọc file XML

Tương ứng với code:
  parser = xml.sax.make_parser()
  parser.setContentHandler(MyHandler())
  parser.parse("books.xml")
```
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

- Output: <xml.dom.minidom.Document object at 0x00000221F9ECB410>.
  + doc chính là toàn bộ cây XML.
```
#### documentElement (Lấy node gốc)
##### tagName
**Ex**
```python
root = doc.documentElement

print(root.tagName) # library
```
#### getElementsByTagName()
##### .getAttribute() (lấy thuộc tính của thẻ)
Trong xml.dom.minidom, để lấy thuộc tính (attribute) của một thẻ, dùng:

element.getAttribute("tên_thuộc_tính")
Cú pháp
value = element.getAttribute(attribute_name)
element: node XML (ví dụ <project>).
attribute_name: tên thuộc tính ("id", "name",...).
Ví dụ

XML:

<projects>
    <project id="P01">
        <employee>
            <hours>20</hours>
        </employee>
    </project>

    <project id="P02">
        <employee>
            <hours>35</hours>
        </employee>
    </project>
</projects>

Python:

from xml.dom import minidom

doc = minidom.parse("lession4.xml")

projects = doc.getElementsByTagName("project")

for project in projects:
    print(project.getAttribute("id"))
Kết quả
P01
P02
Kết hợp với getElementsByTagName()
projects = self.doc.getElementsByTagName("project")

for project in projects:
    project_id = project.getAttribute("id")
    print(project_id)
Nếu muốn sửa thuộc tính

Dùng:

project.setAttribute("id", "P100")

Ví dụ:

project = doc.getElementsByTagName("project")[0]

project.setAttribute("id", "P100")

XML sẽ từ:

<project id="P01">

thành

<project id="P100">
Các hàm làm việc với thuộc tính
Hàm	Chức năng
getAttribute("id")	Lấy giá trị thuộc tính
setAttribute("id", "P01")	Thêm hoặc sửa thuộc tính
hasAttribute("id")	Kiểm tra có thuộc tính hay không
removeAttribute("id")	Xóa thuộc tính

Đối với XML có dạng:

<project id="P01">

thì để lấy "P01" bạn luôn dùng:

project.getAttribute("id")

Đây là cách chuẩn trong xml.dom.minidom.
##### .firstChild
###### .data
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
#### .createElement() (tạo thẻ mới trong cây XML)
```bash
Muốn xuất hiện trong XML, bạn phải dùng appendChild().
```
**Syn**
```bash
element = document.createElement(tagName)

- Input:
  + document: đối tượng Document (thường là self.doc).
  + tagName: tên thẻ muốn tạo ("book", "title", "author"...).
- Output: Giá trị trả về là một đối tượng Element.
```
##### .tagName
**Ex1: Tạo một thẻ <book>**
```python
from xml.dom import minidom

doc = minidom.Document()

book = doc.createElement("book")

print(book.tagName) # book
# Lúc này trong bộ nhớ đã có: <book/>
# Nhưng vì chưa gắn vào cây XML nên chưa thể lưu ra file.
```
#### .createTextNode() (tạo dữ liệu)
**Ex: Tạo thẻ có nội dung**
```python
from xml.dom import minidom

doc = minidom.Document()

title = doc.createElement("title")

text = doc.createTextNode("Python Programming")

title.appendChild(text)

print(title.toprettyxml())
# <title>Python Programming</title>
```
##### .setAttribute()
##### .appendChild() (ghép các node lại với nhau) 
**Ex: Tạo một quyển sách**
```python
from xml.dom import minidom

doc = minidom.Document()
book = doc.createElement("book")

title = doc.createElement("title")
title.appendChild(doc.createTextNode("Python"))

author = doc.createElement("author")
author.appendChild(doc.createTextNode("John"))

book.appendChild(title)
book.appendChild(author)

print(book.toprettyxml())
# <book>
#	  <title>Python</title>
#	  <author>John</author>
# </book>
```
**Ex2: Thêm vào XML gốc**
```python
from xml.dom import minidom

doc = minidom.parse("lession1.xml")

library = doc.documentElement

book = doc.createElement("book")

title = doc.createElement("title")
title.appendChild(doc.createTextNode("Machine Learning"))

book.appendChild(title)

library.appendChild(book)

print(doc.toprettyxml())
# <?xml version="1.0" ?>
# <library>
#    <book>
#        <title>Machine Learning</title>
#    </book>
# </library>
```
#### removeChild() (Xóa node con)
#### toprettyxml() (Xuất XML ra chuỗi có định dạng đẹp)
# Practices
## Đọc tất cả thông tin bằng sax
```python
import xml
import xml.sax

class MyHandler(xml.sax.ContentHandler):
    def __init__(self):
        self.curent = ""
        self.book = {}
        self.books = []
    
    def startElement(self, name, attrs):
        self.current = name

        if name == "book":
            self.book = {}
            
    
    def characters(self, content):
        content = content.strip()

        if not content:
            return
        
        if self.current == "title":
            self.book["title"] = content

        elif self.current == "author":
            self.book["author"] = content

        elif self.current == "year":
            self.book["year"] = content
    
    def endElement(self, name):
        if name == 'book':
            self.books.append(self.book)
        
        self.current = ""

if __name__ == '__main__':
    handler = MyHandler()

    parser = xml.sax.make_parser()
    parser.setContentHandler(handler)
    parser.parse('lession1.xml')

    print(handler.books)
# [{'title': 'Python Programming', 'author': 'John Doe', 'year': '2020'}, {'title': 'Data Science with Python', 'author': 'Jane Smith', 'year': '2021'}]
```
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
