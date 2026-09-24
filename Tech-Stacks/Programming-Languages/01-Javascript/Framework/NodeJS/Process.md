- [require()](#require)
  - [createServer()](#createserver)
    - [.write()](#write)
    - [.url](#url)
    - [.setHeader()](#setheader)
    - [.readFile()](#readfile)
    - [.end()](#end)
  - [listen()](#listen)
---
# require()
```bash
Dùng để import module
```
**Syn**
```bash
const http = require("http");

- http: module có sẵn của NodeJS
```
**Ex: Tạo server**
```js
const http = require("http");

// Tạo server
const server = http.createServer((req, res) => {
    res.write("Hello from NodeJS Server!");
    res.end();
});

// Cho server chạy ở cổng 3000
server.listen(3000, () => {
    console.log("Server đang chạy tại http://localhost:3000");
});

// Trong terminal: node server.js
// Kết quả giả định (Terminal): Server đang chạy tại http://localhost:3000
// Mở trình duyệt: http://localhost:3000
// Kết quả giả định (Trình duyệt): Hello from NodeJS Server!
```
## createServer()
```bash
Dùng để  tạo server
```
**Syn**
```bash
http.createServer((req, res) => {})

- req = request (thông tin người gửi lên)
- res = response (thứ mình gửi lại cho người dùng)
```
### .write()
```bash
Gửi nội dung về cho trình duyệt
```
**Ex**
```js
res.write("Hello from NodeJS Server!");
```
### .url
```bash
Lấy URL người dùng truy cập
```
**Ex**
```js
const http = require("http");

const server = http.createServer((req, res) => {

    // Lấy URL người dùng truy cập
    const url = req.url;

    if (url === "/") {
        res.write("Trang chu");
        res.end();
    }
    else if (url === "/about") {
        res.write("Trang gioi thieu");
        res.end();
    }
    else if (url === "/contact") {
        res.write("Trang lien he");
        res.end();
    }
    else {
        res.write("404 - Khong tim thay trang");
        res.end();
    }

});

server.listen(3000, () => {
    console.log("Server dang chay tai http://localhost:3000");
});
```
### .setHeader()
```bash
Báo cho trình duyệt biết đây là gì
```
**Syn**
```bash
res.setHeader("Content-Type", "text/html")

- ("Content-Type", "text/html"): báo cho trình duyệt biết đây là html
```
**Ex**
```js
const http = require("http");

const server = http.createServer((req, res) => {

    const url = req.url;

    // Quan trọng: báo cho trình duyệt biết đây là HTML
    res.setHeader("Content-Type", "text/html");

    if (url === "/") {
        res.write(`
            <html>
                <head>
                    <title>Trang chu</title>
                </head>
                <body>
                    <h1>Trang chu</h1>
                    <p>Chao mung ban den voi NodeJS</p>
                </body>
            </html>
        `);
        res.end();
    }
    else {
        res.write(`
            <html>
                <body>
                    <h1>404 - Khong tim thay trang</h1>
                </body>
            </html>
        `);
        res.end();
    }

});

server.listen(3000, () => {
    console.log("Server dang chay tai http://localhost:3000");
});
```
### .readFile()
```bash
const http = require("http");
const fs = require("fs");

const server = http.createServer((req, res) => {

    res.setHeader("Content-Type", "text/html");

    if (req.url === "/") {

        // Đọc file index.html
        fs.readFile("index.html", (err, data) => {

            if (err) {
                res.write("Loi doc file");
                res.end();
            } else {
                res.write(data);
                res.end();
            }

        });

    } else {
        res.write("<h1>404 - Not Found</h1>");
        res.end();
    }

});

server.listen(3000, () => {
    console.log("Server dang chay tai http://localhost:3000");
});
```
### .end()
```bash
Kết thúc response
```
## listen()
```bash
dùng để  tạo cổng chạy server 