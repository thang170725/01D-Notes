- [registerRootComponent (Đăng ký component gốc của ứng dụng)](#registerrootcomponent-đăng-ký-component-gốc-của-ứng-dụng)
---
# registerRootComponent (Đăng ký component gốc của ứng dụng)
```bash
Có thể hiểu như:
    Đây là component đầu tiên cần chạy
```
**Ex**
```js
import { registerRootComponent } from 'expo';
import App from './App';

registerRootComponent(App); // Đưa component App cho Expo để chạy
```
# Hook
## @expo-google-fonts/inter
### useFonts (tải font)
**Syn**
```bash
const [loaded] = useFonts({
    FontA,
    FontB
});
# hook trả về [true] hoặc [false]
```
# expo-status-bar
## StatusBar (thanh trên cùng của điện thoại)
```bash
Ví dụ Android
    - 12:00
    - Wifi
    - Pin
```