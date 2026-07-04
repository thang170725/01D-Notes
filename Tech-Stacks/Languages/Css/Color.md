- [HSL (Sử dụng bảng màu theo vòng tròn màu sắc)](#hsl-sử-dụng-bảng-màu-theo-vòng-tròn-màu-sắc)
- [HSLA](#hsla)
- [HSV (Hue, Saturation, Value)](#hsv-hue-saturation-value)
- [background-color (Để thiết lập màu sắc cho nền của phần tử.)](#background-color-để-thiết-lập-màu-sắc-cho-nền-của-phần-tử)
  - [linear-gradient (Để thiết lập dạng màu chuyển)](#linear-gradient-để-thiết-lập-dạng-màu-chuyển)
  - [repeating-linear-gradient](#repeating-linear-gradient)
  - [conic-gradient (đổi màu xoay quanh một điểm trung tâm)](#conic-gradient-đổi-màu-xoay-quanh-một-điểm-trung-tâm)
  - [Radial Gradients (Hiệu ứng màu chuyển lan tỏa ra tứ phía)](#radial-gradients-hiệu-ứng-màu-chuyển-lan-tỏa-ra-tứ-phía)
- [-webkit-text-fill-color (Css nhiều màu vào cho một chữ)](#-webkit-text-fill-color-css-nhiều-màu-vào-cho-một-chữ)
---
# HSL (Sử dụng bảng màu theo vòng tròn màu sắc)
**Syn**
```bash
hsl (hue, saturation, lightness);

- Hue: Là độ của màu trong vòng tròn, có giá trị từ 0 đến 360
    + 0 là màu đỏ
    + 120 là màu xanh lá cây
    + 240 là màu xanh da trời
- Saturation: là cường độ màu, có giá trị từ 0% đến 100%
- Lightness: là độ sáng của màu, có giá trị từ 0% đến 100%
```
# HSLA
```bash
Cách sử dụng giống với HSL nhưng thêm một thành phần alpha vào cuối định dạng độ trong suốt cho màu sắc.
```
**Syn**
```bash
hsla(hue, saturation, lightness, alpha)
```
**Ex**
```html
<div></div>
```
```css
div{
    height: 20px;
    background-color: hsla(0, 100%, 50%, 0.5);
}
```
# HSV (Hue, Saturation, Value)
```bash
Là hệ màu không có kênh sáng tối như grayscale, mà nó phân tách rõ về màu sắc
```
# background-color (Để thiết lập màu sắc cho nền của phần tử.)
**Syn**
```bash
Background-color: CSS colors | transparent

- Transparent: để thiết lập độ trong suốt cho nền
```
## linear-gradient (Để thiết lập dạng màu chuyển)
```bash
Trang web thiết kế dải màu linear-gradient đẹp mắt: https://webgradients.com/
```
**Syn**
```bash
background: linear-gradient(direction | angles, color1, color2, …);
```
## repeating-linear-gradient
## conic-gradient (đổi màu xoay quanh một điểm trung tâm)
**Syn** 
```bash
background-image: conic-gradient([fromangle] [at position,] color [degree], color [degree], ...);
```
**Ex: Tạo hình bàn cờ**
```html
<body>
    <div></div>
</body>
```
```css
body{
   background-image: repeating-conic-gradient(#5f0172 0 25%, #dfdb13 25% 50%);
   background-size: 384px 383px;
}
```
## Radial Gradients (Hiệu ứng màu chuyển lan tỏa ra tứ phía)
**Syn** 
```bash
background | background-image: radial-gradient(shape, size, at position, start-color, ..., last-color);
```
# -webkit-text-fill-color (Css nhiều màu vào cho một chữ)
**Ex**
```html
<div>Gradient</div>
```
```css
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
```