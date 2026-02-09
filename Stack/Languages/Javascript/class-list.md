# classList.toggle()
```bash
- Là một phương thức dùng để thêm hoặc xóa một class khỏi một phần tử HTML.
- Nếu phần tử đó đã có class đó, toggle sẽ xóa nó, nếu chưa có, toogle sẽ thêm vào.
```
**Syn**
```bash
element.classList.toggle(className, [force])
- className: tên class CSS muốn thêm hoặc xóa.
- Force (tùy chọn): Nếu là true luôn thêm,  false là luôn xóa.
```
**Ex**
```html
<button id="myBtn">Toggle màu đỏ</button>
<div id="myBox">Nội dung</div>
```
```js
.red{
    color: #f00;
    font-weight: bold;
}
const btn = document.getElementById('myBtn');
const box = document.getElementById('myBox');

btn.addEventListener('click', function (){
    box.classList.toggle('red');
});
```
Bài tập
Tạo một ô input và thêm giá trị của input vào danh sách thẻ ul
<input type="text">
<button onclick="Add()">Add</button>
<ul></ul>

function Add(){
let v = document.getElementsByTagName('input')[0];
let l = document.createElement('li');
let u = document.getElementsByTagName('ul')[0];
l.textContent = v.value;
u.appendChild(l);
}