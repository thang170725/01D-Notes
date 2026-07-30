- [Bố cục trang HTML](#bố-cục-trang-html)
- [Meta (tiện ích)](#meta-tiện-ích)
  - [link (Liên kết file HTML với file bên ngoài)](#link-liên-kết-file-html-với-file-bên-ngoài)
- [Box Container (phần khung chứa định ra bố cục trang web)](#box-container-phần-khung-chứa-định-ra-bố-cục-trang-web)
  - [header (định ra phần đầu cho website)](#header-định-ra-phần-đầu-cho-website)
  - [main (Chứa tất cả nội dung của một website)](#main-chứa-tất-cả-nội-dung-của-một-website)
  - [article (Để định nghĩa các phần nội dung riêng biệt.)](#article-để-định-nghĩa-các-phần-nội-dung-riêng-biệt)
  - [aside (định ra nội dung một bên sidebar và thường liên quan đến nội dung trong website)](#aside-định-ra-nội-dung-một-bên-sidebar-và-thường-liên-quan-đến-nội-dung-trong-website)
  - [footer (Định ra phần cuối cùng trong văn bản)](#footer-định-ra-phần-cuối-cùng-trong-văn-bản)
  - [Thẻ hr (Định ra một đoạn kẻ gạch để ngăn cách các thẻ)](#thẻ-hr-định-ra-một-đoạn-kẻ-gạch-để-ngăn-cách-các-thẻ)
  - [br (ngắt dòng hiện tại và chuyển sang một dòng mới)](#br-ngắt-dòng-hiện-tại-và-chuyển-sang-một-dòng-mới)
- [Box Detail (phần khung chứa content, định ra nội dùng tran web)](#box-detail-phần-khung-chứa-content-định-ra-nội-dùng-tran-web)
  - [nav (định ra các liên kết và các thanh điều hướng cho website)](#nav-định-ra-các-liên-kết-và-các-thanh-điều-hướng-cho-website)
  - [a (Để tạo liên kết, điều hướng tới trang khác, … )](#a-để-tạo-liên-kết-điều-hướng-tới-trang-khác--)
  - [div (Để định ra một phần nội dung, gom nhóm nội dung)](#div-để-định-ra-một-phần-nội-dung-gom-nhóm-nội-dung)
- [Text](#text)
  - [h1 -\> h6 (Định ra đoạn text tiêu đề)](#h1---h6-định-ra-đoạn-text-tiêu-đề)
  - [p (Định dạng đoạn văn hay văn bản có trong trang web)](#p-định-dạng-đoạn-văn-hay-văn-bản-có-trong-trang-web)
  - [span (định ra đoạn văn bản)](#span-định-ra-đoạn-văn-bản)
  - [pre (Định nghĩa ra đoạn văn bản giữ nguyên các khoảng trắng)](#pre-định-nghĩa-ra-đoạn-văn-bản-giữ-nguyên-các-khoảng-trắng)
  - [b (Định dạng đoạn text sẽ được in đậm)](#b-định-dạng-đoạn-text-sẽ-được-in-đậm)
  - [Thẻ strong (Nhấn mạnh, quan trọng về mặt ngữ nghĩa)](#thẻ-strong-nhấn-mạnh-quan-trọng-về-mặt-ngữ-nghĩa)
  - [i (Định dạng đoạn text sẽ được in nghiêng)](#i-định-dạng-đoạn-text-sẽ-được-in-nghiêng)
  - [em (Nhấn mạnh văn bản về mặt ngữ nghĩa, thường in nghiêng)](#em-nhấn-mạnh-văn-bản-về-mặt-ngữ-nghĩa-thường-in-nghiêng)
  - [small (Định nghĩa ra đoạn văn bản được hiển thị nhỏ hơn)](#small-định-nghĩa-ra-đoạn-văn-bản-được-hiển-thị-nhỏ-hơn)
  - [mark (Định dạng đoạn text sẽ được tô thêm màu nền)](#mark-định-dạng-đoạn-text-sẽ-được-tô-thêm-màu-nền)
  - [del (Đoạn text đó sẽ có dấu gạch ngang ở giữa chữ)](#del-đoạn-text-đó-sẽ-có-dấu-gạch-ngang-ở-giữa-chữ)
  - [ins (Đoạn text xuất hiện trên trang web sẽ có dấu gạch dưới)](#ins-đoạn-text-xuất-hiện-trên-trang-web-sẽ-có-dấu-gạch-dưới)
  - [sub (Đoạn text sẽ tụt xuống dưới giống như chỉ số hóa học)](#sub-đoạn-text-sẽ-tụt-xuống-dưới-giống-như-chỉ-số-hóa-học)
  - [sup (Đoạn text biểu thị giống như số mũ )](#sup-đoạn-text-biểu-thị-giống-như-số-mũ-)
  - [details \& summary (Tạo một phần nội dung có thể mở hoặc đóng)](#details--summary-tạo-một-phần-nội-dung-có-thể-mở-hoặc-đóng)
  - [blockquote (Định nghĩa một đoạn văn bản được trích dẫn từ một nguồn khác, nó sẽ tụt vào so với lề)](#blockquote-định-nghĩa-một-đoạn-văn-bản-được-trích-dẫn-từ-một-nguồn-khác-nó-sẽ-tụt-vào-so-với-lề)
  - [q (Định nghĩa ra một đoạn text trích dẫn ngắn, thẻ này sẽ chèn một dấu nháy vào đoạn text)](#q-định-nghĩa-ra-một-đoạn-text-trích-dẫn-ngắn-thẻ-này-sẽ-chèn-một-dấu-nháy-vào-đoạn-text)
  - [abbr (định nghĩa tên viết tắt hoặc bổ trợ ý nghĩa cho một đoạn text nào đó)](#abbr-định-nghĩa-tên-viết-tắt-hoặc-bổ-trợ-ý-nghĩa-cho-một-đoạn-text-nào-đó)
  - [cite (Dùng để xác định tiêu đề của một việc. chữ sẽ được in nghiêng)](#cite-dùng-để-xác-định-tiêu-đề-của-một-việc-chữ-sẽ-được-in-nghiêng)
  - [bdo (định hướng văn bản)](#bdo-định-hướng-văn-bản)
  - [hgroup (để nhóm các thẻ h1 -\> h6 vào cùng một nhóm. Với điều kiện chúng phải nằm cùng một thẻ cha)](#hgroup-để-nhóm-các-thẻ-h1---h6-vào-cùng-một-nhóm-với-điều-kiện-chúng-phải-nằm-cùng-một-thẻ-cha)
  - [u (định dạng đoạn text hiển thị trên trang web sẽ có dấu gạch chân)](#u-định-dạng-đoạn-text-hiển-thị-trên-trang-web-sẽ-có-dấu-gạch-chân)
  - [s (định nghĩa đoạn text không còn chính xác nữa, đoạn text sẽ bị gạch giống thẻ del)](#s-định-nghĩa-đoạn-text-không-còn-chính-xác-nữa-đoạn-text-sẽ-bị-gạch-giống-thẻ-del)
  - [acronym (Chức năng giống với thẻ abbr. không hỗ trợ ở phiên bản HTML 5)](#acronym-chức-năng-giống-với-thẻ-abbr-không-hỗ-trợ-ở-phiên-bản-html-5)
  - [dialog (định nghĩa ra một hộp thoại hay một cửa số)](#dialog-định-nghĩa-ra-một-hộp-thoại-hay-một-cửa-số)
  - [bdi (phân lập một phần văn bản)](#bdi-phân-lập-một-phần-văn-bản)
- [Form (các thẻ định ra form)](#form-các-thẻ-định-ra-form)
  - [Input (Để lấy dữ liệu khi người dùng nhập vào)](#input-để-lấy-dữ-liệu-khi-người-dùng-nhập-vào)
- [button (Để tạo ra một nút bấm)](#button-để-tạo-ra-một-nút-bấm)
- [Image \& Video \& Audio (ảnh và video)](#image--video--audio-ảnh-và-video)
  - [source (chỉ định tài nguyên đa phượng tiện cho các phần tử media)](#source-chỉ-định-tài-nguyên-đa-phượng-tiện-cho-các-phần-tử-media)
  - [audio (định nghĩa đó là một file âm thanh)](#audio-định-nghĩa-đó-là-một-file-âm-thanh)
  - [video (định nghĩa một video)](#video-định-nghĩa-một-video)
  - [track (dùng để chèn một bản phụ đề vào video)](#track-dùng-đểchèn-một-bản-phụ-đề-vào-video)
  - [img (Để thêm hình ảnh vào trang web)](#img-để-thêm-hình-ảnh-vào-trang-web)
  - [map (xác định bản đồ hình ảnh)](#map-xác-định-bản-đồ-hình-ảnh)
  - [picture (phép hiển thị nhiều hình ảnh khác nhau cho nhiều thiết bị hoặc kích thước màn hình thay đổi)](#picture-phép-hiển-thị-nhiều-hình-ảnh-khác-nhau-cho-nhiều-thiết-bị-hoặc-kích-thước-màn-hình-thay-đổi)
  - [figure (Để chỉ định nội dung khép kín, như hình minh họa, sơ đồ, ảnh, danh sách mã)](#figure-để-chỉ-định-nội-dung-khép-kín-như-hình-minh-họa-sơ-đồ-ảnh-danh-sách-mã)
  - [figcaption (Định nghĩa tiêu đề cho một phần tử figure. Nằm trong thẻ figure)](#figcaption-định-nghĩa-tiêu-đề-cho-một-phần-tử-figure-nằm-trong-thẻ-figure)
  - [iframe (Chỉ định một nội dung định tuyến)](#iframe-chỉ-định-một-nội-dung-định-tuyến)
  - [frameset (xác định bộ khung cho thẻ frame)](#frameset-xác-định-bộ-khung-cho-thẻ-frame)
  - [frame (dùng để nhúng một tài liệu nào đó vào trang web hiện tại)](#frame-dùng-để-nhúng-một-tài-liệu-nào-đó-vào-trang-web-hiện-tại)
  - [object (định nghĩa một đối tượng được nhúng vào tài liệu HTML)](#object-định-nghĩa-một-đối-tượng-được-nhúng-vào-tài-liệu-html)
  - [param (định nghĩa các tham số cho các plugin gắn với thẻ object)](#param-định-nghĩa-các-tham-số-cho-các-plugin-gắn-với-thẻ-object)
- [Draw](#draw)
  - [canvas](#canvas)
- [List (Danh sách)](#list-danh-sách)
  - [ul \& ol \& li \& dl \& dt \& dd](#ul--ol--li--dl--dt--dd)
  - [select \& option (Tạo danh sách xổ xuống danh sách này không dùng để điều hướng)](#select--option-tạo-danh-sách-xổ-xuống-danh-sách-này-không-dùng-để-điều-hướng)
  - [fieldset \& legend (để tạo ra khung bao quanh, nhóm các phần tử có liên quan vào cùng một nhóm)](#fieldset--legend-để-tạo-ra-khung-bao-quanh-nhóm-các-phần-tử-có-liên-quan-vào-cùng-một-nhóm)
  - [legend (để tạo tiêu đề cho thẻ fieldset. Thường kết hợp với thẻ fieldset)](#legend-để-tạo-tiêu-đề-cho-thẻ-fieldset-thường-kết-hợp-với-thẻ-fieldset)
  - [textarea (để tạo ra một vùng nhập dữ liệu nhiều dòng)](#textarea-để-tạo-ra-một-vùng-nhập-dữ-liệu-nhiều-dòng)
  - [datalist (xác định một danh sách có sẵn cho một phần tử )](#datalist-xác-định-một-danh-sách-có-sẵn-cho-một-phần-tử-)
- [Table (Bảng)](#table-bảng)
  - [table (Để định nghĩa một bảng)](#table-để-định-nghĩa-một-bảng)
  - [caption (Để đặt tiêu đề cho một bảng)](#caption-để-đặt-tiêu-đề-cho-một-bảng)
  - [th (định nghĩa tiêu đề cho từng cột)](#th-định-nghĩa-tiêu-đề-cho-từng-cột)
  - [tr (định nghĩa một hàng (dòng) trong bảng)](#tr-định-nghĩa-một-hàng-dòng-trong-bảng)
  - [td (Sẽ định nghĩa một ô tiêu chuẩn trong một bảng)](#td-sẽ-định-nghĩa-một-ô-tiêu-chuẩn-trong-một-bảng)
  - [colgroup (Xác định một nhóm của một hoặc nhiều cột trong bảng để phục vụ cho việc định dạng)](#colgroup-xác-định-một-nhóm-của-một-hoặc-nhiều-cột-trong-bảng-để-phục-vụ-cho-việc-định-dạng)
  - [col (Chỉ định thuộc tính cho mỗi cột)](#col-chỉ-định-thuộc-tính-cho-mỗi-cột)
  - [colspan (Để gộp cột)](#colspan-để-gộp-cột)
  - [rowspan (Nhóm cột theo chiều dọc)](#rowspan-nhóm-cột-theo-chiều-dọc)
- [Progress](#progress)
  - [meter (biểu diễn số dưới dạng thước đo)](#meter-biểu-diễn-số-dưới-dạng-thước-đo)
  - [progress (thể hiện quá trình của một tác vụ)](#progress-thể-hiện-quá-trình-của-một-tác-vụ)
- [Data Attribute (Tự tạo ra thuộc tính riêng của mình)](#data-attribute-tự-tạo-ra-thuộc-tính-riêng-của-mình)
  - [style data Attribute (Để viết CSS cho phần tử HTML dựa và thuộc tính và giá trị của chúng)](#style-data-attribute-để-viết-css-cho-phần-tử-html-dựa-và-thuộc-tính-và-giá-trị-của-chúng)
- [attr()](#attr)
---
# Bố cục trang HTML
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
</head>
<body>
    <header></header>
    <main>
        <aside></aside> <!-- Phần sidebar -->
        <section>
            <article></article>
        </section> <!-- Phần content -->
    </main>
    <footer></footer>
</body>
</html>
```
# Meta (tiện ích)
## link (Liên kết file HTML với file bên ngoài)
```bash
Thẻ Link không có thẻ đóng. Các viết tắt: link:css.
```
**Syn**
```bash
<link rel="stylesheet" href="Tester.css">

- rel
    + stylesheet    : giá trị được sử dụng phổ biến nhất. Liên kết với một biểu định kiểu bên ngoài.
    + icon          : Một tài nguyên biểu tượng. (<link rel="icon" href="./image/Hulk.jpg">)
    + preconnect    : 
- href  : gắn một liên kết là URL vào file html.
```
# Box Container (phần khung chứa định ra bố cục trang web)
## header (định ra phần đầu cho website)
```bash
Có thể chứa logo và các thanh điều hướng.
```
## main (Chứa tất cả nội dung của một website)
```bash
Trong một tài liệu chỉ có duy nhất một thẻ main và thẻ main đó không được nằm trong các thẻ sau: 
    <article>, <aside>, <footer>, <header>, hoặc <nav>.
```
## article (Để định nghĩa các phần nội dung riêng biệt.)
```bash
Khi ta nhìn vào một thẻ article có thể biết được một phần nội dung chính nhưng không thể thấy hết toàn bộ nội dung.
```
## aside (định ra nội dung một bên sidebar và thường liên quan đến nội dung trong website)
```bash
Chức năng giống với article nhưng khác ở chỗ article định ra một phần nội dung chính có liên quan đến website. Aside định ra nội dung không liên quan đến weside. Định ra phần nội dung phụ.
```
## footer (Định ra phần cuối cùng trong văn bản)
## Thẻ hr (Định ra một đoạn kẻ gạch để ngăn cách các thẻ)
## br (ngắt dòng hiện tại và chuyển sang một dòng mới)
```bash
Thẻ br không có thẻ đóng. 
```
**Syn** 
```bash
<br> hoặc <br/>
```
# Box Detail (phần khung chứa content, định ra nội dùng tran web)
## nav (định ra các liên kết và các thanh điều hướng cho website)
## a (Để tạo liên kết, điều hướng tới trang khác, … )
**Syn**
```bash
<a href="" title="tôi là thuộc tính title" target='_blank'></a>

- href  : Chỉ định URL của trang liên kết đến. Dùng “#” khi chưa cần gán link điều hướng cho thẻ.
- target: Chỉ định nơi mở tài liệu được liên kết. 
    + _blank: Tài liệu được mở ở của số khác.
    + _parent
    + _self
    + _top
```
## div (Để định ra một phần nội dung, gom nhóm nội dung)
# Text
## h1 -> h6 (Định ra đoạn text tiêu đề)
```bash
Cỡ chữ giảm dần từ 1 đến 6. 
```
## p (Định dạng đoạn văn hay văn bản có trong trang web)
## span (định ra đoạn văn bản)
```bash
Mặc định là display: inline;
```
## pre (Định nghĩa ra đoạn văn bản giữ nguyên các khoảng trắng)
## b (Định dạng đoạn text sẽ được in đậm)
```bash
Chỉ làm chữ in đậm, không mang ý nghĩa ngữ nghĩa
```
## Thẻ strong (Nhấn mạnh, quan trọng về mặt ngữ nghĩa)
## i (Định dạng đoạn text sẽ được in nghiêng)
## em (Nhấn mạnh văn bản về mặt ngữ nghĩa, thường in nghiêng)
## small (Định nghĩa ra đoạn văn bản được hiển thị nhỏ hơn)
## mark (Định dạng đoạn text sẽ được tô thêm màu nền)
## del (Đoạn text đó sẽ có dấu gạch ngang ở giữa chữ)
## ins (Đoạn text xuất hiện trên trang web sẽ có dấu gạch dưới)
## sub (Đoạn text sẽ tụt xuống dưới giống như chỉ số hóa học)
## sup (Đoạn text biểu thị giống như số mũ )
## details & summary (Tạo một phần nội dung có thể mở hoặc đóng)
```bash
Thường kết hợp với thẻ summary. Để tạo tiêu đề cho thẻ details. Các thẻ bao ngoài nội dung
```
## blockquote (Định nghĩa một đoạn văn bản được trích dẫn từ một nguồn khác, nó sẽ tụt vào so với lề)
## q (Định nghĩa ra một đoạn text trích dẫn ngắn, thẻ này sẽ chèn một dấu nháy vào đoạn text)
## abbr (định nghĩa tên viết tắt hoặc bổ trợ ý nghĩa cho một đoạn text nào đó)
```bash
Thẻ abbr chủ yếu đi kèm với thuộc tính title.
    Di chuyển chuột vào chữ đó ta thấy “Lê Đức Thắng” hiện ra
```
## cite (Dùng để xác định tiêu đề của một việc. chữ sẽ được in nghiêng)
## bdo (định hướng văn bản)
```bash
Display: inline. Thường sử dụng với thuộc tính dir.
```
**Ex**
```html
<bdo dir=’ltr’>…</bdo>
<bdo dir=’rtl’>…</bdo>
```
## hgroup (để nhóm các thẻ h1 -> h6 vào cùng một nhóm. Với điều kiện chúng phải nằm cùng một thẻ cha)
## u (định dạng đoạn text hiển thị trên trang web sẽ có dấu gạch chân)
## s (định nghĩa đoạn text không còn chính xác nữa, đoạn text sẽ bị gạch giống thẻ del)
## acronym (Chức năng giống với thẻ abbr. không hỗ trợ ở phiên bản HTML 5)
## dialog (định nghĩa ra một hộp thoại hay một cửa số)
## bdi (phân lập một phần văn bản)
# Form (các thẻ định ra form)
## Input (Để lấy dữ liệu khi người dùng nhập vào)
**Syn**
```bash
<input 
    type=’file’ 
    accept='image/*' 
    value='' 
    name=''
    placeholder=''
>

- type : quy định chức năng của thẻ input đó.
    + text: tạo ra trường nhập văn bản.
    + password: trường nhập mật khẩu, các kí tự sẽ bị che đi bằng các ký tự *.
    + submit: tạo một nút bấm (để submit để nộp gửi lên form).
    + button: tạo một nút bấm.
    + checkbox: ô để tích.
    + Radio: ô để tích hình tròn.
    + Color: loại ô màu sác.
    + Date:
    + Time:
    + Search: tìm kiếm.
    + file: tạo ra trường thêm file.
    + range: tạo ra thanh kéo.
    + Week:
    + Number: kiểu số.
    + url: kiểu đường dẫn cho trang web.
    + email: kiểu email.
- accept : là thuộc tính của type=file, dùng để giới hạn loại file mà người dùng được chọn
    + image/* → nhóm MIME type của ảnh, tất cả định dạng ảnh
    + Cho phép: image/png, image/jpeg, image/jpg, image/webp, image/gif, image/svg+xml, … Không cho chọn: .exe, .pdf, .mp4, .zip
- value         : Để xác định giá trị mặc định cho ô đầu vào.   
- name          : Để xác tên cho ô đầu vào, dùng khi người dùng submit thông tin.
- placeholder   : Để đặt một văn bản mẫu cho ô đầu vào.
- required      : ô dữ liệu bắt buộc phải nhập trước khi submit file HTML lên sever.
- disabled      : Nếu giá trị là true thì đồng nghĩa người dùng không thể nhập hay thao tác với ô này.
- size          : Xác định độ rộng của ô đầu vào, giá trị là number + đơn vị
- max-length    : Xác định số kí tự tối đa mà người dùng được phép nhập vào ô
- min & max     : Xác định giá trị tối thiểu hay tối đa khi nhập ô đầu vào
- autocomplete  : Gợi ý các lựa chọn để người dùng nhập dữ liệu nhanh và dễ dàng hơn
- step          : Thường được sử dụng trong cá loại nhập số, dùng để xác định giá trị bước nhảy của ô
```
# button (Để tạo ra một nút bấm)
# Image & Video & Audio (ảnh và video)
## source (chỉ định tài nguyên đa phượng tiện cho các phần tử media)
## audio (định nghĩa đó là một file âm thanh)
```bash
Có 3 định dạng được hỗ trợ:
    - MP3
    - Wav
    - Ogg
```
**Ex**
```html
<audio src="partial-quran-recitation-from-juz-amma-344966.mp3" controls autoplay></audio>
```
## video (định nghĩa một video)
```bash
Nói cách khác nó sẽ nhúng một video vào trình duyệt.

Hiện nay, có 3 loại file video được hỗ trợ đó là: MP4, WebM, và Ogg.

Các trình duyệt hỗ trợ:
    - MP4: Chrome, Firefox, Opera, Safari, IE.
    - WebM: Chrome, Firefox, Opera.
    - Ogg: Chrome, Firefox, Opera.
```
## track (dùng để chèn một bản phụ đề vào video)
```bash
Nó không có thẻ đóng. File phụ đề phải có đuôi vtt
```
**Cách tạo một tập tin phụ đề**
```bash
Bước 1: Tạo một tập tin phụ đề.
    Mở notepad lên.
    Bấm vào tab "File" rồi chọn "Save As".
    Đặt tên cho tập tin xong rồi lưu lại.
    (Lưu ý: Endcoding chọn UTF-8, và tập tin phải có phần đuôi là .vtt)

Bước 2: Viết nội dung cho tập tin phụ đề.
    Nội dung của một tập tin phụ đề phải được tắt đầu bằng cụm từ WEBVTT
    Cách xác định thời điểm hiển thị phụ đề khá đơn giản, dưới đây là nội dung của tập tin phude.vtt
        WEBVTT

        00:00:00.500 --> 00:00:02.000
        ý !?

        00:00:02.000 --> 00:00:05.500
        Con bươm bướm kìa !

        00:00:06.000 --> 00:00:08.000
        Nó đẹp quá ba mẹ ơi =))

        00:00:09.000 --> 00:00:10.000
        Thế éo nào!? @_@
```
**Ex**
```html
<video controls style="width:100%">
    <source src="../file/bunny.mp4">
    <track src="../file/phude.vtt" default>
</video>
```
## img (Để thêm hình ảnh vào trang web)
```bash
Nó không có thẻ đóng.
```
## map (xác định bản đồ hình ảnh)
```bash
Bản đồ hình ảnh là một hình ảnh chứa các khu vục có thể nhấp được.
```
## picture (phép hiển thị nhiều hình ảnh khác nhau cho nhiều thiết bị hoặc kích thước màn hình thay đổi)
## figure (Để chỉ định nội dung khép kín, như hình minh họa, sơ đồ, ảnh, danh sách mã)
```bash  
display: block;
```
## figcaption (Định nghĩa tiêu đề cho một phần tử figure. Nằm trong thẻ figure)
## iframe (Chỉ định một nội dung định tuyến)
```bash 
Nó sử dụng để nhúng một tài liệu khác vào trang của bạn. tác dụng khá giống với thẻ img, khác biệt là ở chỗ nó sẽ nhúng một tài liệu thay vì chỉ nhúng một hình ảnh như thẻ img.
```
## frameset (xác định bộ khung cho thẻ frame)
## frame (dùng để nhúng một tài liệu nào đó vào trang web hiện tại)
```bash
(tài liệu ở đây rất đa dạng, có thể là một trang web khác, tập tin pdf, tấm hình, ....) phải được đặt bên trong phần tử <frameset>. Nó không có thẻ đóng
```
## object (định nghĩa một đối tượng được nhúng vào tài liệu HTML)
```bash
Sử dụng thẻ object để nhúng các tệp đa phương tiện (flash, âm thanh, video, PDF. v. v) vào trang của bạn. có thể nhúng một trang web khác vào trang của bạn. Nếu xem xét kỹ thì thực chất các thẻ, img, audio, iframe. v. v. đều có thể thay thế được bằng thẻ object.
```
## param (định nghĩa các tham số cho các plugin gắn với thẻ object)
```bash
Trong HTML 5 đã thêm vào hai thẻ mới để nhúng các file âm thanh, video đó là thẻ audio và thẻ video.
```
# Draw
## canvas
```bash
Bạn dùng <canvas> khi cần:
    - Vẽ hình động (animations)
    - Tạo trò chơi 2D
    - Vẽ biểu đồ, sơ đồ (chart, graph)
    - Xử lý ảnh (image processing)
    - Visualize dữ liệu hoặc AI (ví dụ như bounding box, filter ảnh)
```
**Ex** 
```html
<canvas id="myCanvas" width="400" height="200" style="border:1px solid #000000;"></canvas>
```
# List (Danh sách)
## ul & ol & li & dl & dt & dd
## select & option (Tạo danh sách xổ xuống danh sách này không dùng để điều hướng)
## fieldset & legend (để tạo ra khung bao quanh, nhóm các phần tử có liên quan vào cùng một nhóm)
## legend (để tạo tiêu đề cho thẻ fieldset. Thường kết hợp với thẻ fieldset)
## textarea (để tạo ra một vùng nhập dữ liệu nhiều dòng)
## datalist (xác định một danh sách có sẵn cho một phần tử )
# Table (Bảng)
## table (Để định nghĩa một bảng)
## caption (Để đặt tiêu đề cho một bảng)
```bash
thẻ <caption> phải được đặt ngay sau thẻ <table>. Chỉ có thể đặt một <caption> cho một thẻ <table>
```
## th (định nghĩa tiêu đề cho từng cột)
## tr (định nghĩa một hàng (dòng) trong bảng)
## td (Sẽ định nghĩa một ô tiêu chuẩn trong một bảng)
## colgroup (Xác định một nhóm của một hoặc nhiều cột trong bảng để phục vụ cho việc định dạng)
```bash
Sử dụng thẻ <colgroup> kết hợp với thẻ <col> để định dạng cho các cột. 
```
## col (Chỉ định thuộc tính cho mỗi cột)
```bash
Thẻ <col> đặc biết hữu ích trong việc áp dụng kiểu cho toàn bộ các cột thay vì phải lặp lại cho từng ô, từng hàng. Thẻ này không có thẻ đóng. 
```
## colspan (Để gộp cột)
## rowspan (Nhóm cột theo chiều dọc)
# Progress
## meter (biểu diễn số dưới dạng thước đo)
## progress (thể hiện quá trình của một tác vụ)

# Data Attribute (Tự tạo ra thuộc tính riêng của mình)
**Syn**
```bash
data-*
data-* = “”
```
## style data Attribute (Để viết CSS cho phần tử HTML dựa và thuộc tính và giá trị của chúng) 
```bash
Giá trị thuộc tính không phân biệt chữ hoa, chữ thường.
```
**Syn**
```bash
[data-* = “”]{}
```
**Ex**
```html
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
```
# attr()
```html
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
```