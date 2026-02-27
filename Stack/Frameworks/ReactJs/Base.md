- [Directory Structure](#directory-structure)
- [Introduction](#introduction)
- [Installation](#installation)
- [Cấu trúc test \& luồng hoạt động](#cấu-trúc-test--luồng-hoạt-động)
- [React.createElement()](#reactcreateelement)
- [className](#classname)
---
# Directory Structure
```bash
ReactJs/                    # mình dùng thư mục này để xem kiến thức cơ bản về ReactJS
├── JSX_Componentsd         # mình dùng file này để hiểu JSX, Function Components, Props (Cơ bản)
├── State_Lifecycle.md      # mình dùng file này để quản lý dữ liệu & Vòng đời
├── 03_forms_events.md      # Handling events, Controlled vs Uncontrolled Components
├── Hooks_Advanced.md       # mình dùng file này để sử dụng useRef, useMemo, useCallback, Custom Hooks
├── Context_Routing.md      # mình dùng file này để thao tác liên quan đến URL trên frontend
└── External_Libs           # mình dùng file này để chứa các thư viện bên ngoài 
```
# Introduction
```bash
- ReactJS là một Framework do FaceBook tạo ra để xây UI. Mọi thứ = Component
  + Khả năng mở rộng tốt, tái sử dụng cao
  + Hiệu suất cao
  + Phát triển nhanh chóng
  + Khả năng tương thích ngược
  + Tương lai sáng
- ReactJS được sử dụng để xây dụng ứng dụng 1 trang. React cho phép chúng ta tạo các thành phần UI có thể tái sử dụng.
- React hoạt động như thế nào?
  + Thay vì thao tác trức tiếp DOM của trình duyệt, React tạo ra một DOM ảo trong bộ nhớ, nơi nó thực hiện tất cả các thao tác cần thiết, trước khi thức hiện các thay đổi trong DOM của trình duyệt.
```
# Installation
**2024-2026**
```bash
1. npm create vite@latest react-basic -- --template react
2. cd react-basic
3. npm install
4. npm run dev | npm run dev -- --host
```
# Cấu trúc test & luồng hoạt động
Xem trong link này để hiểu rõ cấu trúc: [form-frontend](../../microservice/form.md)
**Flow Chart**
```bash
1. khi gõ npm start: sẽ gọi đến script trong package.json
  "start": "react-scripts start"
  - bật dev server
  - đọc public/index.html
  - tìm entry JS

2. public/index.html: của ngõ duy nhất
  trình duyệt chỉ thấy một div trống, react sẽ nhét toàn bộ app vào đây.
  React không chạy từ src/ trực tiếp

3. src/index.js: entry point
  Lấy <div id="root"> Render App component vào đó
  File này KHÔNG nên chứa logic → chỉ là “công tắc bật app”

4. src/App.jsx: root component, Component cao nhất
  Quản lý: layout tổng, router, provider (sau này)

5. pages/HomePage.jsx: 'Mỗi trang = 1 file' (Đại diện cho 1 màn hình)
  Gọi:
  - components
  - services
  KHÔNG chứa:
  - logic phức tạp
  - gọi API trực tiếp (nhiều)
  Nếu app có router → pages là nơi map route

6. components/: Cục gạch UI
  Chức năng: Component nhỏ, Tái sử dụng
  Không biết:
  - API ở đâu
  - state toàn cục
components không import services

7. services/: giao tiếp với backend
  Chức năng:
  - Gọi API
  - Trả data “sạch”
  UI KHÔNG fetch trực tiếp. Đổi backend → sửa 1 chỗ.

8. styles/ – STYLE TOÀN CỤC / MODULE
  Chức năng: CSS, theme, layout chung
  Không nhét CSS lung tung vào component khi project lớn

9. utils/ – CÔNG CỤ HỖ TRỢ
  Ví dụ:
  utils/
  └── formatDate.js
  Hàm nhỏ. Không phụ thuộc React
  Dùng cho: components, services

10. constants/ – HẰNG SỐ HỆ THỐNG
  export const API_URL = "http://localhost:8080";
  Tránh hard-code

11. hooks/ (chưa dùng)
  Custom hook: useUser(), useAuth()
  Logic React tái sử dụng

12. store/ (chưa dùng)
  State global: Redux, Zustand, Context
  Khi state vượt quá 2–3 component
```

**Ex**
**src/App.jsx**
```jsx
function Header() {
  return <h1>My App</h1>
}

function Content() {
  return <p>Welcome ReactJs</p>
}

function Footer() {
  return <footer>In the end</footer>
}

export default function App() {
  return (
    <>
      <Header />
      <Content />
      <Footer />
    </>
  )
}
```
**src/main.jsx**
```jsx
import { StrictMode } from 'react'
import { createRoot } from 'react-dom/client'
import App from './App.jsx'

createRoot(document.getElementById('root')).render(
  <StrictMode>
    <App />
  </StrictMode>
)
```





**src/components/Hello.jsx**
```jsx
export default function Hello({ name }) {
  return <h2>Hello {name} 👋</h2>;
}
```
**src/services/user.service.js**
```js
export function getUserMock() {
  return {
    id: 1,
    name: "Test User",
  };
}
```
**src/styles/main.css**
```css
body {
  font-family: sans-serif;
}
```
**Chạy app**
```bash
cd frontend/web-cra
npm start
```
# React.createElement()
```bash
Để tạo ra đối tượng.
```
**Syn** 
```bash
React.createElement(value1, value2, value3);

- Value1 là thẻ, function
- Value2 là object
- Value3 là nội dung
```
**Ex**
```js
import React from 'react';
import ReactDOM from 'react-dom/client';

const myElement = React.createElement('h1', {}, 'I do not use JSX!');

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(myElement);
```
# className
```bash
Để đặt tên class cho các thẻ HTML
import React from 'react';import ReactDOM from 'react-dom/client';

const myElement = <h1 className="myclass">Hello World</h1>;

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(myElement);
Phần 2
React Render HTML
React hiển thị HTML cho trang web bằng cách sử dụng hàm có tên là createRoot() và phương thức render.
createRoot()
Để lấy một đối số, một phần tử HTML.
Mục đích của hàm là xác định phần tử HTML nơi thành phần React sẽ được hiển thị.
render()
Được gọi để xác định thành phần React sẽ được hiển thị.
Hiển thị ở đâu?
Có một thư mục khác trong thư mục gốc của dự án React có tên là pubic trong thư mục này có một tệp là index.html
Bạn sẽ thấy một div duy nhất trong phần thân của tệp này. Đây là nơi ứng dụng React sẽ được hiển thị.

Cần vào thư mục dự án chạy lệnh npm start mới có thể mở trình duyệt.
import React from "react";
import ReactDOM from "react-dom/client";
const container = document.getElementById("root");
const root = ReactDOM.createRoot(container);
root.render(<div>hello world!!!</div>);

import React from 'react';
import ReactDOM from 'react-dom/client';

const myelement = (
  <table>
    <tr>
      <th>Name</th>
    </tr>
    <tr>
      <td>John</td>
    </tr>
    <tr>
      <td>Elsa</td>
    </tr>
  </table>
);

const container = document.getElementById('root');
const root = ReactDOM.createRoot(container);
root.render(myelement);
