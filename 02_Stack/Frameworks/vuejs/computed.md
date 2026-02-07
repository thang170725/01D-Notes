# computed – Giá trị tính toán
```bash
- Tạo giá trị phụ thuộc vào dữ liệu khác.
- Tự cập nhật khi dữ liệu gốc đổi.
```
```js
<script setup>
import { ref, computed } from 'vue'

const price = ref(100)
const quantity = ref(2)

const total = computed(() => {
  return price.value * quantity.value
})
</script>

<template>
  <p>Total: {{ total }}</p>
</template>

- Tự động cập nhật
- Tối ưu performance hơn function thường
```

# get() & set()
```js
const fullName = computed({
  get() {
    return firstName.value + ' ' + lastName.value
  },
  set(val) {
    const parts = val.split(' ')
    firstName.value = parts[0]
    lastName.value = parts[1]
  },
})
```