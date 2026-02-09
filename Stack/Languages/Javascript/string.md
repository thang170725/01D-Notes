- [](#)
---
# .trim() & trimstart() & trimEnd()
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
RegExp (Biểu thức chính quy)
Cú pháp: /pattern/modifiers 
    • pattern là chuỗi Regular Expression 
    • modifiers là thông số cấu hình cho chuỗi pattern, và nó có các giá trị sau: 
        ◦ i : so khớp không quan tâm đến chữ hoa chữ thường.
        ◦ g: so khớp toàn bộ chuỗi cần tìm .
        ◦ m: so khớp luôn cả các dữ liệu xuống dòng (multiline).
/[A-Z]/g
khớp từ A-Z
/[1-9]/g
khớp từ 1-9
/\d/g
khớp với kết quả là số
/\D/g
khớp với kết quả không là số
/\w/g
khớp với kết quả là a-z, A-Z, 0-9, _
/\W/
Tìm các ký tự không phải là chữ cái
/\s/g
khớp với kết quả là dấu cách, tab, newline
/^web/
khớp với chuỗi bắt đầu bằng web
/web$/
khớp với chuỗi kết thúc bằng web
(x|y)
Tìm ký tự x hoặc y
n+
Tìm 1 hoặc nhiều chữ n liên tiếp nhau
n*
Tìm 0 hoặc nhiều chữ n liên tiếp nhau
n?
Tìm 0 hoặc 1 chữ n
.
Tìm ký tự bất kỳ
{X}
Kiểm tra ký tự xuất hiện đúng X lần
{X, Y}
Xuất hiện X → Y lần
{X,}
Xuất hiện ít nhất X lần
/s
Cho phép cả khoảng trắng
.match()
Trả về một mảng với các kết quả khớp. Trả về null nếu không tìm thấy kết quả khớp.
Cú pháp: text.match(paterrn);
function main(){
   let text = "Hello world";
   console.log(text.match("w"));

}
main()
[ 'w', index: 6, input: 'Hello world', groups: undefined ]
let text = "123456789";
let result = text.match(/[0-9]/g);

document.getElementById("demo").innerHTML = result;
1,2,3,4,5,6,7,8,9
.test()
Trả về True/False nếu chuỗi khớp hoặc không khớp với biểu thức chính quy.
Cú pháp: pattern.test(text)
let a = /hello/.test('chào là hello world')
console.log(a)
true

.exec()
.replace()