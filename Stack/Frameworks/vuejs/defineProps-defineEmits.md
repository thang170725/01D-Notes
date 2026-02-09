
```bash
- Vue chỉ cho dữ liệu chảy theo 1 chiều
    + CHA  ──(props)──▶  CON
    + CHA  ◀─(emit)───  CON
- Con KHÔNG được sửa trực tiếp dữ liệu của Cha
- Con chỉ được:
    + NHẬN dữ liệu → defineProps
    + BÁO lại Cha → defineEmits
    + Nếu bạn nắm được sơ đồ này → 90% Vue sẽ sáng ra.
```
defineProps()
Luồng dữ liệu cha -> Con
**Ex**
```js
<script setup>
import { ref } from 'vue'
import Child from './Child.vue'

const title = ref('Xin chào')
</script>

<template>
  <Child :title="title" />
</template>

- Cha có dữ liệu: title
```
**Component CON**
```js
<script setup>
const props = defineProps({
  title: String
})
</script>

<template>
  <h1>{{ props.title }}</h1>
</template>
```

# defineEmits()
```bash
- Luồng dữ liệ con -> cha.
- VẤN ĐỀ
    + Con không được sửa props, vậy làm sao báo Cha sửa?
    + CÂU TRẢ LỜI: emit event
```
**Ex**
**Component con**
```js
<script setup>
const emit = defineEmits(['changeTitle'])

function clickMe() {
  emit('changeTitle', 'Tiêu đề mới')
}
</script>

<template>
  <button @click="clickMe">Đổi tiêu đề</button>
</template>
```
**Component cha**
```js
<script setup>
import { ref } from 'vue'
import Child from './Child.vue'

const title = ref('Xin chào')

function onChangeTitle(newTitle) {
  title.value = newTitle
}
</script>

<template>
  <h1>{{ title }}</h1>
  <Child @changeTitle="onChangeTitle" />
</template>
```