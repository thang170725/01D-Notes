- [Giới thiệu](#giới-thiệu)
- [Cấu trúc](#cấu-trúc)
- [Kiểm tra react đã được thêm vào dự án hay chưa](#kiểm-tra-react-đã-được-thêm-vào-dự-án-hay-chưa)
- [Upgrade to React 18](#upgrade-to-react-18)
- [Cấu trúc test \& luồng hoạt động](#cấu-trúc-test--luồng-hoạt-động)
---
# Giới thiệu
```bash
- ReactJS là một Framework để xây UI
- Mọi thứ = Component
- UI = hàm của state
    • Được đánh giá thân thiện với SEO
    • Khả năng mở rộng tốt, tái sử dụng cao
    • Hiệu suất cao
    • Phát triển nhanh chóng
    • Khả năng tương thích ngược
    • Tương lai sáng
- ReactJS được sử dụng để xây dụng ứng dụng 1 trang.
- React cho phép chúng ta tạo các thành phần UI có thể tái sử dụng.
- React là một khuôn khổ Javascript frontend, là một thư viên Javascript do FaceBook tạo ra.
```
# Cấu trúc
```bash
ReactJs/
├── 01_jsx_components.md     # Gom: JSX, Function Components, Props (Cơ bản)
├── 02_state_lifecycle.md    # Gom: useState, useEffect (Quản lý dữ liệu & Vòng đời)
├── 03_forms_events.md       # Handling events, Controlled vs Uncontrolled Components
├── 04_hooks_advanced.md     # useRef, useMemo, useCallback, Custom Hooks
├── 05_context_routing.md     # useContext (Global State), React Router
└── external_libs             # Chứa các thư viện bên ngoài 
```
**Chi tiết nội dung**
```bash
1. 01_jsx_components.md (Nền tảng)
Nội dung: Cú pháp JSX (viết HTML trong JS), cách tạo Component, và quan trọng nhất là Props.

Tại sao: Props chỉ là tham số truyền vào Component, nó rất đơn giản nên không cần tách riêng 1 folder. Để cạnh JSX sẽ giúp bạn thấy được cách dữ liệu truyền từ cha xuống con.

2. 02_state_lifecycle.md (Linh hồn của React)
Nội dung: useState (biến có khả năng render lại giao diện) và useEffect (xử lý side-effects như gọi API).

Lưu ý: Hãy ghi chú rõ quy tắc "Không thay đổi State trực tiếp" (Immutability) tại đây.

3. 03_forms_events.md (Tương tác)
Nội dung: Cách bắt sự kiện onClick, onChange trong React. Cách quản lý dữ liệu trong thẻ <input> (Controlled Components).

Tại sao: Phần này rất hay dùng nên tách riêng giúp bạn tra cứu nhanh khi làm Form đăng ký/đăng nhập.

4. 04_hooks_advanced.md (Tối ưu hiệu năng)
Nội dung: useMemo, useCallback (tránh render thừa), useRef (truy cập trực tiếp DOM).

Tại sao: Đây là phần ranh giới giữa Junior và Middle. Khi app của bạn chạy chậm, bạn sẽ mở file này lên để tìm cách tối ưu.

5. 05_context_routing.md (Cấu trúc App lớn)
Nội dung: useContext để truyền dữ liệu xuyên nhiều tầng mà không cần Props. Cách chia trang web với React Router.
6. external_libs
  + Nơi chức các thư viện bên ngoài của reactJS
---


# React hoạt động như thế nào?
Thay vì thao tác trức tiếp DOM của trình duyệt, React tạo ra một DOM ảo trong bộ nhớ, nơi nó thực hiện tất cả các thao tác cần thiết, trước khi thức hiện các thay đổi trong DOM của trình duyệt.

# Cài đặt ReactJS trên Linux & Khởi tạo
    1. sudo apt update
    2. sudo apt install curl -y
    3. curl --version
    4. curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
    5. source ~/.bashrc   # hoặc ~/.zshrc nếu dùng zsh
    6. nvm install --lts
    7. nvm use --lts
    8. npx create-react-app my-app
    9. cd my-app
    10. npm start
**Case2: 2024-2026**
```bash
1. npm create vite@latest react-basic -- --template react
2. cd react-basic
3. npm install
4. npm run dev
```
# Kiểm tra react đã được thêm vào dự án hay chưa
1. npx create-react-app my-app. my-app là tên dự án
2. cd my-app. 
3. npm list react – Kiểm tra version của dự án react. Nếu chưa có. Chạy lệnh npm install react react-dom.
4. npm start. ReactJs sẽ chạy dự án mặc định ở port 3000, ta có thể mở trình duyệt và truy cập đường dẫn http://localhost:3000.

# Upgrade to React 18
Để nâng cấp phiên bản của react lên phiên bản mới nhất.
Từ thư mục dự án gỡ lệnh: npm i react@latest react-dom@latest

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
