- [:root \& var() (Định nghĩa các biến CSS toàn cục có thể tái sử dụng nhiều lần)](#root--var-định-nghĩa-các-biến-css-toàn-cục-có-thể-tái-sử-dụng-nhiều-lần)
- [title (Dùng để bổ sung ý nghĩa cho nội dung. Nằm trong thẻ)](#title-dùng-để-bổ-sung-ý-nghĩa-cho-nội-dung-nằm-trong-thẻ)
---
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