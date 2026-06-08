- [Introduction](#introduction)
- [text (Màu chữ)](#text-màu-chữ)
- [Background Color (xử lý màu cho background)](#background-color-xử-lý-màu-cho-background)
  - [bg- (css màu nền)](#bg--css-màu-nền)
  - [Background linear-to- (dải màu chuyển)](#background-linear-to--dải-màu-chuyển)
    - [from- (màu bắt đầu)](#from--màu-bắt-đầu)
    - [via- (màu ở giữa)](#via--màu-ở-giữa)
    - [to- (màu ở cuối)](#to--màu-ở-cuối)
- [shadow](#shadow)
---
# Introduction
```bash
- Dùng để xử lý màu sắc (text-color, background-color, border-color).
```
# text (Màu chữ)
**Ex1**
```js
<p className="text-red-500">Red text</p>
<p className="text-blue-600">Blue text</p>
<p className="text-slate-800">Dark text</p>
<p className="text-[#ff5733]">Custom color</p>
<p className="text-[rgb(255,255,255)]">White</p>
<p className="text-[rgba(255,255,255,0.7)]">White 70%</p>
<p className="text-[oklch(95%_0.01_240)]">Text OKLCH</p>
```
# Background Color (xử lý màu cho background)
## bg- (css màu nền)
**Ex**
```html
<div className="bg-red-500"></div>
<div className="bg-blue-100"></div>
<div className="bg-slate-800"></div>

<!-- Màu HEX / RGB / custom (chuẩn giống w-[200px]) -->
<div className="bg-[#ff5733]"></div>
<div className="bg-[rgb(255,0,0)]"></div>
<div className="bg-[rgba(0,0,0,0.5)]"></div>
```
**Ex2: Background image (Dùng URL trực tiếp)**
```html
<div className="bg-[url('/images/bg.png')] bg-cover bg-center"></div>
```
## Background linear-to- (dải màu chuyển)
```html
<div className="bg-linear-to-r from-blue-500 to-purple-500"></div>

<!-- Hoặc custom màu: -->
<!-- <div className="bg-gradient-to-r from-[#ff5733] to-[#00ffcc]"></div> -->
```
### from- (màu bắt đầu)
### via- (màu ở giữa)
### to- (màu ở cuối)
✅ Border cơ bản
<div className="border">...</div>


👉 mặc định: 1px solid #e5e7eb

🎨 Border màu
border-red-500
border-slate-300
border-[#ff5733]
# shadow
```bash
className="shadow-[0_4px_10px_rgba(14,165,233,0.4)]"
```