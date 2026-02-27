- [skew() – skewX() – skewY()](#skew--skewx--skewy)
---
# skew() – skewX() – skewY()
```bash
Dùng để bẻ góc độ của các cạnh.
```
**Syn**
```bash
transform: skew(xdeg, ydeg);
```
**Ex**
```html
<div>skew 20deg</div>
<div>skew 20deg 20deg</div>
```
```css
div{
    display: inline-block;
}
div:nth-child(1){
    margin-left: 100px;
    width: 100px;
    height: 100px;
    background-color: #f00;
    transform: skew(20deg);
}
div:nth-child(2){
    margin-left: 100px;
    margin-top: 100px;
    width: 100px;
    height: 100px;
    background-color: #f00;
    transform: skew(20deg, 20deg);
}
```
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