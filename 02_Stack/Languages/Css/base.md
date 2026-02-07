- [Cấu trúc](#cấu-trúc)
---
# Cấu trúc
```bash
- layout-spacing.md     # Bố cục & vị trí 
- typograpy-color.md    # Trang trí màu sác, diện mạo
- visual-style.md       # Trang trí bề mặt
- interaction-motion.md # Trạng thái động & biến đổi không gian
- practice_cases.md     # code mẫu tổng hợp
```
# Ways CSS
```bash
- inline: Viết thẳng vào thẻ html thông qua thuộc tính style=” …”.
- external: Viết vào file css riêng rồi link vào html. (khuyến cáo sử dụng).
- internal: Viết vào thẻ <head> … </head> thông qua thẻ <style> … </style> trong file html.
```

word-Wrap 
Cho phép đoạn text xuống hàng cho dù chữ đó dài cỡ nào đi nữa.
Cú pháp:
    • word-wrap: Normal | break-word | initial | inherit;
    • normal: Trạng thái mặc định, tức là hiển thị theo mặc định của trình duyệt.
    • break-word: Sẽ nhảy xuống hàng nếu chữ quá dài.
    • initial: Trở về trang thái mặc định.
    • inherit: Kế thừa giá trị từ thẻ HTML cha.
word-Break
Có tác dụng xử lý xuống hàng, tức là bạn có thể cho một chuỗi hiển thị và xuống hàng tại bất kì vị trí nào miễn là nó đã hiển thị full width.
Cú pháp: 
word-break: normal | break-all | keep-all | initial | inherit;
normal: Trạng thái mặc định, tức là sẽ dừng xuống hàng theo mặc định.
break-all: Có thể xuống hàng bất kì lúc nào khi nó đã hiển thị full width.
keep-all: Xuống hàng nếu chữ hiển thị sẽ bị tràn (overflow).
initial: Trở về trang thái mặc định.
inherit: Kế thừa giá trị từ thẻ HTML cha.
text-transform
Thiết lập chữ in hoa hay thường.
value:
    • uppercase: Thiết lập chữ in.
    • lowercase: Thiết lập chữ thường.
    • none: Không thiết lập gì cả.
Text spacing
text-indent
Định nghĩa vị trí xuất hiện ở đầu, giống như lùi vào đầu dòng mấy px.
value: number + unit
letter-spacing 
Tăng hoặc giảm khoảng cách giữa các ký tự trong chữ.
Cú pháp:
letter-spacing: value;
value:
    • normal: Không thay đổi khoảng cách giữa các kí tự.
    • number + unit: Tăng hoặc giảm khoảng cách giữa các kí tự + đơn vị.
    • inherit: Kế thừa thuộc tính của thành phần cha.
line-height
Căn khoảng cách giữa các dòng.
value:
    • normal: Không thay đổi khoảng cách.
    • Number + unit: Tăng hoặc giảm khoảng cách giữa các dòng có thể là số tự nhiên hay thập phân có thể có đơn vị hoặc không.
    • inherit: Thừa hưởng thuộc tính cha của nó.
word-spacing
Để xác định khoảng cách giữa các chữ.
value: number + unit;
white-spacing
Chỉ định cách xử lý khoảng trắng bên trong một phần tử.
value:
    • normal: Khoảng trắng sẽ xuất hiện bình thường.
    • noswap: Văn bản sẽ hiển thị trên cùng một hàng chỉ xuống hàng khi gặp <br>.
    • pre: Văn bản sẽ hiển thị trên cùng một hàng, chỉ ngắt dòng tại đoạn văn bản sử dụng thẻ pre.
    • pre-line: Văn bản sẽ tự động bao lại khi cần thiết và xuống hàng.
    • pre-swap: Văn bản sẽ tự động bao lại khi cần thiết và xuống hàng.
    • inherit: Kế thừa thành phần từ thuộc tính cha.
text-shadow 
Để tạo ra hiệu ứng đổ bóng cho chữ.

Cú pháp:
text-shadow: h-shadow | v-shadow | blur-radius | color | none | initial | inherit;
    • h-shadow: Vị trí bóng ngang so với chữ, số âm sẽ đẩy lên trên và số dương sẽ đẩy xuống dưới.
    • v-shadow: Vị trí bóng dọc so với chứ, số âm sẽ đẩy lui phía sau và số dương sẽ đẩy tới phía trước.
    • blur-radius: Độ nhòe của chữ bóng, tính bằng pixel.
    • color: Màu sắc của bóng, chấp nhận các.
Nếu bạn muốn shadow có nhiều màu sắc thì hãy bổ sụng thêm shadow cho nó và chúng cách nhau bởi dấu phẩy.
CSS fonts
Cú pháp:
font: style | variant | weight | size/height | family;
font-family 
Có thể lấy font chữ ở: googlefont
Generic family
Font family
Serif
ít nét trang trí (chân chữ) vượt ra ngoài thân chữ.
Times New Roman
Georgia
Palatino
Baskerville
Sans-serif
Nhóm font không sử dụng nét trang trí (không chân)
Arial
Arial Black
Verdana
Tahoma
Impact
Gill Sans
Monospace
Nhóm các font mà khoảng cách các chữ đều bằng nhau.
Courier New
Lucida Console
Andalé Mono
Courier
Lucida
Monaco
Cursive
Nhóm font chữ có độ cong mềm giống chữ viết tay.
Bradley Hand
Brush Script MT
Comic Sans MS
<="" td="" style="box-sizing: border-box;">
Fantasy
Nhóm các font chữ nghệ thuật, cách điệu.
Luminari

font-style
Để thiết lập chữ in thường hoặc in nghiêng.
value:
    • normal: Bình thường.
    • italic: In nghiêng.
    • oblique: In nghiêng.
font-weight
Để làm đậm chữ, hay làm dày chữ.
Bằng số: 100, 200, 300, 400, 500, 600, 700,800, 900.
Bằng chữ: normal (400), bold (700), bolder (đậm hơn phần tử cha), lighter (nhạt hơn phần tử cha).
font-variant 
chuyển các "ký tự in thường” trong văn bản sang dạng "ký tự in hoa" hay không. Những ký tự được chuyển sang in hoa sẽ có kích thước nhỏ hơn ký tự in hoa bình thường.
normal
Không chuyển các ký tự in thường sang dạng ký tự in hoa.
small-caps
Chuyển các ký tự in thường sang dạng ký tự in hoa.
initial
Sử dụng giá trị mặc định của nó.(normal)
inherit
 Kế thừa giá trị thuộc của phần tử cha
font-size
Để thiết lập kích cỡ của chữ. Sử dụng number + đơn vị có trong CSS.
Nhúng font chữ bên ngoài vào trang web
Có thể sử dụng google font https://fonts.google.coma/
CSS Lists
Cú pháp:
list-style: style | position | image;
list-style-type
Xác định kiểu của chỉ mục.
value:
    • none
    • armenian
    • circle
    • cjk-ideographic
    • decimal
    • decimal-leading-zezo
    • disc
    • georgian
    • hebrew
    • hiragana
    • hiragana-iroha
    • katakana
    • katakana-iroha
    • lower-alpha
    • lower-greek
    • lower-latin
    • lower-roman
    • square
    • upper-alpha
    • upper-latin
    • upper-roman
    • inherit
list-style-image
Thay thế các chỉ mục bằng chỉ mục hình ảnh.
value: url(‘…’);
list-style-position
Xác định vị trí hiển thị của các chỉ mục so với đoạn text.
value:
    • none: Không hiển thị image list, đây là dạng mặc định.
    • inherit: Kế thừa thuộc tính của phần tử cha.
    • inside: Xác định chỉ mục nằm bên trong nôi dung.
    • outside: Xác định chỉ mục nằm bên ngoài nội dung.
Flexbox
Cần khai báo display: flex;
<div>
  <div class="box1">Box1</div>
  <div class="box2">Box2</div>
  <div class="box3">Box3</div>
 </div>

body > div{
      background-color: #a8a8;
      display: flex;
}
body > div > div{
      background-color: #fdd;
}
.box1{
      background-color: transparent;
}

justify-content
Để căn chỉnh các thể con theo chiều ngang.






align-items
    • Dùng khi Flex container chỉ có 1 hàng, nó căn intem trong 1 hàng theo chiều dọc
Cú pháp: align-items: value
Value:
    • start (flex-start): Căn theo vị trí bắt đầu (hàng bắt đầu)
    • end (flex-end): Căn theo vị trí kết thúc (hàng kết thúc)
    • center: Căn vào giữa
    • stretch: Căng ra theo chiều dọc
    • baseline: căn ở đường cơ sở của containter
 <div>
  <div class="box1">Box1</div>
  <div class="box2">Box2</div>
  <div class="box3">Box3</div>
 </div>

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

flex-direction
Chỉ định hướng của các mục linh hoạt.
Cú pháp: flex-direction: value;
value:
    • row: Các thẻ được sắp xếp theo chiều ngang, hướng từ trái qua phải.
    • row-reverse: Các thẻ được sắp xếp theo chiều ngang, hướng từ phải qua trái.
    • column: Các mục linh hoạt được hiển thị theo chiều dọc, dưới dạng cột.
    • column-reverse: Tương tự như cột nhưng theo thứu tự ngược lại.
    • initial: Sử dụng lại giá trị mặc định.
    • inherit: Kế thừa thuộc tính của phần tử cha.
gap
Để tạo khoảng cách giữa các box.
flex-flow
Là thuộc tính gộp của flex-direction, flex-wrap.
Cú pháp: flex-flow: direction wrap;
flex-wrap
Khi thay đổi kích thước trình duyệt, tự động xuống dòng khi kích thước trình duyệt nhỏ lại.
Cú pháp: flex-wrap: value;
value:
    • nowrap: Không xuống dòng.
    • wrap: Tự động xuống dòng.
    • wrap-reverse:
    • initial:
    • inherit:
<body>
  <div></div>
  <div></div>
  <div></div>
</body>

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

align-content 
    • Dùng để căn dọc item khi container có nhiều hàng item (áp dụng khi có flex-wrap: wrap)
    • Có thể áp dụng vào để tạo menu dọc
Cú pháp: align-content: value;
Value:
    • Center: căn ra giữa 
    • Stretch
    • Flex-start
    • Flex-end
    • Space-around
    • Space-between
    • Space-evently
<div id="main">
  <div style="background-color:coral;"></div>
  <div style="background-color:lightblue;"></div>
  <div style="background-color:pink;"></div>
</div>
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

flex-shrink
flex-grow
    • Chỉ định mức độ tăng mà mục đó sẽ tăng lên so mới các mục linh hoạt còn lại bên trong cùng một vùng chứa. 
Cú pháp: flex-grow: 3
<div id="main">
  <div style="background-color:coral;"></div>
  <div style="background-color:lightblue;"></div>
  <div style="background-color:khaki;"></div>
  <div style="background-color:pink;"></div>
  <div style="background-color:lightgrey;"></div>
</div>
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
flex
Là viết tắt của 3 thuộc tính con
Cú pháp:
flex: flex-grow flex-shrink flex-basis;
flex: [tỉ lệ mở rộng] [tỉ lệ co lại] [kích thước cơ bản];
Ví dụ
Tạo Menu 1 cấp

<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Menu</title>
    <style>
        *{
            padding: 0;
            box-sizing: border-box;
            margin: 0;
        }
        nav{
            position: relative;
            width: 100vw;
            height: 60px;
            background-color: #333;
        }
        nav ul{
            list-style: none;
            position: absolute;
        }
        nav ul li{
            float: left;
            width: 16.66vw;
            height: 60px;
        }
        nav ul li a{
            text-decoration: none;
            font-weight: 900;
            text-transform: uppercase;
            height: 60px;
            display: flex;
            justify-content: center;
            align-items: center;
        }
        nav ul li:hover a{
            background-color: #66ff99;
            border-radius: 20px;
            transition: all 0.7s;
        }
        nav ul li:active a{
            opacity: 0.8;
            background-color: #66ff99;
        }
        @media  (max-width: 500px) {
            nav ul li{
                float: none;
                width: 100vw;
                background-color: #333;
            }
            nav ul li a{
                width: 100%;
                background-color: #333;
            }
        }
    </style>
</head>
<body>
    <nav>
        <ul>
            <li><a href="#">Home</a></li>
            <li><a href="#">New</a></li>
            <li><a href="#">Feedbacks</a></li>
            <li><a href="#">More</a></li>
            <li><a href="#">About</a></li>
            <li><a href="#">Contact</a></li>
        </ul>
    </nav>
</body>
</html>
Tạo Menu 2 cấp

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        *{
            padding: 0;
            margin: 0;
            box-sizing: border-box;
            color: #fff;
        }
        nav{
            display: block;
            height: 50px;
            background-color: #222;
        }
        nav > ul{
            display: flex;
            width: 100%;
            height: 50px;
            justify-content: space-evenly;
            align-items: center;
            list-style: none;
        }
        nav > ul > li{
            position: relative;
        }
        nav > ul > li > a{
            display: flex;
            text-decoration: none;
            font-size: 25px;
            text-transform: uppercase;
            font-weight: 900;
            width: 150px;
            height: 50px;
            justify-content: center;
            align-items: center;
        }
        nav > ul > li > div{
            display: block;
            position: absolute;
            width: 120%;
            left: -15px;
        }
        nav > ul > li > div > a{
            display: none;
            text-align: center;
            text-decoration: none;
            font-size: 20px;
            font-weight: 900;
            text-transform: uppercase;
            padding: 20px;
        }
        nav > ul > li:hover > a{
            transition: all .5s;
            background-color: #fff;
            color: #222;
        }
        nav > ul > li:hover > div > a{
            display: block;
            background-color: #222;
            transition: all .5s;
        }
        nav > ul > li:hover > div > a:hover{
            transition: all .5s;
            background-color: #fff;
            color: #222;
        }
        @media (max-width: 600px){
            nav{
                height: auto;
            }
            nav > ul{
                display: block;
                width: 100%;
            }
            nav > ul > li{
                width: 100%;
            }
            nav > ul > li > a{
                display: flex;
                width: 100%;
                height: auto;
                padding: 15px 0;
                font-size: 20px;
                background-color: #222;
            }
            nav > ul > li > div{
                position: static;
                width: 100%;
                background-color: #333;
                display: none;
                flex-direction: column;
            }
            nav > ul > li:hover > div{
                display: flex;
            }
            nav > ul > li > div > a{
                display: block;
                width: 100%;
                padding: 10px;
                font-size: 18px;
            }
            nav > ul > li:hover > div > a:hover{
                background-color: #fff;
                color: #222;
            }
        }
    </style>
</head>
<body>
    <nav>
        <ul>
            <li>
                <a href="#">Home</a>

                <div>
                    <a href="#">Home1</a>
                    <a href="#">Home2</a>
                    <a href="#">Home3</a>
                    <a href="#">Home4</a>
                    <a href="#">Home5</a>
                </div>
            </li>
            <li>
                <a href="#">Pages</a>

                <div>
                    <a href="#">Pages1</a>
                    <a href="#">Pages2</a>
                    <a href="#">Pages3</a>
                    <a href="#">Pages4</a>
                    <a href="#">Pages5</a>
                </div>
            </li>
            <li>
                <a href="#">Contact</a>

                <div>
                    <a href="#">Contact1</a>
                    <a href="#">Contact2</a>
                    <a href="#">Contact3</a>
                    <a href="#">Contact4</a>
                    <a href="#">Contact5</a>
                </div>
            </li>
            <li>
                <a href="#">Link</a>

                <div>
                    <a href="#">Link1</a>
                    <a href="#">Link2</a>
                    <a href="#">Link3</a>
                    <a href="#">Link4</a>
                    <a href="#">Link5</a>
                </div>
            </li>
            <li>
                <a href="#">Base</a>

                <div>
                    <a href="#">Base1</a>
                    <a href="#">Base2</a>
                    <a href="#">Base3</a>
                    <a href="#">Base4</a>
                    <a href="#">Base5</a>
                </div>
            </li>
            <li>
                <a href="#">Login</a>

                <div>
                    <a href="#">Login1</a>
                    <a href="#">Login2</a>
                    <a href="#">Login3</a>
                    <a href="#">Login4</a>
                    <a href="#">Login5</a>
                </div>
            </li>
        </ul>
    </nav>
</body>
</html>


Grid
    • Tạo ra bố cục dạng lưới với các hàng và cột, giúp thiết kế web đễ dàng hơn. Mặc định width: 100% 
    • Có thể điều chỉnh kích thước khoảng cách bằng cách sử dụng một trong các thuộc tính sau. Vẫn có thể sử dụng được các thuộc tính flexbox
Cú pháp: display: grid;

<body>
    <div>
        <div></div>
        <div></div>
        <div></div>
    </div>
</body>

body > div{
    display: grid;
}
div > div{
    width: 200px;
    height: 50px;
    margin: 20px;
    background-color: #f00;
}
grid-template-columns
Tạo ra số cột và kích thước giữa các cột. Các giá trị sẽ tương ứng với số cột và kích thước chiều rộng của nó từ trái sang phải.

<body>
    <div>
        <div></div>
        <div></div>
        <div></div>
    </div>
</body>

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
grid-template-row
Tạo ra số hàng và kích thước giữa các hàng. Các giá trị sẽ tương ứng với số hàng và kích thước chiều rộng của nó từ trên xuống dưới.
row-gap
Chỉ định khoảng cách giữa các hàng trong bố cục dạng lưới.
column-gap
Xác định kích thước khoảng cách theo cột.
Cú pháp: column-gap: number + unit
gap
Chỉ định khoảng cách giữa các cột, hàng trong bố cục dạng lưới, flexbox hoặc nhiều cột.
Lưu ý: Nếu có một column-rule giữa các cột, nó sẽ xuất hiện ở giữa khoảng cách.
Cú pháp: gap: row-gap column-gap

<div id="big">
     <div class="small"></div>
      <div class="small"></div>
      <div class="small"></div>
 </div>

 #big{
    width: 100%;
    height: 300px;
    display: grid;
    gap: 30px;
}
 .small{
    background-color: #333;
    margin: 2px;
}
Tables
border-collapse
Loại bỏ đường viền dư thừa đó.
Cú pháp:
border-collapse: value;
value:
    • collapse
            
