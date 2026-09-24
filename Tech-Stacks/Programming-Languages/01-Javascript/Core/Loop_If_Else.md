- [if ... else](#if--else)
- [switch case](#switch-case)
- [? :](#-)
- [for](#for)
- [While \& do while](#while--do-while)
- [forEach()](#foreach)
	- [break](#break)
	- [continue](#continue)
---
# if ... else
```bash
if(điều_kiện){…}
else if(điều_kiện){…}
else{…}
```
# switch case
**Syn**
```bash 
switch(tham_số_truyền_vào)
{
	case value_1: {…break;}
	case value_2: {…break;}
	…
	default: {…}
}
```
# ? :
```js
let age = 20;
let result = age >= 18 ? "Đủ tuổi" : "Chưa đủ tuổi";

// let age = 20;
// let result;

// if (age >= 18) {
//   result = "Đủ tuổi";
// } else {
//   result = "Chưa đủ tuổi";
// }
```
# for
```bash
Là vòng lặp biết trước số lần lặp.
```
**Ex**
```js
function main(){
   var arr = [1,2,3,4,5,6,7,8,9,10];
   for(let i of arr) {
      console.log(i);
   }
}
main()

// 1
// 2
// 3
// 4
// 5
// 6
// 7
// 8
// 9
// 10
```
# While & do while
```bash
- while		: Vòng lặp chưa biết trước số lần lặp.
- do while	: Vòng lặp, lặp ít nhất một lần.
```
**Syn: while**
```js
while(điều_kiện){
…
Điều kiện lặp;
}
```
**Syn: do while**
```bash
do{
…
Điều kiện lặp;
} while(điều kiện);
```
# forEach() 
```bash
Dùng để lặp qua các phần tử thường sử dụng trong mảng.
```
## break
```bash
Để phá vỡ vòng lặp kể cả khi điều kiện vẫn đang đúng.
```
## continue
```bash
Tiếp tục một vòng lặp khác và bỏ qua các đoạn code phía sau nó trong cùng vòng lặp.
```