# If else
```bash
if(điều_kiện){…}
else if(điều_kiện){…}
else{…}
```
JS Switch
switch case
switch(tham_số_truyền_vào)
{
	case value_1: {…break;}
	case value_2: {…break;}
	…
	default: {…}
}
# ? :
```js
let age = 20;
let result = age >= 18 ? "Đủ tuổi" : "Chưa đủ tuổi";

// let age = 20;
// let result;

// if (age >= 18) {
//   result = "Đủ tuổi";
// } else {
//   result = "Chưa đủ tuổi";
// }
```

JS Loop for 
Là vòng lặp biết trước số lần lặp.
Cú pháp:
for(<khai báo biến>; <điều kiện dừng>; <điều kiện lặp>) {…}
JS Loop for in
Thích hợp cho việc lặp qua mảng, chuỗi, nhóm các phần tử.
JS Loop for Of
Lặp qua các giá trị của một đối tượng có thể lặp lại.
Nó cho phép bạn lặp qua các cấu trúc dữ liệu có thể lặp lại như mảng, chuỗi, map, NodeList, …
function main(){
   var arr = [1,2,3,4,5,6,7,8,9,10];
   for(let i of arr) {
      console.log(i);
   }
}
main()

1
2
3
4
5
6
7
8
9
10
JS loop While
Vòng lặp chưa biết trước số lần lặp.
while(điều_kiện){
…
Điều kiện lặp;
}

Vòng lặp, lặp ít nhất một lần.
cú pháp:
do{
…
Điều kiện lặp;
} while(điều kiện);
JS break
forEach() 
Dùng để lặp qua các phần tử thường sử dụng trong mảng.
break
Để phá vỡ vòng lặp kể cả khi điều kiện vẫn đang đúng.
continue
Tiếp tục một vòng lặp khác và bỏ qua các đoạn code phía sau nó trong cùng vòng lặp.
Javascript Label