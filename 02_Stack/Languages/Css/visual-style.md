- [Box-shadow](#box-shadow)
- [backround-image](#backround-image)
- [border](#border)
  - [border-style \& Border-width \& Border-color](#border-style--border-width--border-color)
  - [border-top-style \& border-right-style \& border-bottom-style \& border-left-style](#border-top-style--border-right-style--border-bottom-style--border-left-style)
- [Những website lấy icon](#những-website-lấy-icon)
---
# Box-shadow
```bash
- Để tạo bóng cho khối bao ngoài.
```
**Syn**
```bash
Box-shadow: h-shadow v-shadow blur spread color | inset | initial | inherit
Trong đó:
    • h-shadow: Vị trí bóng ngang so với chữ, số âm sẽ đẩy lên trên và số dương sẽ đẩy xuống dưới.
    • v-shadow: Vị trí bóng dọc so với chứ, số âm sẽ đẩy lui phía sau và số dương sẽ đẩy tới phía trước.
    • blur-radius: Độ nhòe của chữ bóng, tính bằng pixel.
    • spread: Kích thước của bóng tối.
    • color: Màu sắc của bóng, chấp nhận các inset: thay đổi bóng từ bên ngoài vào trong thay vì từ trong ra ngoài.
    • initial: Thiết lập giá trị mặc định.
    • inherit: Kế thừa giá trị từ thẻ HTML cha.
```
# backround-image
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

background-repeat 
Để Lặp hình nền hoặc không.
background-repeat: value;
value:
    • repeat-x: Lặp theo chiều ngang.
    • repeat-y: Lặp theo chiều dọc.
    • repeat: Lặp full block.
    • space: Lặp các góc của khối.
    • round: Lặp full khối.
    • no-repeat: Không lặp.
    • space-repeat: Lặp bỏ trống phần giữa theo chiều dọc.
    • round-space: Lặp bỏ trống phần giữa theo chiều ngang.
# border 
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
## border-style & Border-width & Border-color
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
## border-top-style & border-right-style & border-bottom-style & border-left-style
```bash
- Thiết lập đường viền trên top.
- Thiết lập đường viền bên phải.
- Thiêt lập đường viền dưới.
- Thiết lập đường viền bên trái.
```


border-image
Sử dụng hình ảnh làm đường viền của phần tử.
border-image-source
Chỉ định đường dẫn chứa hình ảnh được sử dụng để làm đường viền.
border-image-slice
Chỉ định cách cắt hình ảnh như thế nào.
border-image-width
Chỉ định độ rộng của hình ảnh.
border-image-outset
Chỉ định số lượng mà khu vực hình ảnh vượt qua ngoài cái hộp (box) của nó.
border-image-repeat
Chỉ định hình ảnh nên được lặp lại (repeated), làm tròn (rounded) hay kéo dài (stretched).
border-radius
Thiết lập bo góc cho viền. giá trị là number + đơn vị.
    • Nếu có 4 giá trị thì lần lượt là top-left, top-right, bottom-right, bottom-left.
    • Nếu có 3 giá trị thì lần lượt là top-left, toprihgt-bottom-left, bottom-right.
    • Nếu có 2 giá trị thì lần lượt là topleft-bottomright, topright-bottomleft.
    • Nếu có 1 giá trị thì giá trị đó là cả 4 góc.
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <style>
        body > div{
            position: relative;
            width: 100px;
            height: 100px;
            background-color: #000;
            border-radius: 10px / 20px;
        }
    </style>
</head>
<body>
    <div>
   </div>
</body>
</html>

Thiết lập góc bo tròn cho phần tử, sử dụng đường chéo để chỉ định bán kính bo tròn theo các góc khác nhau.
10px (bo tròn trên dưới)
20px (bo tròn trái phải)
Website tạo đường bo góc
    • Fancy-boder-radius
border-top-left-radius
Góc trên bên trái sẽ được uốn cong. Có thể truyền 1 hoặc 2 giá trị.
border-top-right-radius
Góc trên bên phải sẽ được uốn cong. Có thể truyền 1 hoặc 2 giá trị.
border-bottom-left-radius
Góc dưới bên trái sẽ được uốn cong. Có thể truyền 1 hoặc 2 giá trị.
border-bottom-right-radius
Góc dưới bên phải sẽ được uốn cong. Có thể truyền 1 hoặc 2 giá trị.
# Những website lấy icon 
    • Fontawasome
    • Adnjs
    • Boxicons.com
    • Ionicons
outline-color
Thiết lập màu sắc.
outline-offset
Thêm khoảng trắng vào giữa outline và border. Khoảng trắng là trong suốt.
Text
Text Color
Thiết lập màu sắc cho chữ.
Cú pháp:
color: CSS colors;

Text decoration
Cú pháp:
text-decoration: line | color | style | thickness;
text-decoration-line
Dùng để thiết lập một đường gạch cho văn bản.
Cú pháp:
text-decoration-line: none | underline | line-through | overline | initial | inherit;
    • none: Không có đường gạch chân.
    • underline: Tạo một đường gạch chân.
    • overline: Tạo một đường gạch trên đầu văn bản.
    • line-through: Tạo một đường gạch giữa văn bản.
    • initial: Sử dụng giá trị mặc định.
    • inherit: Kế thừa thuộc tính từ phần tử cha.
text-decoration-color
Để thiết lập màu sắc cho đường gạch chân. Sử dụng khi có khai báo text-decoration.
Cú pháp:
text-decoration-color: CSS colors | initial | inherit
text-decoration-style
Thiệt lập kiểu đường gạch.
value:
    • solid: Giá trị mặc định, đường gạch là đường nét liền thẳng.
    • double: 2 đường thẳng song song với nhau.
    • dotted: Đường thẳng chấm bi, nét đứt.
    • dashed: Đường thẳng nét đứt.
    • wavy: Đường sóng.
    • initial: Lấy giá trị mặc định.
    • inherit: Lấy giá trị giống phần tử cha.
text-decoration-thickness
Để thiết lập độ dày cho đường gạch.
value:
    • auto: Chọn độ dày dựa vào trình duyệt
    • from-font: Nếu tệp font chữ chứa thông tin về độ dày, thì sử dụng giá trị đó, nếu không thì có chức năng giống auto
    • length/percetage: Chỉ định độ dày theo chiều dài hoặc %
    • initial: Lấy giá trị mặc định
    • inherit: Lấy giá trị giống phần tử cha
text-overflow
Text-overflow chỉ hoạt động hay thực thi khi ta thiết lập thuộc tính white-space: nowrap và thiết lập overflow: hidden.
Cú pháp:
text-overflow: clip | ellipsis;
    • Clip: Nội dung tràn ra sẽ bị cắt bỏ không hiển thị.
    • Elipsis: Nội dung tràn bị ẩn và tự thêm vào dấu ba chấm …