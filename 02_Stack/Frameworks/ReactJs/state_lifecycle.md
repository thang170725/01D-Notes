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
React elements
    • Sử dụng props giống như với attribute của thẻ html
    • 2 props class, for => className, htmlFor
    • Phải tuân theo quy ước có sẵn
React components
    • Sử dụng props giống như đối số cho component
    • Tự do đặt tên props
    • Đặt theo camelcase
    • Có thể bao gồm dấu gạch ngang
Chú ý:
    • Props “key” là props đặc biệt
    • Props cơ bản là đối số của component => props có thể là bất cứ kiểu dữ liệu gì
    • Sử dụng destructuring
    • Component do chúng ta định nghĩa phải viết in hoa kí tự đầu
    • Chọn component trong một object
    • Booleans, null and undefind không được render
    • Kết hợp toán tử logic để render theo điều kiện

SPA – single-Page Application (ứng dụng trang đơn hay ứng dụng một trang)
    • reactJS là 1 trang trong những thư viện tạo ra SPA
    • goohle, facebook, twitter đang sử dụng 
SPA, MPA (multi-Page Application)
SPA 
    • được cho là cách tiếp cận hiện đại hơn. 
    • Không yêu cầu tải lại trang trong quá trình sử dụng
MPA
    • là cách tiếp tận cổ điển hơn
    • tải lại trang trong quá trính sử dụng
so sánh SPA và MPA
SPA – CSR (client side rendering)
    • nhanh hơn khi sử dụng
    • phần lớn tài nguyên được tải trong lần đầu
    • trang chủ chỉ tải thêm dữ liệu mới khi cần
    • có phần font-end riêng biệt
    • không thân thiện với SEO như MPA
    • trải nghiệm trên thiết bị di động tốt hơn
    • dễ dàng tái sử dụng code
    • chia team phát triển song song
    • phát triển mobile app dễ dàng
    • phụ thuộc hoàn toàn vào Js
    • khi nhiều người sử dụng thì tốt hơn về phía sever
MPA – SSR (sever side rendering)
    • chậm hơn khi sử dụng
    • luôn tải lại trang 
    • font-end và back-end phụ thuộc vào nhau nhiều, được đặt trong cùng một dự án
    • có thể không cần Js
    • phù hợp khi không cần phát triển Web
Events
Giống như sự kiện của HTML DOM, React có thể thực hiện các hoạt động dựa trên sự kiện của người dùng.
React có cùng sự kiện với HTML.
Trình xử lý sự kiện được viết bên trong dấu ngoặc nhọn.

import React from "react";
import ReactDOM from "react-dom/client";

function Shoot(){
    const shoot = () => {
        alert("Great shot!");
    }
    return (
        <button onClick={shoot}>Take the shot!</button>
    )
}

const container = document.getElementById("root");
const root = ReactDOM.createRoot(container);
root.render(<Shoot />);

function Football() {
  const shoot = (a) => {
    alert(a);
  }

  return (
    <button onClick={() => shoot("Goal!")}>Take the shot!</button>
  );
}

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<Football />);

import React from 'react';
import ReactDOM from 'react-dom/client';

function Football() {
  const shoot = (a, b) => {
    alert(b.type);
  }

  return (
    <button onClick={(event) => shoot("Goal!", event)}>Take the shot!</button>
  );
}

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<Football />);
React Conditionals
function Goal(props) {
  const isGoal = props.isGoal;
  if (isGoal) {
    return <MadeGoal/>;
  }
  return <MissedGoal/>;
}

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<Goal isGoal={false} />);


function Garage(props) {
  const cars = props.cars;
  return (
    <>
      <h1>Garage</h1>
      {cars.length > 0 &&
        <h2>
          You have {cars.length} cars in your garage.
        </h2>
      }
    </>
  );
}

const cars = ['Ford', 'BMW', 'Audi'];
const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<Garage cars={cars} />);

