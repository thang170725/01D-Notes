- [Units](#units)
- [Box](#box)
  - [Height/Width \& max-height \& max-width](#heightwidth--max-height--max-width)
  - [background](#background)
    - [background-attachment](#background-attachment)
    - [background-size](#background-size)
    - [background-position](#background-position)
    - [background-clip](#background-clip)
    - [background-origin](#background-origin)
  - [margin](#margin)
  - [padding](#padding)
  - [outline](#outline)
  - [outline-width](#outline-width)
  - [outline-style](#outline-style)
  - [Position](#position)
  - [resize](#resize)
- [text](#text)
  - [text-indent](#text-indent)
  - [letter-spacing \& line-height \& word-spacing](#letter-spacing--line-height--word-spacing)
  - [white-spacing](#white-spacing)
  - [text-align \& text-align-last](#text-align--text-align-last)
  - [direction](#direction)
  - [vertical-align](#vertical-align)
- [Flexbox](#flexbox)
  - [justify-content \& align-items](#justify-content--align-items)
  - [align-content](#align-content)
  - [flex-flow](#flex-flow)
    - [flex-direction](#flex-direction)
    - [flex-wrap](#flex-wrap)
  - [gap](#gap)
    - [row-gap](#row-gap)
    - [column-gap](#column-gap)
  - [flex-shrink](#flex-shrink)
  - [flex-grow](#flex-grow)
- [Grid](#grid)
  - [grid-template-columns](#grid-template-columns)
  - [grid-template-row](#grid-template-row)
---
# Units
```bash
Xác định đơn vị cho các phần tử.
Đơn vị tuyệt đối (absolute)
    • cm: centimet (2.54cm = 96px)
    • mm: milimet (254mm =96px)
    • in: inch (1in = 96px)
    • px: điểm ảnh, là đơn vị nhỏ nhất
    • pt: (1pt = 4/3px)
    • pc: (1pc >= 20px)
Đơn vị tương đối (relative)
    • %: Là đơn vị tham chiếu tỉ lệ so với một phần tử cha của nó dựa vào kích thước.
    • em: Là đơn vị tham chiếu tỉ lệ so với phần tử cha của nó dựa vào giá trị font-size.
    • rem: Là đơn vị tham chiếu tỉ lệ so với phần tử gốc của một website dựa vào thuộc tính font-size. Biến đổi thuộc tính font-size khi khai báo trong thẻ html.
    • ex: Liên quan đến chiều cao của font chữ hiện tại (hiếm khi được sử dụng).
    • ch: Liên quan đến chiều rộng.
    • vw: Tương đối 1% width của kích thước cửa sổ trình duyệt (viewport).
    • vh: Tương đối 1% height của kích thước cửa sổ trình duyệt (viewport).
    • Vmin: Tương đối 1% của kích thước cửa sổ trình duyệt nhỏ hơn.
    • Vmax: Tương đối 1% của kích thước cửa sổ trình duyệt lớn hơn.
```
**Ex: Thiết lập kích thước cho thẻ div với các đơn vị tuyệt đối**
```html
<div id="div1"></div>
<div id="div2"></div>
<div id="div3"></div>
<div id="div4"></div>
<div id="div5"></div>
<div id="div6"></div>
```
```css
*{
    margin: 0;
}
div{
    background-color: #33ff66;
    display: inline-block;
}
#div1{
    height: 1cm;
    width: 1cm;
}
#div2{
    height: 1mm;
    width: 1mm;
}
#div3{
    height: 1in;
    width: 1in;
}
#div4{
    height: 1px;
    width: 1px;
}
#div5{
    height: 1pt;
    width: 1pt;
}
#div6{
    height: 1pc;
    width: 1pc;
}
```
# Box
## Height/Width & max-height & max-width
```bash
Thiết lập chiều dài, chiều rộng cho khối bao ngoài.
```
## background
```bash
Là cách viết gộp của các thuộc tính trong background.
```
**Syn**
```bash
background: color | image | position | size | repeat | origin | clip | attachment | initial | inherit
```
### background-attachment
```bash
Chỉ định hình ảnh sẽ cố định hay cuộn theo trang web.
```
**Syn**
```bash
background-attachment: value;

- sroll: Hình nền bị cuốn theo khi kéo thanh croll.
- local: Hình nền sẽ bị cuốn theo khi kéo thanh croll.
- fixed: Hình nền sẽ nằm ở một vị trí cố định mặc cho ta kéo thanh croll. Khi lướt có thể đề lên cả phần tử khác.
- initial: Sử dụng giá trị mặc định của nó.
- inherit: Kế thừa phần tử cha của nó.
```
**Ex**
```html
<div></div>
<p>Welcome to HTML - CSS</p>
```
```css
body{
    height: 2000px;
}
div{
    width: 500px;
    height: 500px;
    margin: 30px 20px;
    background-image: url(./image/Hulk.jpg);
    background-size: contain;
    background-attachment: scroll;
}
p{
    margin: 30px 20px;
}
```
### background-size
```bash
Thiết lập kích thước của hình nền.
```
**Syn**
```bash
background-size: value;

- Number + unit:
- contain: đưa tỉ lệ về đúng kích thước và vừa phù hợp với khối bao ngoài
- cover: cho hình ảnh full block có thể bị cắt bớt hình ảnh đi 
```
### background-position
```bash
Thiết lập vị trí của hình nền trong thẻ cha.
```
**Syn**
```bash
background-position: value;

- Top
- Left
- Right
- Bottom
- Center
- …
```
### background-clip 
```bash
- Xác định phạm vi được thiết lập cho phần tử. Chỉ được hiển thị trên website tại vùng đã cài đặt thuộc tính background-clip. 
- Nên thêm tiền tố -webkit cho safari và một số trình duyệt khác.
```
**Syn**
```bash
background-clip: value;

- border-box
- padding-box
- content-box
- text
- initial
- inherit
- …
```
**Ex**
```html
<div>WelCome to HaNoi</div>
```
```css
div{
    font-family: sans-serif;
    font-size: 30px;
    font-weight: 900;
    background-image: linear-gradient(to right, #ff0000, #00ff00);
    background-clip: text;
    color: transparent;
}
```
### background-origin
```bash
Thiết lập phạm vi mà hình nền sẽ xuất hiện. Phần được hiển thị sẽ tính từ vùng cài đặt background-origin trở vào trong.
```
**Syn**
```bash
background-origin: value;

- border-box
- padding-box
- content-box
- initial
- inherit
```
## margin
```bash
- Nếu có 4 giá trị thì các giá trị lần lượt là top, right, bottom, left.
- Nếu có 3 giá trị thì các giá trị lần lượt là top, right-left, bottom.
- Nếu có 2 giá trị thì các giá trị lần lượt là top-bottom, right-left.
- Nếu có 1 giá trị thì giá trị đó là top-right-bottom-left.
```
## padding
```bash
Chỉ định khoảng đệm thêm vào cho content.
```
## outline
```bash
- Là một đường kẻ xung quanh phần tử, nằm bên ngoài border để làm nổi bật phần tử. 
- có thể thiết lập các giá trị giống với border. Nó có thể đè lên các phần tử khác. 
- Ngoài ra outline không là một phần trong kích thước của phần tử. độ rộng và chiều cao không bị ảnh hưởng bởi độ rộng của outline.
```
**Syn**
```bash
outline: outline-width | outline-style | outline-color
```
**Ex**
```html
<div></div>
```
```css
div{
    width: 50px;
    height: 50px;
    outline: 2px solid;
    border: 2px solid #ff0000;
    margin: 20px;
}
```
## outline-width
```bash
Xác định độ rộng.
```
## outline-style
```bash
Xác định kiểu đường viền.
```
**Syn**
```bash
outline-style: value;

- Dotter
- Dashed
- Solid
- Double
- Groove
- Ridge
- Inset 
- Outset
- None
- Hidden
```
## Position
```bash
- Chỉ định loại phương pháp định vị được sử dụng cho một phần tử.
```
**Syn**
```bash
position: value;

- static: Mặc định, sẽ hiển thị theo đúng thứ tự của nó.
- relative: Định vị tuyệt đối, lúc này các thẻ bên trong coi là thẻ cha.
- absolute: Định vị tương đối theo thẻ cha.
- fixed: Định vị tương đối cho cửa sổ trình duyệt, khi kéo thanh cuộn nó không bị ẩn đi.
- Sticky: Nếu đi kèm với top: 0 khi scroll sẽ dính ở trên đầu website.
- inherit: Thừa hưởng thuộc tính của phần tử cha.
```
**Ex**
```html
<div></div>
```
```css
div{
    width: 100px;
    height: 100px;
    background: red;
    position: fixed;
    top: 0; /*khi dùng fix có thể di chuyển bằng, top, left, ... */
}
```
## resize
```bash
Định dạng cho vùng nội dung người dùng có thể thay đổi kích thước. Phải sử dụng cùng overflow đối với các thẻ khác. Sử dụng cùng thẻ textarea thì không cần overflow.
```
**Syn**
```bash
resize: value;

- both: Người dùng có thể thay đổi cả chiều cao và chiều rộng của thành phần.
- none: Người dùng không được thay đổi.
- horizontal: Người dùng có thể thay đổi chiều ngang.
- vertical: Người dùng có thể thay đổi chiều dọc.
```
# text
## text-indent
```bash
Định nghĩa vị trí xuất hiện ở đầu, giống như lùi vào đầu dòng mấy px.
```
## letter-spacing & line-height & word-spacing
```bash
- letter-spacing  : khoảng cách giữa các ký tự trong chữ.
- line-height     : khoảng cách giữa các dòng.
- word-spacing    : Để xác định khoảng cách giữa các chữ.
```
**Syn: letter-spacing**
```bash
letter-spacing: value;

- normal: Không thay đổi khoảng cách giữa các kí tự.
- number + unit: Tăng hoặc giảm khoảng cách giữa các kí tự + đơn vị.
- inherit: Kế thừa thuộc tính của thành phần cha.
```
**Syn: line-height**
```bash
line-height: value;

- normal: Không thay đổi khoảng cách.
- Number + unit: Tăng hoặc giảm khoảng cách giữa các dòng có thể là số tự nhiên hay thập phân có thể có đơn vị hoặc không.
- inherit: Thừa hưởng thuộc tính cha của nó.
```
## white-spacing
```bash
Chỉ định cách xử lý khoảng trắng bên trong một phần tử.
```
**Syn**
```bash
white-spacing: value;

- normal: Khoảng trắng sẽ xuất hiện bình thường.
- noswap: Văn bản sẽ hiển thị trên cùng một hàng chỉ xuống hàng khi gặp <br>.
- pre: Văn bản sẽ hiển thị trên cùng một hàng, chỉ ngắt dòng tại đoạn văn bản sử dụng thẻ pre.
- pre-line: Văn bản sẽ tự động bao lại khi cần thiết và xuống hàng.
- pre-swap: Văn bản sẽ tự động bao lại khi cần thiết và xuống hàng.
- inherit: Kế thừa thành phần từ thuộc tính cha.
```
## text-align & text-align-last
```bash
- text-align        : Để căn chỉnh content của một phần tử.
- text-align-last   : Căn chỉnh dòng cuối cùng của các đoạn văn bản.
```
**Syn: text-align**
```bash
text-align: value;

- center: Căn giữa.
- left: Căn trái.
- right: Căn phải.
- justify: Căn đều so với lề trái và lề phải
```
**Syn: text-align-last**
```bash
text-align-last: value;

- auto: Dòng cuối cùng căn đều và căn trái.
- left: Căn dòng cuối sang trái.
- right: Căn dòng cuối sang phải.
- center: Căn dòng cuối ra giữa.
- justify: Căn dòng cuối san đều ra 1 dòng.
- start: Căn dòng cuối sang trái.
- end: Căn dòng cuối sang phải.
- initial: Lấy giá trị mặc định.
- inherit: Lấy giá trị của phần tử cha.
```
## direction
```bash
Thiết lập hướng của văn bản.
```
**Syn**
```bash
direction: value;

- ltr: Hướng văn bản từ trái sang phải.
- rtl: Hướng văn bản từ phải sang trái.
```
## vertical-align
```bash
Để căn chỉnh content khi nội dung được lồng ghép vào nhau. Chỉ hoạt động với image hoặc thẻ bao ngoài có thuộc tính display: table-cell.
```
**Syn**
```bash
vertical-align: values;

- auto
- baseline: Mặc đinh.
- sub: Căn chỉnh phần tử xuống dưới đường cơ sở.
- super: Căn chỉnh phần tử lên trên đường cơ sở.
- top: Căn chỉnh phần tử lên trên cùng của dòng chữ.
- middle: Căn chỉnh phần tử vào giữa dòng chữ.
- bottom: Căn chỉnh phần tử xuống dưới cùng của dòng chữ. 
- Text-top
- Text-bottom
- Inherit
```
# Flexbox
## justify-content & align-items
```bash
- justify-content : Để căn chỉnh các thẻ con theo chiều ngang.
- align-items     : căn intem trong 1 hàng theo chiều dọc
```
**Syn1: align-items**
```bash
align-items: value;

- start (flex-start): Căn theo vị trí bắt đầu (hàng bắt đầu)
- end (flex-end): Căn theo vị trí kết thúc (hàng kết thúc)
- center: Căn vào giữa
- stretch: Căng ra theo chiều dọc
- baseline: căn ở đường cơ sở của containter
```
**Ex1: align-items**
```html
<div>
 <div class="box1">Box1</div>
 <div class="box2">Box2</div>
 <div class="box3">Box3</div>
</div>
```
```css
body > div{
      background-color: #a8a8;
      display: flex;
      width: 100%;
      height: 500px;
      justify-content: center;
      align-items: flex-start;
}
body > div > div{
     background-color: #fdd;
}
.box1{
      background-color: transparent;
}
```
## align-content 
```bash
- Dùng để căn dọc item khi container có nhiều hàng item (áp dụng khi có flex-wrap: wrap)
- Có thể áp dụng vào để tạo menu dọc
```
**Syn**
```bash
align-content: value;

- Center: căn ra giữa 
- Stretch
- Flex-start
- Flex-end
- Space-around
- Space-between
- Space-evently
```
**Ex**
```html
<div id="main">
  <div style="background-color:coral;"></div>
  <div style="background-color:lightblue;"></div>
  <div style="background-color:pink;"></div>
</div>
```
```css
#main {
  width: 90px;
  height: 300px;
  border: 1px solid #c3c3c3;
  display: flex;
  flex-wrap: wrap;
  align-content: center;
}

#main div{
  width: 50px;
  height: 80px;
}
```
## flex-flow
```bash
Là thuộc tính gộp của flex-direction, flex-wrap.
```
**Syn** 
```bash
flex-flow: direction wrap;
```
### flex-direction
```bash
Chỉ định hướng của các mục linh hoạt.
```
**Syn**
```bash
flex-direction: value;

- row: Các thẻ được sắp xếp theo chiều ngang, hướng từ trái qua phải.
- row-reverse: Các thẻ được sắp xếp theo chiều ngang, hướng từ phải qua trái.
- column: Các mục linh hoạt được hiển thị theo chiều dọc, dưới dạng cột.
- column-reverse: Tương tự như cột nhưng theo thứu tự ngược lại.
- initial: Sử dụng lại giá trị mặc định.
- inherit: Kế thừa thuộc tính của phần tử cha.
```
### flex-wrap
```bash
Khi thay đổi kích thước trình duyệt, tự động xuống dòng khi kích thước trình duyệt nhỏ lại.
```
**Syn**
```bash
flex-wrap: value;

- nowrap: Không xuống dòng.
- wrap: Tự động xuống dòng.
- wrap-reverse
- initial
- inherit
```
**Ex**
```bash
<body>
  <div></div>
  <div></div>
  <div></div>
</body>
```
```css
body{
    display: flex;
    flex-wrap: wrap;
}
div{
    background-color: #f00;
    width: 300px;
    height: 300px;
    margin: 50px;
}
```
## gap
```bash
Để tạo khoảng cách giữa các box.
```
### row-gap
```bash
Chỉ định khoảng cách giữa các hàng trong bố cục dạng lưới.
```
### column-gap
```bash
Xác định kích thước khoảng cách theo cột.
```
**Syn**
```bash
column-gap: number + unit
```
## flex-shrink
## flex-grow
```bash
Chỉ định mức độ tăng mà mục đó sẽ tăng lên so mới các mục linh hoạt còn lại bên trong cùng một vùng chứa. 
```
**Ex**
```html
<div id="main">
  <div style="background-color:coral;"></div>
  <div style="background-color:lightblue;"></div>
  <div style="background-color:khaki;"></div>
  <div style="background-color:pink;"></div>
  <div style="background-color:lightgrey;"></div>
</div>
```
```css
#main {
  width: 350px;
  height: 100px;
  border: 1px solid #c3c3c3;
  display: flex;
}

#main div:nth-of-type(1) {flex-grow: 1;}
#main div:nth-of-type(2) {flex-grow: 2;}
#main div:nth-of-type(3) {flex-grow: 2;}
#main div:nth-of-type(4) {flex-grow: 1;}
#main div:nth-of-type(5) {flex-grow: 1;}
```
# Grid
```bash
- Tạo ra bố cục dạng lưới với các hàng và cột, giúp thiết kế web đễ dàng hơn. Mặc định width: 100% 
- Có thể điều chỉnh kích thước khoảng cách bằng cách sử dụng một trong các thuộc tính sau. Vẫn có thể sử dụng được các thuộc tính flexbox
```
**Syn**
```bash
display: grid;
```
**Ex**
```html
<body>
    <div>
        <div></div>
        <div></div>
        <div></div>
    </div>
</body>
```
```css
body > div{
    display: grid;
}
div > div{
    width: 200px;
    height: 50px;
    margin: 20px;
    background-color: #f00;
}
```
## grid-template-columns
```bash
Tạo ra số cột và kích thước giữa các cột. Các giá trị sẽ tương ứng với số cột và kích thước chiều rộng của nó từ trái sang phải.
```
**Ex**
```html
<body>
    <div>
        <div></div>
        <div></div>
        <div></div>
    </div>
</body>
```
```css
body > div{
    display: grid;
    grid-template-columns: 200px 200px 200px;
}
div > div{
    width: 150px;
    height: 50px;
    margin: 20px;
    background-color: #f00;
}
```
## grid-template-row
```bash
Tạo ra số hàng và kích thước giữa các hàng. Các giá trị sẽ tương ứng với số hàng và kích thước chiều rộng của nó từ trên xuống dưới.
```
