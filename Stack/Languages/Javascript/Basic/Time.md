- [Create (Nhóm khởi tạo)](#create-nhóm-khởi-tạo)
  - [Date](#date)
- [Process (nhóm xử lý thời gian)](#process-nhóm-xử-lý-thời-gian)
  - [setTimeout() \& setInterval()](#settimeout--setinterval)
  - [clearTimeout() \& clearInterval()](#cleartimeout--clearinterval)
  - [toUTCString()](#toutcstring)
  - [.toLocaleDateString()](#tolocaledatestring)
  - [Date.parse()](#dateparse)
  - [Date.now()](#datenow)
  - [Get](#get)
  - [.getFullYear() \& .getHours()  \& .getMinutes() \& .getSeconds() \& .getMiliseconds() \& .getTime()](#getfullyear--gethours---getminutes--getseconds--getmiliseconds--gettime)
  - [.getDate()](#getdate)
    - [getDay()](#getday)
  - [.getUTCMonth() \& .getUTCDate() \& .getUTCFullYear() \& .getUTCMonth() \& .getUTCDay() \& .getUTCHours() \& .getUTCMinutes() \& .getUTCSeconds() \& .getUTCMiliseconds()](#getutcmonth--getutcdate--getutcfullyear--getutcmonth--getutcday--getutchours--getutcminutes--getutcseconds--getutcmiliseconds)
  - [getTimezoneOffset()](#gettimezoneoffset)
  - [.setFullYear() \& setMonth() \& setDate() \& setHours() \& setMinutes() \& setSeconds()](#setfullyear--setmonth--setdate--sethours--setminutes--setseconds)
---
# Create (Nhóm khởi tạo)
## Date
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
# Process (nhóm xử lý thời gian)
## setTimeout() & setInterval()
```bash
- setTimeout  : Dùng để thực hiện một hàm sau một khoảng thời gian xác định. Chỉ chạy 1 lần.
- setInterval : Dùng để lặp lại một hàm sau mỗi khoảng thời gian xác định. Chạy liên tục cho đến khi bị dừng.
```
**Syn**
```bash
setTimeout(function, time);
setInterval(function, time);

- function : Hàm cần thực hiện.
- time     : Thời gian chờ (mili giây - ms).
```
**Ex**
```js
function hello(){
    console.log("Hello");
}

setTimeout(hello, 2000);   // chạy 1 lần sau 2s
setInterval(hello, 2000);  // lặp lại mỗi 2s
```
## clearTimeout() & clearInterval()
```bash
- clearTimeout  : Hủy một setTimeout trước khi nó chạy.
- clearInterval : Dừng một setInterval đang lặp.
```
**Syn**
```bash
clearTimeout(id);
clearInterval(id);

- id : giá trị được trả về khi gọi setTimeout hoặc setInterval.
```
**Ex**
```html
<button>Dừng</button>
<p></p>
```
```js
let i = 0;
let text = document.getElementsByTagName("p")[0];

function time(){
    text.innerHTML = i++;
}

let run = setInterval(time, 1000);

document.getElementsByTagName("button")[0].onclick = function(){
    clearInterval(run);
}
```
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
## .toLocaleDateString()
```bash
dùng để chuyển đổi một đối tượng Date thành một chuỗi biểu diễn ngày tháng theo quy ước địa phương.
```
**Syn**
```bash
const date = new Date()
date.toLocaleDateString(locales, options)

- Input:
  + locales: 
    - "vi-VN"  // Việt Nam
    - "en-US"  // Mỹ
    - "ja-JP"  // Nhật
  + options: Obj để custom format (viết trong {})
    - weekday: "long" | "short",
    - year: "numeric" | "2-digit",
    - month: "numeric" | "2-digit" | "long" | "short",
    - day: "numeric" | "2-digit"
```
**Ex**
```js
const today = new Date();

const formatted = today.toLocaleDateString("vi-VN", {
    weekday: "long",
    day: "2-digit",
    month: "2-digit",
    year: "numeric",
});

console.log(formatted); // Thứ Tư, 01/04/2026
```
## Date.parse()
```bash
Trả về giá trị mili giây khoảng cách từ ngày 1 tháng 1 năm 1970.
```
## Date.now()
```js
console.log(Date.now()); // 1711790000000
```
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