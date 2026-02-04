- [Cấu trúc thư mục](#cấu-trúc-thư-mục)
  - [details \& summary](#details--summary)
  - [canvas](#canvas)
  - [blockquote](#blockquote)
  - [q](#q)
  - [abbr](#abbr)
  - [address](#address)
  - [cite](#cite)
  - [bdo](#bdo)
  - [code](#code)
  - [base](#base)
  - [Thẻ hr](#thẻ-hr)
  - [br](#br)
  - [ul \& ol \& li \& dl \& dt \& dd](#ul--ol--li--dl--dt--dd)
  - [select \& option](#select--option)
  - [fieldset \& legend](#fieldset--legend)
- [table](#table)
  - [caption](#caption)
  - [th \& tr \& td](#th--tr--td)
---
# Cấu trúc thư mục
```bash
Html/
├── 01_form_metadata.md   # Cấu trúc boilerplate, thẻ <head>, meta, title, link
├── 02_text_content.md    # Các thẻ văn bản: h1-h6, p, span, br, hr, strong, em...
├── 03_grouping_layout.md # Thẻ khối & bố cục: div, main, section, article, header, footer, aside, ul, ol, li
├── 04_forms_input.md     # Form, input (các loại), button, select, textarea, label
├── 05_media_links.md     # Thẻ a (link), img, video, audio, iframe
└── 06_tables_others.md   # Table, các thẻ hiếm dùng hoặc thẻ đặc biệt (canvas, svg...)
```
**Chi tiết nội dung từng file**
```bash
1. 01_form_metadata.md
    + Nơi chứa những thứ "không hiển thị trực tiếp" nhưng cực kỳ quan trọng.
    + Nội dung: Cấu trúc !DOCTYPE, <html>, <head>, <meta charset="UTF-8">, <meta name="viewport"> (cho mobile), cách chèn CSS/JS.
2. 02_text_content.md
    + Tập trung vào ngữ nghĩa của văn bản.
    + Nội dung: Phân biệt khi nào dùng <b> vs <strong>, <i> vs <em>. Cách dùng các thẻ heading để làm SEO.
3. 03_grouping_layout.md
    + Đây là "xương sườn" để bạn kết hợp với CSS Layout sau này.
    + Nội dung: Các thẻ Semantic (thẻ có nghĩa) như <nav>, <footer>. Đừng quên ghi chú về sự khác biệt giữa Block (div, p) và Inline (span, a).
4. 04_forms_input.md
    + Các phần liên quan đến form nhập liệu
5. 05_media_links.md
    + Cách kết nối dữ liệu bên ngoài. (a, video, ...)
```

## details & summary
Tạo một phần nội dung có thể mở hoặc đóng. Thường kết hợp với thẻ summary.
Để tạo tiêu đề cho thẻ details. Các thẻ bao ngoài nội dung


## canvas
Một phần tử HTML cho phép vẽ bằng JavaScript.
Bạn dùng <canvas> khi cần:
    • Vẽ hình động (animations)
    • Tạo trò chơi 2D
    • Vẽ biểu đồ, sơ đồ (chart, graph)
    • Xử lý ảnh (image processing)
    • Visualize dữ liệu hoặc AI (ví dụ như bounding box, filter ảnh)
Cú pháp: <canvas id="myCanvas" width="400" height="200" style="border:1px solid #000000;"></canvas>
## blockquote
Định nghĩa một đoạn văn bản được trích dẫn từ một nguồn khác, nó sẽ tụt vào so với lề. 
## q
Định nghĩa ra một đoạn text trích dẫn ngắn, thẻ này sẽ chèn một dấu nháy vào đoạn text.
## abbr 
Để định nghĩa tên viết tắt hoặc bổ trợ ý nghĩa cho một đoạn text nào đó. Thẻ abbr chủ yếu đi kèm với thuộc tính title.

Di chuyển chuột vào chữ đó ta thấy “Lê Đức Thắng” hiện ra

## address
Để xác định thông tin liên lạc của tác giả, thẻ này thường đượng in nghiêng. 
## cite
Dùng để xác định tiêu đề của một việc. chữ sẽ được in nghiêng.
## bdo
Cho phép bạn chỉ định hướng văn bản từ trái sang phải hay từ phải sang trái. Display: inline. Thường sử dụng với thuộc tính dir.
<bdo dir=’ltr’>…</bdo>
<bdo dir=’rtl’>…</bdo>

## code
Để báo hiệu đây là một đoạn code.
Thẻ kbd
Dùng để xác định một từ hoặc một cụm từ măng ý nghiawx là một phím hoặc một tổ hợp phím. Với font chữ mặc định là monospace.
Thẻ samp
Để xác định đầu ra mẫu từ một chương trình máy tính. Nội dungg bên trong được hiển thị bằng phông chữ monospace.
Thẻ var
Sẽ định nghĩa một biến. Nó được sử dụng để đánh dấu tên một biến, các nội dung trong thẻ var sẽ được hiển thị khác với thông thường.
Thẻ time
Định dạng thời gian.
Thẻ hgroup 
Thẻ <hgroup> … </hgroup> để nhóm các thẻ h1 -> h6 vào cùng một nhóm. Với điều kiện chúng phải nằm cùng một thẻ cha. Hỗ trợ tất cả thuộc tính css.
Thẻ u 
Thẻ <u> … </u> định dạng đoạn text hiển thị trên trang web sẽ có dấu gạch chân. Có thể sử dụng tất cả thuộc tính của css.
Thẻ s 
Thẻ <s> … </s> định nghĩa đoạn text không còn chính xác nữa, đoạn text sẽ bị gạch giống thẻ del. Sử dụng được tất cả thuộc tính trên css.
Thẻ acronym
Chức năng giống với thẻ abbr. không hỗ trợ ở phiên bản HTML 5.
Thẻ dialog
thẻ <dialog> … </dialog> định nghĩa ra một hộp thoại hay một cửa số
thẻ bdi
thẻ <bdi> … </bdi> có chức năng phân lập một phần văn bản mà phần tử đó có khả năng được định dạng theo một hướng khác so với những phần văn bản còn lại. được dùng khi muốn phân lập một nội dung mà ta chưa thể xác định được hướng của nó. Dislay: inline
Điểu hướng & nút bấm
## base 
 Thẻ <base> dùng để xác định một "đường dẫn cơ sở" trong trang web, không có thẻ đóng. "Đường dẫn cơ sở" này sẽ kết hợp với những "đường dẫn tương đối" để tạo ra đường dẫn tuyệt đối. Đường dẫn cơ sở không kết hợp với những đường dẫn tuyệt đối trong trang web.
Ngoài ra, thẻ <base> còn được dùng để xác định kiểu mở liên kết mặc định cho những liên kết chưa được thiết lập kiểu mở liên kết.
 Lưu ý: Thẻ <base> chỉ có hiệu lực với những đường dẫn nằm phía dưới nó. Do đó, nếu bạn muốn áp dụng thẻ <base> cho tất cả các đường dẫn trong trang web thì bạn nên đặt nó ở vị trí đầu tiên trong phần tử <head>
Thẻ embed
Thẻ <embed> … </embed> để xác định một vùng chứa cho một ứng dụng bên ngoài hoặc nội dung tương tác.
Thuật toán tạo nút bấm có hiệu ứng bằng skew

## Thẻ hr 
Định ra một đoạn kẻ gạch để ngăn cách các thẻ.

## br
Thẻ br có tác dụng ngắt dòng hiện tại và chuyển sang một dòng mới. Thẻ br không có thẻ đóng. 
Cú pháp: <br> hoặc <br/>

## ul & ol & li & dl & dt & dd

## select & option
Tạo danh sách xổ xuống danh sách này không dùng để điều hướng. 



## fieldset & legend
Thẻ <fieldset> … </fieldset> để tạo ra khung bao quanh, nhóm các phần tử có liên quan vào cùng một nhóm
Thẻ legend 
Thẻ <legend> … </legend> để tạo tiêu đề cho thẻ fieldset. Thường kết hợp với thẻ fieldset
Thẻ textarea 
Thẻ <textarea> … </textarea> để tạo ra một vùng nhập dữ liệu nhiều dòng
Thẻ datalist 
Thẻ <datalist> … </datalisst> thường kết hợp với thẻ input và option, có chức năng xác định một danh sách có sẵn cho một phần tử <input>. cung cấp chức năng "autocomplete" cho các phần tử <input>, người dùng sẽ thấy một danh sách thả xuống các tùy chọn trước khi họ nhập dữ liệu
Thẻ output
Thẻ <output> … </output> đại diện cho một kết quả tính toán (như là kết quả của một câu lệnh script)
Ví dụ
Tạo form đăng nhập cơ bản
<div class="login">
<form action="">
<h1>LOGN IN</h1>
<label for="">Username</label>
<input type="text" name="" id="">
<label for="">Password</label>
<input type="password" name="" id="">
<button>Submit</button>
</form>
</div>
.login{
width: 400px;
height: 500px;
border-radius: 20px;
box-shadow: 0px 0px 20px rgba(0,0,0,0.75);
background-position: center;
overflow: hidden;
}

form{
display: block;
box-sizing: border-box;
padding: 40px;
width: 100%;
height: 100%;
backdrop-filter: brightness(80%);
flex-direction: column;
display: flex;
gap: 5px;
background-color: #000;
}

h1{
color: #fff;
font-size: 2em;
text-shadow: 0px 0px 20px rgba(0,0,0,0.5);
text-align: center;
}

label{
color: #fff;
text-transform: uppercase;
font-size: 10px;
letter-spacing: 2px;
padding-left: 10px;
}

input{
color: #fff;
background: rgba(255,255,255,0.3);
height: 40px;
line-height: 40px;
border-radius: 20px;
padding: 0px 20px;
border: none;
margin-bottom: 20px;
}

button{
background: rgb(45,126,231);
height: 40px;
border-radius: 40px;
border: none;
margin: 10px 0px;
box-shadow: 0px 0px 5px rgba(0,0,0,0.3);
color: #fff;
font-size: 12px;
text-transform: uppercase;
}
Ảnh & Video
Thẻ img
Để thêm hình ảnh vào trang web. Nó không có thẻ đóng.
Thuộc tính src
Chỉ định đường dẫn của ảnh.
Thuộc tính alt
Khi ảnh không hoạt động.
Thuộc tính width
Chỉ định chiều rộng.
Thuộc tính height
Chỉ định chiều cao.

Thẻ map
Để xác định bản đồ hình ảnh. Bản đồ hình ảnh là một hình ảnh chứa các khu vục có thể nhấp được.
Thuộc tính name
Chỉ định tên của bản đồ hình ảnh.
Thẻ area
Được sử dụng để định nghĩa một khu vực trong Image Map.
Thuộc tính shape
Chỉ định hình dạng.
    • rect | rectangle – Hình chữ nhật.
    • circ | circle – Hình tròn.
    • poly | polygon – Đa giác.
Thuộc tính coords
Nếu shape là rect thì coords = “left, top, right, bottom”
Nếu shape là circ thì coords = “x, y, r”
Nếu shape là poly thì coords = “x1, y1, x2, y2,…”
Thuộc tính alt
Xác định đoạn văn bản thay thế.
Thuộc tính href
Xác định nguồn cảu ảnh thay thế
Xem ví dụ ở đây: https://www.w3schools.com/html/html_images_imagemap.asp
Thẻ picture 
Cho phép hiển thị nhiều hình ảnh khác nhau cho nhiều thiết bị hoặc kích thước màn hình thay đổi
Xem ví dụ ở đây: https://www.w3schools.com/html/tryit.asp?filename=tryhtml_images_picture1
Thẻ figure 
Để chỉ định nội dung khép kín, như hình minh họa, sơ đồ, ảnh, danh sách mã, v.v ... display: block;
Thẻ figcaption
Định nghĩa tiêu đề cho một phần tử figure. Nằm trong thẻ figure. 
Vùng chọn
Thẻ iframe
Chỉ định một nội dung định tuyến. Nó sử dụng để nhúng một tài liệu khác vào trang của bạn. tác dụng khá giống với thẻ img, khác biệt là ở chỗ nó sẽ nhúng một tài liệu thay vì chỉ nhúng một hình ảnh như thẻ img.
Thẻ frameset
Thẻ <frameset> … </frameset> xác định bộ khung cho thẻ frame.
Thẻ frame 
Thẻ frame dùng để nhúng một tài liệu nào đó vào trang web hiện tại (tài liệu ở đây rất đa dạng, có thể là một trang web khác, tập tin pdf, tấm hình, ....) phải được đặt bên trong phần tử <frameset>. Nó không có thẻ đóng
Thẻ object
Thẻ <object> … <oject> sẽ định nghĩa một đối tượng được nhúng vào tài liệu HTML. Sử dụng thẻ object để nhúng các tệp đa phương tiện (flash, âm thanh, video, PDF. v. v) vào trang của bạn. có thể nhúng một trang web khác vào trang của bạn. Nếu xem xét kỹ thì thực chất các thẻ, img, audio, iframe. v. v. đều có thể thay thế được bằng thẻ object.
Thẻ param
Thẻ param định nghĩa các tham số cho các plugin gắn với thẻ object. Trong HTML 5 đã thêm vào hai thẻ mới để nhúng các file âm thanh, video đó là thẻ audio và thẻ video.

# table
Để định nghĩa một bảng.

## caption 
Để đặt tiêu đề cho một bảng, thẻ <caption> phải được đặt ngay sau thẻ <table>. Chỉ có thể đặt một <caption> cho một thẻ <table>

## th & tr & td
- th: định nghĩa tiêu đề cho từng cột.
- tr: định nghĩa một hàng (dòng) trong bảng
- td: Sẽ định nghĩa một ô tiêu chuẩn trong một bảng

Thẻ colgroup 
Xác định một nhóm của một hoặc nhiều cột trong bảng để phục vụ cho việc định dạng. Sử dụng thẻ <colgroup> kết hợp với thẻ <col> để định dạng cho các cột. 
Thẻ col 
Chỉ định thuộc tính cho mỗi cột trong một phần tử <colgroup>. Thẻ <col> đặc biết hữu ích trong việc áp dụng kiểu cho toàn bộ các cột thay vì phải lặp lại cho từng ô, từng hàng. Thẻ này không có thẻ đóng. 
Thuộc tính colspan
Để gộp cột.
Thuộc tính rowspan
Thuộc tính span
Nhóm cột theo chiều dọc.
Hiệu ứng thanh kéo
Thẻ meter 
Thẻ <meter> … </meter> biểu diễn số dưới dạng thước đo.
Thẻ progress 
Thẻ <progress> … </progress> sẽ thể hiện quá trình của một tác vụ. giống với biểu thị dạng thước đo, hiển thị tiến trình làm việc.
Data Attribute
Tự tạo ra thuộc tính riêng của mình.
Cú pháp:
    • data-*
    • data-* = “”
style data Attribute
Để viết CSS cho phần tử HTML dựa và thuộc tính và giá trị của chúng. Giá trị thuộc tính không phân biệt chữ hoa, chữ thường.
Cú pháp:
[data-* = “”]{}
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <style>
    [data-color="đỏ"]{
      color: #ff0000;
    }
    [data-color="vàng"]{
      color: #fffb00;
    }
  </style>
</head>
<body>
  <p data-color="vàng">Welcome to HTML - CSS</p>
  <p data-color="đỏ">Welcome to HTML - CSS</p>
</body>
</html>

attr() trong HTML
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <style>
    p::after{
      content: attr(data-name);
    }
  </style>
</head>
<body>
  <p data-name="Lê Đức Thắng"></p>
</body>
</html>
