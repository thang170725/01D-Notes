- [Window](#window)
---
# Window
```bash
Được hỗ  trợ bởi tất cả các trình duyệt. Nó biểu diễn của sổ của trình duyệt.
Tất cả các đối tượng, hàm và biến Javascript toàn cục đều tự động trở thành thành viên của đối tượng window.
Biến toàn cục là thuộc tính của đối tượng window.
Hàm toàn cục là phương thức của đối tượng window.
window.innerWidth
Đưa ra giá trị kích thước chiều rộng của vùng xem, khu vục nội dung trang web được hiển thị, đơn vị là pixels.
window.innerHeight
Đưa ra giá trị kích thước chiều cao của vùng xem, khu vục nội dung trang web được hiển thị, đơn vị là pixels.
function main(){
    let w = window.innerWidth;
    let h = window.innerHeight;
    console.log(w,h);
}
main();
1366 645
```