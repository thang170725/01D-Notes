- [transform](#transform)
  - [skew() – skewX() – skewY() (Dùng để bẻ góc độ của các cạnh.)](#skew--skewx--skewy-dùng-để-bẻ-góc-độ-của-các-cạnh)
  - [translate() – translateX() – translateY() (Di chuyển đối tượng từ vị tri hiện tại của nó)](#translate--translatex--translatey-di-chuyển-đối-tượng-từ-vị-tri-hiện-tại-của-nó)
  - [scale() – scaleX() – scaleY() (Dùng để kéo giãn đối tượng HTML)](#scale--scalex--scaley-dùng-để-kéo-giãn-đối-tượng-html)
- [transform-origin (thay đổi vị trí của các phần tử được chuyển đổi)](#transform-origin-thay-đổi-vị-trí-của-các-phần-tử-được-chuyển-đổi)
- [transitions (Tạo ra hiệu ứng, chuyển động thay đổi từ giá trị này sang giá trị khác)](#transitions-tạo-ra-hiệu-ứng-chuyển-động-thay-đổi-từ-giá-trị-này-sang-giá-trị-khác)
  - [transition-delay (xác định khoản thời gian trì hoãn)](#transition-delay-xác-định-khoản-thời-gian-trì-hoãn)
- [animations (tạo các hiệu ứng di chuyển)](#animations-tạo-các-hiệu-ứng-di-chuyển)
  - [animation-play-state (chỉ định hoạt ảnh ảnh đang chạy hoặc tạm dừng)](#animation-play-state-chỉ-định-hoạt-ảnh-ảnh-đang-chạy-hoặc-tạm-dừng)
- [@keyfames  (Chỉ định tác vụ thay đổi của animation)](#keyfames--chỉ-định-tác-vụ-thay-đổi-của-animation)
- [Matrix() (Là tổng hợp các hiệu ứng)](#matrix-là-tổng-hợp-các-hiệu-ứng)
- [rotate() (Dùng để xoay đối tượng HTML theo một góc độ nào đó)](#rotate-dùng-để-xoay-đối-tượng-html-theo-một-góc-độ-nào-đó)
- [CSS Pseudo-classes (thao tác với con trỏ chuột tạo ra một số thay đổi cho thuộc tính nào đó)](#css-pseudo-classes-thao-tác-với-con-trỏ-chuột-tạo-ra-một-số-thay-đổi-cho-thuộc-tính-nào-đó)
  - [:focus (Để chọn và định dang phần tử được lấy nét. Thường sử dụng cho thẻ input)](#focus-để-chọn-và-định-dang-phần-tử-được-lấy-nét-thường-sử-dụng-cho-thẻ-input)
  - [:valid (Để định dạng các phần tử biểu mẫu hợp lệ)](#valid-để-định-dạng-các-phần-tử-biểu-mẫu-hợp-lệ)
- [CSS Pseudo-elements](#css-pseudo-elements)
  - [::before (Để chèn một số nội dung trước nội dung của phần tử)](#before-để-chèn-một-sốnội-dung-trước-nội-dung-của-phần-tử)
  - [::after (Để chèn một số nội dung sau nội dung của phần tử)](#after-để-chèn-một-số-nội-dung-sau-nội-dung-của-phần-tử)
- [cursor (Xác định hình dạng con trỏ chuột khi trỏ qua một phần tử)](#cursor-xác-định-hình-dạng-con-trỏ-chuột-khi-trỏ-qua-một-phần-tử)
- [pointer-events (Xác định xem liệu một phần tử nào đó có phản ứng với các sự kiện con trỏ hay không)](#pointer-events-xác-định-xem-liệu-một-phần-tử-nào-đó-có-phản-ứng-với-các-sự-kiện-con-trỏ-hay-không)
---
# transform
## skew() – skewX() – skewY() (Dùng để bẻ góc độ của các cạnh.)
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
## translate() – translateX() – translateY() (Di chuyển đối tượng từ vị tri hiện tại của nó)
**Syn**
```bash
transform: translate();

- translate(x, y)
- translateX(x)
- translateY(y)
Trong đó: x là di chuyển sang phải (nếu số dương) và sang trái (nếu số âm). y là di chuyển xuống (nếu số dương) và lên (nếu số âm).
```
## scale() – scaleX() – scaleY() (Dùng để kéo giãn đối tượng HTML)
**Syn**
```bash
transform: scale(x, y) (x là kéo dài theo chiều rộng, y là kéo dài theo chiều cao)
…
```
# transform-origin (thay đổi vị trí của các phần tử được chuyển đổi)
```bash
Các phép biến đổi 2d có thể thay đổi trục x và y của một phần tử. Các phép biến đổi 3d cũng có thể thay đổi trục z của một phần tử.
Lưu ý: Thuộc tính này phải được sử dụng cùng với thuộc tính biến đổi transform.
```
**Syn**
```bash
transform-origin: x-axis y-axis z-axis | initial | inherit

    - x-axis: Xác định vị trí của chế độ xem ở trục x. Có những giá trị left, center, right, length, %.
    - y-axis: Xác định vị trí của chế độ xem ở trục y. Có những giá trị top, center, bottom, length, %.
    - z-axis: Xác định vị trí của chế độ xem ở trục z trong không gian 3d. có giá trị là length.
    - initial: Đặt thuộc tính thành giá trị mặc định của nó.
    - inherit: Thừa hưởng giá trị của phần tử cha.
```
# transitions (Tạo ra hiệu ứng, chuyển động thay đổi từ giá trị này sang giá trị khác)
```bash 
Có 2 đầu vào bắt buộc là thuộc tính cần thay đổi và thời gian để tạo ra quá trình thay đổi.
```
**Syn**
```bash
trasition: name time timing-function, …;

- timing-function
    + ease: Bắt đầu chậm sau đó nhanh dần và gần kết thúc lại chậm từ từ.
    + linear: Bắt đầu và kết thúc tốc độ là như nhau.
    + ease-in: Chậm lúc đầu.
    + ease-out: Chậm lúc kết thúc.
    + ease-in-out: Chậm lúc bắt đầu và kết thúc.
```
## transition-delay (xác định khoản thời gian trì hoãn)
```bash
Đơn vị là giá trị unit + “s” (VD: 1s;)
```
# animations (tạo các hiệu ứng di chuyển)
**Syn: (chú ý về thứ tự khai báo)**
```bash
animation: name | duration | timing-function | delay | iteration-count | direction | fill;

- name              : Là tên của hiệu ứng, phần mà được định nghĩa trong keyframe (tự đặt).
- duration          : Chỉ định thời gian từ lúc hiệu ứng bắt đầu cho đến khi kết thúc. Đơn vị là s(giây).
- timing-function   : Để thay đổi trạng thái của đối tượng.
    + linear: giữ tốc độ như nhau từ lúc bắt đầu cho đến khi kết thúc.
    + ease: bắt đầu chậm sau đó nhanh và kết thúc chậm dần.
    + ease-in: bắt đầu chậm.
    + ease-out: kết thúc chậm.
    + ease-in-out: bắt đầu chậm và kết thúc chậm.
- delay             : Chỉ định thời gian chờ trước khi hiệu ứng bắt đầu thực thi. Đơn vị là s(giây)
- iteration-count   : Chỉ định số lần hiệu ứng lập lại. giá trị là số, không có đơn vị hoặc infinite (lặp vô hạn).
- direction         : Định dạng hướng di chuyển của đối tượng.
    + normal: di chuyên về phía trước.
    + reverse: di chuyển theo hướng về phía sau.
    + alternate: di chuyển về phía trước rồi di chuyển về phía sau.
    + alternate-reverse: di chuyển về phía sau rồi di chuyển về phía trước.
- fill              : Định dạng trạng thái của đối tượng.
    + forwards: trạng thái của đối tượng sẽ đẽ thể hiện như cấu hình cuối cùng trong quy tắc keyframe.
    + backwards: trạng thái của đối tượng sẽ đẽ thể hiện như cấu hình đầu tiên trong quy tắc keyframe (lưu ý chỉ trong thời gian diễn ra hiệu ứng).
    + both: sự hòa trộn giữa forwards và backwards.
```
## animation-play-state (chỉ định hoạt ảnh ảnh đang chạy hoặc tạm dừng)
# @keyfames <animation-name> (Chỉ định tác vụ thay đổi của animation)
**Syn** 
```bash
from{}…to{}… hoặc %{}
```
# Matrix() (Là tổng hợp các hiệu ứng)
**Syn**
```bash
matrix(scaleX, skewY, skewX, scaleY, translateX, translateY)
```
# rotate() (Dùng để xoay đối tượng HTML theo một góc độ nào đó)
# CSS Pseudo-classes (thao tác với con trỏ chuột tạo ra một số thay đổi cho thuộc tính nào đó) 
## :focus (Để chọn và định dang phần tử được lấy nét. Thường sử dụng cho thẻ input)
**Ex: Khi click vào ô input thì ô input đó chuyển thành màu xanh**
```html
<input type="text">
```
```css
input:focus{
  background-color: aqua;
}
```
## :valid (Để định dạng các phần tử biểu mẫu hợp lệ)
**Ex**
```html
<input type="text">
```
```css
input:focus:valid{
  background-color: aqua;
}
```
# CSS Pseudo-elements
## ::before (Để chèn một số nội dung trước nội dung của phần tử)
## ::after (Để chèn một số nội dung sau nội dung của phần tử)
**Ex: ::before và ::after**
```html
<div>Welcome to VietNam</div>
```
```css
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
```
# cursor (Xác định hình dạng con trỏ chuột khi trỏ qua một phần tử)
**Syn** 
```bash
cursor: value;

- pointer: Hình ngón tay
- zoom-in: Hình biểu tượng zoom dấu +
```
**Ex**
```html
<img class="zoom-img" src="scatter.png" alt="Zoom Image">
```
```css
.zoom-img {
width: 300px;
height: auto;
transition: transform 0.3s ease;
}

.zoom-img:hover {
transform: scale(1.5);
cursor: zoom-in;
}
```
# pointer-events (Xác định xem liệu một phần tử nào đó có phản ứng với các sự kiện con trỏ hay không)
**Syn**
```bash
Pointer-events: auto | none | initial | inherit
```
**Ex**
```html
<a href="https://www.w3schools.com/cssref/tryit.php?filename=trycss3_pointer-events">Click</a>
```
```css
a{
  pointer-events: none;
}
```