CSS Display
Xác định cách hiển thị của khối bao quanh.
Cú pháp: 
display: value;
value:
    • inline: Bao quanh phần nội dung (text) và không thể thiết lập được width và height khi display: inline;
    • block: Bắt đầu trên một dòng mới với width: 100% màn hình. Có thể thiết được width và height.
    • inline-block: Kết hợp 2 thuộc tính inline và block cho phép cài đặt wodth, height, top, bottom, … khác với display: block là inline-block không xuống dòng sau mỗi thuộc tính và có thể đặt cạnh 2 thuộc tính với nhau
    • Contents: làm cho vùng chứa biến mất, làm cho các phần tử con là phần tử của phần đó lên cấp độ tiếp theo trong DOM
    • Flex: hiển thị một phần tử dưới dạng thùng chứa linh hoạt cấp khối
    • Inline-flex: giống flex và có cấp độ cao hơn flex
    • Grid: hiển thị một phần tử dưới dạng lưới chứa linh hoặt cấp khối
    • Inline-grid: giống grid và có cấp đọ cao hơn grid
    • Table: để phần tử hoạt động giống như phần tử table
    • Table-caption: phần tử hoạt động như phần tử caption
    • Table-column-group: phần tử hoạt động giống như phần tử colgroup
    • Table-footer-group: phần tử hoạt động giống như phần tử tfoot
    • Table-row-group: phần tử hoạt động giống phần tử tbody
    • Table-cell: phần tử hoạt động giống nhưu phần tử td
    • Table-column: phần tử hoạt động giống như phần tử col
    • Table-row: phần tử hoạt động giống như phần tử tr
    • Inline-table: phần tử được hiển thị dưới dạng bảng cấp độ nội tuyến
    • List-item: hiển thị phần tử hoạt động giống như phần tử li
    • Run-in: hiển thị một phần tử dưới dạng khối hoặc nội tuyến, tùy thuộc vào ngữ cảnh
    • None: không hiển thị lên màn hình
    • Initial: cài đặt giá trị mặc định
    • Inherit: kế thừa thuộc tính của phần tử cha


