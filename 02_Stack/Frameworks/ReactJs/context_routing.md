- [react-router-dom](#react-router-dom)
  - [BrowserRouter \& Routes \& Route \& Link](#browserrouter--routes--route--link)
  - [useNavigate()](#usenavigate)
---
# react-router-dom
```bash
- Để làm “chuyển trang” trong ứng dụng React
- React là SPA (Single Page Application) → KHÔNG reload trang như web truyền thống
- react-router-dom giúp:
    + Đổi URL (/login, /profile, /settings)
    + Nhưng vẫn ở cùng 1 trang HTML
    + React chỉ đổi component hiển thị
```
**Install**
```bash
1. npm install react-router-dom
```
## BrowserRouter & Routes & Route & Link
```bash
- BrowserRouter	    : Bao toàn bộ app
- Routes	        : Chứa danh sách route
- Route	            : Khai báo 1 đường dẫn
- Link	            : Chuyển trang KHÔNG reload
```
**Ex: (3 trang)**
**Cấu trúc**
```bash
App.jsx
Home.jsx
About.jsx
Login.jsx
```
```js
import { BrowserRouter } from "react-router-dom";
import App from "./App";

createRoot(document.getElementById("root")).render(
  <BrowserRouter>
    <App />
  </BrowserRouter>
);
```
**App.jsx**
```js
import { Routes, Route, Link } from "react-router-dom";
import Home from "./Home";
import About from "./About";
import Login from "./Login";

function App() {
  return (
    <div>
      {/* Menu */}
      <nav>
        <Link to="/">Home</Link> |{" "}
        <Link to="/about">About</Link> |{" "}
        <Link to="/login">Login</Link>
      </nav>

      {/* Nơi render page */}
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
        <Route path="/login" element={<Login />} />
      </Routes>
    </div>
  );
}

export default App;
```
**Route hoạt động thế nào?**
```bash
<Route path="/login" element={<Login />} />

Nếu URL là: /login
React render: <Login />
Không reload trang
Chỉ đổi component
```
**Link dùng để làm gì?**
```bash
Thay cho <a>
Sai (reload trang)      : <a href="/login">Login</a>
Đúng (SPA)              : <Link to="/login">Login</Link>
```
## useNavigate()
**1️⃣ Khai báo route**
```js
<Route path="/profile" element={<MyProfile />} />
```
**2️⃣ DropdownItem giữ nguyên**
```js
<DropdownItem
  icon={User}
  label="My Profile"
  onClick={() => navigate("/profile")}
/>
```
**3️⃣ Dùng useNavigate**
```js
import { useNavigate } from "react-router-dom";

const navigate = useNavigate();
```