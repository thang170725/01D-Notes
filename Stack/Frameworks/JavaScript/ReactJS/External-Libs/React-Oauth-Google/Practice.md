- [Quy trình sử dụng login google trong reactJS](#quy-trình-sử-dụng-login-google-trong-reactjs)
---
# Quy trình sử dụng login google trong reactJS
**Step 1: Vào https://console.cloud.google.com/**
```bash
1. Tạo project
2. Vào APIs & Services → Credentials
3. Create Credentials → OAuth Client ID
4. Chọn:
    - Web application
    - Thêm:
        + Authorized origins:
        + http://localhost:3000
    => Sau đó bạn sẽ có: CLIENT_ID = xxxxx.apps.googleusercontent.com
```
**Step 2: Bọc App bằng Provider**
```bash
import { GoogleOAuthProvider } from "@react-oauth/google";

<GoogleOAuthProvider clientId="YOUR_CLIENT_ID">
  <App />
</GoogleOAuthProvider>
```
**Step 3: Tạo nút login nhanh (Optional)**
```bash
import { GoogleLogin } from "@react-oauth/google";

<GoogleLogin
  onSuccess={(credentialResponse) => {
    console.log(credentialResponse);
  }}
  onError={() => {
    console.log("Login Failed");
  }}
/>
```
**Step 4: Decode user info**
```bash
1. npm install jwt-decode
2.
    import { jwtDecode } from "jwt-decode";
    const user = jwtDecode(credentialResponse.credential);

    console.log(user);
# bạn sẽ có 
# {
#   name: "Thắng",
#   email: "...",
#   picture: "...",
# }
```