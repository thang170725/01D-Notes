- [console.log() \& document.write()](#consolelog--documentwrite)
- [window.alert() | alert() \& confirm() \& prompt()](#windowalert--alert--confirm--prompt)
- [comments](#comments)
- [var \& let \& const](#var--let--const)
- [typeof](#typeof)
- [Number() \& ParseInt() \& ParseFloat()](#number--parseint--parsefloat)
- [Sorting Objects](#sorting-objects)
  - [5](#5)
  - [3](#3)
- [Gán](#gán)
---
# console.log() & document.write()
```bash
- console.log       : In giá trị ở ô Console của Inspect Element.
- document.write    : In giá trị nên trình duyệt người dùng.
```
**Syn** 
```bash
- console.log(value);
- document.write(value);
```
# window.alert() | alert() & confirm() & prompt()
```bash
- alert : In ra một bảng thông báo.
```
**Syn**
```js
alert("I am a robot"); // window.alert(“I am a robot”);
```
# comments 
```bash
Để chú thích ra câu lệnh ở file js
```
**Syn**
```bash
- // - chú thích 1 dòng
- /* */ - chú thích nhiều dòng
```
# var & let & const
**Syn**
```bash
var | let | const + <variable>;

- var: Chỉ định biến toàn cục (được khuyến cáo sử dụng).
- let: Chỉ định biến cục bộ.
- const: Chỉ định biến không thể thay đổi nữa.
```
# typeof
```bash
- Để kiểm tra kiểu dữ liệu của biến.  
```
**Syn**
```bash
typeof variable;
```
# Number() & ParseInt() & ParseFloat()
```bash
- Number    : Ép sang kiểu số.
```
**Ex1: Number**
```js
var a = "100.12345";
var b = Number(a);
document.write(typeof b); // number
```
**Ex2: ParseInt**
```js
var a = "123"; // kiểu chuỗi
var b = new Object("123"); // kiểu đối tượng
var c = 123.52; // kiểu số thực
var result = parseInt(a) + parseInt(b) + parseInt(c);
document.write(result); // 369
```
**Ex3: ParseFloat**
```js
var str = "12.34";
console.log(typeof parseFloat(str)) // Number
```
toPrecision()
Xác định chiều dài của một số cho trước.
var a = 100.12345;
var b = 34.5643;
var result = a+b;
var check = result.toPrecision(6);
document.write(a +" + "+ b + " = " + result.toPrecision(6));
document.write('<br>' + typeof check);
100.12345 + 34.5643 = 134.688
string
toFixed() 
Chuyển một số thành một chuỗi đồng thời xác định lấy sau dấu phẩy bao nhiêu số.
var a = 1566.12345;
var b = a.toFixed(3);
document.write(b + '<br>' + typeof b);
1566.123
string
toExponential()
Chuyển một số thành một số với cơ số mũ là 10.
var a = 1566;
var b = a.toExponential();
document.write(b);
1.566e+3 (1.566x)
Number.isInteger() 
Kiểu tra xem một số có phải kiểu số nguyên hay không.
var a = 10;
console.log(Number.isInteger(a));
true
Number.EPSILON
Trả về sự khác biệt giữa các số dấu phẩy động nhỏ nhất lớn hơn 1 và 1.
Có giá trị là 2.220446049250313e-16.
Number.isFinite(number) 
Kiểm tra một số có phải số hữu hạn hay không.
var a = 10/3;
var c = '10/2';
var b = Number.isFinite(a);
var d = Number.isFinite(c);
document.write(b+'<br/>');
document.write(d);
true
false
Number.isNaN() 
Kiểm tra xem số truyền vào có phải giá trị NaN (Not-a-number) không.
Number.isSafeInteger() 
Kiểm tra xem một số có phải là môt safe intege không.
Safe number là những số có thể được biểu diễn chính xác theo chuẩn EEE-754 ( tất cả các số nằm trong khảng từ 253-1 đến -(253-1)).
Number.MAX_SAFE_INTEGER
Biểu thị số nguyên an toàn tối đa trong Javascript.
function main(){
   let text = Number.MAX_SAFE_INTEGER;
   console.log(text.valueOf());

}
main()
9007199254740991
Number.MIN_SAFE_INTEGER
Biểu thị số nguyên an toàn nhỏ nhất trong Javascript.
Number.MAX_VALUE
Trả về số lớn nhất có thể trong Javascript.
Number.MIN_VALUE
Trả về số nhỏ nhất có thể có trong Javascript.
Number.POSITIVE_INFINITY
Trả về số vô cực dương, một số cao hơn bất kỳ số nào khác. 
Number.NEGATIVE_INFINITY
Trả về số vô cực âm, một số nhỏ hơn bất kỳ số nào khác.
prototype
Cho phép bạn thêm các thuộc tính và phương thức mới vào số. Là mooth thuộc tính có sẵn với tất cả các đối tượng Javascript.
function N(){
   return this.valueOf() / 2;
}
function main(){
   let n = 55;
   Number.prototype.N = function(){
      return this.valueOf()+2;
   };
   console.log(n.N());

}
main()
57
toLocalString()
Trả về một số dưới dạng chuỗi, sử dụng định dạng ngôn ngữ địa phương. Định dạng ngôn ngữ phục thuộc vào thiết lập ngôn ngữ trên máy tính của bạn.
Math
PI 
 Trả về số Pi.
function main(){
    let n = Math.PI;
    console.log(n)
}
main()
3.141592653589793
Math.E
Trả về giá trị E.
sqrt()
Trả về căn bậc 2.
console.log(Math.sqrt(4))
2
Math.sqrt1_2
Trả về căn bậc 2 của 1 phần 2.
Math.LN2
Trả về giá trị ln(2).
Math.LN10
Trả về giá trị của ln(10).
Math.LOG2E
Trả về giá trị của .
Math.Log10E
Trả về giá trị của .
round() 
Làm tròn số.
function main(){
    let n = Math.round(12.1234);
    console.log(n)
}
main()
12
Math.ceil()
Làm tròn trên.
function main(){
    let n = Math.ceil(12.1234);
    console.log(n)
}
main()
13
floor()
Làm tròn dưới.
function main(){
    let n = Math.floor(12.1234);
    console.log(n)
}
main()
12
Math.trunc()
Trả về phần nguyên của một số.
Math.sign()
Trả về 1 nếu là số dương, -1 nếu là số âm, NaN nếu không truyền gì vào, 0 là các trường hượp còn lại.
pow()
Trả về giá trị mũ.
function main(){
    let n = Math.pow(4,2);
    console.log(n)
}
main()
16
Math.abs()
Trả về giá trị tuyệt đối.
Math.sin()
Trả về giá trị sin, đơn vị radian.
Math.cos()
Trả về giá trị cos, đơn vị radian.
min() 
Trả về số nhỏ nhất.
console.log(Math.min(1,2,3,4,5))
1
Math.max()
Trả về số lớn nhất.
random() 
Trả về một số ngẫu nhiên nhỏ hơn 1.
Bài tập
Tạo ngẫu nhiên số từ 0 -> 100
function main(){
   for(let i=0; i<100; i++){
      let ran = parseInt(Math.random()*101);
      console.log(ran);
   }
}
main()

Tạo ngẫu nhiên số từ 1 -> 10
function main(){
   for(let i=0; i<51; i++){
      let ran = parseInt(Math.random()*10)+1;
      console.log(ran);
   }
}
main()

Tạo ngẫu nhiên số từ min -> max
function main(){
   min = 3;
   max = 9;
   for(let i=0; i<51; i++){
      let ran = parseInt(min + Math.random() * (max + 1 - min));
      console.log(ran);
   }
}
main()

Tạo 100 số ngẫu nhiên từ 1 đến 1000 không trùng nhau.

Strings
Trong javascript chuỗi cũng có thể coi là một mảng nên có thể lấy giá trị chuỗi giống như ở mảng được. 
Cú pháp:
    • var | let <name> = “ … “; - basic String
    • var | let <name> = ‘ … ‘; - basic String
    • var | let <name> = new String(value ); - Object String
    • var | let <name> = ` … `; -  template String
giữa “” và ‘’ không có khác biệt. template có ưu điểm hơn là có thể nhúng biểu thức vào chuỗi, viết chuỗi trên nhiều dòng dễ dàng và có thể sử dụng được biểu thức câu lệnh trong chuỗi.
length
Để đếm số ký tự trong chuỗi.
Cú pháp:
<variable>.length;
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>
<body>
  <script type="text/javascript">
    var Str = "Hello Wolrd";
    console.log(Str.length);
  </script>
</body>
</html>
11
Number, Object -> String
Ép kiểu từ số sang chuỗi.
Cú pháp:
    • <variable1>.toString(); – không được dùng với null hoặc undefinded (sẽ lỗi).
    • <variable> + “”;
    • String(num);
Giá trị radix (2-36):
    • 2 - kết quả trả về sẽ là số được biểu diễn dưới dạng nhị phân.
    • 8- kết quả trả về sẽ là số được biểu diễn dưới dạng bát phân.
    • 16- kết quả trả về là số được biểu diễn dưới dạng thập lục phân.
var Number = 17;
console.log(typeof Number);
Number = Number.toString();
console.log(typeof Number);
number
string
var a = 100;
var result = a.toString(2);
document.write(result);

+
Dùng để công chuỗi
let value = 789;
let str = value + "";  // "789"
${} - template string
Để nhúng một biểu thức javascript vào chuỗi.
let name = "Thắng";
let age = 20;
let str = `${name} is ${age}`;
Thắng is 20
CharAt() | at()
Lấy ra ký tự ở vị trí thứ n.
Cú pháp:
    • <variable>.charAt(); // mặc định lấy ra ký tự đầu tiên.
    • <variable>.charAt(n); // lấy ra ký tự thứ n
let a = "Hello World";
console.log(a.charAt());
console.log(a.charAt(6));
H
W
CharCodeAt()
Lấy ra mã số của ký tự ở vị trí thứ n trong bảng mã ASCII hoặc Unicode.
let a = "alpha";
console.log(a.charCodeAt());
console.log(a.charCodeAt(6));
97
NaN
.indexOf() and .search()
Dùng để tìm kiếm chuỗi hoặc ký tự trong chuỗi mẹ. Trả về vị trí bắt đầu xuất hiện.
var Str = "Hello Wolrd";
console.log(Str.indexOf('W'));
console.log(Str.search('W'));
6
6
lastIndexOf()
Dùng để tìm kiếm chuỗi hoặc ký tự trong chuỗi mẹ. Trả về vị trí bắt đầu xuất hiện. Nếu chuỗi có nhiều phần tử thỏa mãn điều kiện thì kết quả sẽ trả về vị trí cuối cùng.
Cú pháp:
<variable>.lastIndexOf(value);
.sclice(), .substring() and .substr()
Để cắt ký tự, chuỗi con trong chuỗi khác.
var Str = "Hello Wolrd";
console.log(Str.substring(6,11));
console.log(Str.slice(6,11));
console.log(Str.substr(6,5));
World
World
World

.replace()
Để thay đổi một chuỗi. 
a = a.replace("coder", "programer");
console.log(a);
Hello, My name is programer
Javascript không cho phép thay thế chuỗi giống như thay thế ở mảng.
let arr = ["a", "b", "c", "d"];
console.log(arr);
arr[0] = "e";
console.log(arr);
let str = "abcd";
console.log(str);
str[0] = "e";
console.log(str);
 ['a', 'b', 'c', 'd']
 ['e', 'b', 'c', 'd']
abcd
abcd
replaceAll()
Để thay thế chuỗi con trong chuỗi mẹ. Sự khác biệt giữa replace và replaceAll là replace chỉ thay thế chuỗi con đầu tiên được tìm thấy trong chuỗi mẹ còn replaceAll thì thay thế tất cả chuỗi con.
Cú pháp:
<variable>.replaceAll(value1, value2);
    • value1: Chuỗi cần thay thế.
    • value2: Chuỗi thay thế.
.toUpperCase()
Để chuyển chuỗi thành chữ hoa.
Cú pháp: <variable>.toUpperCase();
.toLowerCase()
Để chuyển chuỗi về chữ thường.
Cú pháp: <variable>.toLowerCase();
concat()
Để nối chuỗi với nhau, có thể thay thế bằng dấu + để nối chuỗi.
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>
<body>
  <script type="text/javascript">
    let Text1 = "Hello," + " Wolrd" + " I am from VN";
    let Text2 = "";
    Text2 = Text2.concat("hello,", " World", " I am from VN");
    console.log(Text1);
    console.log(Text2);
  </script>
</body>
</html>
Hello, Wolrd I am from VN
Hello, World I am from VN
.split()
Để chuyển đổi chuỗi sang mảng.
let a = "Hello World i am from Viet Nam"
a = a.split(" ");
for(var i = 0; i < a.length; i++){
  console.log(a[i]);
}
Hello
World
i
am
from
Viet
Nam

.padStart()
Thêm một ký tự hoặc một chuỗi nào đó vào phần đầu của chuỗi.
Cú pháp:
<variable>.padStart(<value1>, <value2>);
       value1: Độ dài của chuỗi sau cùng.
       value2: Chỉ định thêm cái gì vào chuỗi.
let a = "VietNam";
a = a.padStart(8, "O");
console.log(a);
OVietNam
padEnd()
Thêm một ký tự hoặc một chuỗi nào đó vào phần cuối của chuỗi.
Cú pháp:
<variable>.padEnd(<value1>, <value2>);
       value1: Độ dài của chuỗi sau cùng.
       value2: Chỉ định thêm cái gì vào chuỗi.
let a = "VietNam";
a = a.padStart(8, "O");
console.log(a);
VietNamO
repeat()
Để lặp lại một chuỗi nào đó.
Cú pháp:
<variable>.repeat(n) – Chỉ định lặp lai n lần.
function main(){
   let text = "Hello";
   console.log(text.repeat(3));

}
main()
'HelloHelloHello'
includes()
Để tìm kiếm chuỗi con trong chuỗi mẹ. trả về true, false.
Cú pháp:
<variable>.includes(value);
function main(){
   let text = "Hello world";
   console.log(text.includes("world"));

}
main()
True

startsWith()
Kiểm tra xem chuỗi có bắt đầu bằng một chuỗi hoặc một ký tự nào đó không. Trả về true hoặc false.
function main(){
   let text = "Hello world";
   console.log(text.startsWith("world"));

}
main()
False

endsWith() 
Xác định một chuỗi có kết thúc bằng một kí tự hoặc một chuỗi được người dùng cung cấp hay không. Trả về True, ngược lại hàm trả về False.
function main(){
   let text = "Hello world";
   console.log(text.endsWith("world"));

}
main()
True

matchAll()
function main(){
   let text = "Hello world";
   console.log(text.matchAll("w"));

}
main()
Iterator {}
valueOf()
Trả về giá trị nguyên thủy của một chuỗi, không thay đổi chuỗi gốc.
Có thể sử dụng để chuyển đổi một đối tượng chuỗi thành một chuỗi.
Small()
Sẽ bao chuỗi trong cặp thẻ <small>...</small>, khiến chữ hiển thị nhỏ hơn mặc định trên trình duyệt.
let text = "Hello";
let result = text.small();
console.log(result); // <small>Hello</small>

Arrays
Trong một Array có thể chứa các kiểu dữ liệu dữ liệu khác nhau.

Cú pháp:
    • var | let | const <name> = new Aray( value1, value2, … ); - không được khuyến khích dùng.
    • var | let | const <name> = [value1, value2, … ]; 
    • var | let | const [biến1, biến2, …] = tên biến;
isArray()
Kiểm tra xem có phải một Array không. Không thể dùng typeOf để kiểm tra xem phần tử cố phải một mảng hay không.
Cú pháp: Array.isArray(<variable>);
.length
Lấy chiều dài của một Array.
.join() 
Để nối các phần tử của mảng lại với nhau thành một chuỗi.
Các phần tử được ngăn cách nhau bởi kí tự do người dùng quy định. Nếu không truyền ký tự ngăn cách vào thì giá trị mặc định là dấu phẩy ",".
Cú pháp:
array.join(separator);
    • separator: là kí tự sẽ ngăn cách các phần tử với nhau, mặc định mang giá trị là dấu ",".
Hàm sẽ trả về một chuỗi, và mảng cũ không ảnh hưởng gì cả.
    <h1>Learning Programs</h1>
    <button onclick="myFunction()">Courses</button>
    <p id="demo"></p>
    <script>
      function myFunction() {
        var display = ["PHP", "HTML", "CSS", "JS"];
        var x = document.getElementById("demo");
        x.innerHTML = display.join('&&');
      }

.split()
let str = "apple,banana,orange";
let arr = str.split(",");
console.log(arr);
["apple", "banana", "orange"]
valueOf()
Hàm này có tác dụng tương tự như hàm array.join() , có nghĩa là nó sẽ nối các phần tử với nhau vào một chuỗi cách nhau bởi dấu phẩy.
let a = [1,2,3,4,5,6,7];
console.log(a.valueOf());

.forEach()
Để đuyệt qua từng phần tử của mảng.
 // type 2
 a.forEach(function (Number){
    console.log(Number);
 }
 );
 // type 3
 a.forEach( (Numbers) => {console.log(Numbers)});

1
2
3
4
5
6
7
8
9
…
every()
Kiểm tra tất cả phần tử trong mảng phải thỏa mãn điều kiện gì đó. Trả về true, false.
let a = [1,2,3,4,5];
a = a.every(function (Number){
   return Number % 2 == 0;
})
console.log(a);
false
some()
Kiểm tra ít nhất một phần tử trong mảng phải thỏa mãn điều kiện gì đó.
let a = [1,2,3,4,5];
a = a.some(function (Number){
  return Number % 2 == 0;
})
console.log(a);
true
find()
Tìm phần tử trong mảng rồi in ra màn hình. Chỉ trả về một giá trị.
filter()
Tìm phần tử trong mảng thỏa mãn điều kiện. trả về nhiều giá trị nếu thỏa mãn.
let a = [1,2,3,4,5,6,7];
// code 1
for(var i = 0; i < a.length; i++){
  if(a[i] > 4){
    console.log(a[i]);
  }
}
// code 2
a = a.filter(function (Number){
  return (Number > 4);
})
console.log(a); // khi này a đang là một đối tương (object)
5
6
7
(3) [5, 6, 7]0: 51: 62: 7
length: 3
[[Prototype]]: Array(0)

.push()
Hàm này sẽ thêm phần tử vào cuối mảng.
let a = [1,2,3,4,5,6,7];
a.push(8,9,10)
console.log(a.valueOf());

.pop()
Lấy phần tử cuối cùng trong mảng. không có tham số truyền vào.
let a = [1,2,3,4,5,6,7];
a.pop();
console.log(a.valueOf());

shift()
Hàm xóa phần tử đầu tiên của mảng, sau đó dồn các phần tử phía sau xuống một bậc.
Không có tham số truyền vào.
let a = [1,2,3,4,5,6,7];
console.log(a[1]);
a.shift();
console.log(a[1]);
2
3
unshift()
Thêm một phần tử vào vị trí đầu tiên của mảng, đồng thời đẩy các phẩn từ phía sau lên một bậc. có tham số truyền vào.
let a = [1,2,3,4,5,6,7];
console.log(a[1]);
a.unshift(0);
console.log(a[1]);
2
1
splice()
Thêm một mảng vào trong một mảng tại vị trí chỉ định.
var Text = ['Hello', 'i', 'am', 'a', 'coder'];
document.write(Text+'<br>');
Text.splice(1,0,['i', 'from', 'to Viet Nam']);
document.write(Text)
Hello,i,am,a,coder
Hello,i,from,to Viet Nam,i,am,a,coder
.sort()
Dùng để sắp xếp. nếu là số thì sắp xếp tăng dần, nếu là chữ thì sắp xếp theo bảng chữ cái. 
var N = [2,4,1,6,8];
N.sort();
document.write(N + '<br>');
var T = ['lee', 'quoc', 'viet', 'anh'];
T.sort()
document.write(T);
1,2,4,6,8
anh,lee,quoc,viet
.reverse()
Có tác dụng đảo ngược phần tử đầu xuống cuối và cứ tuần tự như thế.
function main(){
   let arr = [1,2,3,4,5];
   console.log(arr.reverse());
}
main()
5,4,3,2,1
.concat()
Dùng để nối hai mảng riêng biệt thành một mảng.
function main(){
   let arr = [1,2,3,4,5];
   let arr2 = [6,7,8,9,10];
   console.log(arr.concat(arr2));
}
main()
Array(10) [ 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 ]
.slice()
Dùng đê lấy một hay một số phần tử trong mảng.
function main(){
   let arr = [1,2,3,4,5];
   console.log(arr.slice(0,2));
}
main()
[ 1, 2 ]
.indexOf() 
Để tìm kiếm phần từ trong mảng.
function main(){
   let arr = [1,2,3,4,5];
   console.log(arr.indexOf(3));
}
main()
2
lastIndexOf() 
Tìm và trả về vị trí xuất hiện cuối cùng trong mảng nếu phần tử đó xuất hiện nhiều lần.
function main(){
   let arr = [1,2,3,3,4,5];
   console.log(arr.lastIndexOf(3));
}
main()
3
reduce() 
Hàm reduce sẽ duyệt qua từng phần tử trong mảng, sau đó trả về một giá trị cuối cùng, giá trị này phụ thuộc vào chương trình của hàm mà bạn truyền vào reduce.
reduceRight() 
Công dụng giống reduce nhưng duyệt mảng từ phải qua trái.
filter()
Để lặp qua các phần tử trong mảng, dùng để lọc các phần tử trong mảng theo một điều kiện nào đó.
function main(){
   let arr = [1,2,3,3,4,5];
   let list = arr.filter(function(item){
      return item > 3;
   })
   console.log(list);
}
main()
[4, 5]
copyWithin()
Để sao chép các phần tử trong mảng với vị trí bắt đầu và kết thúc việc sao chép được xác định.
fill() 
Để thay đổi giá trị của tất cả các phần tử trong mảng thành một giá trị mới.
function main(){
   let arr = [1,2,3,4,5];
   console.log(arr.fill(7, 0, 2));
}
main()
[ 7, 7, 3, 4, 5 ]
findIndex()
Để tìm vị trí đầu tiên của phần tử được tìm thấy thỏa điều kiện nào đó.
at()
Trả vể một phần tử được lập chỉ mục từ một mảng. Giống [].
flat()
Nối các phần tử của mảng con.
toSpliced()
includes()
findLast()
findLastIndex()
toSorted()
ToReversed()
Bài tập
Kiểm tra xem phần tử đã cho có phải Array hay không
let a = "Hello World i am from Viet Nam";
console.log(Array.isArray(a));
false
Tạo mảng và xuất ra màn hình 
var languages = ['Java', 'C++', 'Javascript'];
document.write(languages);




Object constructor
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <div id="output1"></div>
    <hr>
    <div id="output2"></div>
    <script>
        function User1(firstName, lastName, age) {
            this.firstName = firstName;
            this.lastName = lastName;
            this.age = age;
            this.getName = function() {
                return `${this.firstName} ${this.lastName}`;
            }
        }
        var User2 = function (firstName, lastName, age){
            this.firstName = firstName;
            this.lastName = lastName;
            this.age = age;
            this.getName = function() {
                return `${this.firstName} ${this.lastName}`;
            }
        }
        var user1 = new User1("Thắng", "Lê", 2005);
        var user2 = new User2("Sơn", "Nguyễn", 2000);

        var outputDiv1 = document.getElementById("output1");
        var outputDiv2 = document.getElementById("output2");
        for (var a in user1) {
            if (typeof user1[a] === "function") {
                outputDiv1.innerHTML += `${a}: ${user1[a]()}<br/>`;
            } else{
                outputDiv1.innerHTML += `${a}: ${user1[a]}<br/>`;
            }
        }
        for (var a in user2) {
            if (typeof user2[a] === "function") {
                outputDiv2.innerHTML += `${a}: ${user2[a]()}<br/>`;
            } else{
                outputDiv2.innerHTML += `${a}: ${user2[a]}<br/>`;
            }
        }
    </script>
</body>
</html>

This
Trong js, từ khóa this đề cập đến một đối tượng.
Object.values()
Tạo ra một mảng từ giá trị thuộc tính trong đối tượng. Mảng này chỉ lấy giá trị của Object.
let a = {
    name: "Json",
    age: 18,
    address: "London"
}
console.log(Object.values(a));
(3) ['Json', 18, 'London']
0: "Json"
1: 18
2: "London"
length: 3
[[Prototype]]: Array(0)
Advance (nâng cao)

Events - DOM
Đặt một hành động tác động lên các đối tượng HTML, qua đó ta có thể bắt được sự kiện và yêu cầu javascript thực thi một chương trình nào đó.
    • Sử dụng trực tiếp vào thẻ HTML thông qua từ khóa js.
    • Sử dụng chấm sự kiện.
    • Sử dụng addEventListener.
Sử dụng trực tiếp vào thẻ HTML thông qua từ khóa js
Xảy ra khi click vào đối tuộng được gắn thuộc tính .
<button onclick="display1()">BUTTON1</button>
<input type="button" value="BUTTON2" onclick="display2()">
 <input type="submit" value="BUTTON3" onclick="display3()">

function display1(){
    alert("Hello World!!");
}
function display2(){
     confirm("Hello World!!");
            }
            function display3(){
                prompt("Hello World!!");
            }


Sử dụng chấm sự kiện
Lưu ý: với cách này cần kết hợp với lấy giá trị element.
<!DOCTYPE html>
<html>
    <head>
        <title>Tester</title>
    </head>
    <body>
        <!--Tạo nút bấm (có 3 cách)-->
        <button>BUTTON1</button>
        <input type="button" value="BUTTON2" id="display1">
        <input type="submit" value="BUTTON3" class="display2">
        <script type="text/javascript">
        // Dùng fuction để đóng gói sự kiện
            function Display1(){
                let c = document.getElementsByTagName("button");
                // lấy bằng tag name thi khi gọi đến phải gọi như mảng
                c[0].onclick = function d(){
                    alert("Hello World");
                }
            }
            function Display2(){
                let c = document.getElementById("display1");
                c.onclick = function d(){
                    confirm("Hello World");
                }
            }
            function Display3(){
                let c = document.getElementsByClassName("display2");
                // lấy bằng class name thì khi gọi đến phải gọi như mẳng
                c[0].onclick = function d(){
                    prompt("Hello World");
                }
            }
            // Gọi hàm
            Display1();
            Display2();
            Display3();
        </script>
    </body>
</html>


# Sorting Objects
insertAdjacentHTML
Đây là một phương thức nâng cao và hay nhất, cách sử dụng nó để thêm HTML rất linh động.
Cú pháp: insertadjacentHTML(position, html)
    • position là vị trí muốn thêm (afterbegin, afterend, afterbegin, beforeend)
    • html là nội dung cần thêm
Vị trí của position:
<!-- beforebegin -->
<p>
<!-- afterbegin -->
Main Content
<!-- beforeend -->
</p>
<!-- afterend –
ví dụ
Tạo thẻ và render vào browser

<div></div>
var box = document.getElementsByTagName('div');
var h1 = document.createElement('h1');
box[0].appendChild(h1);
Thêm một thẻ vào cuối

<h1>The Element Object</h1>
<h2>The insertAdjacentHTML() Method</h2>

<button onclick="myFunction()">Insert</button>
<p>Click "Insert" to insert a paragraph after the header.</p>

<h2 id="myH2">My Header</h2>
function myFunction() {
        const h2 = document.getElementById("myH2");
        let html = "<h3>My new paragraph.</h3>";
        h2.insertAdjacentHTML("afterend", html);
      }
Mở webcam
<video autoplay></video>

let web = document.getElementsByTagName('video')[0];
navigator.mediaDevices.getUserMedia({video: true})
.then(stream => {
web.srcObject = stream;
})
.catch(err => {
console.error("lỗi truy cập webcam: ", err);
})
Chụp một khung hình từ webcam và chuyển thành ảnh JPEG
const canvas = document.createElement('canvas');
const context = canvas.getContext('2d');

canvas.width = video.videoWidth;
canvas.height = video.videoHeight;

context.drawImage(video, 0, 0, canvas.width, canvas.height);

const imageData = canvas.toDataURL('image/jpeg');

Object
Entries()
Làm nó đơn giản để sử dụng đối tượng trong vòng lặp. Hàm này chuyển một object thành mảng các cặp [key, value].
Ví dụ:
const data = {
    "Monday": ["Math", "English"],
    "Tuesday": ["Physics", "PE"]
};

console.log(Object.entries(data));
[
["Monday", ["Math", "English"]],
["Tuesday", ["Physics", "PE"]]
]
const data = {
    Monday: ["Math", "English"],
    Tuesday: ["Physics", "PE"]
};

for (const [day, slots] of Object.entries(data)) {
    console.log(day);
    console.log(slots);
}
Monday, Tuesday
["Math", "English"], ["Physics", "PE"]
Sẽ trả về văn bản đã được render, có nghĩa là phần tử nào bị ẩn đi bởi css sẽ không được hiển thị.
Có thể gây ra lỗ hổng bảo mật nếu bạn chèn nội dung do người dùng cung cấp mà không kiểm tra kĩ lưỡng.
window.print()
In nội dung của cửa sổ trình duyệt hiện tại. Nó sẽ đưa đến một cửa số chuyên để in ấn ra giấy.
Cú pháp: Window.print();
JS Operators
Phép tính
+
2 + 3
5
-
3 – 2
1
*
2 * 2
4
/
4/2
2
%
5%2
1
**
2 ** 3
8
++
2++ hoặc ++2
3
--
2— hoặc --2
1
Ví dụ về cộng trước và cộng sau
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
</head>
<body>
    <script src="Tester.js"></script>
</body>
</html>
let a = 2;
let b = 2;
let c = a++;
let d = ++b;
console.log(c + " - " + a);
console.log(d + " - " + b);

2 – 3 // c và a
3 – 3 // d và b
Gán
=
a =  2
Giá trị của a bằng 2 trong bộ nhớ
+=
a += 2
a cộng thêm 2 đơn vị
-=
a -= 2
a trừ đi 2 đơn vị
*=
a *= 2
a = a*2
%=
a  %= 2
a = a % 2
**=
a **= 2
a = a**2
&=
x &= y
x = x & y
^=
x^= y
x =  x ^ y
|=
x |= y
x = x | y
<<=
x <<= y
x = x << y
>>=
x >>= y
y = x >> y
>>>
Là toán tử dịch phải không dấu

<<<
Là toán tử dịch trái không dấu

&&=
Chưa học

||=
Chưa học

??=
Chưa học

&=
Là toán tử bitwise AND (AND bit). Sử dụng phép nhân hệ nhị phân.
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
</head>
<body>
    <script src="Tester.js"></script>
</body>
</html>
let a = 10;
a &= 9;
console.log(a);


8
Đổi sang hệ nhị phân:
10 = 1010
9 = 1001
Thực hiện phép and
0 and 1 = 0
1 and 0 = 0
0 and 0 = 0
1 and 1 = 1
Kết quả được: 1000
Đổi sang hệ thập phân được: 8

^=
Là phép toán XOR. Giống nhau thì trả về false (0) khác nhau trả về true (1).
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
</head>
<body>
    <script src="Tester.js"></script>
</body>
</html>
let a = 10;
a ^= 9;
console.log(a);


3
Đổi sang hệ nhị phân:
10 = 1010
9 = 1001
Thực hiện phép xor
0 xor 1 = 1
1 xor 0 = 1
0 xor 0 = 0
1 xor 1 = 0
Kết quả được: 0011
Đổi sang hệ thập phân được: 3
|=
Là một toán tử gán bitwise OR. Sử dụng phép cộng nhị phân.
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
</head>
<body>
    <script src="Tester.js"></script>
</body>
</html>
let a = 10;
a |= 9;
console.log(a);


11
Đổi sang hệ nhị phân:
10 = 1010
9 = 1001
Thực hiện phép xor
0 or 1 = 1
1 xor 0 = 1
0 xor 0 = 0
1 xor 1 = 1
Kết quả được: 1011
Đổi sang hệ thập phân được: 11
<<=
Là toán tử dịch trái ở hệ nhị phân.
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
</head>
<body>
    <script src="Tester.js"></script>
</body>
</html>
let a = 10;
a <<= 2;
console.log(a);


40
Đổi sang hệ nhị phân:
10 = 1010
Thực hiện phép dịch trái 2 bit
Kết quả được: 101000
Đổi sang hệ thập phân được: 40
>>=
Là toán tử dịch phải ở hệ nhị phân.
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
</head>
<body>
    <script src="Tester.js"></script>
</body>
</html>
let a = 10;
a >>= 2;
console.log(a);


2
Đổi sang hệ nhị phân:
10 = 1010
Thực hiện phép dịch phải 2 bit
Kết quả được: 10
Đổi sang hệ thập phân được: 2
JS Data type
    • Number: Kiểu dữ liệu số.
    • String: Kiểu dữ liệu chuỗi, kí tự.
    • BigInt: Kiểu dữ liệu số lớn.
    • Boolean: Kiểu true/false.
    • Null: Không có giá trị nào thỏa mãn.
    • Undefined: Giá trị chưa được gán hoặc giá trị không xác định.
    • Symbol:
    • Object: Kiểu đối tượng.
Ví dụ về undefined
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <script>
        var a;
        document.write(a);
    </script>
</body>
</html>

Exponential Notation
Là biểu diễn số mũ.
Ví dụ: 
    • 123e5 = 12300000 (123x10^5)
    • 123e-5 = 0.00123 (123x10^-5)
instaneof
Kiểm tra kiểu dữ liệu xem có phải là kiểu dữ liệu cho trước không.
JS Destructuring
Là phương pháp để hoán đổi giá trị của 2 biến cho nhau.
Cú pháp:
[a, b] = [b, a];

JS BigInt
Một số quá lớn không thể biểu diễn ở kiểu number được thì ta có thể biểu diễn ở kiểu BigInt().
Cú pháp:
let | var | const <variable> = BigInt(number);
let a = BigInt(88888888888888888888);
console.log(a + " -  " + typeof(a));
88888888888888885248 – bigint
JS Arrays 2 levels
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>
<body>
  <script type="text/javascript">
    var A = [
      [1,2,3,4],
      [2,3,4,5],
      [3,4,5,6],
      [4,5,6,7],
    ]
    var A1 = new Array(
      new Array(1,2,3,4),
      new Array(1,2,3,4),
      new Array(1,2,3,4),
      new Array(1,2,3,4),
    )
    document.write(A[1][2] + '<br>');
    document.write(A1[1][2])
  </script>
</body>
</html>
4
3
Date
Nó sẽ lấy ra đầy đủ ngày, tháng, năm, giờ, … có thể truyền tham số đầu vào hoặc không, tham số trong dấu nháy
var | let | const <variable> = new Date();
    • New date()
    • New date(date String)
    • New date(year, month)
    • New Date(year, month, day)
    • New Date(year, month, day, hours)
    • New Date(year, month, day, hours, minutes)
    • New Date(year, month, day, hours, minutes, seconds)
    • New Date(year, month, day, hours, minutes, seconds, ms)
    • New Date(miniseconds)
const d = new Date();
console.log(d);
Wed Feb 05 2025 10:09:00 GMT+0700 (Indochina Time)
toDateString()
Chuyển đổi sang định dạng chuỗi dễ đọc hơn.
let date = new Date()
var result = date.toDateString()
console.log(result, typeof result)
[ 'Sat Feb 22 2025', 'string' ]
toUTCString()
Để chuyển đổi đối tượng Date thành một chuỗi biểu diễn thời gian theo giờ UTC.
Việt Nam là giờ UTC+7 tức là chênh so với giờ UTC 7 tiếng.
function main(){
    let date = new Date();
    console.log(date.toUTCString())
    console.log(typeof date.toUTCString())
}
main();
'Mon, 24 Feb 2025 13:55:44 GMT'
'string'
toISOString()
Để chuyển đổi một đối tượng date thành một chuỗi theo định dạng ISO 8601. Đây là một định dạng chuẩn quốc tế để biểu diễn ngày và giờ.
function main(){
    let date = new Date();
    console.log(date.toISOString())
    console.log(typeof date.toISOString())
}
main();
'2025-02-24T13:59:40.389Z'
'string'
toLocaleDateString()
dùng để chuyển đổi một đối tượng Date thành một chuỗi biểu diễn ngày tháng theo quy ước địa phương.
function main(){
    let date = new Date();
    console.log(date.toLocaleDateString("vi-VN"))
    console.log(typeof date.toISOString())
}
main();
'24/2/2025'
String

Date.parse()
Trả về giá trị mili giây khoảng cách từ ngày 1 tháng 1 năm 1970.
getFullYear()
Để lấy ra năm.
const d = new Date();
console.log(d.getFullYear());
2025
getMonth()
Để lấy ra tháng. Nhưng phải công thêm 1 thì mới ra tháng hiện tại.
let date = new Date()
console.log(date.getUTCMonth())
1
getDate()
Để lấy ra ngày trong tháng.
function main(){
    let date = new Date();
    console.log(date.getDate(), typeof date.getDate())
}
main()
[ 26, 'number' ]
getDay()
Để lấy ra ngày trong tuần. Nhưng phải cộng thêm 1 mới ra ngày thực tế.
function main(){
    let date = new Date();
    console.log(date.getDay(), typeof date.getDay())
}
main()
[ 3, 'number' ]
.getHours()
Để lấy ra giờ trong ngày.
function main(){
    let date = new Date();
    console.log(date.getHours(), typeof date.getHours())
}
main()
[ 16, 'number' ]
.getMinutes()
Để lấy ra phút.
function main(){
    let date = new Date();
    console.log(date.getMinutes(), typeof date.getMinutes())
}
main()
[ 54, 'number' ]
.getSeconds()
Để lấy ra giây.
function main(){
    let date = new Date();
    console.log(date.getSeconds(), typeof date.getSeconds())
}
main()
[ 20, 'number' ]
getMiliseconds()
Để lấy ra mili giây.
getTime()
Trả về mili giây thời gian tính từ nhày 1 tháng 1 năm 1970.
getUTCDate()
Giống với getDate.
getUTCFullYear()
Giống voiwss getFullYear
getUTCMonth()
Giống với getmonth.
getUTCDay() 
Giống với getDay.
getUTCHours()
Giống với getHours.
getUTCMinutes()
Giống với Minutes.
getUTCSeconds()
Giống với getSeconds.
getUTCMiliseconds()
Giống với getMiliseconds.
getTimezoneOffset()
trả về sự khác biệt (tính bằng phút) giữa giờ địa phương và giờ UTC.
function main(){
    let date = new Date();
    console.log(date.getTimezoneOffset())
}
main()
-420 (phút)
Tương ứng với 7 tiếng UTC+7
setFullYear()
Để cài đặt một năm nào đó.
function main(){
    let date = new Date();
    date.setFullYear(2023)
    console.log(date.toDateString())
}
main()
'Sun Feb 26 2023'
Tất cả các giá trị ngày tháng năm, … đều bị thay đổi.
setMonth()
Để cài đặt một tháng nào đó.
setDate()
Để cài đặt một ngày trong tháng nào đó.
setHours()
Để cài đặt một giờ nào đó.
setMinutes()
Để cài đặt một phút nào đó.
setSeconds()
Để cài đặt một giây nào đó.
Thuật toán cập nhật thứ, ngày, tháng, năm bằng javascript

JS Sets
Là một tập hợp các giá trị duy nhất.
Mỗi giá trị chỉ có thể xuất hiện 1 lần trong Set.
Các giá trị có thể thuộc bất ký loại nào, giá trị nguyên thủy hoặc đối tượng.
function main(){
   let s = new Set([1,2,3,4,5,5]);
   console.log(s, typeof s);
}
main()
[ Set { 0: 1, 1: 2, 2: 3, 3: 4, 4: 5 }, 'object' ]
add()
function main(){
   let s = new Set();
   s.add(1);
   s.add(2);
   s.add(3);
   s.add(3);
   console.log(s, typeof s);
}
main()
[ Set { 0: 1, 1: 2, 2: 3 }, 'object' ]
Kiểm tra một đối tượng có phải kiểu dữ liệu set hay không
function main(){
   let s = new Set([1,2]);
   console.log(s instanceof Set);
}
main()
True

has()
Trả về true nếu giá trị được chỉ định tồn tại trong một tập hợp.
function main(){
   let s = new Set([1,2]);
   console.log(s.has(1));
}
main()
true
values()
Trả về một đối tượng Iterator với các giá trị trong một Set.
Keys()
Trả về giá trị giống như values(). Điều này làm cho Set tương thích với Maps.
entries()
JS Maps
Chứa các cặp key – value. 
Map cho phép bất kỳ kiểu dữ iệu nào làm key, duy trì thứ tự chèn, được tối ưu cho việc thêm, xóa và tìm kiếm các phần tử.
function main(){
   let m = new Map([
      ['name', 'John'],
      ['age', 30]
   ]);
   console.log(m, typeof m);
}
main()
[ Map { 'name': 'John', 'age': 30 }, 'object' ]
set()
Để thêm phần tử vào Map.
function main(){
   let m = new Map([
      ['name', 'John'],
      ['age', 30]
   ]);
   m.set("address", "New York");
   console.log(m);
}
main()
Map { 'name': 'John', 'age': 30, 'address': 'New York' }
get()
Để lấy ra giá trị của một key.
function main(){
   let m = new Map([
      ['name', 'John'],
      ['age', 30]
   ]);
   console.log(m.get("age"));
}
main()
30
size
Trả về số phần tử trong Map.
function main(){
   let m = new Map([
      ['name', 'John'],
      ['age', 30]
   ]);
   console.log(m.size);
}
main()
2
delete()
Xóa một phần tử trong Map.
clear ()
Xóa tất cả phần tử trong Map.
has()
Trả về true nếu khóa tồn tại trong Map.
foreach()
entries()
keys()
values()
as Keys
groupBy()

kiểm tra kiểu dữ liệu của biến.
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <script>
        var a = 100.12345;
        document.write(typeof a);
        document.write('<br>' + a.constructor);
    </script>
</body>
</html>
number
function Number() { [native code] }
JS Destructuring
Là cú pháp gán cấu trúc giải nén các thuộc tính đối tượng thành các biến.
function main(){
   let student = {
      name: "mickey",
      address: "USA"
   }
   let {name, address} = student;
   console.log(name, typeof name);
}
main(
[ 'mickey', 'string' ]

function main(){
   let student = {
      name: "mickey",
      address: "a11"
   }
   let {name, address, country = "US"} = student;
   console.log(student.get(contry));
}
main()
contry is not defined
Xem ví dụ thêm ở đây: https://www.w3schools.com/js/js_destructuring.asp
JS Errors
Xem ví dụ ở đây: https://www.w3schools.com/js/js_errors.asp
JS Hoisting
Xem ví dụ ở đây: https://www.w3schools.com/js/js_hoisting.asp
JS Strict Mode
Xem ví dụ ở đây: https://www.w3schools.com/js/js_strict.asp
JS this Keyword
Xem ví dụ ở đây: https://www.w3schools.com/js/js_this.asp
JS Classes
Xem ví dụ ở đây: https://www.w3schools.com/js/js_classes.asp
JS Modules
Xem ví dụ ở đây: https://www.w3schools.com/js/js_modules.asp
Cho phép bạn chia nhỏ mã của mình thành các tệp riêng biệt. Điều này giúp duy trì cơ sở mã dễ  dàng hơn.
Các Modules được nhập từ bên ngoài bằng câu lệnh import.
Các Modules cũng dựa và type= “module” trong thẻ script.

20
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <script type="module" src="./Tester.js"></script>
</body>
</html>
export let a = 20;

import { a } from './min.js';
console.log(a);

JS JSON (Javascript Object Notation)
Xem ví dụ ở đây: https://www.w3schools.com/js/js_json.asp
JSON là một loại định dạng và vận chuyển dữ liệu. Thường được sử dụng khi dữ liệu được gửi tử máy chủ đến trang web.
Định dạng của JSON là văn bản (String).
JSON.parse()
Để chuyển một chuỗi JSON thành một đối tượng Javascript.
function main(){
   let json = `{"employees": [
      {"firstName": "John", "lastName": "Doe"},
      {"firstName": "Anna", "lastName": "Smith"},
      {"firstName": "Peter", "lastName": "Jones"}
   ]}`;
   console.log(typeof json);
   let data = JSON.parse(json);
   console.log(data.employees[0]);
}
main()
String
{ firstName: 'John', lastName: 'Doe' }
JS Debugging
JS Style Guide
JS Mistakes
JS Performance
JS Reserved Words
JS Objects
JS Functions
JS Classes
JS Async
JS Brower BOM (Browser Object Model)
Cho phép Javascript nói chuyện với trình duyệt. Không có tiêu chuẩn chính thức nào cho mô hình trình duyệt BOM.
Các trình duyệt hiện đại đã triển khai (gần như) cùng các phương thức và thuộc tính cho tương tác Javascript, nên thường được gọi là BOM.
JS Window
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

JS AJAX
JS JSON
JS vs jQuery
JS Graphics
JS Exampbles
JS References
ParentNode
Trả về thẻ cha của nó.
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Tester</title>
</head>
<body>
  <div></div>
  <script>
    var a = document.getElementsByTagName('div')[0].parentNode;
    console.log(a);
  </script>
</body>
</html>



ParentNode.nodeName
Trả về tên của thẻ cha.
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Tester</title>
</head>
<body>
  <div></div>
  <script>
    var a = document.getElementsByTagName('div')[0].parentNode.nodeName;
    console.log(a);
  </script>
</body>
</html>


ParentElement
Trả về thuộc tính ra của phần tử 
Bài tập
Tạo ra một thẻ có thể đóng được bằng js
<!DOCTYPE html>
<html>
<head>
<style>
div {
  box-sizing: border-box;
  padding: 16px;
  width: 100%;
  background-color: red;
  color: #fff;
}
.closebtn {
  float: right;
  font-size: 30px;
  font-weight: bold;
  cursor: pointer;
}
.closebtn:hover {
  color: #000;
}
</style>
</head>
<body>

<div>
  <span onclick="this.parentElement.style.display = 'none';" class="closebtn">&times;</span>
  <p>To close this container, click on the X symbol to the right.</p>
</div>

</body>
</html>


Xóa phần tử có trong một bảng bằng js
<!DOCTYPE html>
<html>
  <head>
    <title>Xóa thẻ HTML</title>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
  </head>
  <body>
    <h1>Xóa thẻ HTML</h1>
    <table border="1" cellspacing="0" cellpadding="5">
      <tr>
        <td>1</td>
        <td>Tiêu đề thứ nhất</td>
        <td>
          <input type="button" value="Delete" />
        </td>
      </tr>
      <tr>
        <td>2</td>
        <td>Tiêu đề thứ hai</td>
        <td>
          <input type="button" value="Delete" />
        </td>
      </tr>
      <tr>
        <td>3</td>
        <td>Tiêu đề thứ ba</td>
        <td>
          <input type="button" value="Delete" />
        </td>
      </tr>
      <tr>
        <td>4</td>
        <td>Tiêu đề thứ tư</td>
        <td>
          <input type="button" value="Delete" />
        </td>
      </tr>
    </table>
    <script>
      window.onload = function () {
        // Lấy danh sách button
        var button = document.getElementsByTagName("input");

        // Lặp qua từng button
        for (var i = 0; i < button.length; i++) {
          // gán sự kiện click
          button[i].addEventListener("click", function () {
            // Lấy thẻ tr
            var parent = this.parentElement.parentElement;
            // và thực hiện xóa
            parent.remove();
          });
        }
      };
    </script>
  </body>
</html>



Thay đổi hình ảnh bằng js
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Javascript Example</title>
    </head>
    <body>
        <div>
            <img id="hinhanh" src="https://1.bp.blogspot.com/-uzsrHsDROtg/XlpeZ0ywb-I/AAAAAAAAWQo/k9qQ-Y0_cfI6YR8fZemH0y_OccSQi1mwACLcBGAsYHQ/s1600/Anh-gai-xinh-deo-kinh%2B%252827%2529.jpg" alt="Hình ảnh" width="300px" height="300px"/>
        </div> 
        <input type="button" id="btn1" value="Đổi Hình"/>
        <input type="button" id="btn2" value="Trở về hình cũ"/>         
        <script language="javascript">        
            var hinh1 = 'https://1.bp.blogspot.com/-uzsrHsDROtg/XlpeZ0ywb-I/AAAAAAAAWQo/k9qQ-Y0_cfI6YR8fZemH0y_OccSQi1mwACLcBGAsYHQ/s1600/Anh-gai-xinh-deo-kinh%2B%252827%2529.jpg';
            var hinh2 = 'https://s3.cloud.cmctelecom.vn/tinhte1/2018/04/4295142_GirlXinh_ThienITCollection-Part7_5.jpg';       
            document.getElementById("btn1").onclick = function(){
                document.getElementById("hinhanh").src = hinh2;
            };
            document.getElementById("btn2").onclick = function(){
                document.getElementById("hinhanh").src = hinh1;
            };      
        </script>       
    </body>
</html>

Thêm, thay thế nội dung
id
thêm id vào thẻ HTML;
element | biến.id = “value”;
className
thêm class vào thẻ HTML;
element | biến.className = ‘value’;
ví dụ:
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>
<body>
  <p></p>
  <p></p>
  <script language="javascript" type="text/javascript">
    var content = document.getElementsByTagName('p');
    // thay thế nội dung thẻ p
    content[0].innerHTML = "this content is created from innerHTML";
    // thêm id="text"
    content[0].id = "text";
    // thêm class="text"
    content[0].className = 'text';
  </script>
</body>
</html>
1. Thay đổi thuộc tính thẻ html bằng Javascript
Để thay đổi giá trị của thuộc tính HTML thì ta sử dụng cú pháp như sau:
1
document.getElementById("element").attributeName = "new value";
Để lấy giá trị của thuộc tính HTML ta sử dụng cú pháp sau:
1
document.getElementById("element").attributeName;
Trong đó attributeName là tên của thuộc tính mà bạn cần xử lý. Tùy vào mỗi thẻ html mà có các thuộc tính khác nhau. Dưới đây là danh sách các thuộc tính thường dùng nhất.
Quá đơn giản phải không nào, rất giống với cách thay đổi và lấy nội dung bên trong thẻ HTML. Từ đây có thể suy ra rằng trong Javascript để thiết lập (set) và lấy (get) thì sử dụng chung một cú pháp, chỉ khác nhau ở chỗ gán bằng và không có gán bằng.
Ví dụ: Xây dựng chương trình khi click vào một button thì chuyển nó thành textbox, và tiếp tục click vào textbox thì sẽ đổi thành button
DemoRUN
1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
21
22
23
24
25
<html>
    <body>
        <script language="javascript">
          function change()
          {
             // Lấy đối tượng
             var object = document.getElementById("object");

             // lấy thuộc tính type
             var type = object.type;

             // kiểm tra thuộc tính type và thay đổi
            if (type == "button"){

               object.type = 'text';
            }
            else{
                object.type = "button";
            }

          }
        </script>
        <input type="button" value="CLick me" onclick="change()" id="object" />
    </body>
</html>
style
.style.CSSname
Để thêm hoặc thay đổi css cho thẻ, thuộc tính nào đó
Element.style.CSSname = “…”;
Element.style = ‘attribute: value, ….’
Ví dụ:
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <h1>Hello World!!</h1>
    <h1>Hello World!!</h1>
    <script></script>
    <script type="text/javascript">
        var a = document.getElementsByTagName('h1');
        a[0].style.color = '#ff0000';
        a[1].style = "color: #aeae";
    </script>
</body>
</html>

Children
Thuộc tính children trả về các giá trị con của nó
Element.children;
setAttribute
Để gán giá trị cho thẻ input thì ta có hai cách, thứ nhất là sử dụng thuộc tính value, thứ hai là sử dụng phương thức setAttribute.
Cài đặt thời gian

Websocket
new WebSocket()
Dùng để tạo websocket, mở kết nối chưa gửi, chưa nhận gì cả.
Cú pháp:
const ws = new WebSocket("ws://localhost:8765");
.onopen
Dùng để báo đã kết nối, chuẩn bị gửi dữ liệu
Cú pháp:
ws.onopen = () => {
    console.log("WebSocket connected");
};
.send()
Gửi dữ liệu lên server
Cú pháp:
ws.send("Hello server");
ws.send(JSON.stringify({
    x: 100,
    y: 200
}));
.onmessage()
Nhận dữ liệu từ server
Cú pháp:
ws.onmessage = (event) => {
    console.log(event.data);
};
.onerror()
.onclose()