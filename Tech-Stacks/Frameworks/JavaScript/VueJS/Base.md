# Các bước cài đặt
```bash 
1. Cài Node.js (nếu chưa có) & kiểm tra: node -v, npm -v
2. npm create vue@latest my-vue-app & cd my-vue-app : Tạo dự án Vue.js bằng Vite. my-vue-app là tên project bạn muốn.
3. npm install                                      : Cài các dependency
4. npm run                                          : Bạn sẽ thấy URL như http://localhost:5173/ xuất hiện, mở trình duyệt là thấy Vue chạy
5. npm run build                                    : Build dự án (biến thành HTML + JS tĩnh). Các file tĩnh HTML, JS, CSS. Đây là thứ bạn có thể deploy lên server hoặc Docker.
6. ls dist                                          : Sau khi build xong, bạn sẽ có thư mục dist/
```bash

# Bước 6: Preview build
```bash
npm run preview
Lệnh này sẽ chạy server tạm thời để xem file đã build.
```

# Bước 7: Sửa code thử
Mở src/App.vue. Thay đổi nội dung ví dụ:
```html
<template>
  <div>
    <h1>Xin chào Vue!</h1>
    <button @click="count++">Nhấn tôi: {{ count }}</button>
  </div>
</template>

<script setup>
import { ref } from 'vue'
const count = ref(0)
</script>
Lưu lại và refresh trình duyệt, bạn sẽ thấy nút tăng số đếm.
Tip: Đây là cách nhanh nhất để build thử một dự án Vue đơn giản, có đầy đủ HTML + CSS + JS trong thư mục dist.
```