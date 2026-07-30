# Installation
**Check (Kiểm tra)**
```bash
node -v
npm -v
npx -v (react native sử dụng npm react-native init … để khởi tạo project)
java -version
javac -version (nếu chưa có thì chạy lệnh sudo apt install openjdk-21-jdk)
```
**Build dự án bằng Expo CLI**
```bash
1. npm install -g expo-cli
2. expo –version
3. npx create-expo-app my-first-app
4. cd my-first-app
5. npx start (chạy app)
    - sau đó bấm a để chạy trên android studio
```
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