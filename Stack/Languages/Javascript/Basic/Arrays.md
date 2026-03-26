- [Create (tạo)](#create-tạo)
  - [new Array \& \[\]](#new-array--)
  - [isArray()](#isarray)
  - [.length](#length)
  - [.join()](#join)
  - [.split()](#split)
  - [valueOf()](#valueof)
  - [.forEach()](#foreach)
  - [every()](#every)
  - [some()](#some)
- [Filter (lọc)](#filter-lọc)
  - [.find()](#find)
  - [.filter()](#filter)
- [Shape (xử lý hình dạng)](#shape-xử-lý-hình-dạng)
  - [.push()](#push)
  - [.pop()](#pop)
  - [shift()](#shift)
  - [unshift()](#unshift)
  - [splice()](#splice)
  - [.sort()](#sort)
  - [.reverse()](#reverse)
  - [.concat()](#concat)
  - [.slice()](#slice)
  - [.indexOf()](#indexof)
  - [lastIndexOf()](#lastindexof)
- [Process (xử lý mảng)](#process-xử-lý-mảng)
  - [.reduce()](#reduce)
  - [reduceRight()](#reduceright)
  - [.filter()](#filter-1)
  - [copyWithin()](#copywithin)
  - [fill()](#fill)
  - [findIndex()](#findindex)
  - [at()](#at)
  - [flat()](#flat)
  - [toSpliced()](#tospliced)
  - [includes()](#includes)
  - [findLast()](#findlast)
  - [findLastIndex()](#findlastindex)
  - [toSorted()](#tosorted)
  - [ToReversed()](#toreversed)
---
# Create (tạo)
## new Array & []
```bash
Trong một Array có thể chứa các kiểu dữ liệu dữ liệu khác nhau.
```
**Syn**
```bash
- var | let | const <name> = new Aray( value1, value2, … ); - không được khuyến khích dùng.
- var | let | const <name> = [value1, value2, … ]; 
- var | let | const [biến1, biến2, …] = tên biến;
```
## isArray()
```bash
Kiểm tra xem có phải một Array không. Không thể dùng typeOf để kiểm tra xem phần tử cố phải một mảng hay không.
```
**Syn** 
```bash
Array.isArray(<variable>);
```
## .length
```bash
Lấy chiều dài của một Array.
```
## .join() 
```bash
Để nối các phần tử của mảng lại với nhau thành một chuỗi.
Các phần tử được ngăn cách nhau bởi kí tự do người dùng quy định. Nếu không truyền ký tự ngăn cách vào thì giá trị mặc định là dấu phẩy ",".
```
**Syn**
```bash
array.join(separator);

- separator: là kí tự sẽ ngăn cách các phần tử với nhau, mặc định mang giá trị là dấu ",".
```
## .split()
**Ex**
```js
let str = "apple,banana,orange";
let arr = str.split(",");

console.log(arr); // ["apple", "banana", "orange"]
```
## valueOf()
```bash
Hàm này có tác dụng tương tự như hàm array.join() , có nghĩa là nó sẽ nối các phần tử với nhau vào một chuỗi cách nhau bởi dấu phẩy.
```
**Ex**
```bash
let a = [1,2,3,4,5,6,7];
console.log(a.valueOf());
```
## .forEach()
```bash
Để đuyệt qua từng phần tử của mảng.
```
**Ex**
```js
// type 2
a.forEach(function (Number){
   console.log(Number);
}
);

// type 3
a.forEach( (Numbers) => {console.log(Numbers)});

// 1
// 2
// 3
// 4
// 5
// 6
// 7
// 8
// 9
…
```
## every()
```bash
Kiểm tra tất cả phần tử trong mảng phải thỏa mãn điều kiện gì đó. Trả về true, false.
```
**Ex**
```js
let a = [1,2,3,4,5];
a = a.every(function (Number){
   return Number % 2 == 0;
})

console.log(a); // false
```
## some()
```bash
Kiểm tra ít nhất một phần tử trong mảng phải thỏa mãn điều kiện gì đó.
```
**Ex**
```js
let a = [1,2,3,4,5];
a = a.some(function (Number){
  return Number % 2 == 0;
})

console.log(a); // true
```
# Filter (lọc)
## .find()
```bash
- Tìm phần tử trong mảng rồi in ra màn hình. 
- Chỉ trả về một giá trị.
```
**Ex1: Tìm số đầu tiên > 10**
```js
const numbers = [3, 7, 12, 5, 20];

const result = numbers.find((num) => num > 10);

console.log(result); // 12

// find sẽ trả về phần tử đầu tiên thỏa mãn điều kiện
```
**Ex2: Tìm user có id = 2**
```js
const users = [
  { id: 1, name: "Nam" },
  { id: 2, name: "Linh" },
  { id: 3, name: "Huy" },
];

const user = users.find((item) => item.id === 2);

console.log(user);
// { id: 2, name: "Linh" }
```
## .filter()
```bash
Tìm phần tử trong mảng thỏa mãn điều kiện. trả về nhiều giá trị nếu thỏa mãn.
```
**Ex1: Không dùng filter**
```js
let a = [1,2,3,4,5,6,7];

for(var i = 0; i < a.length; i++){
  if(a[i] > 4){
    console.log(a[i]);
  }
}
```
**Ex2: dùng filter**
```js
a = a.filter(function (Number){
  return (Number > 4);
})

console.log(a); // khi này a đang là một đối tương (object)
// 5
// 6
// 7
// (3) [5, 6, 7]0: 51: 62: 7
// length: 3
// [[Prototype]]: Array(0)
```
**Ex3: Lấy tất cả user có id > 1**
```js
const users = [
  { id: 1, name: "Nam" },
  { id: 2, name: "Linh" },
  { id: 3, name: "Huy" },
];

const result = users.filter((item) => item.id > 1);

console.log(result);
/*
[
  { id: 2, name: "Linh" },
  { id: 3, name: "Huy" }
]
*/
```
# Shape (xử lý hình dạng)
## .push()
```bash
Hàm này sẽ thêm phần tử vào cuối mảng.
```
**Ex**
```js
let a = [1,2,3,4,5,6,7];
a.push(8,9,10)
console.log(a.valueOf());
```
## .pop()
```bash
Lấy phần tử cuối cùng trong mảng. không có tham số truyền vào.
```
**Ex**
```js
let a = [1,2,3,4,5,6,7];
a.pop();
console.log(a.valueOf());
```
## shift()
```bash
Hàm xóa phần tử đầu tiên của mảng, sau đó dồn các phần tử phía sau xuống một bậc.
Không có tham số truyền vào.
```
**Ex**
```js
let a = [1,2,3,4,5,6,7];
console.log(a[1]);
a.shift();

console.log(a[1]);

// 2
// 3
```
## unshift()
```bash
Thêm một phần tử vào vị trí đầu tiên của mảng, đồng thời đẩy các phẩn từ phía sau lên một bậc. có tham số truyền vào.
```
**Ex**
```js
let a = [1,2,3,4,5,6,7];
console.log(a[1]);
a.unshift(0);
console.log(a[1]);

// 2
// 1
```
## splice()
```bash
Thêm một mảng vào trong một mảng tại vị trí chỉ định.
```
**Ex**
```js
var Text = ['Hello', 'i', 'am', 'a', 'coder'];
document.write(Text+'<br>');
Text.splice(1,0,['i', 'from', 'to Viet Nam']);
document.write(Text)

// Hello,i,am,a,coder
// Hello,i,from,to Viet Nam,i,am,a,coder
```
## .sort()
```bash
Dùng để sắp xếp. nếu là số thì sắp xếp tăng dần, nếu là chữ thì sắp xếp theo bảng chữ cái. 
```
**Ex1**
```js
var N = [2,4,1,6,8];
N.sort();
```
**Ex2: sắp xếp list object**
```bash
- < 0	: a đứng trước b
- > 0	: b đứng trước a
- 0	    : giữ nguyên
```
```js
const exercises = [
  { name: "Squat", order_index: 2 },
  { name: "Push-up", order_index: 1 },
  { name: "Plank", order_index: 3 }
];

exercises.sort((a, b) => a.order_index - b.order_index);

console.log(exercises);

// [
//   { name: "Push-up", order_index: 1 },
//   { name: "Squat", order_index: 2 },
//   { name: "Plank", order_index: 3 }
// ]
```
## .reverse()
```bash
Có tác dụng đảo ngược phần tử đầu xuống cuối và cứ tuần tự như thế.
```
**Ex**
```js
let arr = [1,2,3,4,5];

console.log(arr.reverse()); // 5,4,3,2,1
```
## .concat()
```bash
Dùng để nối hai mảng riêng biệt thành một mảng.
```
**Ex**
```js
let arr = [1,2,3,4,5];
let arr2 = [6,7,8,9,10];

console.log(arr.concat(arr2)); // [ 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 ]
```
## .slice()
```bash
Dùng đê lấy một hay một số phần tử trong mảng.
```
**Ex**
```js
let arr = [1,2,3,4,5];

console.log(arr.slice(0,2)); // [ 1, 2 ]
```
## .indexOf() 
```bash
Để tìm kiếm phần từ trong mảng.
```
**Ex**
```js
let arr = [1,2,3,4,5];

console.log(arr.indexOf(3)); // 2
```
## lastIndexOf() 
```bash
Tìm và trả về vị trí xuất hiện cuối cùng trong mảng nếu phần tử đó xuất hiện nhiều lần.
```
**Ex**
```js
let arr = [1,2,3,3,4,5];
   
console.log(arr.lastIndexOf(3)); // 3
```
# Process (xử lý mảng)
## .reduce() 
```bash
Hàm reduce sẽ duyệt qua từng phần tử trong mảng, sau đó trả về một giá trị cuối cùng, giá trị này phụ thuộc vào chương trình của hàm mà bạn truyền vào reduce.
```
**Ex: tính tổng**
```js
const arr = [1, 2, 3, 4, 5];

const sum = arr.reduce((acc, cur) => acc + cur, 0);

console.log(sum); // 15

// acc (accumulator): giá trị tích lũy
// cur: phần tử hiện tại
// 0: giá trị khởi tạo
```
## reduceRight() 
```bash
Công dụng giống reduce nhưng duyệt mảng từ phải qua trái.
```
## .filter()
```bash
Để lặp qua các phần tử trong mảng, dùng để lọc các phần tử trong mảng theo một điều kiện nào đó.
```
**Ex**
```js
let arr = [1,2,3,3,4,5];

let list = arr.filter(function(item){
   return item > 3;
})

console.log(list); // [4, 5]
```
## copyWithin()
```bash
Để sao chép các phần tử trong mảng với vị trí bắt đầu và kết thúc việc sao chép được xác định.
```
## fill() 
```bash
Để thay đổi giá trị của tất cả các phần tử trong mảng thành một giá trị mới.
```
**Ex**
```js
let arr = [1,2,3,4,5];

console.log(arr.fill(7, 0, 2)); //[ 7, 7, 3, 4, 5 ]
```
## findIndex()
```bash
Để tìm vị trí đầu tiên của phần tử được tìm thấy thỏa điều kiện nào đó.
```
## at()
```bash
Trả vể một phần tử được lập chỉ mục từ một mảng. Giống [].
```
## flat()
```bash
Nối các phần tử của mảng con.
```
## toSpliced()
## includes()
## findLast()
## findLastIndex()
## toSorted()
## ToReversed()
