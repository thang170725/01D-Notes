- [!important](#important)
- [@layer (giúp Tailwind quản lý thứ tự ưu tiên và hỗ trợ tree-shaking (loại bỏ CSS không dùng))](#layer-giúp-tailwind-quản-lý-thứ-tự-ưu-tiên-và-hỗ-trợ-tree-shaking-loại-bỏ-css-không-dùng)
  - [@layer base (Dùng cho các style nền tảng)](#layer-base-dùng-cho-các-style-nền-tảng)
  - [@layer components (Dùng cho các component tái sử dụng)](#layer-components-dùng-cho-các-component-tái-sử-dụng)
- [@layer utilities (Dùng để tạo utility class giống như utility của Tailwind)](#layer-utilities-dùng-để-tạo-utility-class-giống-như-utility-của-tailwind)
- [@apply](#apply)
---
# !important
```bash
- Tailwind v3 trở xuống: đặt ! ở đằng trước.
- Tailwind v4: đặt ! ở đằng sau.
  Ví dụ:
    Tailwind v3
      <p class="!text-2xl">
          Hello
      </p>
      ✅ Đúng

    Tailwind v4
      <p class="text-2xl!">
          Hello
      </p>

      ✅ Đúng
```
**Ex1: Ghi đè class khác**
```html
<p class="text-blue-500 !text-red-500">
    Hello
</p>

<!-- 
text-blue-500 → chữ xanh
!text-red-500 → chữ đỏ vì có !important

CSS tương đương:

color: blue;
color: red !important;
-->
```
# @layer (giúp Tailwind quản lý thứ tự ưu tiên và hỗ trợ tree-shaking (loại bỏ CSS không dùng))
```bash
Là một tính năng của Tailwind CSS dùng để đăng ký CSS vào các layer của Tailwind.

Trong Tailwind có 3 layer chính:
  - @layer base
  - @layer components
  - @layer utilities
```
## @layer base (Dùng cho các style nền tảng)
**Ex**
```css
@layer base {
  h1 {
    font-size: 2rem;
  }

  body {
    margin: 0;
  }
}
/* Sau khi build, Tailwind sẽ đặt các rule này vào phần base. */
```
## @layer components (Dùng cho các component tái sử dụng)
**Ex**
```css
@layer components {
  .btn-primary {
    @apply px-4 py-2 rounded bg-blue-500 text-white;
  }
}

/* Sử dụng: */
<button class="btn-primary">
  Save
</button>
```
# @layer utilities (Dùng để tạo utility class giống như utility của Tailwind)
**Ex**
```css
@layer utilities {
  .rotate-y-180 {
    transform: rotateY(180deg);
  }
}

/* Sau đó: */
<div class="rotate-y-180">
/* sử dụng y hệt utility mặc định của Tailwind. */
```
# @apply