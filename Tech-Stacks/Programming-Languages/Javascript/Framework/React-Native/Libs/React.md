- [Context](#context)
  - [createContext (tạo ra một Context có thể tưởng tượng như một kho dữ liệu chung)](#createcontext-tạo-ra-một-context-có-thể-tưởng-tượng-như-một-kho-dữ-liệu-chung)
    - [.Provider (Bỏ dữ liệu vào hộp)](#provider-bỏ-dữ-liệu-vào-hộp)
  - [useContext (lấy dữ liệu từ trong hộp)](#usecontext-lấy-dữ-liệu-từ-trong-hộp)
- [useState()](#usestate)
- [useEffect()](#useeffect)
---
# Context
**Ex1: Không dùng Context**
```bash
Giả sử bạn có ứng dụng như sau:
    App
    │
    ├── Home
    │    ├── Header
    │    │      └── Avatar
    │    └── ProductList
    │
    └── Setting

Người dùng đăng nhập
    const user = {
        name: "Thắng",
        avatar: "avatar.png"
    }

Bây giờ component
    Avatar

    muốn biết
        user.name
    thì phải truyền như thế này.

App
function App() {
    const user = {
        name: "Thắng"
    };

    return <Home user={user} />;
}

↓

Home nhận

function Home({ user }) {
    return <Header user={user} />;
}

↓

Header nhận

function Header({ user }) {
    return <Avatar user={user} />;
}

↓

Avatar

function Avatar({ user }) {
    return <Text>{user.name}</Text>;
}

Bạn thấy gì không?

App
↓

Home
↓

Header
↓

Avatar

Chỉ có

Avatar

cần user.

Nhưng

Home

và

Header

vẫn phải nhận rồi truyền tiếp.

Đó gọi là

Prop Drilling

Context sinh ra để giải quyết việc này

Thay vì truyền qua từng tầng

App

↓

Home

↓

Header

↓

Avatar

ta sẽ tạo một "kho dữ liệu chung".

           Context

          user

      name = Thắng

             ▲
             │

App

↓

Home

↓

Header

↓

Avatar

Lúc này

Avatar muốn lấy user

↓

đọc thẳng từ Context.

Không cần Home và Header truyền nữa.
```
## createContext (tạo ra một Context có thể tưởng tượng như một kho dữ liệu chung)
**Syn**
```bash
import { createContext } from "react";

const UserContext = createContext();
# Đến đây Context vẫn rỗng.
# Giống như tạo một cái hộp.
# ┌──────────────┐
#  UserContext
# └──────────────┘
# Chưa có gì bên trong.
```
### .Provider (Bỏ dữ liệu vào hộp)
**Ex**
```js
<UserContext.Provider value={{ name: "Thắng" }}>
    <Home />
</UserContext.Provider>
// Lúc này
// ┌──────────────┐

// name = Thắng

// └──────────────┘
// đã có dữ liệu
```
## useContext (lấy dữ liệu từ trong hộp)
**Ex**
```js
import { useContext } from "react";

function Avatar() {
    const user = useContext(UserContext);

    return (
        <Text>{user.name}</Text>
    );
}
// user = {
//     name: "Thắng"
// }
```
# useState()
# useEffect()
