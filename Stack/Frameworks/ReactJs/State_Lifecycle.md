- [useState()](#usestate)
- [useEffect](#useeffect)
---
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