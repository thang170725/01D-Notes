# ref()
```bash
- Tạo biến reactive có thể thay đổi và Vue tự cập nhật giao diện.
```
```js
<script setup>
import { ref } from 'vue'

const count = ref(0)

const increase = () => {
  count.value++
}
</script>

<template>
  <p>Count: {{ count }}</p>
  <button @click="increase">+</button>
</template>

- Lưu ý:
  + Trong <script>: phải dùng .value
  + Trong <template>: KHÔNG cần .value
```
**Ex: ref với object**
```js
const user = ref({
  name: '',
  age: 0,
})

user.value.name = 'An'
user.value.age = 20
```

# reactive – Object reactive
Dùng khi có object nhiều field
```vue
<script setup>
import { reactive } from 'vue'

const user = reactive({
  name: 'Thắng',
  age: 22
})

const growUp = () => {
  user.age++
}
</script>

<template>
  <p>{{ user.name }} - {{ user.age }}</p>
  <button @click="growUp">Tăng tuổi</button>
</template>


📌 Khác ref:

Không cần .value

Chỉ dùng cho object / array
```

