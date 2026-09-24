- [inline \& external \& internal](#inline--external--internal)
- [Comment](#comment)
- [Combinators](#combinators)
  - [Demo về ~](#demo-về-)
- [Selector](#selector)
- [:root \& var() (Định nghĩa các biến CSS toàn cục có thể tái sử dụng nhiều lần)](#root--var-định-nghĩa-các-biến-css-toàn-cục-có-thể-tái-sử-dụng-nhiều-lần)
- [title (Dùng để bổ sung ý nghĩa cho nội dung. Nằm trong thẻ)](#title-dùng-để-bổ-sung-ý-nghĩa-cho-nội-dung-nằm-trong-thẻ)
---
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
# :root & var() (Định nghĩa các biến CSS toàn cục có thể tái sử dụng nhiều lần)
```bash
Root giúp quản lý theme màu, kích thước, spacing một cách dễ dàng. Chỉnh một lần ảnh hưởng toàn bộ trang. Hưu ích khi làm dark mode, light mode hoặc theme động bằng javascript.
```
**Ex**
```css
:root{
    --bg: #ff0;
}
body{
    background-color: var(--bg);
}
```
# title (Dùng để bổ sung ý nghĩa cho nội dung. Nằm trong thẻ)