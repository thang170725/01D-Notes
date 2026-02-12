- [class](#class)
- [Spread Operator (...)](#spread-operator-)
---
# class
**Ex1: Thêm thuộc tính vào class**
```js
a = {}
a.author = 'thang' // a['author'] = 'thang'
console.log(a)
```
**Ex2: lấy thuộc tính message từ cha**
```js
const c = {
    'name': 'thang',
    'age': 21,
    'message': 'hello'
}
function send ({message}) {
    return message
}
console.log(send(c))
```
**Ex3: lấy name từ object và đổi tên biến**
```js
function send({name: message}) {
    return message
}
```
# Spread Operator (...)
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