CSS z-index
Đưa ra cấp độ hiển thị. cái nào được hiển thị đè lên trước cái nào. Thẻ nào có giá trị cao thì nằm phía trên giá trị thấp thì nằm phía dưới. cần khai báo position.
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        body{
            position: relative;
        }
        div:nth-child(1){
            width: 50px;
            height: 50px;
            background-color: #fffb00;
            z-index: 2;
        }
        div:nth-child(2){
            height: 100px;
            width: 100px;
            background-color: #ff0000;
            z-index: 1;
        }
        div{
            position: absolute;
        }
    </style>
</head>
<body>
    <div></div>
    <div></div>
</body>
</html>

CSS Overflow
Xác định điều gì sẽ xảy ra nếu một thành phần box tràn nội dung.
value:
    • visible: Khi chiều cao của box không đủ chứa text thì text vẫn hiển thị tràn qua box, đây là mặc định.
    • hidden: Khi chiều cao của box không đủ chứa text, text tràn ra sẽ bị ẩn đi.
    • scroll: Sẽ xuất hiện thanh croll khi text bị tràn ra ngoài, sẽ xuất hiện cả thanh croll ngang và dọc.
    • auto: Thanh croll sẽ tự động hiển thị khi text tràn ra ngoài, hiển thị thanh dọc.
    • inherit: Kế thừa thuộc tính của phần tử cha.
