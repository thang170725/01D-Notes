- [Create (tạo)](#create-tạo)
  - ["" \& '' \& new String \& \`\`](#----new-string--)
- [Display (cung cấp thông tin)](#display-cung-cấp-thông-tin)
  - [length](#length)
- [Process (xử lý chuỗi)](#process-xử-lý-chuỗi)
- [.toString() \& String() \& +](#tostring--string--)
  - [${} - template string](#---template-string)
  - [CharAt() | at()](#charat--at)
  - [CharCodeAt()](#charcodeat)
  - [.indexOf() \& .search()](#indexof--search)
  - [lastIndexOf()](#lastindexof)
  - [.sclice() \& .substring() \& .substr()](#sclice--substring--substr)
  - [.replace()](#replace)
  - [replaceAll()](#replaceall)
  - [.toUpperCase() \& .toLowerCase()](#touppercase--tolowercase)
  - [concat()](#concat)
  - [.split()](#split)
  - [.padStart()](#padstart)
  - [padEnd()](#padend)
  - [repeat()](#repeat)
  - [.includes()](#includes)
  - [startsWith()](#startswith)
  - [endsWith()](#endswith)
  - [matchAll()](#matchall)
  - [Iterator {}](#iterator-)
  - [valueOf()](#valueof)
  - [Small()](#small)
  - [.trim() \& trimstart() \& trimEnd()](#trim--trimstart--trimend)
- [RegExp (Biểu thức chính quy)](#regexp-biểu-thức-chính-quy)
  - [.match() (Trả về một mảng với các kết quả khớp. Trả về null nếu không tìm thấy kết quả khớp)](#match-trả-về-một-mảng-với-các-kết-quả-khớp-trả-về-null-nếu-không-tìm-thấy-kết-quả-khớp)
  - [.test() (Trả về True/False nếu chuỗi khớp hoặc không khớp với biểu thức chính quy)](#test-trả-về-truefalse-nếu-chuỗi-khớp-hoặc-không-khớp-với-biểu-thức-chính-quy)
  - [.exec()](#exec)
  - [.replace()](#replace-1)
---
# Create (tạo)
## "" & '' & new String & ``
```bash
- Trong javascript chuỗi cũng có thể coi là một mảng nên có thể lấy giá trị chuỗi giống như ở mảng được. 
- giữa “” và ‘’ không có khác biệt. template có ưu điểm hơn là có thể nhúng biểu thức vào chuỗi, viết chuỗi trên nhiều dòng dễ dàng và có thể sử dụng được biểu thức câu lệnh trong chuỗi.
```
**Syn**
```bash
- var | let <name> = “ … “; - basic String
- var | let <name> = ‘ … ‘; - basic String
- var | let <name> = new String(value ); - Object String
- var | let <name> = ` … `; -  template String
```
# Display (cung cấp thông tin)
## length
```bash
Để đếm số ký tự trong chuỗi.
```
**Ex**
```js
var Str = "Hello Wolrd";
console.log(Str.length); // 11
```
# Process (xử lý chuỗi)
# .toString() & String() & +
```bash
Ép kiểu từ số sang chuỗi.
```
**Syn**
```bash
- <variable1>.toString(); – không được dùng với null hoặc undefinded (sẽ lỗi).
- <variable> + “”;
- String(num);
```
**Ex1: toString()**
```js
var Number = 17;
console.log(typeof Number); // number

Number = Number.toString();
console.log(typeof Number); // string
```
**Ex2**
```js
var a = 100;
var result = a.toString(2);

// 2 - kết quả trả về sẽ là số được biểu diễn dưới dạng nhị phân.
// 8- kết quả trả về sẽ là số được biểu diễn dưới dạng bát phân.
// 16- kết quả trả về là số được biểu diễn dưới dạng thập lục phân.
```
**Ex3: +**
```js
let value = 789;
let str = value + "";  // "789"
```
## ${} - template string
```bash
Để nhúng một biểu thức javascript vào chuỗi.
```
**Ex**
```js
let name = "Thắng";
let age = 20;
let str = `${name} is ${age}`; // Thắng is 20
```
## CharAt() | at()
```bash
Lấy ra ký tự ở vị trí thứ n.
```
**Syn**
```bash
1. <variable>.charAt(); // mặc định lấy ra ký tự đầu tiên.
2. <variable>.charAt(n); // lấy ra ký tự thứ n
```
**Ex**
```js
let a = "Hello World";
console.log(a.charAt()); // H
console.log(a.charAt(6)); // W
```
## CharCodeAt()
```bash
Lấy ra mã số của ký tự ở vị trí thứ n trong bảng mã ASCII hoặc Unicode.
```
**Ex**
```js
let a = "alpha";
console.log(a.charCodeAt()); // 97
console.log(a.charCodeAt(6)); // NaN
```
## .indexOf() & .search()
```bash
Dùng để tìm kiếm chuỗi hoặc ký tự trong chuỗi mẹ. Trả về vị trí bắt đầu xuất hiện.
```
**Ex**
```js
var Str = "Hello Wolrd";
console.log(Str.indexOf('W')); // 6
console.log(Str.search('W')); // 6
```
## lastIndexOf()
```bash
Dùng để tìm kiếm chuỗi hoặc ký tự trong chuỗi mẹ. Trả về vị trí bắt đầu xuất hiện. Nếu chuỗi có nhiều phần tử thỏa mãn điều kiện thì kết quả sẽ trả về vị trí cuối cùng.
```
**Syn**
```bash
<variable>.lastIndexOf(value);
```
## .sclice() & .substring() & .substr()
```bash
Để cắt ký tự, chuỗi con trong chuỗi khác.
```
**Ex**
```js
var Str = "Hello Wolrd";
console.log(Str.substring(6,11)); // World
console.log(Str.slice(6,11)); // World
console.log(Str.substr(6,5)); // World
```
## .replace()
```bash
Để thay đổi một chuỗi.
```
**Ex**
```js 
a = a.replace("coder", "programer");
console.log(a); // Hello, My name is programer

// Javascript không cho phép thay thế chuỗi giống như thay thế ở mảng.
```
## replaceAll()
```bash
Để thay thế chuỗi con trong chuỗi mẹ. Sự khác biệt giữa replace và replaceAll là replace chỉ thay thế chuỗi con đầu tiên được tìm thấy trong chuỗi mẹ còn replaceAll thì thay thế tất cả chuỗi con.
```
**Syn**
```bash
<variable>.replaceAll(value1, value2);

- value1: Chuỗi cần thay thế.
- value2: Chuỗi thay thế.
```
## .toUpperCase() & .toLowerCase()
```bash
- toUpperCase: Để chuyển chuỗi thành chữ hoa.
- toLowerCase: Để chuyển chuỗi về chữ thường.
```
**Syn: toUpperCase**
```bash
<variable>.toUpperCase();
```
**Syn: toLowerCase**
```bash
<variable>.toLowerCase();
```
## concat()
```bash
Để nối chuỗi với nhau, có thể thay thế bằng dấu + để nối chuỗi.
```
**Ex**
```js
let Text1 = "Hello," + " Wolrd" + " I am from VN";
let Text2 = "";
Text2 = Text2.concat("hello,", " World", " I am from VN");
console.log(Text1); // Hello, Wolrd I am from VN
console.log(Text2); // Hello, World I am from VN
```
## .split()
```bash
Để chuyển đổi chuỗi sang mảng.
```
**Ex**
```js
let a = "Hello World i am from Viet Nam"

a = a.split(" ");
for(var i = 0; i < a.length; i++){
  console.log(a[i]);
}

// -- Hello
// World
// i
// am
// from
// Viet
// Nam
```
## .padStart()
```bash
Thêm một ký tự hoặc một chuỗi nào đó vào phần đầu của chuỗi.
```
**Syn**
```bash
<variable>.padStart(<value1>, <value2>);

- value1: Độ dài của chuỗi sau cùng.
- value2: Chỉ định thêm cái gì vào chuỗi.
```
**Ex**
```js
let a = "VietNam";
a = a.padStart(8, "O");
console.log(a); // OVietNam
```
## padEnd()
```bash
Thêm một ký tự hoặc một chuỗi nào đó vào phần cuối của chuỗi.
```
**Syn**
```bash
<variable>.padEnd(<value1>, <value2>);

- value1: Độ dài của chuỗi sau cùng.
- value2: Chỉ định thêm cái gì vào chuỗi.
```
**Ex**
```js
let a = "VietNam";
a = a.padStart(8, "O");

console.log(a); // VietNamO
```
## repeat()
```bash
Để lặp lại một chuỗi nào đó.
```
**Syn**
```bash
<variable>.repeat(n) 

- n: Chỉ định lặp lai n lần.
```
**Ex**
```js
let text = "Hello";

console.log(text.repeat(3)); // 'HelloHelloHello'
```
## .includes()
```bash
Để tìm kiếm chuỗi con trong chuỗi mẹ. trả về true, false.
```
**Syn**
```bash
<variable>.includes(value);
```
**Ex**
```js
let text = "Hello world";
console.log(text.includes("world")); // True
```
## startsWith()
```bash
- Kiểm tra xem chuỗi có bắt đầu bằng một chuỗi hoặc một ký tự nào đó không. 
- Trả về true hoặc false.
```
**Ex**
```js
let text = "Hello world";
console.log(text.startsWith("world")); // False
```
## endsWith() 
```bash
- Xác định một chuỗi có kết thúc bằng một kí tự hoặc một chuỗi được người dùng cung cấp hay không. 
- Trả về True, ngược lại hàm trả về False.
```
**Ex
```js
let text = "Hello world";

console.log(text.endsWith("world")); // True
```
## matchAll()
```js
let text = "Hello world";

console.log(text.matchAll("w"));
```
## Iterator {}
## valueOf()
```bash
- Trả về giá trị nguyên thủy của một chuỗi, không thay đổi chuỗi gốc.
- Có thể sử dụng để chuyển đổi một đối tượng chuỗi thành một chuỗi.
```
**Ex1**
```js
let num = new Number(10)

console.log(num.valueOf()) // 10

// num là object Number
// valueOf() trả về giá trị số thực sự
```
**Ex2: Ví dụ với Date**
```js
let date = new Date()

console.log(date.valueOf()) // 1710412345678

// Đây là timestamp (milliseconds từ 1/1/1970).
```
**Ex3: Ví dụ JavaScript tự gọi valueOf()**
```js
let num = new Number(10)

console.log(num + 5) // 15

// Quy trình:
// num là object
// JS cần số để cộng
// JS tự gọi num.valueOf() 
// lấy 10
// 10 + 5 = 15
```
**Ex4: Ví dụ custom object (hay trong phỏng vấn)**
```js
let obj = {
  valueOf() {
    return 50
  }
}

console.log(obj + 20) // 70

// Vì JS sẽ: obj.valueOf() → 50
// 50 + 20
```
## Small()
```bash
Sẽ bao chuỗi trong cặp thẻ <small>...</small>, khiến chữ hiển thị nhỏ hơn mặc định trên trình duyệt.
```
**Ex**
```js
let text = "Hello";
let result = text.small();

console.log(result); // <small>Hello</small>
```
## .trim() & trimstart() & trimEnd()

```bash
- trim      : Xóa khoảng trắng ở 2 đầu của chuỗi.
- trimstart : Xóa khoảng trắng ở bên trái.
- trimend   : Xóa khoảng trắng ở bên phải.
```

**Ex**

```js
let a = "    Hê lô   ";
console.log(a);
console.log(a.trim());

//     Hê lô
// Hê lô
```
# RegExp (Biểu thức chính quy)
**Syn** 
```bash
/pattern/modifiers 

- pattern là chuỗi Regular Expression 
- modifiers là thông số cấu hình cho chuỗi pattern, và nó có các giá trị sau: 
    + i : so khớp không quan tâm đến chữ hoa chữ thường.
    + g: so khớp toàn bộ chuỗi cần tìm .
    + m: so khớp luôn cả các dữ liệu xuống dòng (multiline).
```
**Ký hiệu cơ bản**
```js
- /[A-Z]/g  : khớp từ A-Z
- /[1-9]/g  : khớp từ 1-9
- /\d/g     : khớp với kết quả là số
- /\D/g     : khớp với kết quả không là số
- /\w/g     : khớp với kết quả là a-z, A-Z, 0-9, _
- /\W/      : Tìm các ký tự không phải là chữ cái
- /\s/g     : khớp với kết quả là dấu cách, tab, newline
- /^web/    : khớp với chuỗi bắt đầu bằng web
- /web$/    : khớp với chuỗi kết thúc bằng web
- (x|y)     : Tìm ký tự x hoặc y
- n+        : Tìm 1 hoặc nhiều chữ n liên tiếp nhau
- n*        : Tìm 0 hoặc nhiều chữ n liên tiếp nhau
- n?        : Tìm 0 hoặc 1 chữ n
- .         : Tìm ký tự bất kỳ
- {X}       : Kiểm tra ký tự xuất hiện đúng X lần
- {X, Y}    : Xuất hiện X → Y lần
- {X,}      : Xuất hiện ít nhất X lần
- /s        : Cho phép cả khoảng trắng
- (?=...)   : kiểm tra điều kiện nhưng không "ăn" ký tự
```
## .match() (Trả về một mảng với các kết quả khớp. Trả về null nếu không tìm thấy kết quả khớp)
**Syn**
```bash
text.match(paterrn);
```
**Ex**
```js
let text = "Hello world";

console.log(text.match("w")); // [ 'w', index: 6, input: 'Hello world', groups: undefined ]
```
## .test() (Trả về True/False nếu chuỗi khớp hoặc không khớp với biểu thức chính quy)
**Ex**
```js
let a = /hello/.test('chào là hello world')
console.log(a) // true
```
## .exec()
## .replace()