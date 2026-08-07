- [axios Itroduction (Là thư viện giúp việc gọi API dễ hơn)](#axios-itroduction-là-thư-viện-giúp-việc-gọi-api-dễ-hơn)
- [Installation](#installation)
- [axios](#axios)
---
# axios Itroduction (Là thư viện giúp việc gọi API dễ hơn)
# Installation
```bash
npm install axios
```
# axios
```bash
Dùng:
import axios from "axios";const response = await axios.get("/users");console.log(response.data);

So sánh đơn giản
GET request
Fetch
const response = await fetch("/users");const data = await response.json();console.log(data);
Axios
const response = await axios.get("/users");console.log(response.data);
Axios ngắn hơn.

POST request
Fetch
await fetch("/users", {  method: "POST",  headers: {    "Content-Type": "application/json"  },  body: JSON.stringify({    name: "Thang"  })});

Axios
await axios.post("/users", {  name: "Thang"});
Axios tự:


JSON.stringify


Content-Type



Query Params
Fetch
const params = new URLSearchParams({  page: 1,  limit: 10});await fetch(`/users?${params}`);

Axios
await axios.get("/users", {  params: {    page: 1,    limit: 10  }});
Axios tiện hơn.

Xử lý lỗi
Đây là khác biệt quan trọng.
Fetch
const response = await fetch("/users");
Nếu API trả:
404
thì Fetch vẫn coi là thành công.
Bạn phải tự kiểm tra:
if (!response.ok) {  throw new Error("API Error");}

Axios
await axios.get("/users");
Nếu API trả:
404
Axios tự nhảy vào:
catch(error)
Ví dụ:
try {  await axios.get("/users");} catch (error) {  console.log(error.response.status);}

Interceptor (điểm mạnh lớn của Axios)
Giả sử mọi request đều cần token.
Axios
axios.interceptors.request.use((config) => {  const token = localStorage.getItem("token");  if (token) {    config.headers.Authorization = `Bearer ${token}`;  }  return config;});
Sau đó:
axios.get("/users");axios.get("/foods");axios.post("/meals");
Tự có token.

Fetch
Bạn phải tự viết wrapper giống cái JsonApi của bạn:
headers.Authorization = `Bearer ${token}`;
Thực chất bạn đang tự xây một phiên bản đơn giản của Axios.

Timeout
Axios
axios.get("/users", {  timeout: 5000});
5 giây không phản hồi là lỗi.

Fetch
Không có sẵn.
Phải dùng:
AbortController
khá dài dòng.

Upload file
Axios
const formData = new FormData();formData.append("image", file);await axios.post(  "/upload",  formData);
Rất đơn giản.

Fetch
Làm được nhưng thường phải xử lý nhiều thứ hơn.

Trong dự án React của bạn
Bạn đang có:
JsonApi()
bọc ngoài:
fetch()
Ví dụ:
await JsonApi("/users", {  params: {    page: 1  }});
Thực tế bạn đã thêm:


Authorization


params


error handling


JSON parsing


rồi.
Nghĩa là bạn đã giải quyết phần lớn nhược điểm của Fetch.

Khi nào dùng Fetch?
Mình thường dùng Fetch khi:


Dự án nhỏ


Không muốn cài thêm thư viện


React/Vite đơn giản


Có thể tự viết wrapper như bạn đang làm


Ví dụ:
JsonApi()FormDataApi()
là đủ.

Khi nào dùng Axios?
Thường dùng khi:


Dự án lớn


Nhiều API


Nhiều interceptor


Refresh token


Retry request


Timeout


Team nhiều người


Ví dụ:
api/ ├── axios.js ├── auth.js ├── meal.js ├── user.js
thì Axios khá tiện.

Kết luận
Với trình độ hiện tại và dự án React + FastAPI của bạn:


Hiểu kỹ fetch, Promise, async/await, URLSearchParams trước.


Wrapper JsonApi() hiện tại của bạn là hướng làm rất tốt.


Chưa cần chuyển sang Axios chỉ vì "nghe nói mạnh hơn".


Thực tế rất nhiều dự án production hiện nay vẫn dùng fetch + một wrapper giống hệt JsonApi của bạn. Khi bạn bắt đầu làm refresh token, interceptor phức tạp hoặc nhiều service hơn, lúc đó sẽ thấy rõ lợi ích của Axios.
```