CSS Layout – float, clear
float
    • Có tác dụng đẩy phần tử sang bên trái hoặc bên phải. nó thường được áp dụng vào việc thiết kế bố cục cho web 
    • layout. Thường đi kèm với clearfix, clear để chia bố cục.
Cú pháp: float: value;
    • inline-start = left: Nằm phía bên trái.
    • inline-end = right: Nằm phía bên phải.
    • none: Nằm tại chính vị trí của nó.
    • inherit: kế thừa giá trị thuộc tính float của phần tử chứa nó.
<div class="box1"></div>
    <div class="box2"></div>
    <div class="box3"></div>

div{
            display: block;
            width: 50px;
            height: 50px;
            float: left;
        }
        .box1{
            background-color: aqua;
        }
        .box2{
            background-color: black;
        }
        .box3{
            background-color: blue;
        }

Ví dụ về xây dụng layout giống trang báo
<div style="width: 600px;">
  <img src="https://via.placeholder.com/200x150" style="float: left; margin-right: 15px; margin-bottom: 10px;">

  <p>
    Đây là đoạn văn bản đầu tiên. Nó sẽ nằm bên phải của ảnh và chảy xuống dưới nếu quá dài. Lorem ipsum dolor sit amet, consectetur adipiscing elit.
    Vivamus lacinia odio vitae vestibulum vestibulum. Cras venenatis euismod malesuada.
  </p>

  <p>
    Đây là đoạn văn bản tiếp theo, sẽ nằm dưới chân ảnh khi hết chỗ bên cạnh.
    Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas.
  </p>
</div>
Ảnh nằm bên trái, text sẽ nằm bên phải nếu còn chỗ,
Text sẽ đổ xuống dưới chân ảnh nếu dài quá.

clear
Khi sử dụng thuộc tính float và muốn phần tử tiếp theo bên dưới (không phải bên trái hoặc bên phải) chứng ta sử dụng tiếp thuộc tính clear.
value:
    • left: Bên trái của thành phần không được float.
    • right: Bên phải thành phần không được float.
    • both: Bên trái vè bên phải thành phần không được float.
    • none: Đây là mặc định của thành phần clear, bên trái và bên phải của thành phần được float.
    • inherit: Xác định thừa hưởng thuộc tính từ thành phần cha.

CSS Pseudo-classes
Dùng để thao thao tác với con trỏ chuột tạo ra một số thay đổi cho thuộc tính nào đó. Pseudo-class có 4 thuộc tính cơ bản
    • :link - Hiển thị hiệu ứng khác để người đọc biết đây là đường liên kết.
    • :visited - thay đổi hiệu ứng hoặc một số thuộc tính để cho biết người dùng đã từng click vào.
    • :hover - Di chuột qua đường link làm thay đổi một số thuộc tính hoặc hiệu ứng.
    • :active – thay đổi hiệu ứng Khi nhập chuột vào và giữ im.
    • :first-child - Xác định phần tử đầu tiên để css nếu nó tìm thấy các phần tử giống nhau hoặc được đặt class giống nhau
    • :last-child - Nó sẽ css vào thuộc tính giống nhau nhưng ở cuối cùng
    • :nth-child(): xác định thẻ thứ mấy mà có cùng tên gọi sẽ được css
    • :lang - định nghĩa một quy tắc đặc biệt cho một ngôn ngữ nào đó trong một phần tử cụ thể.
    • :checked - Phù hợp để css các thuộc tính dạng checkbox, đa số dùng trong input dạng check
    • :disabled - Nó sẽ tìm đến thẻ input nào có thuộc tính disabled để thực hiện các lệnh
    • :enabled - Nó sẽ tìm đến thuộc tính input nào vẫn còn hoạt động (không chứa thẻ disabled) để thực hiện các lệnh 
    • :empty - Nó sẽ css vào thẻ mà không chứa nội dung nào, nếu có nội dung thì :empty sẽ bị mất hiệu lực
    • :required - Nó sẽ css vào input có giá trị required
    • :optional - khi có 2 phần tử input thì nó sẽ css vào phần tử còn lại không có giá trị required
    • :read-only - Nó sẽ css vào phần tử input có phần tử readonly, tức là phần input chỉ đọc
    • :target
    • :out-of-range
Lưu ý: Thứ tụ áp dụng :link < :visited < :hover < : active. Không phân biết chữ hoa và chữ thường. bé hơn được áp dụng trước
CSS Pseudo-elements
::before
Để chèn một số nội dung trước nội dung của phần tử.
::after
Để chèn một số nội dung sau nội dung của phần tử.
Ví dụ về ::before và ::after
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
       div{
        height: 100px;
        width: 100px;
        background-color: #fffb00;
       }
       div::before{
        content: 'this is CSS';
        background-color: #ff0000;
       }
       div::after{
        content: 'this is CSS';
        background-color: #ff0000;
       }
    </style>
</head>
<body>
    <div>Welcome to VietNam</div>
</body>
</html>

