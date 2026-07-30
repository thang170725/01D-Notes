# Framer Motion
```bash
- Là thư viện giúp bạn tạo animation mượt, dễ viết và chuyên nghiệp trong React.
- Nó dùng để:
  + Làm hiệu ứng xuất hiện / biến mất (fade in, fade out)
  + Làm animation khi hover, click
  + Làm chuyển trang
  + Làm sidebar trượt vào/ra
  + Làm drag & drop
  + Tạo layout animation (khi thay đổi vị trí phần tử)
```
**Installation**
```bash
1. npm install framer-motion
```
**Syn**
```bash
import { motion } from "framer-motion";

<motion.div>...</motion.div>

- `initial`    : Trạng thái ban đầu           
- `animate`    : Trạng thái khi chạy          
- `exit`       : Trạng thái khi unmount       
- `transition` : Thời gian & kiểu chuyển động 
- `whileHover` : Animation khi hover          
- `whileTap`   : Animation khi click          
- `variants`   : Tập hợp animation            
```
## AnimatePresence (Giúp chạy animation khi component bị unmount (biến mất khỏi DOM))
**Ex**
```js
import { motion, AnimatePresence } from "framer-motion";

<AnimatePresence>
  {condition && (
    <motion.div
      initial={{ opacity: 0 }}
      animate={{ opacity: 1 }}
      exit={{ opacity: 0 }}
    />
  )}
</AnimatePresence>
```
whileHover là một prop của thư viện Framer Motion (nay là Motion), dùng để xác định animation sẽ chạy khi người dùng đưa chuột (hover) lên phần tử.

Nó không phải của React.

Cú pháp
<motion.div
    whileHover={{
        scale: 1.1
    }}
>
    Hover me
</motion.div>

Nghĩa là:

Bình thường: scale = 1
Hover vào: scale = 1.1
Rời chuột: tự động quay về scale = 1
Ví dụ 1: Phóng to
import { motion } from "framer-motion";

<motion.button
    whileHover={{
        scale: 1.1
    }}
>
    Click me
</motion.button>

Khi hover:

100%  ---> 110%
Ví dụ 2: Đổi màu
<motion.div
    whileHover={{
        backgroundColor: "#3b82f6"
    }}
>
    Card
</motion.div>

Hover vào sẽ đổi màu nền.

Ví dụ 3: Nâng card lên
<motion.div
    whileHover={{
        y: -5
    }}
>
    Card
</motion.div>

y: -5

↓

Card dịch lên 5px.

Ví dụ 4: Nhiều animation cùng lúc
<motion.div
    whileHover={{
        scale: 1.05,
        y: -5,
        rotate: 2
    }}
>
    Exercise
</motion.div>

Hover sẽ:

phóng to
nhấc lên
xoay nhẹ
Thêm transition
<motion.div
    whileHover={{
        scale: 1.05
    }}
    transition={{
        duration: 0.2
    }}
>
    Hover
</motion.div>

Animation sẽ mượt trong 0.2 giây.

Ví dụ với Tailwind
<motion.div
    className="bg-white p-4 rounded-lg shadow"
    whileHover={{
        scale: 1.03,
        y: -4
    }}
>
    Workout Card
</motion.div>
So sánh với CSS :hover

CSS:

.card:hover {
    transform: scale(1.05);
}

Framer Motion:

<motion.div
    whileHover={{
        scale: 1.05
    }}
>

Framer Motion mạnh hơn vì hỗ trợ:

spring animation
drag
gesture
animation chain
layout animation
animate giữa các state
Các prop liên quan

Ngoài whileHover, Motion còn có:

Prop	Khi nào chạy
whileHover	Hover chuột
whileTap	Nhấn chuột
whileFocus	Focus bằng chuột hoặc bàn phím
whileDrag	Kéo (drag)
initial	Trạng thái ban đầu
animate	Trạng thái sau khi render
exit	Khi component bị unmount (thường dùng với AnimatePresence)

Ví dụ:

<motion.button
    whileHover={{ scale: 1.05 }}
    whileTap={{ scale: 0.95 }}
>
    Save
</motion.button>
Hover → nút phóng to 5%.
Nhấn giữ chuột → nút thu nhỏ còn 95%, tạo cảm giác đang được bấm.