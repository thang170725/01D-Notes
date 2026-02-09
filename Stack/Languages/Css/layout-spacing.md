- [Comment](#comment)
- [Combinators](#combinators)
- [Height/Width \& max-height \& max-width](#heightwidth--max-height--max-width)
- [background](#background)
- [margin](#margin)
- [padding](#padding)
- [text-align \& text-align-last](#text-align--text-align-last)
- [Position](#position)
---
# Comment 
```bash
/* … */
```
# Combinators
    • Thẻ1 thẻ2{} - Phân cấp cha con.
    • Thẻ1 > thẻ2{} - Phân cấp cha con một cấp.
    • Thẻ1 + thẻ2{} - css vào phần tử ngay sau.
    • Thẻ1 ~ thẻ 2{} - css vào tất cả các thẻ ngay sau nó và cùng cấp với thẻ 1.
    • :is(element1, element2) … – Để gom nhóm đối tượng nhanh khi chúng có cùng một dòng lệnh.
    • :where(element1, element2, …) - Ở đâu có element1, element2 thì CSS vào đó.
Ví dụ về ~
<main class="heading">
        <div class="heading1"></div>
        <div class="heading2"></div>
        <div class="heading3"></div>
    </main>
    <main class="end"></main>

div{
            width: 100px;
            height: 20px;
            margin: 10px 10px;
        }
        .end{
            width: 100px;
            height: 20px;
            margin: 10px 10px;
        }
        .heading1~div{
            background-color: aqua;
        }

Selector: Có thể là tên thẻ, id (#) hoặc class (.)

*{}
Nếu muốn áp dụng một thuộc tính nào đó cho tất cả các thẻ trong tài liệu.
* { 
   color: #000000;// tất cả chữ sẽ màu đen
}
# Height/Width & max-height & max-width
```bash
Thiết lập chiều dài, chiều rộng cho khối bao ngoài.
```
# background
```bash
Là cách viết gộp của các thuộc tính trong background.
```
**Syn**
```bash
background: color | image | position | size | repeat | origin | clip | attachment | initial | inherit
```
background-attachment
Chỉ định hình ảnh sẽ cố định hay cuộn theo trang web.
background-attachment: value;
value:
    • sroll: Hình nền bị cuốn theo khi kéo thanh croll.
    • local: Hình nền sẽ bị cuốn theo khi kéo thanh croll.
    • fixed: Hình nền sẽ nằm ở một vị trí cố định mặc cho ta kéo thanh croll. Khi lướt có thể đề lên cả phần tử khác.
    • initial: Sử dụng giá trị mặc định của nó.
    • inherit: Kế thừa phần tử cha của nó.
 <div></div>
 <p>Welcome to HTML - CSS</p>
body{
    height: 2000px;
}
div{
    width: 500px;
    height: 500px;
    margin: 30px 20px;
    background-image: url(./image/Hulk.jpg);
    background-size: contain;
    background-attachment: scroll;
}
p{
    margin: 30px 20px;
}
background-size
Thiết lập kích thước của hình nền.
background-size: value;
value:
    • Number + unit:
    • contain: đưa tỉ lệ về đúng kích thước và vừa phù hợp với khối bao ngoài
    • cover: cho hình ảnh full block có thể bị cắt bớt hình ảnh đi 
background-position
Thiết lập vị trí của hình nền trong thẻ cha. 
Cú pháp: background-position: value, …;
value:
    • Top
    • Left
    • Right
    • Bottom
    • Center
    • …
Tạo ra hiệu ứng dải màu chuyển
 <body></body>
 body {
        margin: 0;
        padding: 0;
        background-image: linear-gradient(
          45deg,
          #ff0000,
          #fffb00,
          #5eff00,
          #ff5100,
          #00f7ff,
          #f700e2
        );
        /* chiều rộng tăng 9 lần chiều cao tăng 2 lần */
        background-size: 900% 200%;
        height: 100vh;
        animation: animate 20s linear infinite;
      }
      @keyframes animate {
        /* ở vị trí trái giữa */
        0%{background-position: 0% 50%;}
        /* ở vị trí giữa giữa */
        50%{background-position: 50% 50%;}
        /* ở vị trí phải giữa */
        75%{background-position: 100% 50%;}
        100%{background-position: 0% 50%;}
      }

background-clip 
Xác định phạm vi được thiết lập cho phần tử. Chỉ được hiển thị trên website tại vùng đã cài đặt thuộc tính background-clip. Nên thêm tiền tố -webkit cho safari và một số trình duyệt khác.
Giá trị:
    • border-box
    • padding-box
    • content-box
    • text
    • initial
    • inherit
    • …
Ví dụ về backgound-clip
<div>WelCome to HaNoi</div>

div{
    font-family: sans-serif;
    font-size: 30px;
    font-weight: 900;
    background-image: linear-gradient(to right, #ff0000, #00ff00);
    background-clip: text;
    color: transparent;
}

background-origin
Thiết lập phạm vi mà hình nền sẽ xuất hiện. Phần được hiển thị sẽ tính từ vùng cài đặt background-origin trở vào trong.
Cú pháp: background-origin: value;
Value:
    • border-box
    • padding-box
    • content-box
    • initial
    • inherit
    backdrop-filter
Áp dụng hiệu ứng đồ họa cho khu vực phía sau. Không áp dụng được với opacity, chỉ áp dụng được với rgba, …
Cú pháp:
    • backdrop-filter: value;
    • -webkit-Backdrop-filter: value;
Value:
    • none: là giá trị mặc định
    • filter: sử dụng các giá trị của thuộc tính filter
    • initial: sử dụng thuộc tính mặc định
    • inherit: kế thừa thuộc tính cha

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <link rel="stylesheet" href="Tester.css">
</head>
<body>
  <div>Ví dụ về backdrop filter</div>
</body>
</html>

body{
    background-image: url(./image/background-car.jpg);
    background-size: cover;
}
div{
    width: 100%;
    height: 50px;
    background-color: rgba(255, 255, 255, 0.4);
    position: relative;
    top: 300px;
    -webkit-backdrop-filter: blur(5px);
    backdrop-filter: blur(5px);
}
# margin
```bash
- Nếu có 4 giá trị thì các giá trị lần lượt là top, right, bottom, left.
- Nếu có 3 giá trị thì các giá trị lần lượt là top, right-left, bottom.
- Nếu có 2 giá trị thì các giá trị lần lượt là top-bottom, right-left.
- Nếu có 1 giá trị thì giá trị đó là top-right-bottom-left.
```
# padding
```bash
Chỉ định khoảng đệm thêm vào cho content.
```
outline
Là một đường kẻ xung quanh phần tử, nằm bên ngoài border để làm nổi bật phần tử. có thể thiết lập các giá trị giống với border. Nó có thể đè lên các phần tử khác. Ngoài ra outline không là một phần trong kích thước của phần tử. độ rộng và chiều cao không bị ảnh hưởng bởi độ rộng của outline.
Cú pháp:
outline: outline-width | outline-style | outline-color
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <link rel="stylesheet" href="Tester.css">
</head>
<body>
  <div></div>
</body>
</html>
div{
    width: 50px;
    height: 50px;
    outline: 2px solid;
    border: 2px solid #ff0000;
    margin: 20px;
}


outline-width
Xác định độ rộng.
outline-style
Xác định kiểu đường viền.
Value:
    • Dotter
    • Dashed
    • Solid
    • Double
    • Groove
    • Ridge
    • Inset 
    • Outset
    • None
    • Hidden
# text-align & text-align-last
```bash
- text-align        : Để căn chỉnh content của một phần tử.
- text-align-last   : Căn chỉnh dòng cuối cùng của các đoạn văn bản.
```
Cú pháp:
text-align: value;
value:
    • center: Căn giữa.
    • left: Căn trái.
    • right: Căn phải.
    • justify: Căn đều so với lề trái và lề phải


Cú pháp:
text-align-last: value;
value:
    • auto: Dòng cuối cùng căn đều và căn trái.
    • left: Căn dòng cuối sang trái.
    • right: Căn dòng cuối sang phải.
    • center: Căn dòng cuối ra giữa.
    • justify: Căn dòng cuối san đều ra 1 dòng.
    • start: Căn dòng cuối sang trái.
    • end: Căn dòng cuối sang phải.
    • initial: Lấy giá trị mặc định.
    • inherit: Lấy giá trị của phần tử cha.
direction
Thiết lập hướng của văn bản.
Cú pháp:
direction: value;
value:
    • ltr: Hướng văn bản từ trái sang phải.
    • rtl: Hướng văn bản từ phải sang trái.
vertical-align
Để căn chỉnh content khi nội dung được lồng ghép vào nhau. Chỉ hoạt động với image hoặc thẻ bao ngoài có thuộc tính display: table-cell.
value:
    • auto
    • baseline: Mặc đinh.
    • sub: Căn chỉnh phần tử xuống dưới đường cơ sở.
    • super: Căn chỉnh phần tử lên trên đường cơ sở.
    • top: Căn chỉnh phần tử lên trên cùng của dòng chữ.
    • middle: Căn chỉnh phần tử vào giữa dòng chữ.
    • bottom: Căn chỉnh phần tử xuống dưới cùng của dòng chữ. 
    • Text-top
    • Text-bottom
    • Inherit
# Position
```bash
- Chỉ định loại phương pháp định vị được sử dụng cho một phần tử.
```
**Syn**
```bash
position: value;

- static: Mặc định, sẽ hiển thị theo đúng thứ tự của nó.
- relative: Định vị tuyệt đối, lúc này các thẻ bên trong coi là thẻ cha.
- absolute: Định vị tương đối theo thẻ cha.
- fixed: Định vị tương đối cho cửa sổ trình duyệt, khi kéo thanh cuộn nó không bị ẩn đi.
- Sticky: Nếu đi kèm với top: 0 khi scroll sẽ dính ở trên đầu website.
- inherit: Thừa hưởng thuộc tính của phần tử cha.
```
**Ex**
```html
<div></div>
```
```css
div{
    width: 100px;
    height: 100px;
    background: red;
    position: fixed;
    top: 0; /*khi dùng fix có thể di chuyển bằng, top, left, ... */
}
```