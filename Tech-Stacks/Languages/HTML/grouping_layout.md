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

### div
Để định ra một phần nội dung, gom nhóm nội dung.

### main
Chứa tất cả nội dung của một website. Trong một tài liệu chỉ có duy nhất một thẻ main và thẻ main đó không được nằm trong các thẻ sau: <article>, <aside>, <footer>, <header>, hoặc <nav>.

### header
Để bao quanh và định ra phần đầu tiên cho website. Có thể chứa logo và các thanh điều hướng.

### nav
Để bao quanh và định ra các liên kết và các thanh điều hướng cho website. 

### section
Thường định để bao bọc lấy các nội dung con trong trang web và có thể sử dụng nhiều thẻ section trong trang web. Khi ta nhìn vào một thẻ section thì ta có thể nhìn thấy toàn bộ nội dung mà thẻ đó truyền tải.

### article
Để định nghĩa các phần nội dung riêng biệt. Khi ta nhìn vào một thẻ article có thể biết được một phần nội dung chính nhưng không thể thấy hết toàn bộ nội dung.

### aside
Để bao quanh và định ra nội dung một bên sidebar và thường liên quan đến nội dung trong website. Chức năng giống với article nhưng khác ở chỗ article định ra một phần nội dung chính có liên quan đến website. Aside định ra nội dung không liên quan đến weside. Định ra phần nội dung phụ.

### footer
Định ra phần cuối cùng trong văn bản.