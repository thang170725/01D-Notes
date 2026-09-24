- [BrowserRouter (Bao toàn bộ app)](#browserrouter-bao-toàn-bộ-app)
- [Routes \& Route \& Link](#routes--route--link)
  - [NavLink](#navlink)
  - [useNavigate() (dùng để chuyển hướng (điều hướng) người dùng sang một route/trang khác bằng code JavaScript)](#usenavigate-dùng-để-chuyển-hướng-điều-hướng-người-dùng-sang-một-routetrang-khác-bằng-code-javascript)
---
# BrowserRouter (Bao toàn bộ app)
**Ex**
```js
import { BrowserRouter } from "react-router-dom";
import App from "./App";

createRoot(document.getElementById("root")).render(
  <BrowserRouter>
    <App />
  </BrowserRouter>
);
```
# Routes & Route & Link
```bash
- BrowserRouter	    : 
- Routes	          : Chứa danh sách route
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
## NavLink
```bash
- khi URL khớp với to. NavLink tự động cho trạng thái isActive.
- Dùng khi muốn khớp đường dẫn rồi làm gì đó
```
**Ex**
```js
import { NavLink } from "react-router-dom"

function SidebarItem({ to, label }) {
  return (
    <NavLink
      to={to}
      end
      className={({ isActive }) =>
        `
        flex justify-center gap-3 p-2 mb-1
        transition-all duration-300
        hover:bg-[oklch(50%_0.066_243.157)]
        ${
          isActive
            ? "border-r-4 border-red-700 bg-[oklch(50%_0.066_243.157)] font-semibold"
            : ""
        }
        `
      }
    >
      {label}
    </NavLink>
  )
}

export default SidebarItem
```
## useNavigate() (dùng để chuyển hướng (điều hướng) người dùng sang một route/trang khác bằng code JavaScript)
**Syn**
```bash
const navigate = useNavigate();

navigate("/home"); # chuyển người dùng đếm trang home
```
**Ex**
```js
// 1️⃣ Khai báo route
<Route path="/profile" element={<MyProfile />} />

// 2️⃣ DropdownItem giữ nguyên**
import { useNavigate } from "react-router-dom";

const navigate = useNavigate();
<DropdownItem
  icon={User}
  label="My Profile"
  onClick={() => navigate("/profile")}
/>
```