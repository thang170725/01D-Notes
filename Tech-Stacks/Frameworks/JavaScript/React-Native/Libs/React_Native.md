- [Platform (cho biết app đang chạy trên hệ điều hành nào)](#platform-cho-biết-app-đang-chạy-trên-hệ-điều-hành-nào)
  - [OS (trả về hệ điều hành)](#os-trả-về-hệ-điều-hành)
- [View (giống như div dùng để chứa các component khác)](#view-giống-như-div-dùng-để-chứa-các-component-khác)
- [Text (Dùng để hiển thị chữ)](#text-dùng-để-hiển-thị-chữ)
- [StyleSheet (Nó là một hàm để tạo style)](#stylesheet-nó-là-một-hàm-để-tạo-style)
- [ScrollView (Nó giống như một màn hình có thể kéo lên kéo xuống)](#scrollview-nó-giống-như-một-màn-hình-có-thể-kéo-lên-kéo-xuống)
- [TouchableOpacity (Đây là nút bấm)](#touchableopacity-đây-là-nút-bấm)
- [KeyboardAvoidingView](#keyboardavoidingview)
---
# Platform (cho biết app đang chạy trên hệ điều hành nào)
## OS (trả về hệ điều hành)
**Ex**
```js
Platform.OS // "android" hoặc "ios"
```
# View (giống như div dùng để chứa các component khác)
**Ex**
```js
<View>
    <Text>Hello</Text>
</View>
// ┌──────────────────────┐
// │                      │
// │       Hello          │
// │                      │
// └──────────────────────┘
```
**Ex: Thêm style**
```js
<View
    style={{
        backgroundColor: "red",
        padding: 20
    }}
>
    <Text>Hello</Text>
</View>
// ┌─────────────────┐
// │     Hello       │
// └─────────────────┘
```
# Text (Dùng để hiển thị chữ)
**Ex**
```js
<Text>Hello</Text>
```
# StyleSheet (Nó là một hàm để tạo style)
**Ex: Không dùng StyleSheet**
```js
<Text
    style={{
        fontSize:20,
        color:"red"
    }}
>
```
```bash
Nếu nhiều style
    ↓
rất dài.
```
**Ex2**
```js
const styles = StyleSheet.create({
    title:{
        fontSize:20,
        color:"red"
    }
});

<Text style={styles.title}>
    Hello
</Text>
```
# ScrollView (Nó giống như một màn hình có thể kéo lên kéo xuống)
```bash
Nếu không dùng ScrollView
↓
chỉ thấy
1
2
3
4
=> Các dòng dưới bị mất.

Có ScrollView
↓
Vuốt
1
2
3
4
↓
5
6
7
↓
20
↓
50
↓
100

Khi nào dùng?
    - Danh sách dài

Ví dụ
    - Tin tức
    - Facebook
    - Shopee
    - Danh sách sản phẩm
```
**Ex**
```js
import { ScrollView } from 'react-native';

<ScrollView>
    <Text>1</Text>
    <Text>2</Text>
    ...
    <Text>100</Text>
</ScrollView>
```
# TouchableOpacity (Đây là nút bấm)
**Ex**
```js
import { TouchableOpacity } from 'react-native';

<TouchableOpacity>
    <Text>Đăng nhập</Text>
</TouchableOpacity>
// ┌──────────────┐
// │ Đăng nhập    │
// └──────────────┘
```
**Ex2: Bắt sự kiện**
```js
<TouchableOpacity
    onPress={() => {
        console.log("Đã bấm");
    }}
>
    <Text>Click</Text>
</TouchableOpacity>
```
# KeyboardAvoidingView
```bash
Giả sử có màn hình
    - Email
    - Password
    - Đăng nhập

    Khi bấm vào Password
    ↓
    Bàn phím hiện lên.
        - Email
        - Password
    _____________
    
    ⌨⌨⌨⌨⌨⌨⌨⌨⌨

    Có thể che mất nút:Đăng nhập

    Nếu dùng
        <KeyboardAvoidingView>
            ...
        </KeyboardAvoidingView>
            ↓
        Khi bàn phím hiện
            ↓
        Nó tự đẩy giao diện lên.
```
**Ex**
```js
<KeyboardAvoidingView>
    <TextInput/>
    <TextInput/>
</KeyboardAvoidingView>
```