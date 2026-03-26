- [.PI](#pi)
- [.E](#e)
- [.sqrt()](#sqrt)
- [Math.sqrt1\_2](#mathsqrt1_2)
- [Math.LN2](#mathln2)
- [Math.LN10](#mathln10)
- [Math.LOG2E](#mathlog2e)
- [Math.Log10E](#mathlog10e)
- [round()](#round)
- [Math.ceil()](#mathceil)
- [.floor()](#floor)
- [Math.trunc()](#mathtrunc)
- [Math.sign()](#mathsign)
- [pow()](#pow)
- [Math.abs()](#mathabs)
- [Math.sin()](#mathsin)
- [Math.cos()](#mathcos)
- [min()](#min)
- [Math.max()](#mathmax)
- [Random](#random)
  - [random()](#random-1)
---
## .PI
```bash 
Trả về số Pi.
```
**Ex**
```js
let n = Math.PI;

console.log(n) // 3.141592653589793
```
## .E
```bash
Trả về giá trị E.
```
## .sqrt()
```bash
Trả về căn bậc 2.
```
**Ex**
```js
console.log(Math.sqrt(4)) // 2
```
## Math.sqrt1_2
```bash
Trả về căn bậc 2 của 1 phần 2.
```
## Math.LN2
```bash
Trả về giá trị ln(2).
```
## Math.LN10
```bash
Trả về giá trị của ln(10).
```
## Math.LOG2E
```bash
Trả về giá trị của .
```
## Math.Log10E
```bash
Trả về giá trị của .
```
## round() 
```bash
Làm tròn số.
```
**Ex**
```js
let n = Math.round(12.1234);

console.log(n) // 12
```
## Math.ceil()
```bash
Làm tròn trên.
```
**Ex**
```js
let n = Math.ceil(12.1234);

console.log(n) // 13
```
## .floor()
```bash
Làm tròn dưới.
```
**Ex**
```js
let n = Math.floor(12.1234);

console.log(n) // 12
```
## Math.trunc()
```bash
Trả về phần nguyên của một số.
```
## Math.sign()
```bash
Trả về 1 nếu là số dương, -1 nếu là số âm, NaN nếu không truyền gì vào, 0 là các trường hượp còn lại.
```
## pow()
```bash
Trả về giá trị mũ.
```
**Ex**
```js
let n = Math.pow(4,2);

console.log(n) // 16
```
## Math.abs()
```bash
Trả về giá trị tuyệt đối.
```
**Ex**
```js
const a = Math.abs(3-4) // `1
```
## Math.sin()
Trả về giá trị sin, đơn vị radian.
## Math.cos()
Trả về giá trị cos, đơn vị radian.
## min() 
Trả về số nhỏ nhất.
console.log(Math.min(1,2,3,4,5))
1
## Math.max()
Trả về số lớn nhất.
## Random
### random() 
```bash
Trả về một số ngẫu nhiên nhỏ hơn 1.
```
**Ex: Tạo ngẫu nhiên số từ 0 -> 100**
```bash
for(let i=0; i<100; i++){
      let ran = parseInt(Math.random()*101);
      console.log(ran);
}
```
**Ex2: Tạo ngẫu nhiên số từ 1 -> 10**
```js
for(let i=0; i<51; i++){
      let ran = parseInt(Math.random()*10)+1;
      console.log(ran);
}
```
**Ex3: Tạo ngẫu nhiên số từ min -> max**
```js
min = 3;
max = 9;
   
for(let i=0; i<51; i++){
      let ran = parseInt(min + Math.random() * (max + 1 - min));
      console.log(ran);
}
```