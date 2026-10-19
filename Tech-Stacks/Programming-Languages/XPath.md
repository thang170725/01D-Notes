- [XPath](#xpath)
  - [\<	(Nhỏ hơn)](#nhỏ-hơn)
  - [\&gt (Lớn hơn)](#gt-lớn-hơn)
  - [\<= (Nhỏ hơn hoặc bằng)](#-nhỏ-hơn-hoặc-bằng)
  - [\>= (Lớn hơn hoặc bằng)](#-lớn-hơn-hoặc-bằng)
  - [= (Bằng)](#-bằng)
  - [!= (Khác)](#-khác)
  - [\& (\&)](#-)
  - [" (Dấu nháy kép)](#-dấu-nháy-kép)
  - [' (Dấu nháy đơn)](#-dấu-nháy-đơn)
  - [and (Và)](#and-và)
  - [or (Hoặc)](#or-hoặc)
  - [not() (Phủ định)](#not-phủ-định)
  - [+ (Cộng)](#-cộng)
  - [- (Trừ)](#--trừ)
  - [\* (Nhân)](#-nhân)
  - [div (Chia)](#div-chia)
  - [mod (Chia lấy dư)](#mod-chia-lấy-dư)
- [XPath](#xpath-1)
---
Có, XPath là một ngôn ngữ, chính xác hơn là ngôn ngữ truy vấn và chọn nút trong tài liệu XML/HTML (XML Path Language).

XPath thường được sử dụng trong web scraping, tự động hóa trình duyệt với Selenium hoặc Playwright, và kiểm thử giao diện web.
1. XPath dùng để làm gì?
XPath giúp bạn xác định một phần tử cụ thể trong cấu trúc HTML hoặc XML dựa trên vị trí, thuộc tính, nội dung hoặc mối quan hệ giữa các phần tử.

Ví dụ HTML:
<div class="product">
    <h2>Laptop Dell</h2>
    <span class="price">15000000</span>
</div>


Một số biểu thức XPath tương ứng:
XPath	Ý nghĩa
//h2	Chọn tất cả thẻ h2
//div[@class='product']	Chọn div có thuộc tính class="product"
//span[@class='price']	Chọn span có class là price
//h2/text()	Lấy nội dung văn bản trực tiếp của thẻ h2
//div[@class='product']//span	Chọn các thẻ span nằm bên trong div có class product
2. XPath có giống Python hay JavaScript không?
Không hoàn toàn. XPath và Python/JavaScript có mục đích khác nhau.
Tiêu chí	XPath	Python
Bản chất	Ngôn ngữ truy vấn	Ngôn ngữ lập trình
Mục đích	Tìm và chọn các nút trong tài liệu	Xây dựng chương trình, xử lý dữ liệu, tự động hóa...
Cấu trúc	Biểu thức truy vấn	Biến, hàm, vòng lặp, điều kiện...
Ví dụ	//a[@href]	print("Hello")
XPath có cú pháp và quy tắc riêng, nhưng không phải ngôn ngữ lập trình đa dụng như Python.
3. XPath có những phiên bản nào?
- XPath 1.0: Phiên bản phổ biến trong Selenium và nhiều công cụ xử lý HTML/XML.
- XPath 2.0: Bổ sung nhiều kiểu dữ liệu, hàm và khả năng xử lý biểu thức.
- XPath 3.0 và 3.1: Mở rộng khả năng xử lý dữ liệu và biểu thức phức tạp.
Lưu ý: Không phải công cụ nào cũng hỗ trợ tất cả phiên bản. Trình duyệt thường sử dụng XPath 1.0 khi truy vấn DOM bằng API document.evaluate().

Tóm lại: XPath là một ngôn ngữ truy vấn chuyên biệt (DSL — Domain-Specific Language), được thiết kế để tìm kiếm và lựa chọn các phần tử trong cấu trúc XML hoặc HTML, chứ không phải ngôn ngữ lập trình đa dụng.
# XPath
## &lt;	(Nhỏ hơn)
**Ex**
```bash
ngaycong &lt; 20 # ngaycong < 20
```
## &gt (Lớn hơn)	
```bash
ngaycong &gt; 20 # ngaycong > 20
```
## &lt;= (Nhỏ hơn hoặc bằng)	
```bash
ngaycong &lt;= 20 # ngaycong <= 20
``` 
## &gt;= (Lớn hơn hoặc bằng)
```bash
ngaycong &gt;= 20 # ngaycong >= 20
```
## = (Bằng)	
```bash
ngaycong = 20
```
## != (Khác)	
```bash
ngaycong != 20
```
## &amp; (&)
## &quot; (Dấu nháy kép)
## &apos; (Dấu nháy đơn)
## and (Và)	
```bash
ngaycong > 20 and ngaycong <= 25
```
## or (Hoặc)
```bash
ngaycong < 10 or ngaycong > 25
```
## not() (Phủ định)
```bash
not(ngaycong = 0)
```
## + (Cộng)	
```bash
ngaycong + 5
```
## - (Trừ)
```bash
ngaycong - 20
```
## * (Nhân)
```bash
ngaycong * 150000
```
## div (Chia)
```bash
ngaycong div 2
```
## mod (Chia lấy dư)
```bash
ngaycong mod 2
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