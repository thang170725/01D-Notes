- [w \& h \& min-h-screen](#w--h--min-h-screen)
- [margin](#margin)
- [Padding](#padding)
- [flex](#flex)
  - [basis](#basis)
  - [gap](#gap)
  - [items-center](#items-center)
  - [justify-start \& justify-center \& justify-end \& justify-between \& justify-around \& justify-evenly](#justify-start--justify-center--justify-end--justify-between--justify-around--justify-evenly)
  - [items-start \& items-end \& items-stretch](#items-start--items-end--items-stretch)
  - [flex-wrap](#flex-wrap)
- [grid](#grid)
  - [grid-cols](#grid-cols)
  - [col-span](#col-span)
- [fixed (dính vào màn hình)](#fixed-dính-vào-màn-hình)
- [min](#min)
- [inset](#inset)
---
# w & h & min-h-screen
```bash
- min-h-screen  : chiều cao ít nhất bằng màn hình (= min-height: 100vh).
```
**Ex: Đặt width = 200px cho div trong ReactJs**
```js
<div className="w-[200px]">Nội dung</div>
<div className="w-48">...</div>  // 48x4 = 192px
<div className="w-52">...</div>  // 52x4 = 208px
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
# flex
```bash
- Kích hoạt flexbox.
```
**Ex**
```js
<div className="flex">...</div>

flex-row       // mặc định
flex-col       // dọc
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
# fixed (dính vào màn hình)
```bash
- fixed → không phụ thuộc parent
- Định vị theo viewport
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

inset (viết gọn cho top/right/bottom/left)
📌 inset-0 = top-0 right-0 bottom-0 left-0
👉 Ví dụ overlay
<div class="relative w-64 h-40 bg-green-300">
  <div class="absolute inset-0 bg-black/40 flex items-center justify-center text-white">
    Overlay
  </div>
</div>


🔥 Hay dùng cho:

Overlay

Modal

Hover effect
# min
# inset
```bash
Nó chỉ hoạt động khi element có position (ví dụ: fixed, absolute, relative
```
**Ex**
```html
<div className="fixed inset-0 ..."></div>

<!-- 
fixed: phần tử bám theo viewport
inset-0: kéo full màn hình (trên, dưới, trái, phải = 0)
=> 👉 Kết quả: div phủ toàn bộ màn hình (full screen background 
-->
```