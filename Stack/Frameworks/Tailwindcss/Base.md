- [Introduction](#introduction)
- [Installation](#installation)
- [@apply](#apply)
---
# Introduction
```bash
viết class trực tiếp trong HTML thay vì viết CSS riêng.
```
# Installation
```bash
1. npm install -D tailwindcss postcss autoprefixer
2. npx tailwindcss init -p hoặc npx tailwindcss@3.4.17 init -p (ổn định)
```
**Case2: Cách mới**
```bash
1. npm install tailwindcss @tailwindcss/vite
2. npm install react-router-dom
```
**Ex**
```html
<button class="bg-blue-500 text-white px-4 py-2 rounded">
  Click me
</button>
```
```js
<script src="https://cdn.tailwindcss.com"></script>
```
# @apply
```bash
để tự custom className trong file css
```
**Ex**
```css
.input-light {
    @apply w-full pl-10 pr-3 py-2.5 rounded-xl text-sm transition-all;
    background: #f8fafc;
    border: 1px solid #e2e8f0;
    color: #0f172a;
  }
```