- [Introduction](#introduction)
- [Suspense](#suspense)
- [Lazy (dùng để load component một cách động (lazy load))](#lazy-dùng-để-load-component-một-cách-động-lazy-load)
- [Hook (dùng để "hook" (móc) vào các tính năng của React)](#hook-dùng-để-hook-móc-vào-các-tính-năng-của-react)
  - [useRef (Lưu dữ liệu nội bộ, không vẽ lại)](#useref-lưu-dữ-liệu-nội-bộ-không-vẽ-lại)
    - [.current (lấy giá trị của useRef)](#current-lấy-giá-trị-của-useref)
    - [current.contains()](#currentcontains)
  - [useState()](#usestate)
  - [useEffect](#useeffect)
- [createContext (dùng để chia sẻ dữ liệu giữa nhiều component mà không cần truyền props qua nhiều cấp)](#createcontext-dùng-để-chia-sẻ-dữ-liệu-giữa-nhiều-component-mà-không-cần-truyền-props-qua-nhiều-cấp)
- [Practices](#practices)
  - [Chia sẻ thông tin User bằng Context](#chia-sẻ-thông-tin-user-bằng-context)
---
# Introduction
```bash
- import React from "react" nghĩa là: “Lấy bộ công cụ React để dùng”.
- Ví dụ như bạn chơi LEGO:
  + React = hộp đồ nghề LEGO
  + Trong hộp có:
    - cách tạo khối
    - cách ghép khối
    - cách cập nhật khối
    - cách quản lý trạng thái
```
# Suspense
# Lazy (dùng để load component một cách động (lazy load))
```bash
- Lazy 
  + component chỉ được tải khi thực sự cần, thay vì tải toàn bộ ngay từ đầu.
  + Giúp:
    - Giảm kích thước bundle ban đầu
    - Tăng tốc độ load trang
    - Cải thiện performance
- Suspense dùng để  hiển thị fallback UI (loading) trong lúc chờ component lazy load xong.
```
**Ex**
```js
import Home from "./pages/Home";
import About from "./pages/About";

<Route path="/" element={<Home />} />
<Route path="/about" element={<About />} />
```
```js
import { lazy, Suspense } from "react";

const Home = lazy(() => import("./pages/Home"));
const About = lazy(() => import("./pages/About"));

function App() {
  return (
    <Suspense fallback={<div>Loading page...</div>}>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
      </Routes>
    </Suspense>
  );
}

// Chỉ load page khi user truy cập
// Giảm bundle size ban đầu
// Cải thiện tốc độ load lần đầu
// App scale tốt hơn khi nhiều trang
```
# Hook (dùng để "hook" (móc) vào các tính năng của React)
**Tại sao gọi là "Hook"?**
```bash
Hook nghĩa đen là "cái móc".

React cung cấp rất nhiều tính năng:
  - State
  - Lifecycle
  - Context
  - Ref
  - Reducer
  - ...
=> Hook chính là cách để "móc" component vào các tính năng đó.

Ví dụ
  useState()
  ↓
  Móc component vào hệ thống State.
```
## useRef (Lưu dữ liệu nội bộ, không vẽ lại)
```bash
Dùng cho dữ liệu xử lý frontend, không cần rerender”. Không cần backend hay frontend gì cả — chỉ cần không muốn render lại là dùng useRef

Không dùng để hiển thị -> dùng useRef
```
**Syn**
```bash
const intervalRef = useRef(null);

- Output: 
  {
      current: null
  }
```
### .current (lấy giá trị của useRef)
**Ex**
```js
const myRef = useRef(100);

console.log(myRef);
// {
//     current: 100
// }

console.log(myRef.current); // 100
```
**Sau khi UI render xong (trong useEffect)**
```js
useEffect(() => {
  console.log(dropdownRef.current);
}, []);

{/* <div class="m-0.5 rounded-full w-auto ...">
  ...
</div> */}
```
### current.contains()
```js
dropdownRef.current.contains(e.target) // true / false
```
## useState()
```bash
- Dữ liệu thay đổi theo thời gian
- React sẽ tự re-render khi state thay đổi. State đổi → UI tự đổi
- Cái nào ảnh hưởng đến UI dùng useState.
```
**Ex**
**src/App.jsx**
```js
import { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Bạn đã bấm {count} lần</p>
      <button onClick={() => setCount(count + 1)}>
        Bấm tôi
      </button>
    </div>
  );
}

export default function App() {
  return (
    <>
      <Counter/>
    </>
  )
}
```
**src/main.jsx**
```js
import { StrictMode } from 'react'
import { createRoot } from 'react-dom/client'
import App from './App.jsx'

createRoot(document.getElementById('root')).render(
  <StrictMode>
    <App />
  </StrictMode>
)
```
**Ex2: Realtime**
**src/App.jsx**
```js
import { useState } from "react"

export default function App() {
  const [name, setName] = useState("")

  return (
    <>
      <input 
        type="text"
        onChange={(e) => setName(e.target.value)}
      />
      <p>Hello {name}</p>
    </>
  )
}
```
## useEffect
```bash
- Làm viện phụ sau khi vẽ UI.
- useEffect = chạy code sau khi render xong
```
**syn**
```bash
useEffect(<function>, <dependency>)	
```
# createContext (dùng để chia sẻ dữ liệu giữa nhiều component mà không cần truyền props qua nhiều cấp)
**Syn**
```bash
import { createContext } from "react";

const MyContext = createContext(defaultValue);
```
# Practices
## Chia sẻ thông tin User bằng Context
**Bước 1: Tạo Context**
```js
// UserContext.jsx

import { createContext } from "react";

export const UserContext = createContext(null);
```
**Bước 2: Bọc Provider**
```js
// App.jsx

import { UserContext } from "./UserContext";
import Home from "./Home";

function App() {
  const user = {
    name: "Thắng",
    age: 22
  };

  return (
    <UserContext.Provider value={user}>
      <Home />
    </UserContext.Provider>
  );
}

export default App;
// Ở đây:
// value={user}
// nghĩa là mọi component bên trong đều có thể truy cập user.
```
**Bước 3: Component con sử dụng**
```js
// Home.jsx

import Profile from "./Profile";

function Home() {
  return (
    <div>
      <Profile />
    </div>
  );
}

export default Home;
```
```js
// Profile.jsx

import { useContext } from "react";
import { UserContext } from "./UserContext";

function Profile() {
  const user = useContext(UserContext);

  return (
    <div>
      <h2>{user.name}</h2>
      <p>{user.age}</p>
    </div>
  );
}

export default Profile;

// Không cần truyền:
// App
//  └── Home
//       └── Profile
// không cần
// <Home user={user} />
// <Profile user={user} />
```
Ví dụ 2: Dark Mode
ThemeContext
import { createContext } from "react";

export const ThemeContext = createContext("light");
App
import { ThemeContext } from "./ThemeContext";
import Header from "./Header";

function App() {
  return (
    <ThemeContext.Provider value="dark">
      <Header />
    </ThemeContext.Provider>
  );
}

export default App;
Header
import { useContext } from "react";
import { ThemeContext } from "./ThemeContext";

function Header() {
  const theme = useContext(ThemeContext);

  return (
    <div
      style={{
        background: theme === "dark" ? "#333" : "#fff",
        color: theme === "dark" ? "#fff" : "#000",
      }}
    >
      Header
    </div>
  );
}

export default Header;
Ví dụ 3: Context có state

Đây là cách dùng phổ biến nhất.

// CounterContext.jsx

import { createContext, useState } from "react";

export const CounterContext = createContext();

export function CounterProvider({ children }) {
  const [count, setCount] = useState(0);

  return (
    <CounterContext.Provider
      value={{
        count,
        setCount,
      }}
    >
      {children}
    </CounterContext.Provider>
  );
}

App

import { CounterProvider } from "./CounterContext";
import Counter from "./Counter";

function App() {
  return (
    <CounterProvider>
      <Counter />
    </CounterProvider>
  );
}

Counter

import { useContext } from "react";
import { CounterContext } from "./CounterContext";

function Counter() {
  const { count, setCount } = useContext(CounterContext);

  return (
    <div>
      <h2>{count}</h2>

      <button onClick={() => setCount(count + 1)}>
        +
      </button>

      <button onClick={() => setCount(count - 1)}>
        -
      </button>
    </div>
  );
}

Ở đây tất cả component sử dụng CounterContext sẽ nhận cùng một giá trị count. Khi setCount được gọi, các component đang dùng context sẽ tự động re-render để hiển thị giá trị mới.

Khi nào nên dùng createContext?

Nên dùng khi có dữ liệu được chia sẻ ở nhiều nơi trong cây component, ví dụ:

Thông tin người dùng sau khi đăng nhập (user)
Theme (light/dark)
Ngôn ngữ (i18n)
Giỏ hàng (cart)
Token hoặc trạng thái xác thực (auth)
Cài đặt chung của ứng dụng

Nếu chỉ cần truyền dữ liệu qua 1–2 cấp component thì truyền props thường đơn giản và dễ theo dõi hơn.

Luồng hoạt động
createContext()
       │
       ▼
<MyContext.Provider value={...}>
       │
 ┌─────┴───────────┐
 ▼                 ▼
Component A    Component B
       │
       ▼
useContext(MyContext)
       │
       ▼
Nhận dữ liệu từ Provider

Tóm lại:

createContext() tạo một "kênh" chia sẻ dữ liệu.
Provider cung cấp dữ liệu cho các component con.
useContext() đọc dữ liệu từ Provider gần nhất trong cây component mà không cần truyền qua nhiều lớp props.