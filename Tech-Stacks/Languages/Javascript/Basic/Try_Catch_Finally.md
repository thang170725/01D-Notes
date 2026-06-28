- [Try Catch Finally](#try-catch-finally)
  - [throw new Error()](#throw-new-error)
---
# Try Catch Finally
## throw new Error() 
```bash
- DỪNG ngay lập tức code trong try
- Tạo ra một object Error và chuyển sang catch
```
**Ex**
```js
// Khi bạn viết:
throw new Error("Tên không được để trống")

// Thì JS tạo ra object kiểu này:
// {
//   name: "Error",
//   message: "Tên không được để trống",
//   stack: "..."
// }

// Vì vậy trong catch:
catch (error) {
  setError(error.message)
}

// error.message chính là chuỗi bạn truyền vào new Error().
```