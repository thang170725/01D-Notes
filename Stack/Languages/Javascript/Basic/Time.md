- [setTimeout() \& setInterval()](#settimeout--setinterval)
- [clearInterval()](#clearinterval)
  - [đồng hồ bấm giờ](#đồng-hồ-bấm-giờ)
- [Date](#date)
  - [toUTCString()](#toutcstring)
  - [toLocaleDateString()](#tolocaledatestring)
  - [Get](#get)
  - [.getFullYear() \& .getHours()  \& .getMinutes() \& .getSeconds() \& .getMiliseconds() \& .getTime()](#getfullyear--gethours---getminutes--getseconds--getmiliseconds--gettime)
  - [.getDate()](#getdate)
    - [getDay()](#getday)
  - [.getUTCMonth() \& .getUTCDate() \& .getUTCFullYear() \& .getUTCMonth() \& .getUTCDay() \& .getUTCHours() \& .getUTCMinutes() \& .getUTCSeconds() \& .getUTCMiliseconds()](#getutcmonth--getutcdate--getutcfullyear--getutcmonth--getutcday--getutchours--getutcminutes--getutcseconds--getutcmiliseconds)
  - [getTimezoneOffset()](#gettimezoneoffset)
  - [.setFullYear() \& setMonth() \& setDate() \& setHours() \& setMinutes() \& setSeconds()](#setfullyear--setmonth--setdate--sethours--setminutes--setseconds)
---
# setTimeout() & setInterval()
```bash
- setTimeout    : chỉ được sử dụng với function. Thiết lập một khoảng thời gian nào đó sẽ thực hiện một nhiệm vụ nào đó và nó chỉ thực hiện đúng một lần
- setInterval   : số lần thực hiện lã mãi mãi
```
**Syn**
```bash
setTimeout(function, time);

- function: Là nội dung cần thực hiện, đây là một hàm.
- time: Là khoảng thời gian bao nhiêu (tính bằng mili giây) thì function đó sẽ thực hiện.
```
# clearInterval() 
```bash
Xóa đi một nhiệm vụ nào đó của setTimeout.
```
**Ex**
```html
<button>Dừng</button>
<p></p>
```
```js
let i = 0;
let text = document.getElementsByTagName("p");
function time() {
    text[0].innerHTML = i++;
}
function main() {
    let res = setInterval(time, 1000);
    let stop = document.getElementsByTagName("button");
    stop[0].onclick = function (){
        clearInterval(res)
    }
}
main();
```
## đồng hồ bấm giờ
```js
let second = document.getElementById("seconds");
let minute = document.getElementById("minutes");
let count = 56;
let mis = 0;
function Minute(){
    if(count == "60"){
        count = 0;
        mis += 1;
        minute.innerHTML = mis;
    }
}
function TimeMath(){
    count++;
    if(count < 10){
        count = "0" + count;
    }
    second.innerHTML = count;
    Minute();
}
function main(){
    let res = setInterval(TimeMath, 1000)
    let but = document.getElementById("stop");
    but.onclick = function (){
        clearInterval(res);
    }
}
main()
```
# Date
```bash
Nó sẽ lấy ra đầy đủ ngày, tháng, năm, giờ, … có thể truyền tham số đầu vào hoặc không, tham số trong dấu nháy
```
**Syn**
```bash
var | let | const <variable> = new Date();

- New date()
- New date(date String)
- New date(year, month)
- New Date(year, month, day)
- New Date(year, month, day, hours)
- New Date(year, month, day, hours, minutes)
- New Date(year, month, day, hours, minutes, seconds)
- New Date(year, month, day, hours, minutes, seconds, ms)
- New Date(miniseconds)
```
**Ex1**
```js
const d = new Date();
console.log(d); // Wed Feb 05 2025 10:09:00 GMT+0700 (Indochina Time)
```
toDateString()
Chuyển đổi sang định dạng chuỗi dễ đọc hơn.
let date = new Date()
var result = date.toDateString()
console.log(result, typeof result)
[ 'Sat Feb 22 2025', 'string' ]
## toUTCString()
```bash
Để chuyển đổi đối tượng Date thành một chuỗi biểu diễn thời gian theo giờ UTC.
```
**Ex**
```js
function main(){
    let date = new Date();
    console.log(date.toUTCString())
    console.log(typeof date.toUTCString())
}
main();

// 'Mon, 24 Feb 2025 13:55:44 GMT'
// 'string'
```
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
## toLocaleDateString()
```bash
dùng để chuyển đổi một đối tượng Date thành một chuỗi biểu diễn ngày tháng theo quy ước địa phương.
```
**Ex**
```js
function main(){
    let date = new Date();
    console.log(date.toLocaleDateString("vi-VN"))
    console.log(typeof date.toISOString())
}
main();

// '24/2/2025'
// String
```
Date.parse()
Trả về giá trị mili giây khoảng cách từ ngày 1 tháng 1 năm 1970.
## Get
```bash
Trả về  giá trị thời gian
```
## .getFullYear() & .getHours()  & .getMinutes() & .getSeconds() & .getMiliseconds() & .getTime()
```bash
- getFullYear   : Để lấy ra năm.
- getMonth      : Để lấy ra tháng. Nhưng phải công thêm 1 thì mới ra tháng hiện tại.
- getDate       : Để 
- getHours      : Để lấy ra giờ trong ngày
- getTime       : Để lấy ra mili giây. Trả về mili giây thời gian tính từ nhày 1 tháng 1 năm 1970.
```
**Ex1: getFullYear**
```js
const d = new Date();
console.log(d.getFullYear()); // 2025
```
## .getDate()
```bash
Lấy ra ngày trong tháng 
```
**Ex**
```js
let date = new Date();
console.log(date.getDate(), typeof date.getDate()) // [ 26, 'number' ]
```
**Ex4: getHours**
```js
let date = new Date();
console.log(date.getHours(), typeof date.getHours()) // [ 16, 'number' ]
```
**Ex5: getMinutes**
```js
let date = new Date();
console.log(date.getMinutes(), typeof date.getMinutes()) // [ 54, 'number' ]
```
**Ex6: getSeconds**
```js
let date = new Date();
console.log(date.getSeconds(), typeof date.getSeconds()) // [ 20, 'number' ]
```
### getDay()
```bash
- Để lấy ra ngày trong tuần.
```
**Ex**
```js
let date = new Date();
console.log(date.getDay(), typeof date.getDay()) // [ 3, 'number' ]

// 0	: Chủ nhật
// 1	: Thứ hai
// 2	: Thứ ba
// 3	: Thứ tư
// 4	: Thứ năm
// 5	: Thứ sáu
// 6	: Thứ bảy
```
## .getUTCMonth() & .getUTCDate() & .getUTCFullYear() & .getUTCMonth() & .getUTCDay() & .getUTCHours() & .getUTCMinutes() & .getUTCSeconds() & .getUTCMiliseconds()
**Ex2: getUTCMonth**
```js
let date = new Date()
console.log(date.getUTCMonth()) // 1
```
## getTimezoneOffset()
```bash
trả về sự khác biệt (tính bằng phút) giữa giờ địa phương và giờ UTC.
```
**Ex**
```js
let date = new Date();
console.log(date.getTimezoneOffset()) // -420 (phút) Tương ứng với 7 tiếng UTC+7
```
## .setFullYear() & setMonth() & setDate() & setHours() & setMinutes() & setSeconds()
```bash
- setFullYear   : Để cài đặt một năm nào đó.
- setDate       : Thay đổi ngày trong tháng
```
**Ex**
```js
let date = new Date();
.setFullYear(2023)
console.log(date.toDateString()) // 'Sun Feb 26 2023'
```
**Ex: Cộng thêm 5 ngày**
```js
const date = new Date("2026-03-02")
date.setDate(date.getDate() + 5)

console.log(date) // Sat Mar 07 2026 07:00:00 GMT+0700 (Indochina Time)
```