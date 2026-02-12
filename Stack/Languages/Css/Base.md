
- [Directory Structure](#directory-structure)
- [inline \& external \& internal](#inline--external--internal)
- [Comment](#comment)
- [Combinators](#combinators)
  - [Demo về ~](#demo-về-)
- [Selector](#selector)
---
# Directory Structure
```bash
Css                 # mình dùng thư mục này để xem kiến thức về Css
├── Layout_Spacing  # mình dùng file này để định vị trí, kích thước Box
├── Visual_Style    # mình dùng file này để định hình dạng, phong cách hiển thị
├── Color           # mình dùng file này để định màu sắc      
├── Interaction     # mình dùng file này để tương tác với box cho nó động
├── Pratices        # mình dùng file này để xem code mẫu
└── Base            # mình dùng file này để xem kiến thức cơ bản và tiện ích Css
```
# inline & external & internal
```bash
- inline: Viết thẳng vào thẻ html thông qua thuộc tính style=” …”.
- external: Viết vào file css riêng rồi link vào html. (khuyến cáo sử dụng).
- internal: Viết vào thẻ <head> … </head> thông qua thẻ <style> … </style> trong file html.
```
# Comment 
```bash
/* … */
```
# Combinators
```bash
- Thẻ1 thẻ2{} - Phân cấp cha con.
- Thẻ1 > thẻ2{} - Phân cấp cha con một cấp.
- Thẻ1 + thẻ2{} - css vào phần tử ngay sau.
- Thẻ1 ~ thẻ 2{} - css vào tất cả các thẻ ngay sau nó và cùng cấp với thẻ 1.
- :is(element1, element2) … – Để gom nhóm đối tượng nhanh khi chúng có cùng một dòng lệnh.
- :where(element1, element2, …) - Ở đâu có element1, element2 thì CSS vào đó.
```
## Demo về ~
```html
<main class="heading">
    <div class="heading1"></div>
    <div class="heading2"></div>
    <div class="heading3"></div>
</main>
<main class="end"></main>
```
```css
div{
    width: 100px;
    height: 20px;
    margin: 10px 10px;
}
.end{
    width: 100px;
    height: 20px;
    margin: 10px 10px;
}
.heading1~div{
    background-color: aqua;
}
```
# Selector
```bash
Có thể là tên thẻ, id (#) hoặc class (.)
```

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