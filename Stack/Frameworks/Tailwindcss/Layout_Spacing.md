- [Width \& Height (thiết lập chiều cao \& chiều rộng)](#width--height-thiết-lập-chiều-cao--chiều-rộng)
  - [w \& h](#w--h)
  - [w-full](#w-full)
  - [min-w-](#min-w-)
  - [min-h-screen](#min-h-screen)
- [margin](#margin)
- [Padding](#padding)
- [relative](#relative)
- [flex (Hộp linh hoạt)](#flex-hộp-linh-hoạt)
  - [flex-](#flex-)
  - [flex-row       // mặc định](#flex-row--------mặc-định)
  - [flex-col       // dọc](#flex-col--------dọc)
  - [gap](#gap)
  - [items-center](#items-center)
  - [justify-start \& justify-center \& justify-end \& justify-between \& justify-around \& justify-evenly](#justify-start--justify-center--justify-end--justify-between--justify-around--justify-evenly)
  - [items-start \& items-end \& items-stretch](#items-start--items-end--items-stretch)
  - [flex-wrap](#flex-wrap)
- [grid](#grid)
  - [grid-cols](#grid-cols)
  - [col-span](#col-span)
- [ViewPort (Dùng để định vị trên viewport)](#viewport-dùng-để-định-vị-trên-viewport)
  - [fixed (dính vào màn hình)](#fixed-dính-vào-màn-hình)
    - [inset (viết gọn cho top/right/bottom/left)](#inset-viết-gọn-cho-toprightbottomleft)
  - [:](#)
- [min](#min)
- [z](#z)
---
# Width & Height (thiết lập chiều cao & chiều rộng)
## w & h
**Ex: Đặt width = 200px cho div trong ReactJs**
```js
<div className="w-[200px]">Nội dung</div>
<div className="w-48">...</div>  // 48x4 = 192px
<div className="w-52">...</div>  // 52x4 = 208px
```
## w-full
## min-w-
## min-h-screen
```bash
Chiều cao ít nhất bằng màn hình (= min-height: 100vh).
```
# margin
**Ex1**
```js
m-0
m-2   = 8px
m-4   = 16px
m-8   = 32px
mx-4  // trái + phải
my-2  // trên + dưới
ml-4  // margin-left: 16px
mr-4  // margin-right: 16px
mt-2
mb-6
ml-auto  // đẩy sang phải (trong flex)
mr-auto  // đẩy sang trái (trong flex)
mx-auto  // căn giữa (block)
```
**Ex2**
```js
<header className="flex">
  <div>Logo</div>

  <div className="ml-auto">
    Login / Register
  </div>
</header>

// ml-auto = đẩy khối login sang phải header
```
# Padding
**Padding cơ bản (all sides)**
```js
<div className="p-4">...</div>
```
**Padding theo từng hướng**
```bash
Trên / dưới / trái / phải
pt-4   // top
pb-2   // bottom
pl-6   // left
pr-6   // right

Trục ngang / dọc
px-4   // left + right
py-6   // top + bottom
```
**Padding chính xác px (custom)**
```js
<div className="p-[10px] px-[18px] py-[12px]">
```
# relative
# flex (Hộp linh hoạt)
```bash
- Kích hoạt flexbox.
```
**Ex**
```html
<div className="flex">...</div>
```
## flex-
flex-1 là một utility của Tailwind tương ứng với thuộc tính Flexbox.
<div class="flex">  <div class="flex-1">A</div>  <div>B</div></div>

flex-1 thực chất là gì?
Trong Tailwind:
class="flex-1"
≈
flex: 1;
Theo chuẩn CSS, trình duyệt hiểu thành gần giống:
flex-grow: 1;flex-shrink: 1;flex-basis: 0%;
Ý nghĩa:

"Chiếm hết không gian còn lại có thể chiếm."


Ví dụ đơn giản
<div class="flex">  <div class="w-20">Menu</div>  <div class="flex-1">Content</div></div>
Giả sử container rộng:
1000px
Menu:
80px
thì Content sẽ lấy:
920px

Minh họa:
+------------------------------+| Menu |      Content          |+------------------------------+

Tại sao là số 1?
Trong CSS Flexbox có thuộc tính:
flex-grow
quyết định tỷ lệ chia phần không gian còn lại.
Ví dụ:
<div class="flex">  <div class="flex-1">A</div>  <div class="flex-1">B</div></div>
A: 50%B: 50%
vì:
A: flex-grow = 1B: flex-grow = 1
tỷ lệ:
1 : 1

Ví dụ:
<div class="flex">  <div class="flex-1">A</div>  <div class="flex-2">B</div></div>
(Nếu bạn tự định nghĩa flex-2)
A: 1 phầnB: 2 phần
=> B rộng gấp đôi A.

Trong Tailwind còn có gì?
flex-none
flex: none;
Không co giãn.

flex-auto
flex: auto;
Tự động co giãn theo nội dung.

flex-initial
flex: 0 auto;
Hành vi mặc định.

flex-1
flex: 1;
Chiếm phần không gian còn lại.

Ví dụ thực tế
Thanh tìm kiếm:
<div class="flex gap-2">  <input class="flex-1 border" />  <button>Search</button></div>
Kết quả:
+----------------------------------+| [input................] [button]|+----------------------------------+


Button rộng đúng theo nội dung.


Input dùng flex-1 nên kéo dài chiếm toàn bộ khoảng trống còn lại.



Cách nhớ đơn giản:
flex-1="Tao muốn giãn ra để lấy phần không gian còn thừa."
Số 1 là tỷ lệ chia không gian trong Flexbox. Nếu có nhiều phần tử cùng flex-1, chúng sẽ chia đều phần không gian còn lại theo tỷ lệ 1 : 1 : 1 : ....
## flex-row       // mặc định
## flex-col       // dọc
```
## basis
```bash
- Thiết lập kích thước cho các items.
```
**Syn**
```bash
basis-<number>
flex-basis: calc(var(--spacing) * <number>);
basis-<fraction>
flex-basis: calc(<fraction> * 100%);
basis-full
flex-basis: 100%;
basis-auto
flex-basis: auto;
basis-3xs
flex-basis: var(--container-3xs); /* 16rem (256px) */
basis-2xs
flex-basis: var(--container-2xs); /* 18rem (288px) */
basis-xs
flex-basis: var(--container-xs); /* 20rem (320px) */
basis-sm
flex-basis: var(--container-sm); /* 24rem (384px) */
basis-md
flex-basis: var(--container-md); /* 28rem (448px) */
basis-lg
flex-basis: var(--container-lg); /* 32rem (512px) */
basis-xl
flex-basis: var(--container-xl); /* 36rem (576px) */
basis-2xl
flex-basis: var(--container-2xl); /* 42rem (672px) */
basis-3xl
flex-basis: var(--container-3xl); /* 48rem (768px) */
basis-4xl
flex-basis: var(--container-4xl); /* 56rem (896px) */
basis-5xl
flex-basis: var(--container-5xl); /* 64rem (1024px) */
basis-6xl
flex-basis: var(--container-6xl); /* 72rem (1152px) */
basis-7xl
flex-basis: var(--container-7xl); /* 80rem (1280px) */
basis-(<custom-property>)
flex-basis: var(<custom-property>);
basis-[<value>]
flex-basis: <value>;
```
## gap 
```bash
- gap = khoảng trống giữa các con (margin = khoảng trống quanh từng thằng)
```
**Ex**
```js
<div className="flex gap-4">  
  <div>A</div>
  <div>B</div>
  <div>C</div>
</div>

// Khoảng cách giữa A–B–C = 16px
```
## items-center
```bash
- Chỉ dùng khi có flex hoặc grid.
- items-center = căn giữa theo chiều dọc.
```
**Ex**
```js
<div className="flex items-center">
  <img className="w-8 h-8" />
  <span>Avatar</span>
</div>
```
## justify-start & justify-center & justify-end & justify-between & justify-around & justify-evenly
```bash
căn flex box theo chiều ngang.
```
**Ex1: justify-between**
```html
<div className="flex justify-between">
  <span>Left</span>
  <span>Right</span>
</div>
```
## items-start & items-end & items-stretch
```bash
Căn flex box theo chiều dọc.
```
## flex-wrap
```bash
Tự xuống dòng.
```
# grid
## grid-cols
**Syn**
```bash
grid-cols-{n} # n là số cột
```
## col-span
```bash
Để gộp cột grid.
```
**Syn**
```bash
col-span-{n} # n là số cột cần gộp
```
**Ex**
```html
<div class="grid grid-cols-3 gap-4">
  <div class="...">1</div>
  <div class="...">2</div>
  <div class="...">3</div>
  <div class="col-span-2 ...">4</div>
  <div class="...">5</div>
  <div class="...">6</div>
  <div class="col-span-2 ...">7</div>
</div>
```
# ViewPort (Dùng để định vị trên viewport)
## fixed (dính vào màn hình)
```bash
- fixed → không phụ thuộc parent
```
**Ex**
```js
<div class="fixed top-0 left-0 right-0 bg-white shadow-md p-4">
  Navbar
</div>

<div class="mt-20 p-4">
  Nội dung trang...
</div>
```
### inset (viết gọn cho top/right/bottom/left)
```bash
Nó chỉ hoạt động khi element có position (ví dụ: fixed, absolute, relative)

Hay dùng cho:
  - Overlay
  - Modal
  - Hover effect
```
**Syn**
```bash
inset-0 = top-0 right-0 bottom-0 left-0 # có thể thay 0 thành 1, 2, ...
```
**Ex1**
```html
<div className="fixed inset-0 ..."></div>

<!-- 
fixed: phần tử bám theo viewport
inset-0: kéo full màn hình (trên, dưới, trái, phải = 0)
=> 👉 Kết quả: div phủ toàn bộ màn hình (full screen background 
-->
```
**Ex2: Ví dụ overlay**
```html
<div class="relative w-64 h-40 bg-green-300">
  <div class="absolute inset-0 bg-black/40 flex items-center justify-center text-white">Overlay</div>
</div>
```
## :
lg:ml-65 là sự kết hợp của:
lg:
và
ml-65

1. ml là gì?
ml = margin-left
Ví dụ:
<div class="ml-4">
tương đương:
margin-left: 1rem;

2. 65 là gì?
Trong Tailwind chuẩn, các giá trị phổ biến là:
ml-0ml-1ml-2ml-4ml-8ml-16ml-64...
ml-65 không phải giá trị mặc định của Tailwind.
Nó chỉ hoạt động nếu dự án đã tự mở rộng spacing trong cấu hình.
Ví dụ:
// tailwind.config.jsexport default {  theme: {    extend: {      spacing: {        65: "16.25rem"      }    }  }}
Khi đó:
class="ml-65"
≈
margin-left: 16.25rem;

3. lg: là gì?
Đây là responsive breakpoint.
lg:ml-65
nghĩa là:

Chỉ áp dụng ml-65 khi màn hình đạt kích thước lg trở lên.

Mặc định Tailwind:
sm  >= 640pxmd  >= 768pxlg  >= 1024pxxl  >= 1280px2xl >= 1536px

Ví dụ:
<div class="ml-0 lg:ml-65">
Tương đương:
/* Mobile */margin-left: 0;
/* >= 1024px */@media (min-width: 1024px) {  margin-left: 16.25rem;}

Ví dụ thực tế
Giả sử có sidebar:
Desktop+---------+-------------------+| Sidebar |      Content      |+---------+-------------------+
Sidebar rộng:
260px
Content cần đẩy sang phải:
<main className="lg:ml-65">
=> Trên desktop:
margin-left: 260px
để không bị đè lên sidebar.
Nhưng trên mobile:
margin-left: 0
vì sidebar thường ẩn hoặc nằm dạng drawer.

Cách kiểm tra 65 là bao nhiêu
Tìm trong project:
Ctrl + Shift + F
rồi search:
spacing
hoặc:
65:
trong:
tailwind.config.jstailwind.config.ts
Ví dụ:
extend: {  spacing: {    65: "260px"  }}
thì:
lg:ml-65
nghĩa là:
@media (min-width: 1024px) {  margin-left: 260px;}
Nếu không có cấu hình nào cho 65 thì class này thường sẽ không được Tailwind sinh CSS ra.
# min
# z