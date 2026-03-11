- [class \& Objects](#class--objects)
  - [Object.key()](#objectkey)
  - [Entries()](#entries)
  - [. \& \[\]](#--)
  - [delete](#delete)
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
## . & []
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
Cú pháp:
    • delete <name>.key;
    • delete <name>[‘key’];
Lưu ý: khi key là một hàm thì phải thêm () vào sau key.
Tạo môt đối tượng rỗng, thêm các key  (name, age,  address) vào đối tượng đó và gắn giá trị.  Xuất name của đối tượng sau đó xóa bỏ key name và xuất cả Object lên màn hình.
 var Obj = {};
 Obj.name = "Jason";
 Obj['age'] = 23;
 Obj.address = "36 London England";
 document.write(Obj.name + '<br/>');
 delete Obj.name;
 document.write(Obj.name + Obj.age + Obj.address);
 // Obj.name + " " +  Obj.age + " " + Obj.address
