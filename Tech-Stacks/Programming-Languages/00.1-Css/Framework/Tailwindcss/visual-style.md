- [rounded](#rounded)
- [shadow](#shadow)
- [Text (Chỉnh chữ)](#text-chỉnh-chữ)
  - [font- (chỉnh độ dày của chữ)](#font--chỉnh-độ-dày-của-chữ)
  - [text- (chỉnh độ to, nhỏ của chữ)](#text--chỉnh-độ-to-nhỏ-của-chữ)
- [Border (chỉnh đường viền)](#border-chỉnh-đường-viền)
- [shadow-](#shadow-)
- [Background (Chỉnh nền)](#background-chỉnh-nền)
  - [bg-cover](#bg-cover)
  - [bg-no-repeat](#bg-no-repeat)
  - [bg-center](#bg-center)
- [Backdrop (Chỉnh style đằng sau)](#backdrop-chỉnh-style-đằng-sau)
  - [backdrop-blur- (làm mờ nền phía sau)](#backdrop-blur--làm-mờ-nền-phía-sau)
  - [backdrop-brightness (Điều chỉnh độ sáng nền phía sau)](#backdrop-brightness-điều-chỉnh-độ-sáng-nền-phía-sau)
  - [backdrop-contrast (Tăng/giảm độ tương phản nền)](#backdrop-contrast-tănggiảm-độ-tương-phản-nền)
  - [backdrop-grayscale (Biến nền phía sau thành đen trắng)](#backdrop-grayscale-biến-nền-phía-sau-thành-đen-trắng)
  - [backdrop-hue-rotate (Xoay tông màu)](#backdrop-hue-rotate-xoay-tông-màu)
  - [backdrop-invert (Đảo màu nền phía sau)](#backdrop-invert-đảo-màu-nền-phía-sau)
  - [backdrop-opacity (Thay đổi độ trong suốt của nền phía sau)](#backdrop-opacity-thay-đổi-độ-trong-suốt-của-nền-phía-sau)
  - [backdrop-saturate (Tăng độ rực màu)](#backdrop-saturate-tăng-độ-rực-màu)
  - [backdrop-sepia (Tạo hiệu ứng ảnh cổ)](#backdrop-sepia-tạo-hiệu-ứng-ảnh-cổ)
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
# Text (Chỉnh chữ)
## font- (chỉnh độ dày của chữ)
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
## text- (chỉnh độ to, nhỏ của chữ)
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
# shadow- 
```bash
- shadow-sm	    : bóng rất nhẹ
- shadow	    : bóng mặc định
- shadow-md	    : bóng vừa
- shadow-lg	    : bóng rõ, sâu
- shadow-2xl	: bóng cực sâu
```
# Background (Chỉnh nền)
## bg-cover
## bg-no-repeat
## bg-center
# Backdrop (Chỉnh style đằng sau)
## backdrop-blur- (làm mờ nền phía sau)
```html
<div class="bg-white/20 backdrop-blur-md p-6 rounded-lg">
  Glassmorphism Card
</div>
```
## backdrop-brightness (Điều chỉnh độ sáng nền phía sau)
```html
<div class="bg-white/10 backdrop-brightness-50 p-6">
  Darker Background
</div>
```
## backdrop-contrast (Tăng/giảm độ tương phản nền)
```html
<div class="bg-white/20 backdrop-contrast-200 p-6">
  High Contrast
</div>
```
## backdrop-grayscale (Biến nền phía sau thành đen trắng)
```html
<div class="bg-white/20 backdrop-grayscale p-6">
  Black & White Background
</div>
```
## backdrop-hue-rotate (Xoay tông màu)
```html
<div class="bg-white/20 backdrop-hue-rotate-90 p-6">
  Hue Rotate
</div>
```
## backdrop-invert (Đảo màu nền phía sau)
```html
<div class="bg-white/20 backdrop-invert p-6">
  Inverted Background
</div>
```
## backdrop-opacity (Thay đổi độ trong suốt của nền phía sau)
```html
<div class="bg-white/20 backdrop-opacity-50 p-6">
  Opacity Example
</div>
```
## backdrop-saturate (Tăng độ rực màu)
```html
<div class="bg-white/20 backdrop-saturate-200 p-6">
  Vibrant Colors
</div>
```
## backdrop-sepia (Tạo hiệu ứng ảnh cổ)
```html
<div class="bg-white/20 backdrop-sepia p-6">
  Vintage Style
</div>
```