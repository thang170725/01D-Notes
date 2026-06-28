- [Tạo trường đăng nhập (Username) bằng html + css](#tạo-trường-đăng-nhập-username-bằng-html--css)
- [Tạo icon youtube](#tạo-icon-youtube)
- [Tạo Menu 1 cấp](#tạo-menu-1-cấp)
- [Tạo Menu 2 cấp](#tạo-menu-2-cấp)
- [Kéo dãn thẻ div bằng scale](#kéo-dãn-thẻ-div-bằng-scale)
- [Hiệu ứng thanh trượt từ trái sang phải](#hiệu-ứng-thanh-trượt-từ-trái-sang-phải)
- [Hiệu ứng thanh trượt từ giữa sang 2 bên](#hiệu-ứng-thanh-trượt-từ-giữa-sang-2-bên)
- [Hiệu ứng loading](#hiệu-ứng-loading)
- [Hiệu ứng loading](#hiệu-ứng-loading-1)
- [Hiệu ứng loading](#hiệu-ứng-loading-2)
---
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
.hexagon{
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
# Tạo Menu 1 cấp
```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Menu</title>
    <style>
        *{
            padding: 0;
            box-sizing: border-box;
            margin: 0;
        }
        nav{
            position: relative;
            width: 100vw;
            height: 60px;
            background-color: #333;
        }
        nav ul{
            list-style: none;
            position: absolute;
        }
        nav ul li{
            float: left;
            width: 16.66vw;
            height: 60px;
        }
        nav ul li a{
            text-decoration: none;
            font-weight: 900;
            text-transform: uppercase;
            height: 60px;
            display: flex;
            justify-content: center;
            align-items: center;
        }
        nav ul li:hover a{
            background-color: #66ff99;
            border-radius: 20px;
            transition: all 0.7s;
        }
        nav ul li:active a{
            opacity: 0.8;
            background-color: #66ff99;
        }
        @media  (max-width: 500px) {
            nav ul li{
                float: none;
                width: 100vw;
                background-color: #333;
            }
            nav ul li a{
                width: 100%;
                background-color: #333;
            }
        }
    </style>
</head>
<body>
    <nav>
        <ul>
            <li><a href="#">Home</a></li>
            <li><a href="#">New</a></li>
            <li><a href="#">Feedbacks</a></li>
            <li><a href="#">More</a></li>
            <li><a href="#">About</a></li>
            <li><a href="#">Contact</a></li>
        </ul>
    </nav>
</body>
</html>
```
# Tạo Menu 2 cấp
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        *{
            padding: 0;
            margin: 0;
            box-sizing: border-box;
            color: #fff;
        }
        nav{
            display: block;
            height: 50px;
            background-color: #222;
        }
        nav > ul{
            display: flex;
            width: 100%;
            height: 50px;
            justify-content: space-evenly;
            align-items: center;
            list-style: none;
        }
        nav > ul > li{
            position: relative;
        }
        nav > ul > li > a{
            display: flex;
            text-decoration: none;
            font-size: 25px;
            text-transform: uppercase;
            font-weight: 900;
            width: 150px;
            height: 50px;
            justify-content: center;
            align-items: center;
        }
        nav > ul > li > div{
            display: block;
            position: absolute;
            width: 120%;
            left: -15px;
        }
        nav > ul > li > div > a{
            display: none;
            text-align: center;
            text-decoration: none;
            font-size: 20px;
            font-weight: 900;
            text-transform: uppercase;
            padding: 20px;
        }
        nav > ul > li:hover > a{
            transition: all .5s;
            background-color: #fff;
            color: #222;
        }
        nav > ul > li:hover > div > a{
            display: block;
            background-color: #222;
            transition: all .5s;
        }
        nav > ul > li:hover > div > a:hover{
            transition: all .5s;
            background-color: #fff;
            color: #222;
        }
        @media (max-width: 600px){
            nav{
                height: auto;
            }
            nav > ul{
                display: block;
                width: 100%;
            }
            nav > ul > li{
                width: 100%;
            }
            nav > ul > li > a{
                display: flex;
                width: 100%;
                height: auto;
                padding: 15px 0;
                font-size: 20px;
                background-color: #222;
            }
            nav > ul > li > div{
                position: static;
                width: 100%;
                background-color: #333;
                display: none;
                flex-direction: column;
            }
            nav > ul > li:hover > div{
                display: flex;
            }
            nav > ul > li > div > a{
                display: block;
                width: 100%;
                padding: 10px;
                font-size: 18px;
            }
            nav > ul > li:hover > div > a:hover{
                background-color: #fff;
                color: #222;
            }
        }
    </style>
</head>
<body>
    <nav>
        <ul>
            <li>
                <a href="#">Home</a>

                <div>
                    <a href="#">Home1</a>
                    <a href="#">Home2</a>
                    <a href="#">Home3</a>
                    <a href="#">Home4</a>
                    <a href="#">Home5</a>
                </div>
            </li>
            <li>
                <a href="#">Pages</a>

                <div>
                    <a href="#">Pages1</a>
                    <a href="#">Pages2</a>
                    <a href="#">Pages3</a>
                    <a href="#">Pages4</a>
                    <a href="#">Pages5</a>
                </div>
            </li>
            <li>
                <a href="#">Contact</a>

                <div>
                    <a href="#">Contact1</a>
                    <a href="#">Contact2</a>
                    <a href="#">Contact3</a>
                    <a href="#">Contact4</a>
                    <a href="#">Contact5</a>
                </div>
            </li>
            <li>
                <a href="#">Link</a>

                <div>
                    <a href="#">Link1</a>
                    <a href="#">Link2</a>
                    <a href="#">Link3</a>
                    <a href="#">Link4</a>
                    <a href="#">Link5</a>
                </div>
            </li>
            <li>
                <a href="#">Base</a>

                <div>
                    <a href="#">Base1</a>
                    <a href="#">Base2</a>
                    <a href="#">Base3</a>
                    <a href="#">Base4</a>
                    <a href="#">Base5</a>
                </div>
            </li>
            <li>
                <a href="#">Login</a>

                <div>
                    <a href="#">Login1</a>
                    <a href="#">Login2</a>
                    <a href="#">Login3</a>
                    <a href="#">Login4</a>
                    <a href="#">Login5</a>
                </div>
            </li>
        </ul>
    </nav>
</body>
</html>
```
# Kéo dãn thẻ div bằng scale
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Tester</title>
  <style>
    div{
      width: 100px;
      height: 100px;
      background-color: #000;
      animation: gian 3s infinite linear;
    }
    @keyframes gian {
      0%{transform: scale(0.8);}
      50%{transform: scale(1.2);}
      100%{transform: scale(0.8);}
    }
  </style>
</head>
<body>
 <div></div>
</body>
</html>
```
# Hiệu ứng thanh trượt từ trái sang phải
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <style>
        body > div{
            position: relative;
            width: 500px;
            height: 50px;
            background-color: #000;
        }
        div div{
            position: absolute;
            width: 0;
            height: 3px;
            background-color: #0becf0;
            transition: width 5s linear;
        }
        div:hover div{
            width: 100%;
        }
    </style>
</head>
<body>
    <div>
        <div></div>
    </div>
</body>
</html>
```
# Hiệu ứng thanh trượt từ giữa sang 2 bên
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <style>
        body > div{
            position: relative;
            width: 500px;
            height: 50px;
            background-color: #000;
        }
        div div{
            position: absolute;
            width: 100%;
            height: 3px;
            background-color: #0becf0;
            transition: transform 5s linear;
            transform: scaleX(0);
            transform-origin: 50%;
        }
        div:hover div{
            transform: scaleX(1);
        }
    </style>
</head>
<body>
    <div>
        <div></div>
    </div>
</body>
</html>
```
# Hiệu ứng loading
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Around loading</title>
    <link rel="stylesheet" href="around.css">
</head>
<body>
    <div>
        <div class="spiner">:)</div>
        <div class="bar">
            <span class="dot1"></span>
            <span class="dot2"></span>
            <span class="dot3"></span>
        </div>
        <div class="box">
            <h2>LDT</h2>
        </div>
    </div>
</body>
</html>

body{
    margin: 0px;
    box-sizing: border-box;
}
body > div{
    min-height: 100vh;
    width: 100%;
    background-color: #002266;
    text-align: center;
}
.spiner{
    margin-top: 50px;;
    width: 100px;
    height: 100px;
    display: inline-block;
    border: 10px solid #fff;
    border-radius: 50%;
    border-top: 10px solid #ff8000;
    animation: spiner 2s linear infinite;
    color: #fff;
    font-size: 4.5rem;
}
.bar > span{
    width: 50px;
    height: 50px;
    background-color: #ff8000;
    border-radius: 50%;
    display: inline-block;
    animation: dot 2s ease-in-out infinite both;
}
.bar span.dot1{
    animation-delay: -0.3s;
}
.bar span.dot2{
    animation-delay: -0.15s;
}
.bar span.dot3{
    animation-delay: 0s;
}
@keyframes spiner{
    from{
        transform: rotate(0deg);
    }
    to{
        transform: rotate(360deg);
    }
}
@keyframes dot {
    0%,80%,100%{
        transform: scale(0);
    }
    40%{
        transform: scale(1);
    }
}
.box{
    position: relative;
    width: 200px;
    height: 300px;
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: #000;
    border-radius: 20px;
    overflow: hidden;
    left: 670px;
    top: 100px;
}
.box h2{
    color:color-mix(in srgb, #bcee68, #ff8000);
    text-shadow: 4px 4px #000;
    font-size: 4em;
    z-index: 5;
}
.box::before{
    content: " ";
    position: absolute;
    width: 170px;
    height: 150%;
    background: linear-gradient(#00ccff,#d500f9);
    animation: around 5s linear infinite;
}
.box::after{
    content: ' ';
    position: absolute;
    background: #000;
    top: 5px;
    bottom: 5px;
    right: 5px;
    left: 5px;
    border-radius: 20px;
}
@keyframes around{
    from{
        transform: rotate(0deg);
    }
    to{
        transform: rotate(360deg);
    }
}
```
# Hiệu ứng loading
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <div class="loading">
        <div class="bar"></div>
    </div>
</body>
</html>

body{
    width: 100%;
    height: 100vh;
    margin: 0px;
    box-sizing: border-box;
    background-color: rgba(0, 0, 0, 0.909);
}
.loading{
    position: relative;
    width: 100%;
    min-height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
}
.bar{
    position: absolute;
    width: 500px;
    height: 60px;
    border: 2px solid #a2cd5a;
    border-radius: 20px;
    overflow: hidden;
}
.bar::before{
    content: ' ';
    position: absolute;
    width: 100%;
    height: 100%;
    background-color: color-mix(in srgb, blue, green);
    animation: progress1 5s infinite;
    transform-origin: left;
}
@keyframes progress1{
    from{
        transform: scaleX(0);
    }
    to{
        transform: scaleX(1);
    }
}
.bar::after{
    position: absolute;
    content: "please wait ...";
    width: 100%;
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    color: #fff;
    text-transform: uppercase;
    font-size: larger;
    font-family: Verdana, Geneva, Tahoma, sans-serif;
    font-weight: bolder;
}
```
# Hiệu ứng loading
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Tester</title>
  <link rel="stylesheet" href="Tester.css">
</head>
<body>
  <div id="bkground">
    <div id="logo"></div>
  </div>
</body>
</html>

*{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }
#bkground{
    position: relative;
    width: 100%;
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: rgba(0,0,0,0.75);
}
#logo{
    width: 100px;
    height: 100px;
    display: block;
    border-radius: 50%;
    border: 10px solid #fff;
    border-top: 10px solid #ff6600;
    animation: quay 3s linear infinite;
}
@keyframes quay{
    from{
      transform: rotate(0deg);
    }
    to{
      transform: rotate(360deg);
    }
}
```