CSS Opacity / Transparency 
opacity
Để tạo độ mờ cho khối. nhận giá trị từ 0 đến 1.
CSS [attribute] Selector
Sử dụng để chọn các phần tử có thuộc tính được chỉ định.
Cú pháp:
    • Tag[attribute = “value”]{}
    • Tag[attribute~ = “value”]{}
    • Tag[attribute| = “value”]{}
    • Tag[attribute^ = “value”]{}
    • Tag[attribute$ = “value”]{}
    • Tag[attribute* = “value”]{}
Xem ví dụ ở đây: http://w3schools.com/css/css_attribute_selectors.asp
CSS Forms
:focus
Để chọn và định dang phần tử được lấy nét. Thường sử dụng cho thẻ input.
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Tester</title>
  <link rel="stylesheet" href="Tester.css">
  <style>
    input:focus{
      background-color: aqua;
    }
  </style>
</head>
<body>
 <input type="text">
</body>
</html>

Khi click vào ô input thì ô input đó chuyển thành màu xanh.
:valid
Để định dạng các phần tử biểu mẫu hợp lệ.
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Tester</title>
  <link rel="stylesheet" href="Tester.css">
  <style>
    input:focus:valid{
      background-color: aqua;
    }
  </style>
</head>
<body>
 <input type="text">
</body>
</html>

resize
Định dạng cho vùng nội dung người dùng có thể thay đổi kích thước. Phải sử dụng cùng overflow đối với các thẻ khác. Sử dụng cùng thẻ textarea thì không cần overflow.
Cú pháp:
resize: value;
value:
    • both: Người dùng có thể thay đổi cả chiều cao và chiều rộng của thành phần.
    • none: Người dùng không được thay đổi.
    • horizontal: Người dùng có thể thay đổi chiều ngang.
    • vertical: Người dùng có thể thay đổi chiều dọc.
CSS Counter
Để biểu thị hệ thống phân cấp, đánh số đối tượng.
Xem ví dụ ở đây: https://www.w3schools.com/css/css_counters.asp
CSS Units
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
Thiết lập kích thước cho thẻ div với các đơn vị tuyệt đối
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
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
    </style>
</head>
<body>
    <div id="div1"></div>
    <div id="div2"></div>
    <div id="div3"></div>
    <div id="div4"></div>
    <div id="div5"></div>
    <div id="div6"></div>
</body>
</html>

Tính ưu tiên 
Priority
Example
Inline style
<h1 style="color: pink;">
Id selectors
#navbar
Classes and pseudo-classes
.test, :hover
Attributes
[type="text"]
Elements and pseudo-elements
 h1, ::before, ::after
!important
Để thêm tầm quan trong vào thuộc tính.
Cú pháp:
attribute: value !important;
CSS Math Functions
Xem ví dụ ở đây: https://www.w3schools.com/css/css_math_functions.asp
calc()
Để tính toán, sử dụng kết quả của phép tính để làm giá trị thuộc tính.
max()
Lấy giá trị lớn hơn làm giá trị thuộc tính.
min()
Lấy giá trị nhỏ hơn làm giá trị thuộc tính.
CSS @font-face rule
Định nghĩa ra một font chữ khác mà không có trong ngôn ngữ lập trình, nguồn được lấy từ internet.
Xem ví dụ ở đây: https://www.w3schools.com/css/css3_fonts.asp
transform
Xử lý hiệu ứng 2D, 3D.
translate() – translateX() – translateY()
Di chuyển đối tượng từ vị tri hiện tại của nó.
Cú pháp:
transform: value;
value:
    • translate(x, y)
    • translateX(x)
    • translateY(y)
Trong đó: x là di chuyển sang phải (nếu số dương) và sang trái (nếu số âm). y là di chuyển xuống (nếu số dương) và lên (nếu số âm).
scale() – scaleX() – scaleY()
Dùng để kéo giãn đối tượng HTML. 
Cú pháp:
    • transform: scale(x, y) (x là kéo dài theo chiều rộng, y là kéo dài theo chiều cao)
    • …
Bài tập
Kéo dãn thẻ div bằng scale
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Tester</title>
  <style>
    div{
      width: 100px;
      height: 100px;
      background-color: #000;
      animation: gian 3s infinite linear;
    }
    @keyframes gian {
      0%{transform: scale(0.8);}
      50%{transform: scale(1.2);}
      100%{transform: scale(0.8);}
    }
  </style>
</head>
<body>
 <div></div>
</body>
</html>

Hiệu ứng thanh trượt từ trái sang phải
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <style>
        body > div{
            position: relative;
            width: 500px;
            height: 50px;
            background-color: #000;
        }
        div div{
            position: absolute;
            width: 0;
            height: 3px;
            background-color: #0becf0;
            transition: width 5s linear;
        }
        div:hover div{
            width: 100%;
        }
    </style>
</head>
<body>
    <div>
        <div></div>
    </div>
</body>
</html>

Hiệu ứng thanh trượt từ giữa sang 2 bên
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <style>
        body > div{
            position: relative;
            width: 500px;
            height: 50px;
            background-color: #000;
        }
        div div{
            position: absolute;
            width: 100%;
            height: 3px;
            background-color: #0becf0;
            transition: transform 5s linear;
            transform: scaleX(0);
            transform-origin: 50%;
        }
        div:hover div{
            transform: scaleX(1);
        }
    </style>
</head>
<body>
    <div>
        <div></div>
    </div>
</body>
</html>

Hiệu ứng loading

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Around loading</title>
    <link rel="stylesheet" href="around.css">
</head>
<body>
    <div>
        <div class="spiner">:)</div>
        <div class="bar">
            <span class="dot1"></span>
            <span class="dot2"></span>
            <span class="dot3"></span>
        </div>
        <div class="box">
            <h2>LDT</h2>
        </div>
    </div>
</body>
</html>

