# watch()
```bash
- Theo dõi sự thay đổi
- Dùng khi muốn làm gì đó khi data thay đổi
- Hay dùng cho:
  + Gọi API
  + Validate
  + Lưu localStorage
```
```vue
<script setup>
import { ref, watch } from 'vue'

const age = ref(18)

watch(age, (newAge, oldAge) => {
  console.log('old:', oldAge)
  console.log('new:', newAge)
})
</script>

<template>
  <input type="number" v-model="age">
</template>
```
**Ex**
```js
watch(
  () => props.item,
  (val) => {
    console.log('item changed', val)
  }
)
```
immediate: true là gì?
watch(
  source,
  callback,
  { immediate: true }
)


👉 Callback chạy ngay lần đầu, không đợi thay đổi

# watchEffect – Watch tự động
Vue tự phát hiện dependency
```bash
watchEffect(() => {
  // code
})
```

```bash
<script setup>
import { ref, watchEffect } from 'vue'

const age = ref(18)

watchEffect(() => {
  console.log('Age hiện tại:', age.value)
})
</script>

<template>
  <input type="number" v-model="age">
</template>

Console:
Age hiện tại: 18   // chạy NGAY
Age hiện tại: 20   // khi bạn gõ
Age hiện tại: 21


📌 Điểm khác với watch:

watchEffect chạy lần đầu

watch thì không (mặc định)
```