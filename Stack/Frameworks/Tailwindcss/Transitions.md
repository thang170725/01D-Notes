- [transition-colors (hiệu ứng chuyển động của màu sắc)](#transition-colors-hiệu-ứng-chuyển-động-của-màu-sắc)
- [transition-opacity (Chỉ animate độ trong suốt)](#transition-opacity-chỉ-animate-độ-trong-suốt)
- [transition-transform (Chỉ animate transform (scale, rotate, translate...))](#transition-transform-chỉ-animate-transform-scale-rotate-translate)
- [transition-all (mọi thuộc tính CSS thay đổi đều có hiệu ứng chuyển động)](#transition-all-mọi-thuộc-tính-css-thay-đổi-đều-có-hiệu-ứng-chuyển-động)
  - [ease-in-out](#ease-in-out)
  - [delay-](#delay-)
  - [duration-](#duration-)
---
# transition-colors (hiệu ứng chuyển động của màu sắc)
**Ex**
```html
<li className="p-2 hover:bg-[oklch(50%_0.066_243.157)] transition-colors duration-500">
  <a href="">Dashboard</a>
</li>

<!--
transition-colors → chỉ animate màu (nhẹ & mượt)
duration-500 → 500ms = 0.5s
Hover vào / ra đều mượt
-->
```
# transition-opacity (Chỉ animate độ trong suốt)
# transition-transform (Chỉ animate transform (scale, rotate, translate...))
# transition-all (mọi thuộc tính CSS thay đổi đều có hiệu ứng chuyển động)
**Ex**
```html
<!-- Hover vào sẽ đổi màu ngay lập tức. -->
<button className="bg-blue-500 hover:bg-red-500">
    Button
</button>

<!-- thì khi hover: màu xanh → đỏ sẽ chuyển dần trong 300ms. -->
<button className="bg-blue-500 hover:bg-red-500 transition-all duration-300">
    Button
</button>
```
## ease-in-out
**Ex**
```html
<li className="p-2 hover:bg-[oklch(50%_0.066_243.157)] transition-colors duration-500 ease-in-out">
```
## delay-
**Ex**
```html
<li className="p-2 hover:bg-[oklch(50%_0.066_243.157)] transition-colors delay-500">
```
## duration-