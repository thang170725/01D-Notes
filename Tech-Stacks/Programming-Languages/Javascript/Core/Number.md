- [Number (Xử lý số)](#number-xử-lý-số)
---
# Number (Xử lý số)
## toPrecision()
```bash
Xác định chiều dài của một số cho trước.
var a = 100.12345;
var b = 34.5643;
var result = a+b;
var check = result.toPrecision(6);
document.write(a +" + "+ b + " = " + result.toPrecision(6));
document.write('<br>' + typeof check);
100.12345 + 34.5643 = 134.688
string
```
## toFixed()
```bash
Chuyển một số thành một chuỗi đồng thời xác định lấy sau dấu phẩy bao nhiêu số.
var a = 1566.12345;
var b = a.toFixed(3);
document.write(b + '<br>' + typeof b);
1566.123
string
```
## toExponential()
```bash
Chuyển một số thành một số với cơ số mũ là 10.
var a = 1566;
var b = a.toExponential();
document.write(b);
1.566e+3 (1.566x)
```
## Number.isInteger() 
```bash
Kiểu tra xem một số có phải kiểu số nguyên hay không.
var a = 10;
console.log(Number.isInteger(a));
true
```
## Number.EPSILON
```bash
Trả về sự khác biệt giữa các số dấu phẩy động nhỏ nhất lớn hơn 1 và 1.
Có giá trị là 2.220446049250313e-16.
```
## Number.isFinite(number) 
```bash
Kiểm tra một số có phải số hữu hạn hay không.
var a = 10/3;
var c = '10/2';
var b = Number.isFinite(a);
var d = Number.isFinite(c);
document.write(b+'<br/>');
document.write(d);
true
false
```
## Number.isNaN() 
```bash
Kiểm tra xem số truyền vào có phải giá trị NaN (Not-a-number) không.
```
## Number.isSafeInteger() 
```bash
Kiểm tra xem một số có phải là môt safe intege không.
Safe number là những số có thể được biểu diễn chính xác theo chuẩn EEE-754 ( tất cả các số nằm trong khảng từ 253-1 đến -(253-1)).
```
## Number.MAX_SAFE_INTEGER
```bash
Biểu thị số nguyên an toàn tối đa trong Javascript.
function main(){
   let text = Number.MAX_SAFE_INTEGER;
   console.log(text.valueOf());

}
main()
9007199254740991
```
## Number.MIN_SAFE_INTEGER
```bash
Biểu thị số nguyên an toàn nhỏ nhất trong Javascript.
```
## Number.MAX_VALUE
```bash
Trả về số lớn nhất có thể trong Javascript.
```
## Number.MIN_VALUE
```bash
Trả về số nhỏ nhất có thể có trong Javascript.
```
## Number.POSITIVE_INFINITY
```bash
Trả về số vô cực dương, một số cao hơn bất kỳ số nào khác. 
```
## Number.NEGATIVE_INFINITY
```bash
Trả về số vô cực âm, một số nhỏ hơn bất kỳ số nào khác.
Exponential Notation
Là biểu diễn số mũ.
Ví dụ: 
    • 123e5 = 12300000 (123x10^5)
    • 123e-5 = 0.00123 (123x10^-5)
```
# instaneof
```bash
Kiểm tra kiểu dữ liệu xem có phải là kiểu dữ liệu cho trước không.
JS Destructuring
Là phương pháp để hoán đổi giá trị của 2 biến cho nhau.
Cú pháp:
[a, b] = [b, a];
```
# JS BigInt
```bash
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