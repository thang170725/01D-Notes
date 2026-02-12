- [document.getElementsByTagName()](#documentgetelementsbytagname)
- [document.getElementById()](#documentgetelementbyid)
- [document.getElementsByClassName()](#documentgetelementsbyclassname)
- [document.querySelector()](#documentqueryselector)
- [document.querySelecterAll()](#documentqueryselecterall)
  - [innerHTML \& textContent](#innerhtml--textcontent)
  - [document.createElement() \& appendChild()](#documentcreateelement--appendchild)
- [document.addEventListener() \& removeEventListener()](#documentaddeventlistener--removeeventlistener)
- [removeEvent](#removeevent)
- [click|onclick \& dbclick|ondbclick](#clickonclick--dbclickondbclick)
  - [Tạo một chức năng tra cứu màu sắc](#tạo-một-chức-năng-tra-cứu-màu-sắc)
- [mouseover|onmouseover \& mousemove|onmousemove \& mouseout|onmouseout](#mouseoveronmouseover--mousemoveonmousemove--mouseoutonmouseout)
- [change | onchange](#change--onchange)
- [oninput|input](#oninputinput)
- [keydown | onkeydown \& keypress | onkeypress](#keydown--onkeydown--keypress--onkeypress)
- [load | onload \& loadstart | onloadstart \& loadend | onloadend](#load--onload--loadstart--onloadstart--loadend--onloadend)
- [Progress | onprogress](#progress--onprogress)
- [target](#target)
  - [.value](#value)
- [classList.toggle()](#classlisttoggle)

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
- [document.getElementsByTagName()](#documentgetelementsbytagname)
- [document.getElementById()](#documentgetelementbyid)
- [document.getElementsByClassName()](#documentgetelementsbyclassname)
- [document.querySelector()](#documentqueryselector)
- [document.querySelecterAll()](#documentqueryselecterall)
  - [innerHTML \& textContent](#innerhtml--textcontent)
  - [document.createElement() \& appendChild()](#documentcreateelement--appendchild)
- [document.addEventListener() \& removeEventListener()](#documentaddeventlistener--removeeventlistener)
- [removeEvent](#removeevent)
- [click|onclick \& dbclick|ondbclick](#clickonclick--dbclickondbclick)
  - [Tạo một chức năng tra cứu màu sắc](#tạo-một-chức-năng-tra-cứu-màu-sắc)
- [mouseover|onmouseover \& mousemove|onmousemove \& mouseout|onmouseout](#mouseoveronmouseover--mousemoveonmousemove--mouseoutonmouseout)
- [change | onchange](#change--onchange)
- [oninput|input](#oninputinput)
- [keydown | onkeydown \& keypress | onkeypress](#keydown--onkeydown--keypress--onkeypress)
- [load | onload \& loadstart | onloadstart \& loadend | onloadend](#load--onload--loadstart--onloadstart--loadend--onloadend)
- [Progress | onprogress](#progress--onprogress)
- [target](#target)
  - [.value](#value)
- [classList.toggle()](#classlisttoggle)
---
# document.addEventListener() & removeEventListener()
```bash
- addEventListener    : Gắn một trình xử lý sự kiện.
- removeEventListener : gỡ bỏ event đã add trước đó.
```
**Syn**
```bash
document.addEventListener(event, function, (capture))

- Event: sử dụng ‘click’ thay vì ‘onclick’, không sử dụng tiền tố ‘on’. Sử dụng tất cả các event trong HTML DOM Event Object Reference.
- Function: chức năng sẽ chạy khi sự kiện xảy ra. Khi sự kiện xảy ra một đối tượng sự kiện sẽ được truyền cho hàm làm tham số đầu tiên. Loại đối tượng sự kiện phụ thuộc vào sự kiện được chỉ định. VD: ‘click’ thuộc về đối tượng MouseEvent. Lưu ý là function trong addEventListener() không cần ngoặc.
- Capture: mặc định bằng false. True-trình xử lí được thực thi trong giai đoạn chụp. trình sử lí được thực thi trong giai đoạn sủi bọt.
```
**Ex1**
```html
<button>BUTTON</button>
```
```js
var a = document.getElementsByTagName("button");
a[0].addEventListener('click', function (){
    alert("Hello World!!!");
});
```
**Ex2**
```bash
1. Click Bấm tôi → log
2. Click Gỡ event
3. Click lại Bấm tôi → ❌ không log nữa
```
```html
<button id="btn">Bấm tôi</button>
<button id="remove">Gỡ event</button>
```
```js
<script>
  const btn = document.getElementById("btn");
  const removeBtn = document.getElementById("remove");

  function handleClick() {
    console.log("Đã click!");
  }

  // Gắn event
  btn.addEventListener("click", handleClick);

  // Gỡ event
  removeBtn.addEventListener("click", () => {
    btn.removeEventListener("click", handleClick);
    console.log("Đã gỡ event");
  });
</script>
```
# removeEvent
# click|onclick & dbclick|ondbclick
Khi người dùng click hoặc dbclick thì trả về một result nào đó.

## Tạo một chức năng tra cứu màu sắc
```html
<div id="result"></div>
<input type="text" id="content" />
<button onclick="Color()" id="button">Check</button>
```
```css
div{
    width: 100px;
    height: 100px;
}
```
```js
var button = document.getElementById("button");
var content = document.getElementById("content");
var result = document.getElementById("result");
function Color() {
    result.style.backgroundColor = content.value;
}
```

# mouseover|onmouseover & mousemove|onmousemove & mouseout|onmouseout 
**Ex**
```html
<button>Button</button>
```
```js
var button = document.getElementsByTagName('button');
button[0].onmouseover = function (){
    alert("Welcome to Javascipt");
}
```
# change | onchange
```bash
Gắn một hành động khi giá trị của một phần tử bị thay đổi.
```
**Ex**
```html
<div style="width: 50px; height: 50px;"></div>
  <select  onchange="ChangeColor(this.value)">
    <option value="red">Red</option>
    <option value="blue">Blue</option>
    <option value="green">Green</option>
  </select>
```
```js
function ChangeColor(Color){
    let box = document.getElementsByTagName('div');
    box[0].style.background = Color
}
```

# oninput|input
Xảy ra khi một phần tử được nhập vào. Xảy ra khi giá trị của thẻ input, textarea hoặc select bị thay đổi. oninput gần giống với onchange nhưng thuộc tính onchange, change. Điểm khác là thuộc tính này không cần thả chuột còn onchange, change thì cần thả chuột ra mới thực thi lệnh.
Thay đổi kích cỡ chữ đơn vị px bằng thanh kéo trong HTML, CSS


<input type="range" min="0" max="100" id="scroll">
  <p></p>
  <p id="change">Welcome to VietNam</p>

var a = document.getElementById('scroll');
var b = document.getElementsByTagName('p');
var change = document.getElementById('change');
a.oninput = function (){
      b[0].innerHTML = a.value + "px";
      var c = a.value + "px";
      change.style.fontSize = c;
}

# keydown | onkeydown & keypress | onkeypress
```bash
- Để gắn trình xử lý khi nhấn một nút trên bàn phím.
```
**Ex1**
```js
function main(){
    let inp = document.getElementsByTagName("input");
    let text = document.getElementsByTagName("p")
    inp[0].onkeydown = function (event){
        if(event.key === "Enter") text[0].innerHTML = inp[0].value;
    }
}
main();
```
**Ex2**
```js
function main(){
    let inp = document.getElementsByTagName("input")[0];
    inp.onkeydown = function(){
        alert("bạn đã nhập gì đó vào ô input");
    }
}
main();
```
animationstart || onanimationstart
Xảy ra khi hoạt ảnh CSS bắt đầu.
<div></div>

div{
  width: 100px;
  height: 100px;
  position: relative;
  background-color: #ff0;
}
@keyframes move{
  0%{
    top: 0px;
  }
  100%{
    top: 100px;
  }
}
function main(){
    let C = document.getElementsByTagName("div")[0];
    C.onclick = function(){
        C.style.animation = "move 3s 2"
    }
    C.onanimationstart = function(){
        C.style.backgroundColor = "#f00";
        C.innerHTML = "Start";
    }
}
main()

Tạo ra một hình chữ nhật ban đầu là màu vàng, khi bấm vào hình vuông đó sẽ xuất hiện chữ start, hình đó chuyển thành màu đỏ đầu thời thực hiện phần keyframes.
animationiteration || onanimationiteration
Xảy ra khi hoạt ảnh CSS được lặp lại.
<div></div>

div{
  width: 100px;
  height: 100px;
  position: relative;
  background-color: #ff0;
}
@keyframes move{
  0%{
    top: 0px;
  }
  100%{
    top: 100px;
  }
}
function main(){
    let C = document.getElementsByTagName("div")[0];
    C.onclick = function(){
        C.style.animation = "move 3s 2"
    }
    C.onanimationiteration = function(){
        C.style.backgroundColor = "#f00";
        C.innerHTML = "Start";
    }
}
main()

animationend || onanimationend
Xảy ra khi hoạt ảnh CSS được kết thúc.
<div></div>

div{
  width: 100px;
  height: 100px;
  position: relative;
  background-color: #ff0;
}
@keyframes move{
  0%{
    top: 0px;
  }
  100%{
    top: 100px;
  }
}
function main(){
    let C = document.getElementsByTagName("div")[0];
    C.onclick = function(){
        C.style.animation = "move 3s 2"
    }
    C.onanimationend = function(){
        C.style.backgroundColor = "#f00";
        C.innerHTML = "Start";
    }
}
main()

canplay || oncanplay
Xảy ra khi trình duyệt có thể bắt đầu phát phương tiện, xyar ra khi trình duyệt đã đệm đủ để bắt đầu.
Xem ví dụ ở đây: https://www.w3schools.com/jsref/tryit.asp?filename=tryjsref_oncanplay
focus || onfocus
Thường để focus vào thẻ input. 

<input type="text">
<button>Focus</button>

function main(){
   let a = document.getElementsByTagName("button")[0];
   let b = document.getElementsByTagName("input")[0];
   a.onclick = function(){
      b.focus();
   }

}
main()
blur 
Xóa tiêu điểm khỏi một phần tử.

<input type="text">
    <button>Blur</button>

function main(){
   let a = document.getElementsByTagName("button")[0];
   let b = document.getElementsByTagName("input")[0];
   a.onclick = function(){
      b.blur();
   }

}
main()
resize || onresize
Xảy ra khi của sổ trình duyệt được thay đổi kích thước. resize chỉ có thể sử dụng với đối tượng là window.

<div></div>

div {
            width: 100px;
            height: 50px;
            border: 2px solid;
        }

function main(){
    let t = document.getElementsByTagName("div")[0];
    window.onresize = function(){
        let w = window.innerWidth;
        let h = window.innerHeight;
        t.innerText = w + "x" + h;
    }
}
main();


onabort()
là một sự kiện xảy ra khi quá trình tải một tài nguyên nào đó bị hủy bỏ. Tài nguyên đó có thể là hình ảnh, video, audio, hoặc bất ký tài nguyên nào khác được tải từ máy chủ.
Cho phép bạn xử lý tình huống khi người dùng hoặc trình duyệt chủ động hủy quá trình tải.
Bạn có thể sử dụng để thông báo cho người dùng rằng quá trình tải đã bị hủy, hoặc để hiện thị một thông báo lỗi.
Trong một số trường hợp, bạn có thể cần giải phóng tài nguyên khi quá trình tải bị hủy, ví dụ như đóng kết nối mạng.
# load | onload & loadstart | onloadstart & loadend | onloadend
```bash
- onload    : Lấy dữ liệu, khi đọc thành công.
- onloadend : Tắt loading, luôn chạy cuối.
Afterprint
Beforeprint
Beforeunload
Canplaythrough
Contentmenu
Copy
Cut
Drag
Dragend
Dragstart
Drop
Durationchange
Ended
# Error
Focusin
Focusout
Fullscreenchange
Fullscreenerror
Hashchange
Invalid
Keyup
Load
Loadeddata
Loadedmetadata

Message
# mousedown & mouseup
```bash
- mousedown : Xảy ra khi bạn ấn chuột
- mouseup   : xay ra khi nhả chuột
```
**Ex**
```js
<button id="btn">Bấm tôi</button>

<script>
  const btn = document.getElementById("btn");

  btn.addEventListener("mousedown", () => {
    console.log("Bạn vừa ẤN chuột");
  });
</script>
```
Mouseenter
Mouseleave
Mousewheel
Offline
Online
Open
Packagehide
Packageshow
Paste
Pause
Playying
Popstate
# Progress | onprogress
```bash
- onprogress  : Hiển thị phần trăm tiến trình
Ratechange
Reset
Scroll
Search
Seeked
Seeking
Select
Show
Stalled
Submit
Suspend
Timeupdate
Toggle
Touchcancel
Touchend
Touchmove
Touchstart
Volumechange
Waiting
wheel
Xử lý input & select
Value
Là đại diện cho giá trị của ô input hoặc thẻ select .
Bài tập
Gắn giá trị cho ô input bằng value trong js
<input type="text" id="domain" name="domain" value="" />
<button onclick="setDomain()">Gán giá trị</button>
function setDomain() {
        let domain = "welcome to Javascript";
        document.getElementById("domain").value = domain;
      }

Nhập giá trị từ ô input hiển thị giá trị đó và kiểu dữ liệu lên màn hình
<form>
     <input type="text">
     <button onclick="Alert()">Gửi</button>
</form>
function Alert(){
     input = document.getElementsByTagName('input')[0].value;
     alert(input + typeof input)
}
2string
Hiện thông báo là giá trị của thẻ select
<select onchange="Display(this.value)">
     <option value="Hà nội">Hà Nội</option>
     <option value="Hải Phòng">Hải Phòng</option>
     <option value="Quảng Ninh">Quảng Ninh</option>
</select>
function Display(value){
     alert(value);

# onSubmit
```bash
- submit là event của <form>. Khi bấm nút submit hoặc Enter → form emit event submit
- Mặc định: trình duyệt reload trang
- JS dùng event.preventDefault() để chặn reload và tự xử lý logic
```
**Ex1**
```js
const form = document.querySelector('#myForm')

form.addEventListener('submit', async (event) => {
  event.preventDefault() // ❗ bắt buộc

  console.log('Form đã submit')

  // xử lý logic ở đây
})

// Đây là cách chuẩn – hiện đại – production
```
**Ex3: Lấy dữ liệu từ form khi onSubmit**
```bash
const form = document.querySelector('#myForm')

form.addEventListener('submit', async (event) => {
  event.preventDefault()

  const formData = new FormData(form)

  const data = Object.fromEntries(formData.entries())

  console.log(data)
})

# Nếu form có:
# name="email"
# name="password"

# data sẽ là:
# {
#   email: 'abc@gmail.com',
#   password: '123456'
# }
```
**Ex4: onSubmit + fetch (thực tế nhất)**
```js
const form = document.querySelector('#myForm')

form.addEventListener('submit', async (e) => {
  e.preventDefault()

  const data = Object.fromEntries(
    new FormData(form)
  )

  try {
    const res = await fetch('/api/login', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json'
      },
      body: JSON.stringify(data)
    })

    if (!res.ok) throw new Error(res.status)

    const result = await res.json()
    console.log('Success:', result)
  } catch (err) {
    console.error(err)
  }
})
```
# target
## .value
```bash
- Lấy giá trị hiện tại của input / textarea / select khi có sự kiện xảy ra.
```
**Ex: gõ tới đâu chữ hiện tới đó**
```html
<input id="name" type="text" />
<p id="output"></p>
```
```js
const input = document.getElementById("name");
const output = document.getElementById("output");

input.addEventListener("input", (event) => {
  output.innerText = event.target.value;
});
```
# classList.toggle()
```bash
- Là một phương thức dùng để thêm hoặc xóa một class khỏi một phần tử HTML.
- Nếu phần tử đó đã có class đó, toggle sẽ xóa nó, nếu chưa có, toogle sẽ thêm vào.
```
**Syn**
```bash
element.classList.toggle(className, [force])
- className: tên class CSS muốn thêm hoặc xóa.
- Force (tùy chọn): Nếu là true luôn thêm,  false là luôn xóa.
```
**Ex**
```html
<button id="myBtn">Toggle màu đỏ</button>
<div id="myBox">Nội dung</div>
```
```js
.red{
    color: #f00;
    font-weight: bold;
}
const btn = document.getElementById('myBtn');
const box = document.getElementById('myBox');

btn.addEventListener('click', function (){
    box.classList.toggle('red');
});
```
Bài tập
Tạo một ô input và thêm giá trị của input vào danh sách thẻ ul
<input type="text">
<button onclick="Add()">Add</button>
<ul></ul>

function Add(){
let v = document.getElementsByTagName('input')[0];
let l = document.createElement('li');
let u = document.getElementsByTagName('ul')[0];
l.textContent = v.value;
u.appendChild(l);
}