body{
    margin: 0px;
    box-sizing: border-box;
}
body > div{
    min-height: 100vh;
    width: 100%;
    background-color: #002266;
    text-align: center;
}
.spiner{
    margin-top: 50px;;
    width: 100px;
    height: 100px;
    display: inline-block;
    border: 10px solid #fff;
    border-radius: 50%;
    border-top: 10px solid #ff8000;
    animation: spiner 2s linear infinite;
    color: #fff;
    font-size: 4.5rem;
}
.bar > span{
    width: 50px;
    height: 50px;
    background-color: #ff8000;
    border-radius: 50%;
    display: inline-block;
    animation: dot 2s ease-in-out infinite both;
}
.bar span.dot1{
    animation-delay: -0.3s;
}
.bar span.dot2{
    animation-delay: -0.15s;
}
.bar span.dot3{
    animation-delay: 0s;
}
@keyframes spiner{
    from{
        transform: rotate(0deg);
    }
    to{
        transform: rotate(360deg);
    }
}
@keyframes dot {
    0%,80%,100%{
        transform: scale(0);
    }
    40%{
        transform: scale(1);
    }
}
.box{
    position: relative;
    width: 200px;
    height: 300px;
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: #000;
    border-radius: 20px;
    overflow: hidden;
    left: 670px;
    top: 100px;
}
.box h2{
    color:color-mix(in srgb, #bcee68, #ff8000);
    text-shadow: 4px 4px #000;
    font-size: 4em;
    z-index: 5;
}
.box::before{
    content: " ";
    position: absolute;
    width: 170px;
    height: 150%;
    background: linear-gradient(#00ccff,#d500f9);
    animation: around 5s linear infinite;
}
.box::after{
    content: ' ';
    position: absolute;
    background: #000;
    top: 5px;
    bottom: 5px;
    right: 5px;
    left: 5px;
    border-radius: 20px;
}
@keyframes around{
    from{
        transform: rotate(0deg);
    }
    to{
        transform: rotate(360deg);
    }
}
Hiệu ứng loading

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <div class="loading">
        <div class="bar"></div>
    </div>
</body>
</html>

body{
    width: 100%;
    height: 100vh;
    margin: 0px;
    box-sizing: border-box;
    background-color: rgba(0, 0, 0, 0.909);
}
.loading{
    position: relative;
    width: 100%;
    min-height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
}
.bar{
    position: absolute;
    width: 500px;
    height: 60px;
    border: 2px solid #a2cd5a;
    border-radius: 20px;
    overflow: hidden;
}
.bar::before{
    content: ' ';
    position: absolute;
    width: 100%;
    height: 100%;
    background-color: color-mix(in srgb, blue, green);
    animation: progress1 5s infinite;
    transform-origin: left;
}
@keyframes progress1{
    from{
        transform: scaleX(0);
    }
    to{
        transform: scaleX(1);
    }
}
.bar::after{
    position: absolute;
    content: "please wait ...";
    width: 100%;
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    color: #fff;
    text-transform: uppercase;
    font-size: larger;
    font-family: Verdana, Geneva, Tahoma, sans-serif;
    font-weight: bolder;
}


Matrix()
Là tổng hợp các hiệu ứng.
Cú pháp:
matrix(scaleX, skewY, skewX, scaleY, translateX, translateY)
rotate() 
Dùng để xoay đối tượng HTML theo một góc độ nào đó.
Hiệu ứng loading

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Tester</title>
  <link rel="stylesheet" href="Tester.css">
</head>
<body>
  <div id="bkground">
    <div id="logo"></div>
  </div>
</body>
</html>

*{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }
#bkground{
    position: relative;
    width: 100%;
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: rgba(0,0,0,0.75);
}
#logo{
    width: 100px;
    height: 100px;
    display: block;
    border-radius: 50%;
    border: 10px solid #fff;
    border-top: 10px solid #ff6600;
    animation: quay 3s linear infinite;
}
@keyframes quay{
    from{
      transform: rotate(0deg);
    }
    to{
      transform: rotate(360deg);
    }
}
transform-origin
Cho phép thay đổi vị trí của các phần tử được chuyển đổi. các phép biến đổi 2d có thể thay đổi trục x và y của một phần tử. Các phép biến đổi 3d cũng có thể thay đổi trục z của một phần tử.
Lưu ý: Thuộc tính này phải được sử dụng cùng với thuộc tính biến đổi transform.
Cú pháp:
transform-origin: x-axis y-axis z-axis | initial | inherit
    • x-axis: Xác định vị trí của chế độ xem ở trục x. Có những giá trị left, center, right, length, %.
    • y-axis: Xác định vị trí của chế độ xem ở trục y. Có những giá trị top, center, bottom, length, %.
    • z-axis: Xác định vị trí của chế độ xem ở trục z trong không gian 3d. có giá trị là length.
    • initial: Đặt thuộc tính thành giá trị mặc định của nó.
    • inherit: Thừa hưởng giá trị của phần tử cha.
CSS Transitions
Tạo ra hiệu ứng, chuyển động thay đổi từ giá trị này sang giá trị khác một các mượt mà khi có tương tác người dùng. Có 2 đầu vào bắt buộc là thuộc tính cần thay đổi và thời gian để tạo ra quá trình thay đổi.
Cú pháp:
trasition: name time timing-function, …;
trasition-timing-function
    • ease: Bắt đầu chậm sau đó nhanh dần và gần kết thúc lại chậm từ từ.
    • linear: Bắt đầu và kết thúc tốc độ là như nhau.
    • ease-in: Chậm lúc đầu.
    • ease-out: Chậm lúc kết thúc.
    • ease-in-out: Chậm lúc bắt đầu và kết thúc.
transition-delay
xác định khoản thời gian trì hoãn giữa thời gian một thuộc tính thay đổi và lúc chuyển tiếp thực sự bắt đầu. đơn vị là giá trị unit + “s” (VD: 1s;)
CSS Animations
Dùng để tạo các hiệu ứng di chuyển của các thẻ HTML và được sử dụng khá nhiều trong các hiệu ứng của website hiện nay. Đây là cách viết gộp của tất cả thuộc tính animation.
Cú pháp: (chú ý về thứ tự khai báo)
animation: name | duration | timing-function | delay | iteration-count | direction | fill;
name
Là tên của hiệu ứng, phần mà được định nghĩa trong keyframe (tự đặt).
duration
Chỉ định thời gian từ lúc hiệu ứng bắt đầu cho đến khi kết thúc. Đơn vị là s(giây).
timing-function
Để thay đổi trạng thái của đối tượng.
Giá trị:
    • linear: giữ tốc độ như nhau từ lúc bắt đầu cho đến khi kết thúc.
    • ease: bắt đầu chậm sau đó nhanh và kết thúc chậm dần.
    • ease-in: bắt đầu chậm.
    • ease-out: kết thúc chậm.
    • ease-in-out: bắt đầu chậm và kết thúc chậm.
delay
Chỉ định thời gian chờ trước khi hiệu ứng bắt đầu thực thi. Đơn vị là s(giây)
iteration-count
Chỉ định số lần hiệu ứng lập lại. giá trị là số, không có đơn vị hoặc infinite (lặp vô hạn).
animation-direction
Định dạng hướng di chuyển của đối tượng.
    • normal: di chuyên về phía trước.
    • reverse: di chuyển theo hướng về phía sau.
    • alternate: di chuyển về phía trước rồi di chuyển về phía sau.
    • alternate-reverse: di chuyển về phía sau rồi di chuyển về phía trước.
animation-fill-mode
Định dạng trạng thái của đối tượng.
    • forwards: trạng thái của đối tượng sẽ đẽ thể hiện như cấu hình cuối cùng trong quy tắc keyframe.
    • backwards: trạng thái của đối tượng sẽ đẽ thể hiện như cấu hình đầu tiên trong quy tắc keyframe (lưu ý chỉ trong thời gian diễn ra hiệu ứng).
    • both: sự hòa trộn giữa forwards và backwards.
