- [Box](#box)
  - [Box-shadow](#box-shadow)
  - [background](#background)
    - [backround-image](#backround-image)
    - [background-repeat](#background-repeat)
  - [backdrop-filter](#backdrop-filter)
  - [border](#border)
    - [border-style \& Border-width \& Border-color](#border-style--border-width--border-color)
    - [border-top-style \& border-right-style \& border-bottom-style \& border-left-style](#border-top-style--border-right-style--border-bottom-style--border-left-style)
    - [border-image \& border-image-source \& border-image-slice \& border-image-width \& border-image-outset \& border-image-repeat](#border-image--border-image-source--border-image-slice--border-image-width--border-image-outset--border-image-repeat)
    - [border-radius](#border-radius)
      - [border-top-left-radius \& border-top-right-radius \& border-bottom-left-radius \& border-bottom-right-radius](#border-top-left-radius--border-top-right-radius--border-bottom-left-radius--border-bottom-right-radius)
  - [Display](#display)
  - [z-index](#z-index)
  - [Overflow](#overflow)
  - [float](#float)
    - [clear](#clear)
- [Text](#text)
  - [Text decoration](#text-decoration)
    - [text-decoration-line](#text-decoration-line)
    - [text-decoration-style](#text-decoration-style)
    - [text-decoration-thickness](#text-decoration-thickness)
  - [text-overflow](#text-overflow)
  - [word-wrap \& word-break](#word-wrap--word-break)
  - [text-transform](#text-transform)
  - [text-shadow ](#text-shadow)
- [fonts](#fonts)
  - [font-family](#font-family)
  - [font-style](#font-style)
  - [font-weight](#font-weight)
  - [font-variant](#font-variant)
- [lists](#lists)
  - [list-style-type](#list-style-type)
  - [list-style-image](#list-style-image)
  - [list-style-position](#list-style-position)
---
# Box
## Box-shadow
```bash
- Để tạo bóng cho khối bao ngoài.
```
**Syn**
```bash
Box-shadow: h-shadow v-shadow blur spread color | inset | initial | inherit

- h-shadow: Vị trí bóng ngang so với chữ, số âm sẽ đẩy lên trên và số dương sẽ đẩy xuống dưới.
- v-shadow: Vị trí bóng dọc so với chứ, số âm sẽ đẩy lui phía sau và số dương sẽ đẩy tới phía trước.
- blur-radius: Độ nhòe của chữ bóng, tính bằng pixel.
- spread: Kích thước của bóng tối.
- color: Màu sắc của bóng, chấp nhận các inset: thay đổi bóng từ bên ngoài vào trong thay vì từ trong ra ngoài.
- initial: Thiết lập giá trị mặc định.
- inherit: Kế thừa giá trị từ thẻ HTML cha.
```
## background
### backround-image
```bash
- Để Thiết lập hình nền.
```
**Syn**
```bash
background-image: value;

- url(‘ ’): Truyền vào một link của hình ảnh đó đuôi jpg hoặc png, …
- conic-gradient: Thiết lập màu chuyển.
- linear-gradient: Thiết lập màu chuyển.
```
### background-repeat 
```bash
Để Lặp hình nền hoặc không.
```
**Syn**
```bash
background-repeat: value;

- repeat-x: Lặp theo chiều ngang.
- repeat-y: Lặp theo chiều dọc.
- repeat: Lặp full block.
- space: Lặp các góc của khối.
- round: Lặp full khối.
- no-repeat: Không lặp.
- space-repeat: Lặp bỏ trống phần giữa theo chiều dọc.
- round-space: Lặp bỏ trống phần giữa theo chiều ngang.
```
## backdrop-filter
```bash
Áp dụng hiệu ứng đồ họa cho khu vực phía sau. Không áp dụng được với opacity, chỉ áp dụng được với rgba, …
```
**Syn**
```bash
backdrop-filter: value;

- none: là giá trị mặc định
- filter: sử dụng các giá trị của thuộc tính filter
- initial: sử dụng thuộc tính mặc định
- inherit: kế thừa thuộc tính cha
```
**Ex**
```html
<div>Ví dụ về backdrop filter</div>
```
```css
body{
    background-image: url(./image/background-car.jpg);
    background-size: cover;
}
div{
    width: 100%;
    height: 50px;
    background-color: rgba(255, 255, 255, 0.4);
    position: relative;
    top: 300px;
    -webkit-backdrop-filter: blur(5px);
    backdrop-filter: blur(5px);
}
```
## border 
```bash
- Để thiết lập đường viền cho phần tử. 
- Là cách viết gộp của border-width, border-style, border-color.
```
**Syn**
```bash
border: border-width | border-style | border-color
```
**Ex**
```html
<div></div>
```
```css
*{
    box-sizing: border-box;
}
div{
    width: 400px;
    height: 400px;
    background-color: #f00;
    border-top: 200px solid #abab;
    border-bottom: 200px solid transparent;
    border-left: 100px solid #000;
}
```
### border-style & Border-width & Border-color
```bash
- Thiết lập kiểu viền cho khối bao quanh.
- Thiết lập độ rộng cho viền.
- Thiết lập màu sắc cho viền.
- Nếu có 4 giá trị (top, right, bottom, left).
- Nếu có 3 giá trị (top, right-left, bottom).
- Nếu có 2 giá trị (top-bottom, right-left).
- Nếu có 1 giá trị (top-right-bottom-left).
```
**Syn: border-style**
```bash
Border-style: value;

- dotted: Border sẽ hiển thị là những dấu chấm.
- dashed: Border sẽ hiển thị nét đứt.
- solid: Border sẽ hiển thị đường thẳng liền mạch.
- double: Border sẽ hiển thị 2 đường thẳng.
- groove: Border sẽ hiển thị dạng rãnh 3D.
- ridge: Border sẽ hiển thị dạng viền 3D.
- inset: Border sẽ hiển thị dạng viền trong 3D. 
- outset: Border sẽ hiển thị dạng viền đầu 3D. 
- none: Sẽ không có border.
- hidden: Border sẽ bị ẩn.
```
### border-top-style & border-right-style & border-bottom-style & border-left-style
```bash
- Thiết lập đường viền trên top.
- Thiết lập đường viền bên phải.
- Thiêt lập đường viền dưới.
- Thiết lập đường viền bên trái.
```
### border-image & border-image-source & border-image-slice & border-image-width & border-image-outset & border-image-repeat
```bash
- border-image          : Sử dụng hình ảnh làm đường viền của phần tử.
- border-image-source   : Chỉ định đường dẫn chứa hình ảnh được sử dụng để làm đường viền.
- border-image-slice    : Chỉ định cách cắt hình ảnh như thế nào.
- border-image-width    : Chỉ định độ rộng của hình ảnh.
- border-image-outset   : Chỉ định số lượng mà khu vực hình ảnh vượt qua ngoài cái hộp (box) của nó.
- border-image-repeat   : Chỉ định hình ảnh nên được lặp lại (repeated), làm tròn (rounded) hay kéo dài (stretched).
```
### border-radius
```bash
- Thiết lập bo góc cho viền.
- Website tạo đường bo góc: Fancy-boder-radius
```
**Ex**
```html
<div></div>
```
```css
body > div{
    position: relative;
    width: 100px;
    height: 100px;
    background-color: #000;
    border-radius: 10px / 20px;
}
```
#### border-top-left-radius & border-top-right-radius & border-bottom-left-radius & border-bottom-right-radius
```bash
- border-top-left-radius    : Góc trên bên trái sẽ được uốn cong. Có thể truyền 1 hoặc 2 giá trị.
- border-top-right-radius   : Góc trên bên phải sẽ được uốn cong. Có thể truyền 1 hoặc 2 giá trị.
- border-bottom-left-radius : Góc dưới bên trái sẽ được uốn cong. Có thể truyền 1 hoặc 2 giá trị.
- border-bottom-right-radius: Góc dưới bên phải sẽ được uốn cong. Có thể truyền 1 hoặc 2 giá trị.
```
## Display
```bash
Xác định cách hiển thị của khối bao quanh.
```
**Syn**
```bash
display: value;

- inline: Bao quanh phần nội dung (text) và không thể thiết lập được width và height khi display: inline;
- block: Bắt đầu trên một dòng mới với width: 100% màn hình. Có thể thiết được width và height.
- inline-block: không xuống dòng sau mỗi thuộc tính và có thể đặt cạnh 2 thuộc tính với nhau
- Contents: làm cho vùng chứa biến mất, làm cho các phần tử con là phần tử của phần đó lên cấp độ tiếp theo trong DOM
- Flex: hiển thị một phần tử dưới dạng thùng chứa linh hoạt cấp khối
- Inline-flex: giống flex và có cấp độ cao hơn flex
- Grid: hiển thị một phần tử dưới dạng lưới chứa linh hoặt cấp khối
- Inline-grid: giống grid và có cấp đọ cao hơn grid
- Table: để phần tử hoạt động giống như phần tử table
- Table-caption: phần tử hoạt động như phần tử caption
- Table-column-group: phần tử hoạt động giống như phần tử colgroup
- Table-footer-group: phần tử hoạt động giống như phần tử tfoot
- Table-row-group: phần tử hoạt động giống phần tử tbody
- Table-cell: phần tử hoạt động giống nhưu phần tử td
- Table-column: phần tử hoạt động giống như phần tử col
- Table-row: phần tử hoạt động giống như phần tử tr
- Inline-table: phần tử được hiển thị dưới dạng bảng cấp độ nội tuyến
- List-item: hiển thị phần tử hoạt động giống như phần tử li
- Run-in: hiển thị một phần tử dưới dạng khối hoặc nội tuyến, tùy thuộc vào ngữ cảnh
- None: không hiển thị lên màn hình
- Initial: cài đặt giá trị mặc định
- Inherit: kế thừa thuộc tính của phần tử cha
```
## z-index
```bash
Đưa ra cấp độ hiển thị. cái nào được hiển thị đè lên trước cái nào. Thẻ nào có giá trị cao thì nằm phía trên giá trị thấp thì nằm phía dưới. cần khai báo position.
```
**Ex**
```html
<div></div>
<div></div>
```
```js
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
```
## Overflow
```bash
Xác định điều gì sẽ xảy ra nếu một thành phần box tràn nội dung.
```
**Syn**
```bash
- visible: Khi chiều cao của box không đủ chứa text thì text vẫn hiển thị tràn qua box, đây là mặc định.
- hidden: Khi chiều cao của box không đủ chứa text, text tràn ra sẽ bị ẩn đi.
- scroll: Sẽ xuất hiện thanh croll khi text bị tràn ra ngoài, sẽ xuất hiện cả thanh croll ngang và dọc.
- auto: Thanh croll sẽ tự động hiển thị khi text tràn ra ngoài, hiển thị thanh dọc.
- inherit: Kế thừa thuộc tính của phần tử cha.
```
## float
```bash
Có tác dụng đẩy phần tử sang bên trái hoặc bên phải. nó thường được áp dụng vào việc thiết kế bố cục cho web layout. Thường đi kèm với clearfix, clear để chia bố cục.
```
**Syn**
```bash
float: value;

- inline-start = left: Nằm phía bên trái.
- inline-end = right: Nằm phía bên phải.
- none: Nằm tại chính vị trí của nó.
- inherit: kế thừa giá trị thuộc tính float của phần tử chứa nó.
```
**Ex**
```html
<div class="box1"></div>
<div class="box2"></div>
<div class="box3"></div>
```
```js
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
```
### clear
```bash
Khi sử dụng thuộc tính float và muốn phần tử tiếp theo bên dưới (không phải bên trái hoặc bên phải) chứng ta sử dụng tiếp thuộc tính clear.
```
**Syn**
```bash
- left: Bên trái của thành phần không được float.
- right: Bên phải thành phần không được float.
- both: Bên trái vè bên phải thành phần không được float.
- none: Đây là mặc định của thành phần clear, bên trái và bên phải của thành phần được float.
- inherit: Xác định thừa hưởng thuộc tính từ thành phần cha.
```
# Text
## Text decoration
**Syn**
```bash
text-decoration: line | color | style | thickness;
```
### text-decoration-line
```bash
Dùng để thiết lập một đường gạch cho văn bản.
```
**Syn**
```bash
text-decoration-line: none | underline | line-through | overline | initial | inherit;

- none: Không có đường gạch chân.
- underline: Tạo một đường gạch chân.
- overline: Tạo một đường gạch trên đầu văn bản.
- line-through: Tạo một đường gạch giữa văn bản.
- initial: Sử dụng giá trị mặc định.
- inherit: Kế thừa thuộc tính từ phần tử cha.
```
### text-decoration-style
```bash
Thiệt lập kiểu đường gạch.
```
**Syn**
```bash
text-decoration-style: value:
     
- Solid: Giá trị mặc định, đường gạch là đường nét liền thẳng.
- double: 2 đường thẳng song song với nhau.
- dotted: Đường thẳng chấm bi, nét đứt.
- dashed: Đường thẳng nét đứt.
- wavy: Đường sóng.
- initial: Lấy giá trị mặc định.
- inherit: Lấy giá trị giống phần tử cha.
```
### text-decoration-thickness
```bash
Để thiết lập độ dày cho đường gạch.
```
**Syn**
```bash
text-decoration-thickness: value;

- auto: Chọn độ dày dựa vào trình duyệt
- from-font: Nếu tệp font chữ chứa thông tin về độ dày, thì sử dụng giá trị đó, nếu không thì có chức năng giống auto
- length/percetage: Chỉ định độ dày theo chiều dài hoặc %
- initial: Lấy giá trị mặc định
- inherit: Lấy giá trị giống phần tử cha
```
## text-overflow
```bash
chỉ hoạt động hay thực thi khi ta thiết lập thuộc tính white-space: nowrap và thiết lập overflow: hidden.
```
**Syn**
```bash
text-overflow: clip | ellipsis;

- Clip: Nội dung tràn ra sẽ bị cắt bỏ không hiển thị.
- Elipsis: Nội dung tràn bị ẩn và tự thêm vào dấu ba chấm …
```
## word-wrap & word-break
```bash
- word-wrap     : Cho phép đoạn text xuống hàng cho dù chữ đó dài cỡ nào đi nữa.
- word-break    : cho một chuỗi hiển thị và xuống hàng tại bất kì vị trí nào miễn là nó đã hiển thị full width.
```
**Syn: word-wrap**
```bash
word-wrap: Normal | break-word | initial | inherit;

- normal        : Trạng thái mặc định, tức là hiển thị theo mặc định của trình duyệt.
- break-word    : Sẽ nhảy xuống hàng nếu chữ quá dài.
- initial       : Trở về trang thái mặc định.
- inherit       : Kế thừa giá trị từ thẻ HTML cha.
```
**Syn: word-break**
```bash
word-break: normal | break-all | keep-all | initial | inherit;

- normal: Trạng thái mặc định, tức là sẽ dừng xuống hàng theo mặc định.
- break-all: Có thể xuống hàng bất kì lúc nào khi nó đã hiển thị full width.
- keep-all: Xuống hàng nếu chữ hiển thị sẽ bị tràn (overflow).
- initial: Trở về trang thái mặc định.
- inherit: Kế thừa giá trị từ thẻ HTML cha.
```
## text-transform
```bash
Thiết lập chữ in hoa hay thường.
```
## text-shadow 
```bash
Để tạo ra hiệu ứng đổ bóng cho chữ.
```
**Syn**
```bash
text-shadow: h-shadow | v-shadow | blur-radius | color | none | initial | inherit;

- h-shadow: Vị trí bóng ngang so với chữ, số âm sẽ đẩy lên trên và số dương sẽ đẩy xuống dưới.
- v-shadow: Vị trí bóng dọc so với chứ, số âm sẽ đẩy lui phía sau và số dương sẽ đẩy tới phía trước.
- blur-radius: Độ nhòe của chữ bóng, tính bằng pixel.
- color: Màu sắc của bóng, chấp nhận các.
```
# fonts
**Syn**
```bash
font: style | variant | weight | size/height | family;
```
## font-family 
```bash
Có thể sử dụng google font https://fonts.google.coma/
```
## font-style
```bash
Để thiết lập chữ in thường hoặc in nghiêng.
```
## font-weight
```bash
Để làm đậm chữ, hay làm dày chữ.
```
## font-variant 
```bash
chuyển các "ký tự in thường” trong văn bản sang dạng "ký tự in hoa" hay không. Những ký tự được chuyển sang in hoa sẽ có kích thước nhỏ hơn ký tự in hoa bình thường.
```
# lists
**Syn**
```bash
list-style: style | position | image;
```
## list-style-type
```bash
Xác định kiểu của chỉ mục.
```
**Syn**
```bash
list-style-type: value;

- none
- armenian
- circle
- cjk-ideographic
- decimal
- decimal-leading-zezo
- disc
- georgian
- hebrew
- hiragana
- hiragana-iroha
- katakana
- katakana-iroha
- lower-alpha
- lower-greek
- lower-latin
- lower-roman
- square
- upper-alpha
- upper-latin
- upper-roman
- inherit
```
## list-style-image
```bash
Thay thế các chỉ mục bằng chỉ mục hình ảnh.
```
**Syn**
```bash
list-style-image: url(‘…’);
```
## list-style-position
```bash
Xác định vị trí hiển thị của các chỉ mục so với đoạn text.
```
**Syn**
```bash
list-style-position: value;

- none: Không hiển thị image list, đây là dạng mặc định.
- inherit: Kế thừa thuộc tính của phần tử cha.
- inside: Xác định chỉ mục nằm bên trong nôi dung.
- outside: Xác định chỉ mục nằm bên ngoài nội dung.
```
 tooltips
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