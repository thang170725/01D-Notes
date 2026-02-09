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