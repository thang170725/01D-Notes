- [Axios](#axios)
  - [Installation](#installation)
  - [axios (gửi nhận dữ liệu từ API)](#axios-gửi-nhận-dữ-liệu-từ-api)
    - [axios.get() (lấy dữ liệu)](#axiosget-lấy-dữ-liệu)
    - [axios.post() (gửi dữ liệu)](#axiospost-gửi-dữ-liệu)
    - [axios.put()  (cập nhật dữ liệu)](#axiosput--cập-nhật-dữ-liệu)
    - [axios.delete() (xóa dữ liệu)](#axiosdelete-xóa-dữ-liệu)
---
# Axios 
```bash
- Trong Next.js, axios là thư viện dùng để gửi request HTTP đến API/server để lấy hoặc gửi dữ liệu.
- Nói đơn giản:
    + Frontend muốn lấy danh sách sản phẩm → dùng axios gọi API
    + Form đăng nhập → dùng axios gửi username/password
    + Upload file → dùng axios gửi file lên server
```
**Tại sao không dùng fetch mà lại dùng axios**
```bash
| Trường hợp        | Fetch           | Axios               |
| ----------------- | --------------- | ------------------  |
| Dự án Next.js mới | ✅ Rất hợp      | ⚠️ Không cần thiết  |
| App frontend lớn  | 😐 Hơi dài dòng | ✅ Tiện             |
| Interceptor token | Khó hơn         | ✅ Rất mạnh         |
| Auto JSON         | ❌ cần `.json()`| ✅ có sẵn           |
| Handle lỗi        | Hơi thủ công    | ✅ dễ               |
| Upload progress   | Khó             | ✅ dễ               |
| Timeout           | Phức tạp        | ✅ đơn giản         |

- Nên dùng fetch nếu:
    + Dùng Next.js 13+
    + Chủ yếu fetch data server-side
    + Muốn tận dụng cache/revalidate
    + Project nhỏ hoặc vừa
    + Không cần interceptor phức tạp
- Nên dùng axios nếu:
    + Frontend app lớn
    + Có nhiều auth token
    + Cần interceptors
    + Upload file/progress
    + Handle error tập trung
    + Team quen axios
```
## Installation
```bash
1. npm install axios hoặc yarn add axios
```
## axios (gửi nhận dữ liệu từ API)
**Ex1: Gọi API lấy dữ liệu người dùng**
```ts
// Ví dụ API: https://jsonplaceholder.typicode.com/users

Component Next.js
"use client";

import axios from "axios";
import { useEffect, useState } from "react";

export default function Home() {
  const [users, setUsers] = useState([]);

  useEffect(() => {
    axios
      .get("https://jsonplaceholder.typicode.com/users")
      .then((response) => {
        setUsers(response.data);
      })
      .catch((error) => {
        console.log(error);
      });
  }, []);

  return (
    <div>
      <h1>Danh sách user</h1>

      {users.map((user) => (
        <p key={user.id}>{user.name}</p>
      ))}
    </div>
  );
}
// Luồng hoạt động cực dễ hiểu
// Next.js app
//    ↓
// axios.get(...)
//    ↓
// Gửi request tới API
//    ↓
// API trả dữ liệu JSON
//    ↓
// response.data nhận dữ liệu
//    ↓
// setUsers(...) để hiển thị ra màn hình
// Kết quả

// Màn hình sẽ hiện:

// Danh sách user

// Leanne Graham
// Ervin Howell
// Clementine Bauch
// ...
```
### axios.get() (lấy dữ liệu)
**Syn**
```bash
axios.get("/api/users");
```
### axios.post() (gửi dữ liệu)
**Ex: Ví dụ đăng nhập**
```ts
axios.post("/api/login", {
  email: "abc@gmail.com",
  password: "123456",
});
```
### axios.put()  (cập nhật dữ liệu)
**Ex**
```ts
axios.put("/api/user/1", {
  name: "Thắng",
});
```
### axios.delete() (xóa dữ liệu)
**Ex**
```ts
axios.delete("/api/user/1");
```
