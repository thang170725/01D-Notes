- [functions](#functions)
  - [Tạo hàm tính tổng 2 số](#tạo-hàm-tính-tổng-2-số)
  - [Tạo một giao diện tính tổng 2 số](#tạo-một-giao-diện-tính-tổng-2-số)
- [map()](#map)
---
# functions
```bash
- Dùng để tạo hàm.
```
**Syn**
```bash
- function name(var1, var2, …) {…} – basic function.
- var name = (var1, var2, …) => {…}; - arrow function (ES6).
- var name = function() {…} - Anonymous function (hàm ẩn danh).
```
## Tạo hàm tính tổng 2 số 
```js
// basic function
function Out(a, b) {
    return a + b;
}

// arrow function
var out2 = (a, b) => {return a + b;};
```
## Tạo một giao diện tính tổng 2 số 
```html
<input type="text" placeholder="Operand First" class="Operand">
<span>+</span>
<input type="text" placeholder="Operand Second" class="Operand">
<button>Result</button>
<div>=
    <span id="Result"></span>
</div>
```
```js
var operands = document.getElementsByClassName('Operand');
var result = document.getElementsByTagName('button');
result[0].onclick = function (){
    var dis = document.getElementById('Result');
    var operand1 = parseFloat(operands[0].value);
    var operand2 = parseFloat(operands[1].value);
    dis.innerHTML = operand1+operand2;
}
```
# map()
```js
var a = [1,2,3,4];
var c  = a.map(function (b){
    return b+2;
})
console.log(c); # [3,4,5,6]
```