animation-play-state
chỉ định hoạt ảnh ảnh đang chạy hoặc tạm dừng.
@keyfames <animation-name>
Chỉ định tác vụ thay đổi của animation
Sử dụng from{}…to{}… hoặc %{}
CSS tooltips
Xem ví dụ ở đây: https://www.w3schools.com/css/css_tooltip.asp
CSS filters
Thuộc tính filter xác định các hiệu ứng hình ảnh (như độ mờ và độ bão hòa) cho một phần tử) thường là <img>. Làm mờ chính khối mà ta đặt thuộc tính filter vào.
Cú pháp:
filter: none | blur() | brightness() | contrast() | drop-shadow() | grayscale() | hue-rotate() | invert() | opacity() | saturate() | sepia() | url();
    • none: Giá trị mặc định. 
    • blur(number + unit): Làm mờ cho hình ảnh.
    • brightness(%): điều chỉnh độ sáng của hình ảnh. 0% sẽ làm cho hình ảnh hoàn toàn đen, 100% là mặc định và thể hiện ảnh gốc, nó cho kết quả sáng hơn.
    • Contrast(%): điều chỉnh độ tương phản của hình ảnh. 0% sẽ làm cho hình ảnh toàn đen, 100% là thể hiện hình ảnh gốc và cho độ tương phản cao hơn.
    • Drop-shadow(h-shadow v-shadow blur spread color): áp dụng hiệu ứng đổ bóng cho hình ảnh. h-shadow (bắt buộc) chỉ định giá trị pixel cho bóng ngang, giá trị âm đặt bóng ở bên trái hình ảnh. V-shadow (bắt buộc) chỉ định thuộc tính pixel cho bóng dọc. giá trị âm đặt bóng phía trên hình ảnh. blur(tùy chọn) là giá trị thứ 3 và phải bằng pixel thêm hiệu ứng mờ cho bóng. Giá trị lớn hơn sẽ mờ nhiều hơn bóng trở nên lớn hơn và nhạt hơn, giá trị âm không được phép nếu không có giá trị nào thì giá trị 0 se được sử dụng. spead (tùy chọn) đây là giá trị thứ 4 và phải bằng pixel giá trị dương sẽ làm cho bóng mở rộng và lớn hơn. Giá trị âm sẽ khiến bóng co lại. nếu không được chỉ định thì giá trị là 0. Color (tùy chọn) thêm màu sắc cho bóng nếu không được thêm sẽ theo chỉ định của trình duyệt thương là màu đen. – bộ lọc này tương tự như box-shadow
    • Grayscale(%): chuyển đổi hình ảnh sang thang độ sáng 0% là mặc định và thể hiện ảnh gốc 100% sẽ làm cho ảnh có màu xám hoàn toàn dùng cho ảnh đen trắng. không cho phép giá trị âm
    • Hue-rotate(deg): áp dụng xoay màu sắc trên hình ảnh. Giá trị xác định số độ xung quanh vòng tròn màu mà mẫu hình ảnh sẽ được điều chỉnh. 0 deg là mặc định và đại diện cho hình ảnh gốc giá trị tối đa là 360 deg.
    • Invert(%): đảo ngược các mẫu trong hình ảnh. 0% là mặc định và thể hiện ảnh gốc; 100% sẽ khiến hình ảnh đảo ngược hoàn toàn. Không cho phép giá trị âm.
    • Opacity(%): đặt mức độ mờ cho hình ảnh, mức độ mờ mô tả mức độ trong suốt, 0% là hoàn toàn minh bạch, 100% là thể hiện ảnh gốc. không cho phép giá trj âm
    • Satutare(%): bão hòa hình ảnh 0% sẽ làm cho hình ảnh không bão hòa hoàn toàn 100% là mặc định và đại diện cho hình ảnh gốc giá trị trên 100% mang lại giá trị siêu bão hòa. Không cho phép giá trị âm
    • Sepia(%): chuyển đổi hỉnh ảnh sang màu nâu đỏ, 0% là mặc địnhh và thể hiện giá trị gốc. 100% là hình ảnh có màu nâu đỏ hoàn toàn, không cho phép giá trị âm
    • url(): Hàm url() lấy vị trí của tệp XML chỉ định bộ lọc SVG và có thể bao gồm một neo cho một thành phần bộ lọc cụ thể. Ví dụ: bộ lọc: url(svg-url#element-id)
    • initial: cài đặt giá trị mặc định
    • inherit: cài đặt giá trị theo phần tử cha của nó
CSS Image Shapes
Xem ví dụ ở đây: https://www.w3schools.com/css/css3_image_shapes.asp
CSS object-fit
Xem ví dụ ở đây: https://www.w3schools.com/css/css3_object-fit.asp
CSS object-position
Xem ví dụ ở đây: https://www.w3schools.com/css/css3_object-position.asp

CSS masking
mask-image
Chỉ định một hình ảnh lớp mặt nạ. Có thể là hình ảnh png, svg, gradient css hoặc phần tử <mask> svg.
CSS multiple Columns
CSS Variables
CSS box sizing
box-sizing
thiết lập phạm vi từ đâu đổ vào.
giá trị:
    • content-box
    • border-box
    • initial
    • inherit
Reponsive
    • Để làm cho giao diện web hiển thị tốt trên nhiều kích thước khác nhau (mobile, tablet, desktop, …).
    • Có 3 cách để reponsive:
    • Media queries 
    • Sử dụng đơn vị linh hoạt (%, vw, vh, em, rem)
    • Sử dụng Flexbox và grid
CSS Media Queries 
@media
Sử dụng trong truy vấn phương tiện để áp dụng các kiểu khác nhau cho các loại thiết bị, phương tiện khác nhau truy vấn phương tiện có thể được sử dụng để kiểm tra nhiều thứ chiều rộng và chiều cao của khung hình thiết bị, cung cấp biểu định kiểu phù hợp đáp ứng cho các loại thiết bị.
Thực tế vẫn còn nhiều nữa nhưng với lập trình web thì chúng ta thường sử dụng ba thuộc tính đó thôi. Và trước khi đi vào tìm hiểu các thuộc tính thì ban phải phân biệt hai khái niệm sau:
    • Device: Là thiết bị sử dụng website như Laptop, Desktop, Iphone, …
    • Viewport: Là kích thước hiển thị của giao diện.
Cú pháp:
@media not | only mediatype and (media feature and | or | not media feature) {…}
    • not: Đảo ngược ý nghĩa của toàn bộ truy vấn phương tiện.
    • only: Từ khóa nầy ngăn các trình duyệt cữ khoongg hỗ trợ truy vấn phương tiện áp dụng các kiểu đã chỉ định. Nó không có tác dụng trên các trình duyệt hiện đại.
    • and: Từ khóa này kết hợp một loại phương tiện hoặc một hoặc nhiều tính năng phương tiện.
Xem ví dụ ở đây: https://www.w3schools.com/css/tryit.asp?filename=trycss3_media_queries1
mediatype
Giá trị:
    • all: Dùng cho mọi thiết bị
    • print: Dùng cho máy in
    • screen: Dùng cho máy tính và các thiết bị smart phone
CSS Sass Tutorial
CSS references
@import 
Tham chiếu một stylesheet vào một stylesheet khác thẻ này có chức năng giống thẻ link với rel=” stylesheet”; tốc độ chậm hơn.
title
Dùng để bổ sung ý nghĩa cho nội dung. Nằm trong thẻ.
-webkit-text-fill-color
Css nhiều màu vào cho một chữ.
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <style>
    div{
      display: inline;
      text-transform: uppercase;
      letter-spacing: 0.2em;
      font-weight: 900;
      font-size: 3em;
      font-family: sans-serif;
      background-image: linear-gradient(45deg, #ff0000, #fffb00, #abab00, #00ff00);
      -webkit-text-fill-color: transparent;
      -webkit-background-clip: text;
    }
  </style>
</head>
<body>
  <div>Gradient</div>
</body>
</html>

mix-blend-mode 
Thuộc tính mix-blend-mode chỉ định cách nội dung của phần tử sẽ hòa trộn với nền gốc trực tiếp của nó
mix-blend-mode:normal|multiply|screen|overlay|darken|lighten|colordodge|colorburn|difference|exclusion|hue|saturation|color|luminosity;
    • normal: là giá trị mặc định. Đặt chế độ hòa trộn thành bình thường
    • multiply: đặt chế độ hòa trộn để nhân lên
    • creen: đặt chế độ hòa trộn thành màn hình
    • overlay: đặt chế độ hòa trộn thành lớp phủ
    • darken: đặt chế độ hòa trộn thành tối hơn
    • lighten: đặt chế độ hào trộn thành sáng hơn
    • color-dodge: đặt chế độ hòa trộn thành color-dodge
    • coler-burn: đặt chế độ hòa trộn thành ghi màu
    • difference: đặt chế độ hòa trộn thành sự khác biệt
    • exclusion: đặt chế độ hòa trộn thành loại trừ
    • hue: đặt chế độ hòa trộn thành màu sắc
    • saturation: đặt chế độ hào trộn thành bão hòa
    • color: đặt chế độ hòa trộn thành màu sắc
    • luminosity: đặt chế độ hòa trộn thành độ sáng
VD:

.normal {mix-blend-mode: normal;}
.multiply {mix-blend-mode: multiply;}
.screen {mix-blend-mode: screen;}
.overlay {mix-blend-mode: overlay;}
.darken {mix-blend-mode: darken;}
.lighten {mix-blend-mode: lighten;}
.color-dodge {mix-blend-mode: color-dodge;}
.color-burn {mix-blend-mode: color-burn;}
.difference {mix-blend-mode: difference;}
.exclusion {mix-blend-mode: exclusion;}
.hue {mix-blend-mode: hue;}
.saturation {mix-blend-mode: saturation;}
.color {mix-blend-mode: color;}
.luminosity {mix-blend-mode: luminosity;}





pointer-events
Xác định xem liệu một phần tử nào đó có phản ứng với các sự kiện con trỏ hay không.
Cú pháp:
Pointer-events: auto | none | initial | inherit
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        a{
            pointer-events: none;
        }
    </style>
</head>
<body>
    <a href="https://www.w3schools.com/cssref/tryit.php?filename=trycss3_pointer-events">Click</a>
</body>
</html>

Không thể click được vào link nào vì link liên kết này không hoạt động.
Tạo button có hiệu ứng bằng HTML CSS

<a href="#">Button</a>
*{
        margin: 0;
        padding: 0;
        box-sizing: border-box;
        font-family: 'Poppins', sans-serif;
       }
       body{
        display: flex;
        justify-content: center;
        align-items: center;
        min-height: 100vh;
       }
       a{
        position: relative;
        font-size: 1.5em;
        border: 2px solid #000;
        padding: 10px 30px;
        letter-spacing: 0.1em;
        text-decoration: none;
        background-color: #ff6600;
        z-index: 1;
       }
a::before{
        content: "";
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background-color: #fff;
        z-index: -1;
        transform: scaleX(1);
        transform-origin: left;
        transition: transform 0.7s ease;
       }
       a:hover::before{
        transform-origin: right;
        transform: scaleX(0);
        transition: transform 0.7s ease;
       }
       a:hover{
        color: #fff;
       }

Tạo hiệu ứng loading

    <div class="loading"></div>

.loading{
    position: relative;
    width: 200px;
    height: 200px;
    background: conic-gradient(#0000 10%, #8f44fd);
    border-radius: 50%;
    animation: rotate 1.5s linear 0.4s infinite;
}
.loading::before{
    position: absolute;
    content: "";
    left: 15px;
    right: 15px;
    top: 15px;
    bottom: 15px;
    background-color: #fff;
    border-radius: 50%;
}
@keyframes rotate {
    0% {transform: rotate(0deg);}
    100%{transform: rotate(360deg);}
}
cursor
Xác định hình dạng con trỏ chuột khi trỏ qua một phần tử.
Cú pháp: cursor: value;
    • pointer: Hình ngón tay
    • zoom-in: Hình biểu tượng zoom dấu +
<img class="zoom-img" src="scatter.png" alt="Zoom Image">

.zoom-img {
width: 300px;
height: auto;
transition: transform 0.3s ease;
}

.zoom-img:hover {
transform: scale(1.5);
cursor: zoom-in;
}


Alias
All-scroll
Auto
Cell
Col-resize
Context-menu
Copy
Crosshair
Default
e-resize
ew-resize
grab
grabbing
help
move
n-resize
ne-resize
nesw-resize
ns-resize
nw-resize
nwse-resize
no-drop
none
not-allowed

progress
row-resize
s-resize
se-resize
sw-resize
text
Url
Vertical-text
w-resize
wait
zoom-out
initial
inherit

Hiệu ứng Parallax
Tạo icon

Biến
:root & var()
Định nghĩa các biến CSS toàn cục có thể tái sử dụng nhiều lần.
Root giúp quản lý theme màu, kích thước, spacing một cách dễ dàng. Chỉnh một lần ảnh hưởng toàn bộ trang. Hưu ích khi làm dark mode, light mode hoặc theme động bằng javascript.
ví dụ:
:root{
        --bg: #ff0;
    }
    body{
        background-color: var(--bg);
    }