function Goal(props) {
  const isGoal = props.isGoal;
  return (
    <>
      { isGoal ? <MadeGoal/> : <MissedGoal/> }
    </>
  );
}

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<Goal isGoal={false} />);
React Lists
Trong React, bạn sẽ hiển thị danh sách bằng một số loại vòng lặp.

import React from "react";
import ReactDOM from "react-dom/client";

function Car(props){
    return <li>{props.name}</li>
}

function Box(){
    const transportations = ["bike", "bus", "car", "train"];
    return (
        <ul>
            {transportations.map((n) => <Car name={n} />)}
        </ul>
    )
}

const container = document.getElementById("root");
const root = ReactDOM.createRoot(container);
root.render(<Box/>);
React Forms
React sử dụng biểu mẫu để cho phép người dùng tương tác với trang web.

React Memo
Sử dụng momo sẽ khiến React bỏ qua việc render một thành phần nếu props của nó không thay đổi. Điều này có thể cải thiện hiệu suất.
React CSS Styling
Có rất nhiều cách để định dạng React bằng CSS. 
React Sass Styling
Là một bộ tiền xử lý CSS, được thực thi trên máy chủ và gửi CSS đến trình duyệt.
Để cài đặt sass: npm i sass
React Hooks
Hooks đã được thêm vào React trong phiên bản 16.8
Hooks cho phép các thành phần hàm cos quyền truy cập vào trạng thái và các tính năng React khác. Vì lý do này, các thành phần lớp thường không cần thiết nữa.
Hook thường thay thế các thành phần lớp, nhưng không có hoạch xóa lớp khỏi React.
useState
Cho phép chúng ta theo dõi trạng thái trong một thành phần hàm.
Trạng thái thường đề cập đến dữ liệu hoặc thuộc tính cần theo dõi trong một ứng dụng.
# useEffect
```bash
- Làm viện phụ sau khi vẽ UI.
- useEffect = chạy code sau khi render xong
```
**syn**
```bash
useEffect(<function>, <dependency>)	

```
useContent

useReducer
useMemo
Custom Hooks
map()
Dùng để lặp qua một mảng và hiển thị danh sách các phần tử trên giao diện.
Cú pháp: 
array.map((item, index) => {
  return <JSX_element />;
});
key={index}
Khi bạn render danh sách bằng .map(), bạn phải thêm các thuộc tính key để giúp React nhận biết và theo dõi các phần tử trong danh sách một cách hiệu quả.
React dùng key để biết phần tử nào thay đổi, thêm hoặc xóa khi render, tăng hiệu suất cập nhật DOM ảo
Ví dụ
Menu 1 cấp 
App.js
index.js
import React from "react";
import Menu from './index';
function App(){
  return (
    <div>
      <Menu />
      <h1>Nội dung chính</h1>
    </div>
  );
}

export default App;

import React from "react";
import ReactDom from 'react-dom/client'
import App from "./App";
const MenuItems = [
  {label: "Trang Chủ", link: '/'},
  {label: "Giới Thiệu", link: '/about'},
  {label: "Sản phẩm", link: '/products'},
  {label: "Liên Hệ", link: '/contact'}
];

const Menu = () => {
  return (
    <nav>
      <ul style={styles.menu}>
        {MenuItems.map((item, index) => (
          <li key={index} style={styles.MenuItems}>
            <a href={item.link} style={styles.link}>{item.label}</a>
          </li>
        ))}
      </ul>
    </nav>
  );
};

const styles = {
  menu: {
    display: 'flex',
    listStyle: 'none',
    padding: 0,
    margin: 0,
    backgroundColor: '#333'
  },
  MenuItems: {
    padding: '10px 20px',
  },
  link: {
    color: 'white',
    textDecoration: 'none',
  },
};

export default Menu;

const root = ReactDom.createRoot(document.getElementById('root'));
root.render(<App/>)
React Exercises