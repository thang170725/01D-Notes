# v-html 
```bash
- Dùng để render (hiển thị) chuỗi HTML như HTML thật, thay vì hiển thị nó như text bình thường.
- v-html = “nhét HTML động vào DOM”
```
**Ex: Không dùng v-html**
```js
<template>
  <p>{{ content }}</p>
</template>

<script setup>
const content = '<b>Xin chào</b>'
</script>

- Kết quả hiển thị trên màn hình: <b>Xin chào</b>
- HTML không được render, chỉ là chữ.
```
**Ex: Dùng v-html**
```js
<template>
  <p v-html="content"></p>
</template>

<script setup>
const content = '<b>Xin chào</b>'
</script>

- Kết quả hiển thị: Xin chào. Thẻ <b> được hiểu là HTML thật.
```