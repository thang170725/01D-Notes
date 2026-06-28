- [Data type](#data-type)
- [Operator](#operator)
  - [5](#5)
  - [3](#3)
- [Gán](#gán)
- [Variable](#variable)
  - [var \& let \& const](#var--let--const)
  - [Spread Operator (...)](#spread-operator-)
  - [Optional Chaining Operator (Optional Chaining)](#optional-chaining-operator-optional-chaining)
---
# Data type
    • Number: Kiểu dữ liệu số.
    • String: Kiểu dữ liệu chuỗi, kí tự.
    • BigInt: Kiểu dữ liệu số lớn.
    • Boolean: Kiểu true/false.
    • Null: Không có giá trị nào thỏa mãn.
    • Undefined: Giá trị chưa được gán hoặc giá trị không xác định.
    • Symbol:
    • Object: Kiểu đối tượng.
## typeof
```bash
- Để kiểm tra kiểu dữ liệu của biến.  
```
**Syn**
```bash
typeof variable;
```
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
# Operator
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
# Variable
## var & let & const
**Syn**
```bash
var | let | const + <variable>;

- var: Chỉ định biến toàn cục (được khuyến cáo sử dụng).
- let: Chỉ định biến cục bộ.
- const: Chỉ định biến không thể thay đổi nữa.
```
## Spread Operator (...)
**Ex1: Dùng với list**
```js
const a = [1, 2, 3];
const b = [...a, 4]; // b = [1, 2, 3, 4];
```
**Ex2: Dùng với Object**
```js
const user = { name: "An", age: 20 };
const newUser = { ...user, age: 21 }; // { name: "An", age: 21 }
```
## Optional Chaining Operator (Optional Chaining)
```bash
- Nó cho phép bạn truy cập property an toàn khi object có thể là null hoặc undefined.
- Nếu object không tồn tại → trả về undefined thay vì lỗi.
```
**Ex: Không dùng optional chaining**
```js
const user = null

console.log(user.name)

// Lỗi:
// Cannot read properties of null
```
**Ex2: Dùng optional chaining**
```js
const user = null

console.log(user?.name)

// Kết quả:
// undefined
```
**Ex2**
```js
const todayExercises = weekPrograms?.week_menu?.[selectedDay]

// nếu weekPrograms tồn tại
//   lấy week_menu
//     nếu week_menu tồn tại
//       lấy selectedDay
```
**Ex3**
```js
const weekPrograms = {
  week_menu: {
    Mon: ["Push Up"],
    Tue: ["Squat"]
  }
}

const selectedDay = "Mon"

const todayExercises =
  weekPrograms?.week_menu?.[selectedDay] || []

console.log(todayExercises)

// ["Push Up"]
```