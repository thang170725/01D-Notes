- [useRef](#useref)
---
# useRef
```bash
- Lưu dữ liệu nội bộ, không vẽ lại
- dùng cho dữ liệu xử lý frontend, không cần rerender”. Không cần backend hay frontend gì cả — chỉ cần không muốn render lại là dùng useRef
- Không dùng để hiển thị -> dùng useRef
```
## .current
**Khi bạn có**
```js
const dropdownRef = useRef(null);
console.log(dropdownRef.current); // null
```
**Sau khi UI render xong (trong useEffect)**
```js
useEffect(() => {
  console.log(dropdownRef.current);
}, []);

{/* <div class="m-0.5 rounded-full w-auto ...">
  ...
</div> */}
```
### current.contains()
```js
dropdownRef.current.contains(e.target) // true / false
```