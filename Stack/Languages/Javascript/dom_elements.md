- [document.getElementsByTagName()](#documentgetelementsbytagname)
- [document.getElementById()](#documentgetelementbyid)
- [document.getElementsByClassName()](#documentgetelementsbyclassname)
- [document.querySelector()](#documentqueryselector)
- [document.querySelecterAll()](#documentqueryselecterall)

---

# document.getElementsByTagName()
truy xuất đến thẻ HTML thông qua chính tên thẻ đó. Làm việc như một mảng.

# document.getElementById()
Truy xuất đến thẻ HTML thông qua ID. 

# document.getElementsByClassName()
truy xuất đến thẻ HTML thông qua class. Làm việc như một mảng.

# document.querySelector()
Truy xuất đến thẻ HTML thông qua thẻ HTML, nó có độ chính xác cao vì có thẻ từ thẻ cha để tim thẻ con giống với CSS. Chỉ select ra 1 phần tử

# document.querySelecterAll()
Chức năng giống document.querySelecter nhưng nó có thể select ra nhiều phần tử. nó được sử dụng như một mảng.
## innerHTML & textContent
- Thay thế toàn bộ nội dung của thẻ HTML hoặc chỉ text.
- Sự khác biệt textContent với innerHTML:
  + textContent chỉ hiểu chữ thường (text), không chạy HTML.
  + innerHTML hiểu cả HTML (có thể chèn thẻ).
    + d.textContent = "<b>Hello</b>"; // Hiển thị: <b>Hello</b> (y nguyên chữ)
    + d.innerHTML = "<b>Hello</b>";   // Hiển thị: Hello (in đậm)
**Syn**  
```js
<variable>.innerHTML = value;
```
## document.createElement() & appendChild()
Phương thức tạo phần tử (thẻ HTML) và render vào giao diện người dùng.
**Ex**
```js
let d = document.createElement('div');
document.body.appendChild(d);
```