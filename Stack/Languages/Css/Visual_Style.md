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