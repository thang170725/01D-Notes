- [rounded](#rounded)
- [shadow](#shadow)
- [font (chỉnh chữ)](#font-chỉnh-chữ)
- [Border (chỉnh đường viền)](#border-chỉnh-đường-viền)
- [text](#text)
- [Background (Chỉnh nền)](#background-chỉnh-nền)
  - [bg-cover](#bg-cover)
  - [bg-no-repeat](#bg-no-repeat)
  - [bg-center](#bg-center)
- [Backdrop (Chỉnh style đằng sau)](#backdrop-chỉnh-style-đằng-sau)
  - [backdrop-blur](#backdrop-blur)
---
# rounded
```bash
- Bo góc cho phần tử.
```
**Syn**
```bash
- rounded-sm	: bo nhẹ
- rounded	    : bo vừa
- rounded-md	: bo trung bình
- rounded-lg	: bo khá lớn
- rounded-xl	: bo rất lớn
- rounded-full	: bo tròn hoàn toàn
- rounded-tl-lg : bo 1 góc trên trái
- rounded-bl-lg : bo 1 góc dưới trái
```
**Ex**
```js
<div class="w-40 h-20 bg-blue-500 rounded-lg"></div>
```
# shadow
```bash
- Đổ bóng lớn (large shadow) cho phần tử.
- Dùng để tạo cảm giác nổi lên khỏi nền.
```
**Syn**
```bash
- shadow-sm	    : bóng rất nhẹ
- shadow	      : bóng mặc định
- shadow-md	    : bóng vừa
- shadow-lg	    : bóng rõ, sâu
- shadow-xl	    : bóng rất sâu
- shadow-2xl	: bóng cực sâu
```
**Ex**
```js
<div class="w-40 h-20 bg-white shadow-lg"></div>

Trông giống card nổi.
```
# font (chỉnh chữ)
**Ex**
```js
<p className="font-thin">Thin (100)</p>
<p className="font-light">Light (300)</p>
<p className="font-normal">Normal (400)</p>
<p className="font-medium">Medium (500)</p>
<p className="font-semibold">Semi Bold (600)</p>
<p className="font-bold">Bold (700)</p>
<p className="font-extrabold">Extra Bold (800)</p>
<p className="font-black">Black (900)</p>
```
**Ex1: Hover đổi độ dày**
```html
<li className="font-medium hover:font-semibold transition-all duration-300">
  Dashboard
</li>
```
**Ex2: sidebar menu**
```html
<Link
  to="/dashboard"
  className="block p-2 font-medium text-white hover:font-semibold transition-all duration-300"
>
  Dashboard
</Link>
```
# Border (chỉnh đường viền)
**Chỉnh độ dày**
```bash
border       // 1px
border-2     // 2px
border-4     // 4px
border-8     // 8px
border-t
border-b
border-l
border-r
```
**Chỉnh kiểu đường viền**
```bash
border-dashed
border-dotted
border-double
```
**Ex**
```html
<div className="border border-slate-300 rounded-md p-4">
  Card
</div>
```
# text 
```bash
- shadow-sm	    : bóng rất nhẹ
- shadow	    : bóng mặc định
- shadow-md	    : bóng vừa
- shadow-lg	    : bóng rõ, sâu
- text-xl	    : bóng rất sâu
- shadow-2xl	: bóng cực sâu
```
# Background (Chỉnh nền)
## bg-cover
## bg-no-repeat
## bg-center
# Backdrop (Chỉnh style đằng sau)
## backdrop-blur