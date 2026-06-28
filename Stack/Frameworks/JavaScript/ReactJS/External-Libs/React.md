- [Introduction](#introduction)
- [Suspense](#suspense)
- [Lazy (dùng để load component một cách động (lazy load))](#lazy-dùng-để-load-component-một-cách-động-lazy-load)
- [Hook (dùng để "hook" (móc) vào các tính năng của React)](#hook-dùng-để-hook-móc-vào-các-tính-năng-của-react)
  - [useRef (Lưu dữ liệu nội bộ, không vẽ lại)](#useref-lưu-dữ-liệu-nội-bộ-không-vẽ-lại)
    - [.current (lấy giá trị của useRef)](#current-lấy-giá-trị-của-useref)
    - [current.contains()](#currentcontains)
- [useState()](#usestate)
- [useEffect](#useeffect)
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
# useState()
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
# useEffect
```bash
- Làm viện phụ sau khi vẽ UI.
- useEffect = chạy code sau khi render xong
```
**syn**
```bash
useEffect(<function>, <dependency>)	
```