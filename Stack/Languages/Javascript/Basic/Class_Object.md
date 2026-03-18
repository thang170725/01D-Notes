- [class \& Objects](#class--objects)
  - [Object.key()](#objectkey)
  - [Entries()](#entries)
  - [.key \& \['key'\]](#key--key)
  - [delete](#delete)
- [Prototype](#prototype)
---
# class & Objects
```bash
- Trên thực tế thường khai báo các đối tượng bằng từ khóa const.
```
**Syn**
```bash
- const | let | var <name> = new Object(key: value1, key: value2, …);
- const | let | var <name> = new Object();
- const | let | var <name> = { key: value1, key: value2, …};
- const | let | var <name> = {};
```
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
## Object.key()
```bash
Trả về một mảng chứa tất cả key (thuộc tính) của một object.
```
**Ex**
```js
const user = {
  name: "Thang",
  age: 25,
  city: "Bac Giang"
}

console.log(Object.keys(user)) // ["name", "age", "city"]
```
## Entries()
```bash
Chuyển một class thành mảng các cặp [key, value].
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
```
## .key & ['key']
```bash
Dùng để thêm key-value hoặc lấy ra value.
```
**Syn**
```bash
- <name>.key = value;
- <name>[‘key’] = value;
- <name>[“key”] = value;
```
## delete
```bash
Để xóa một key ra khỏi Object.

```
**Syn**
```bash
- delete <name>.key;
- delete <name>[‘key’];
```
# Prototype
```bash
- Trong Prototype-based programming, object có thể kế thừa trực tiếp từ object khác.
- JavaScript dùng Prototype chain để tìm thuộc tính.
```
**Ex1: Demo cơ bản prototype**
```js
function Person(name) {
  this.name = name
}

Person.prototype.sayHello = function () {
  console.log("Hello " + this.name)
}

const p1 = new Person("Thang")
p1.sayHello() // Hello Thang

// Điều xảy ra
// p1
//  ↓
// Person.prototype
//  ↓
// Object.prototype
//  ↓
// null
```
**Ex2: Demo class (thực chất vẫn là prototype)**
```js
class Person {
  constructor(name) {
    this.name = name
  }

  sayHello() {
    console.log("Hello " + this.name)
  }
}

const p = new Person("Thang")
p.sayHello() // Thực chất JS chuyển thành: Person.prototype.sayHello
```