# Tạo trường đăng nhập (Username) bằng html + css
**Ex1**
```html
 <div class="input-box">
  <input type="text" required>
  <label for="">Username</label>
 </div>
```
```css
*{
    padding: 0;
    margin: 0;
    box-sizing: border-box;
    font-family: sans-serif;
}
body{
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 100vh;
    background-color: #1d2b3e;
}
.input-box{
    position: relative;
    width: 280px;
    margin: 20px 0;
}
.input-box label{
    position: absolute;
    top: 50%;
    left: 5px;
    transform: translateY(-50%);
    font-size: 16px;
    color: rgba(255,255,255, 0.3);
    padding: 0 5px;
    pointer-events: none;
}
.input-box input{
    width: 100%;
    padding: 10px;
    background: transparent;
    border: 1.8px solid rgba(255,255,255,0.3);
    outline: none;
    border-radius: 5px;
    color: #fff;
    transition: 0.5s;
}
.input-box input:focus~label,
.input-box input:valid~label{
    top: 0;
    left: 10px;
    font-size: 11px;
    background: #1d2b3e;
    transition: 0.5s;
}
```
**Ex2**
```html
 <div id="UserName">
  <input type="text">
  <label for="">Username</label>
  <i class="fa-solid fa-user"></i>
 </div>
```
```css
*{
    padding: 0;
    margin: 0;
    box-sizing: border-box;
    font-family: sans-serif;
}
body{
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 100vh;
}
#UserName{
    position: relative;
    border: 2px solid #000;
    border-radius: 5px;
}
#UserName input{
    padding: 10px 10px;
    border: none;
    width: 260px;
    outline: none;
}
#UserName label{
    position: absolute;
    top: 50%;
    left: 5px;
    transform: translateY(-50%);
    pointer-events: none;
}
#UserName input:focus~label{
    top: 0px;
    left: 10px;
    font-size: 15px;
    border: none;
    background: #fff;
    padding: 0px 8px;
    transition: .5s;
}
.fa-user{
    margin: 0 7px;
}
```
# Tạo icon youtube
```html
<body>
    <div class="wrapper">
        <div class="hexagon"></div>
        <div class="hexInner1"></div>
        <div class="hexInner2"></div>
        <div class="triangle"></div>
    </div>
</body>
```
```css
*{
    padding: 0;
    margin: 0;
}
body{
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 100vh;
}
.wrapper{
    position: relative;
    width: 400px;
    height: 400px;
    display: flex;
    justify-content: center;
    align-items: center;
}
. hexagon{
    position: absolute;
    width: 10em;
    height: 17.32em;
    background-color: rgb(255, 0, 0);
    border-radius: 1em / 0.5em;
    transform: rotate(90deg);
}


.hexagon::before, .hexagon::after{
    content: "";
    position: absolute;
    width: inherit;
    height: inherit;
    background-color: inherit;
    border-radius: inherit;
}
.hexagon::before{
    transform: rotate(60deg);
}
.hexagon::after{
    transform: rotate(120deg);
}

.hexInner1{
    position: absolute;
    width: 10em;
    height: 17.32em;
    background-color: #fff;
    border-radius: 1em / 0.5em;
    transform: rotate(90deg) scale(0.65);
}
hexInner1::before, .hexInner1::after{
    content: "";
    position: absolute;
    width: inherit;
    height: inherit;
    background-color: inherit;
    border-radius: inherit;
}

.hexInner1::before{
    transform: rotate(60deg);
}
.hexInner1::after{
    transform: rotate(120deg);
}
.hexInner2{
    position: absolute;
    width: 10em;
    height: 17.32em;
    background-color: rgb(255, 0, 0);
    border-radius: 1em / 0.5em;
    transform: rotate(90deg) scale(0.59);
}
.hexInner2::before, .hexInner2::after{
    content: "";
    position: absolute;
    width: inherit;
    height: inherit;
    background-color: inherit;
    border-radius: inherit;
}
.hexInner2::before{
    transform: rotate(60deg);
}
.hexInner2::after{
    transform: rotate(120deg);
}
.triangle{
    position: absolute;
    border-top: 50px solid transparent;
    border-left: 80px solid #fff;
    border-bottom: 40px solid transparent;
    left: 172px;
}
```