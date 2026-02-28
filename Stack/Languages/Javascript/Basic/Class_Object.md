- [class](#class)
- [Objects](#objects)
  - [. \& \[\]](#--)
  - [delete](#delete)
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
- [class](#class)
- [Objects](#objects)
  - [. \& \[\]](#--)
  - [delete](#delete)
---
# Objects
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