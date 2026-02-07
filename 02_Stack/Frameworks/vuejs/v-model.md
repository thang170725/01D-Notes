# v-model – Two-way binding
```bash
- binding 2 chiều (two-way binding)
v-model THẬT RA LÀ GÌ?

Dòng này 👇

<Child v-model="title" />


Vue sẽ tự dịch ngầm thành 👇

<Child
  :modelValue="title"
  @update:modelValue="title = $event"
/>
```

```js
<script setup>
import { ref } from 'vue'

const name = ref('')
</script>

<template>
  <input v-model="name">
  <p>Xin chào {{ name }}</p>
</template>

Rất hay dùng trong form
```


