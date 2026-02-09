v-for – Lặp danh sách
<script setup>
const items = ['Vue', 'React', 'Angular']
</script>

<template>
  <ul>
    <li v-for="(item, index) in items" :key="index">
      {{ item }}
    </li>
  </ul>
</template>