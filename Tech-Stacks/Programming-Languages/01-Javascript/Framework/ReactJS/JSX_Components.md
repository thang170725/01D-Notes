- [React JSX](#react-jsx)
- [Components](#components)
- [Props](#props)
---
# React JSX
```bash
- Cho phép viết các đoạn mã HTML trong React một cách dễ dàng và có cấu trúc hơn. React sử dụng JSX để xây dựng bố cục thay vì javascript thông thường. JSX giúp tạo ra các React element.
- JSX giúp cho việc xây dựng các ứng dụng một cách nhanh hơn, dễ tối ưu trong việc biên soạn code sang js.
- JSX dễ xem lỗi trong quá trình triển khai bởi hầu hết các lỗi sẽ được hiển thị trong quá trình biên soạn, không như các đoạn mã HTML có thể thừa thiếu các thẻ khiến trình biên dịch hiển thị sai. JSX thì hoàn toàn ngược lại nó sẽ hiển thị lỗi.
- Cú pháp khá giống với HTML nên dễ dàng cho việc chuyển đổi.
Nếu code React trong file HTML. Phải lick thư viện Babel vào HTML. Tạo ra biến gắn tất cả thẻ giống như gán biến bằng thẻ. Tất cả các code js ở trong {}, {{}}, ‘’, “”. Phải lấy link JSX code mới chạy được và thêm type=”text/babel”.
```
# Components
```bash
- Là đoạn mã độc lập và có thể tái sử dụng. Chúng có mục đích như các hàm Javascript nhưng hoạt động riêng biệt và trả về HTML.
- Component có hai loại: Class components và Function components.
- Hiện tại người ta đề xuất sử dụng Function components cùng với Hooks.
```
**Ex1: Class components**
```bash
import React from "react";
import ReactDOM from "react-dom/client";

class Car extends React.Component {
  render() {
    return <h2>Hi, I am a Car!</h2>;
  }
}

const container = document.getElementById("root");
const root = ReactDOM.createRoot(container);
root.render(<Car/>);
```
**Ex2: Functions components**
```js
import React from "react";
import ReactDOM from "react-dom/client";

function Car() {
    return <h2>Hi, I am a Car!</h2>;
}

const container = document.getElementById("root");
const root = ReactDOM.createRoot(container);
root.render(<Car/>);
```
# Props
```bash
- Là các đối số được truyền vào các thành phần React. 
- Props được truyền vào các thành phần thông qua các thuộc tính HTML. Props là viết tắt của properties.
```
**Ex**
**src/App.jsx**
```js
function User(props){
  return <p>{props.name} - {props.age}</p>
}

export default function App() {
  return (
    <>
      <User name="Thắng" age={22}/>
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