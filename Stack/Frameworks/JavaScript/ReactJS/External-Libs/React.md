- [Introduction](#introduction)
- [Suspense](#suspense)
- [Lazy (dùng để load component một cách động (lazy load))](#lazy-dùng-để-load-component-một-cách-động-lazy-load)
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
