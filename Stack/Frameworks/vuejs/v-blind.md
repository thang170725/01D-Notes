# Directive : (v-bind) – Binding dữ liệu
```bash
- : là viết tắt của v-bind
- Dùng để nối dữ liệu JS với HTML
- :abc="xyz" -> abc nhận GIÁ TRỊ của biến xyz
```
**Trường hợp không dùng binding**
```bash
<template>
  <img src="avatar.png">
</template>

- src cố định, JS không can thiệp được.
```
**Ex**
```js
<img :src="avatar">

- Nghĩa là: Lấy giá trị biến avatar trong JS → gán cho thuộc tính src
```
**Ex**
```js
<template>
  <img :src="avatar" width="150">
</template>

<script setup>
import { ref } from 'vue'

const avatar = ref('https://vuejs.org/logo.png')
</script>

- Kết quả:
    + Vue đọc avatar
    + Gán vào src
    + Khi avatar đổi → ảnh đổi
```

## Demo thay đổi giá trị → UI đổi (quan trọng)
```js
<script setup>
  import { ref } from 'vue'

  const color = ref('red')
  const changeColor = () => {
    color.value = 'blue'
  }
</script>

<template>
  <p :style="{ color: color }">
    Dòng chữ này đổi màu
  </p>

  <button @click="changeColor">Đổi màu</button>
</template>
```

VẬY abc LÀ GÌ? CÓ TỰ ĐẶT KHÔNG?

👉 PHỤ THUỘC abc LÀ GÌ

🔹 TRƯỜNG HỢP 1: PROP BẠN TỰ ĐỊNH NGHĨA → ✔️ TỰ ĐẶT
Component con
defineProps({
  title: String
})

Component cha
<Child :title="title" />


👉 title là:

do bạn đặt

con và cha phải trùng tên

✔️ TÙY Ý đặt tên

🔹 TRƯỜNG HỢP 2: v-model → ❌ KHÔNG ĐƯỢC TỰ ĐẶT
<Child v-model="title" />


Vue bắt buộc dùng:

:modelValue="title"
@update:modelValue="..."


👉 Các tên này là quy ước của Vue

modelValue

update:modelValue

❌ Không đổi thành myValue, value123

🔹 TRƯỜNG HỢP 3: COMPONENT THƯ VIỆN (Dialog, Input…) → ❌ KHÔNG TỰ ĐẶT
<Dialog v-model="show" />


👉 Dialog đã định nghĩa sẵn:

prop nào

event nào

Bạn phải dùng đúng tên nó yêu cầu

3️⃣ SAU DẤU = LÀ GÌ?
:abc="xyz"


👉 xyz:

là biến JS

là expression

do bạn tự đặt

✔️ Hoàn toàn tự do

4️⃣ VÍ DỤ ĐỐI CHIẾU DỄ NHỚ
Ví dụ A – Tự đặt
<Child :hello="msg" />

defineProps({ hello: String })


✔️ OK

Ví dụ B – Sai vì không trùng tên
<Child :hi="msg" />

defineProps({ hello: String })


❌ Con nhận undefined

5️⃣ VÍ DỤ VỚI v-model (NHỚ KỸ)
Vue viết ngầm
<Child v-model="title" />


⇓

<Child
  :modelValue="title"
  @update:modelValue="title = $event"
/>


👉 modelValue KHÔNG PHẢI do bạn đặt

**Nếu đổi giá trị avatar để image thay đổi thì tại sao không đổi trong src đi mà lại đổi trong biến avatar làm gì, một cái là đổi một lần trong src, một cái là đổi thông qua biến rồi gán lại vào src**