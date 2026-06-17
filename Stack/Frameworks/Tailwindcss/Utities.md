- [!important](#important)
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


⚠️ Vẫn có thể chạy để tương thích ngược, nhưng đã bị đánh dấu là deprecated (không khuyến khích dùng nữa).
@layer là một tính năng của Tailwind CSS dùng để đăng ký CSS vào các layer của Tailwind, giúp Tailwind quản lý thứ tự ưu tiên và hỗ trợ tree-shaking (loại bỏ CSS không dùng).

Trong Tailwind có 3 layer chính:

@layer base
@layer components
@layer utilities
1. @layer base

Dùng cho các style nền tảng.

Ví dụ:

@layer base {
  h1 {
    font-size: 2rem;
  }

  body {
    margin: 0;
  }
}

Sau khi build, Tailwind sẽ đặt các rule này vào phần base.

2. @layer components

Dùng cho các component tái sử dụng.

Ví dụ:

@layer components {
  .btn-primary {
    @apply px-4 py-2 rounded bg-blue-500 text-white;
  }
}

Sử dụng:

<button class="btn-primary">
  Save
</button>
3. @layer utilities

Dùng để tạo utility class giống như utility của Tailwind.

Ví dụ:

@layer utilities {
  .rotate-y-180 {
    transform: rotateY(180deg);
  }
}

Sau đó:

<div class="rotate-y-180">

sử dụng y hệt utility mặc định của Tailwind.

Trong đoạn code của bạn
@layer utilities {
  .font-ui {
    font-family: var(--font-sans);
  }

  .font-display {
    font-family: var(--font-display);
  }

  .text-gradient {
    @apply bg-clip-text text-transparent;
    background-image: linear-gradient(
      135deg,
      #fff 0%,
      #94a3b8 100%
    );
  }
}

nghĩa là bạn đang khai báo 3 utility mới:

font-ui
font-display
text-gradient

để dùng giống utility Tailwind:

<h1 class="font-display text-gradient">
  Hello
</h1>
Tại sao không viết CSS bình thường?

Bạn hoàn toàn có thể viết:

.text-gradient {
  ...
}

nhưng dùng @layer có lợi ích:

1. Đúng thứ tự ưu tiên

Tailwind sắp xếp CSS theo:

base
↓
components
↓
utilities

nên không bị lỗi ghi đè khó hiểu.

2. Hỗ trợ purge/tree-shaking

Khi build production, Tailwind biết đây là utility của nó và xử lý tối ưu hơn.

3. Dùng được @apply

Ví dụ:

.text-gradient {
  @apply bg-clip-text text-transparent;
}

Tailwind sẽ biên dịch thành CSS thật.

Hiểu đơn giản

Đoạn này:

@layer utilities {
  .text-gradient {
    @apply bg-clip-text text-transparent;
    background-image: linear-gradient(...);
  }
}

có thể hiểu như:

"Hãy thêm một utility class mới tên là text-gradient vào hệ thống utility của Tailwind."

để sau này dùng:

<span class="text-gradient">
  AI Assistant
</span>

giống hệt như bạn dùng:

<span class="text-red-500">

hay

<span class="font-bold">

vậy.
Bạn đang nói tới:

.font-ui {
  font-family: var(--font-sans);
}

.font-display {
  font-family: var(--font-display);
}

trong khi:

.text-gradient {
  @apply bg-clip-text text-transparent;
  background-image: linear-gradient(...);
}

lại có @apply.

Lý do là @apply chỉ dùng khi muốn tái sử dụng utility class của Tailwind.

Trường hợp .font-ui
.font-ui {
  font-family: var(--font-sans);
}

Ở đây:

var(--font-sans)

là một CSS Variable.

Ví dụ:

:root {
  --font-sans: "Inter", sans-serif;
}

Tailwind không có utility nào tương đương:

font-family: var(--font-sans)

nên không thể viết:

@apply ???;

được.

Phải viết CSS thuần:

font-family: var(--font-sans);
Trường hợp .font-display

Tương tự:

.font-display {
  font-family: var(--font-display);
}

Nếu:

--font-display: "Playfair Display", serif;

thì Tailwind cũng không biết biến CSS đó là gì.

Nên phải viết:

font-family: var(--font-display);
Trường hợp .text-gradient
.text-gradient {
  @apply bg-clip-text text-transparent;
  background-image: linear-gradient(...);
}

Ở đây:

bg-clip-text
text-transparent

đều là utility có sẵn của Tailwind.

Ví dụ:

class="bg-clip-text text-transparent"

là hợp lệ.

Nên có thể gom lại:

@apply bg-clip-text text-transparent;
Nếu không dùng @apply thì sao?

Đoạn:

@apply bg-clip-text text-transparent;

tương đương gần như:

background-clip: text;
-webkit-background-clip: text;

color: transparent;

Người viết có thể viết trực tiếp:

.text-gradient {
  background-clip: text;
  -webkit-background-clip: text;
  color: transparent;

  background-image: linear-gradient(...);
}

nhưng dùng @apply ngắn gọn hơn.

Quy tắc dễ nhớ
Dùng @apply

Khi thuộc tính đã có utility Tailwind:

@apply text-sm;
@apply rounded-xl;
@apply flex;
@apply items-center;
@apply text-transparent;
Không dùng @apply

Khi là CSS đặc biệt hoặc giá trị động:

font-family: var(--font-display);

background-image: linear-gradient(...);

clip-path: polygon(...);

animation: custom-animation;

backdrop-filter: blur(20px);

vì Tailwind không có utility tương ứng hoặc không biết giá trị cụ thể là gì.

Nói ngắn gọn: .font-ui và .font-display không dùng @apply vì chúng đang gán CSS Variable (var(...)), còn .text-gradient dùng @apply vì nó tận dụng các utility Tailwind có sẵn (bg-clip-text, text-transparent).
Câu hỏi rất hay. Lý do là @apply chỉ hoạt động với các utility class đã tồn tại trong Tailwind, chứ không phải với mọi CSS.
Ví dụ:
@apply text-sm rounded-xl;
được vì Tailwind có sẵn:
class="text-sm rounded-xl"

Nhưng đoạn này:
background-image: linear-gradient(  135deg,  #fff 0%,  #94a3b8 100%);
Tailwind không có utility nào chính xác như vậy để @apply.
Bạn không thể viết:
@apply linear-gradient(...);
vì linear-gradient(...) không phải utility class.

Nếu muốn dùng @apply cho gradient thì sao?
Bạn phải định nghĩa gradient đó thành một utility trước.
Ví dụ Tailwind có:
class="bg-gradient-to-r from-white to-slate-400"
thì có thể:
.text-gradient {  @apply bg-gradient-to-r from-white to-slate-400;}
Nhưng gradient này chỉ là một số mẫu mà Tailwind hỗ trợ.

Vấn đề trong code của bạn
background-image: linear-gradient(  135deg,  #fff 0%,  #94a3b8 100%);
Gradient này dùng:


góc 135°


màu tùy chỉnh


điểm dừng (color stop) tùy chỉnh


Tailwind không có sẵn utility tương ứng chính xác.
Vì vậy người viết giữ nguyên CSS:
background-image: linear-gradient(...);

Có thể cấu hình để dùng @apply không?
Có.
Trong cấu hình Tailwind, bạn có thể tạo utility riêng.
Ví dụ:
@layer utilities {  .bg-brand-gradient {    background-image: linear-gradient(      135deg,      #fff 0%,      #94a3b8 100%    );  }}
Sau đó:
.text-gradient {  @apply bg-clip-text text-transparent bg-brand-gradient;}
Nhưng thực chất bạn chỉ đang:


Tạo utility mới


Rồi @apply utility đó


Kết quả CSS cuối cùng giống hệt.

Hiểu đơn giản
@apply không phải là:

"gom mọi CSS lại"

mà là:

"sao chép CSS từ các utility class Tailwind đã tồn tại"

Nên:
@apply text-sm;
✔ Được
@apply rounded-xl;
✔ Được
@apply bg-clip-text;
✔ Được
@apply linear-gradient(135deg,...);
❌ Không được vì đó là giá trị CSS, không phải utility class của Tailwind.