# v-if / v-show – Điều kiện hiển thị
```bash
<p v-if="isLogin">Đã đăng nhập</p>
<p v-else>Chưa đăng nhập</p>
<p v-show="isLogin">Ẩn/hiện bằng CSS</p>

- Khác nhau:
    + v-if: render / destroy
    + v-show: chỉ toggle display
```