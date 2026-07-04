- [Structure System](#structure-system)
  - [README.md (Hướng dẫn project)](#readmemd-hướng-dẫn-project)
  - [App.tsx (root component)](#apptsx-root-component)
  - [index.js (entry point)](#indexjs-entry-point)
  - [package.json](#packagejson)
  - [app.json (Thông tin ứng dụng)](#appjson-thông-tin-ứng-dụng)
  - [babel.config.js (Babel dùng để biên dịch JavaScript)](#babelconfigjs-babel-dùng-để-biên-dịch-javascript)
---
# Structure System
```bash
Cấu trúc của một dự án React Native phụ thuộc vào việc bạn dùng React Native CLI, Expo, hay framework như Expo Router. Tuy nhiên, đa số các dự án hiện nay đều có cấu trúc tương tự nhau.
```
**Ex: một dự án React Native được tổ chức theo hướng dễ mở rộng**
```bash
my-app/
│
├── android/                # Mã nguồn Android
├── ios/                    # Mã nguồn iOS
│
├── src/                    # Toàn bộ source code
│   ├── assets/
│   │   ├── images/
│   │   ├── fonts/
│   │   └── icons/
│   │
│   ├── components/
│   ├── screens/
│   ├── navigation/
│   ├── services/
│   ├── api/
│   ├── hooks/
│   ├── context/
│   ├── store/
│   ├── utils/
│   ├── constants/
│   ├── types/
│   ├── theme/
│   └── App.tsx | App.js
│
├── .gitignore
├── app.json
├── babel.config.js
├── metro.config.js
├── package.json
├── tsconfig.json
├── index.js
└── README.md
```
**Quy định file không đưa lên Git**
```bash
- node_modules/
- android/build/
- ios/build/
- .env
```
**Luồng hoạt động của ứng dụng**
```bash
Một ứng dụng React Native thường có luồng như sau:
    index.js
        │
        ▼
    App.tsx
        │
        ▼
    Providers
    (Auth, Redux, Theme...)
        │
        ▼
    Navigation
        │
        ▼
    Screen
        │
        ├── Components
        ├── Hooks
        ├── Services
        │      │
        │      ▼
        │     API
        │      │
        │      ▼
        │   Backend
        │
        └── Store / Context
```
## README.md (Hướng dẫn project)
1. android/
android/

Chứa toàn bộ project Android native.

Ví dụ:

android/
    app/
    gradle/
    build.gradle
    settings.gradle

Dùng khi:

build APK
cấu hình Firebase Android
thêm package native
thay đổi icon, splash screen native
cấu hình permissions

Nếu chỉ viết React Native bình thường thì rất ít khi phải đụng vào.

2. ios/
ios/

Tương tự Android.

Chứa project Xcode.

Dùng để:

build IPA
cấu hình Pod
Firebase iOS
Push Notification
Permission
3. src/

Đây là nơi chứa 100% code JavaScript/TypeScript của ứng dụng.

Ví dụ

src/

Bên trong thường chia như sau.

assets/

Chứa tài nguyên.

assets/
    images/
    fonts/
    icons/
    videos/

Ví dụ

assets/
    logo.png
    avatar.png
    background.jpg

Import

<Image source={require("../assets/logo.png")} />
components/

Các component dùng lại.

Ví dụ

components/
    Button.tsx
    Input.tsx
    Header.tsx
    Avatar.tsx
    Loading.tsx

Ví dụ Button

<Button
    title="Login"
    onPress={login}
/>

Không chứa logic nghiệp vụ lớn.

Chỉ chuyên hiển thị UI.

screens/

Mỗi màn hình là một Screen.

Ví dụ

screens/
    Home/
        HomeScreen.tsx

    Login/
        LoginScreen.tsx

    Profile/
        ProfileScreen.tsx

Một screen thường gồm:

UI
gọi API
xử lý dữ liệu
dùng component

Ví dụ

LoginScreen

    Header
    Input
    Password
    Button
navigation/

Quản lý điều hướng.

Ví dụ

navigation/
    AppNavigator.tsx
    AuthNavigator.tsx
    BottomTabs.tsx
    RootNavigator.tsx

Ví dụ

<NavigationContainer>

    <Stack.Navigator>

        <Stack.Screen
            name="Home"
        />

    </Stack.Navigator>

</NavigationContainer>
api/

Nơi gọi REST API.

Ví dụ

api/
    authApi.ts
    userApi.ts
    productApi.ts

Ví dụ

export const login = () => {
    return axios.post(...)
}

Không chứa UI.

services/

Đây là tầng xử lý.

Ví dụ

services/
    authService.ts
    storageService.ts
    notificationService.ts

Khác api ở chỗ:

API chỉ gọi server.

Service có thể:

gọi API
lưu AsyncStorage
xử lý dữ liệu
cache
validate

Ví dụ

login()

↓

api.login()

↓

saveToken()

↓

return user
hooks/

Custom Hook.

Ví dụ

hooks/
    useAuth.ts
    useTheme.ts
    useUser.ts

Ví dụ

const {user} = useAuth()
context/

Nếu dùng React Context.

context/
    AuthContext.tsx
    ThemeContext.tsx

Ví dụ

<AuthProvider>

    <App />

</AuthProvider>
store/

Nếu dùng:

Redux
Redux Toolkit
Zustand
MobX

Ví dụ

store/
    authSlice.ts
    userSlice.ts
    productSlice.ts
    index.ts
utils/

Các hàm tiện ích.

Ví dụ

utils/
    formatDate.ts
    currency.ts
    validate.ts

Ví dụ

formatMoney(1200000)

↓

1.200.000đ
constants/

Các hằng số.

Ví dụ

constants/
    Colors.ts
    Strings.ts
    Routes.ts

Ví dụ

export const API_URL = "...";
types/

Nếu dùng TypeScript.

types/
    user.ts
    auth.ts
    product.ts

Ví dụ

export interface User {

    id:number

    name:string

}
theme/

Quản lý giao diện.

theme/
    colors.ts
    typography.ts
    spacing.ts

Ví dụ

colors.primary

spacing.md
## App.tsx (root component)
```bash
Thường chỉ:
    - Provider
    - Navigation
    - Theme
    - Store
Không nên viết quá nhiều logic.
```
**Ex**
```js
function App(){
    return (
        <NavigationContainer>
            <RootNavigator/>
        </NavigationContainer>
    )
}
```
## index.js (entry point)
```bash
Đây là . React Native chạy file này đầu tiên.
```
## package.json
```bash
Ví dụ
    {
      "scripts": {
        "android": "...",
        "ios": "...",
        "start": "..."
      }
    }

Chứa
    - dependency
    - version
    - script
    - package

Ví dụ
    npm install
Đọc file này để biết cần cài gì.
```
## app.json (Thông tin ứng dụng)
**Ex**
```bash
{
    "name":"ShoppingApp",
    "displayName":"Shopping App"
}
```
## babel.config.js (Babel dùng để biên dịch JavaScript)
**Ex**
```js
module.exports = {
    presets: ['module:@react-native/babel-preset'],
};

Đôi khi dùng để cấu hình:
    - alias
    - plugin
    - metro.config.js
    - Cấu hình Metro Bundler.
```

Một số lưu ý về tổ chức dự án
Với dự án nhỏ, bạn có thể tổ chức theo loại thành phần (components, screens, services, hooks...) như ví dụ trên vì đơn giản và dễ hiểu.
Với dự án lớn, nhiều đội hiện nay thích tổ chức theo tính năng (feature-based), ví dụ:
src/
├── features/
│   ├── auth/
│   │   ├── api/
│   │   ├── components/
│   │   ├── hooks/
│   │   ├── screens/
│   │   └── types.ts
│   ├── profile/
│   └── products/
├── navigation/
├── shared/
│   ├── components/
│   ├── hooks/
│   ├── utils/
│   └── theme/

Cách này giúp mọi mã nguồn liên quan đến một tính năng nằm cùng một nơi, thuận tiện bảo trì khi dự án phát triển lớn.

Nếu bạn mới học React Native, mình khuyên bắt đầu với cấu trúc theo loại thành phần (components, screens, services, hooks...). Khi đã quen và ứng dụng có nhiều module, hãy chuyển dần sang cấu trúc theo tính năng để dễ mở rộng và quản lý hơn.
# [...] (Destructuring Array trong js)
Ví dụ

const arr = [10, 20];

Muốn lấy phần tử đầu tiên

const [a] = arr;

console.log(a);

Kết quả

10

Nếu

const result = useFonts(...);

thì

result

là

[true]

Nên người ta viết

const [fontsLoaded] = useFonts(...)

để lấy phần tử đầu tiên.