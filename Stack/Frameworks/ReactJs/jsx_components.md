- [React JSX](#react-jsx)
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
import React from "react";
import ReactDOM from "react-dom/client";

let myElement = <h1 id="greet">Welcome to ReactJs</h1>;

const container = document.getElementById("root");
const root = ReactDOM.createRoot(container);
root.render(myElement);

import React from 'react';
import ReactDOM from 'react-dom/client';

const myElement = <h1>I Love JSX!</h1>;

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(myElement);

import React from 'react';
import ReactDOM from 'react-dom/client';

const myElement = <h1>React is {5 + 5} times better with JSX</h1>;

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(myElement);

import React from 'react';import ReactDOM from 'react-dom/client';

const myElement = (
  <ul>
    <li>Apples</li>
    <li>Bananas</li>
    <li>Cherries</li>
  </ul>);

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(myElement);

import React from 'react';import ReactDOM from 'react-dom/client';
const myElement = (
    <>
      <p>I am a paragraph.</p>
      <p>I am a paragraph too.</p>
    </>
  );
const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(myElement);
<body>
  <div id="root">
    <p>I am a paragraph.</p>
    <p>I am a paragraph too.</p>
  </div>
</body>

React.createElement()
Để tạo ra đối tượng.
Cú pháp: React.createElement(value1, value2, value3);
    • Value1 là thẻ, function
    • Value2 là object
    • Value3 là nội dung
import React from 'react';
import ReactDOM from 'react-dom/client';

const myElement = React.createElement('h1', {}, 'I do not use JSX!');

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(myElement);
className
Để đặt tên class cho các thẻ HTML
import React from 'react';import ReactDOM from 'react-dom/client';

const myElement = <h1 className="myclass">Hello World</h1>;

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(myElement);
React Components
Là đoạn mã độc lập và có thể tái sử dụng. Chúng có mục đích như các hàm Javascript nhưng hoạt động riêng biệt và trả về HTML.
Component có hai loại: Class components và Function components.
Hiện tại người ta đề xuất sử dụng Function components cùng với Hooks.
Class components

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
Functions components

import React from "react";
import ReactDOM from "react-dom/client";

function Car() {
    return <h2>Hi, I am a Car!</h2>;
}

const container = document.getElementById("root");
const root = ReactDOM.createRoot(container);
root.render(<Car/>);


import React from "react";
import ReactDOM from "react-dom/client";

function Greet() {
    return <p>Good Morning</p>
}

function Name(){
    return (
        <>
            <Greet/>
            <p>My Name is John Doe</p>
            <p>welcome to VietNam</p>
        </>
    );

}
const container = document.getElementById("root");
const root = ReactDOM.createRoot(container);
root.render(<Name/>);

Trong file Car.js

function Car() {
  return <h2>Hi, I am a Car!</h2>;}

export default Car;
import React from 'react';
import ReactDOM from 'react-dom/client';import Car from './Car.js';

const root = ReactDOM.createRoot(document.getElementById('root'));

root.render(<Car />);
Ví dụ
import React from "react";
import ReactDOM from "react-dom/client";

function Poem(){
  return <pre>
    <i>khi</i> con <mark>tu hú</mark> gọi bầy
    <b>lúa</b> chiêm đang chín trái cây ngọt dần
  </pre>;
}

function Form(){
  return (
    <>
      <p>H<sub>2</sub>+X<sup>2</sup></p>
    </>
  )
}

const results = <>
  <Poem/>
  <Form/>
</>

const root = ReactDOM.createRoot(document.getElementById('root'))
root.render(results)

# Props
```bash
- Là các đối số được truyền vào các thành phần React. Props được truyền vào các thành phần thông qua các thuộc tính HTML. Props là viết tắt của properties.
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

