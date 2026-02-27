- [lucide-react](#lucide-react)
- [fontawesome](#fontawesome)
- [Recharts](#recharts)
- [Framer Motion](#framer-motion)
  - [AnimatePresence](#animatepresence)
---
# lucide-react
**installation**
```bash
npm install lucide-react
```
**website lấy icons**
```bash
1. https://lucide.dev/icons
```
# fontawesome
**Installation**
```bash
1. npm install @fortawesome/react-fontawesome
2. npm install @fortawesome/fontawesome-svg-core
3. npm install @fortawesome/free-solid-svg-icons
4. npm install @fortawesome/free-regular-svg-icons
5. npm install @fortawesome/free-brands-svg-icons
```
**Ex**
```js
import React from "react";
import { FontAwesomeIcon } from "@fortawesome/react-fontawesome";
import { faCoffee } from "@fortawesome/free-solid-svg-icons";

function App() {
  return (
    <div>
      <h1>Ví dụ Font Awesome</h1>
      <FontAwesomeIcon icon={faCoffee} />
    </div>
  );
}

export default App;
```
# Recharts
```bash
- Recharts là thư viện vẽ biểu đồ cho ReactJS, xây dựng dựa trên SVG và D3.
- Dùng để tạo:
  + Bar chart
  + Line chart
  + Pie chart
  + Area chart
  + Composed chart
  + Responsive chart
- https://recharts.org | https://recharts.org/en-US/examples
```
**Installation**
```bash
npm install recharts
```
**Ex: Line Chart**
```js
import {
  LineChart, Line, XAxis, YAxis,
  CartesianGrid, Tooltip, Legend
} from "recharts";

const data = [
  { name: "Jan", uv: 400 },
  { name: "Feb", uv: 300 },
  { name: "Mar", uv: 500 },
];

export default function MyChart() {
  return (
    <LineChart width={400} height={300} data={data}>
      <CartesianGrid strokeDasharray="3 3" />
      <XAxis dataKey="name" />
      <YAxis />
      <Tooltip />
      <Legend />
      <Line type="monotone" dataKey="uv" stroke="#8884d8" />
    </LineChart>
  );
}
```
# Framer Motion
```bash
- Là thư viện giúp bạn tạo animation mượt, dễ viết và chuyên nghiệp trong React.
- Nó dùng để:
  + Làm hiệu ứng xuất hiện / biến mất (fade in, fade out)
  + Làm animation khi hover, click
  + Làm chuyển trang
  + Làm sidebar trượt vào/ra
  + Làm drag & drop
  + Tạo layout animation (khi thay đổi vị trí phần tử)
```
**Installation**
```bash
1. npm install framer-motion
```
**Syn**
```bash
import { motion } from "framer-motion";

<motion.div>...</motion.div>

- `initial`    : Trạng thái ban đầu           
- `animate`    : Trạng thái khi chạy          
- `exit`       : Trạng thái khi unmount       
- `transition` : Thời gian & kiểu chuyển động 
- `whileHover` : Animation khi hover          
- `whileTap`   : Animation khi click          
- `variants`   : Tập hợp animation            
```
## AnimatePresence
```bash
- Giúp chạy animation khi component bị unmount (biến mất khỏi DOM)
```
**Ex**
```js
import { motion, AnimatePresence } from "framer-motion";

<AnimatePresence>
  {condition && (
    <motion.div
      initial={{ opacity: 0 }}
      animate={{ opacity: 1 }}
      exit={{ opacity: 0 }}
    />
  )}
</AnimatePresence>
```