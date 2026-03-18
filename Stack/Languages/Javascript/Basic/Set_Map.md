JS Sets
Là một tập hợp các giá trị duy nhất.
Mỗi giá trị chỉ có thể xuất hiện 1 lần trong Set.
Các giá trị có thể thuộc bất ký loại nào, giá trị nguyên thủy hoặc đối tượng.
function main(){
   let s = new Set([1,2,3,4,5,5]);
   console.log(s, typeof s);
}
main()
[ Set { 0: 1, 1: 2, 2: 3, 3: 4, 4: 5 }, 'object' ]
add()
function main(){
   let s = new Set();
   s.add(1);
   s.add(2);
   s.add(3);
   s.add(3);
   console.log(s, typeof s);
}
main()
[ Set { 0: 1, 1: 2, 2: 3 }, 'object' ]
Kiểm tra một đối tượng có phải kiểu dữ liệu set hay không
function main(){
   let s = new Set([1,2]);
   console.log(s instanceof Set);
}
main()
True

has()
Trả về true nếu giá trị được chỉ định tồn tại trong một tập hợp.
function main(){
   let s = new Set([1,2]);
   console.log(s.has(1));
}
main()
true
values()
Trả về một đối tượng Iterator với các giá trị trong một Set.
Keys()
Trả về giá trị giống như values(). Điều này làm cho Set tương thích với Maps.
entries()
JS Maps
Chứa các cặp key – value. 
Map cho phép bất kỳ kiểu dữ iệu nào làm key, duy trì thứ tự chèn, được tối ưu cho việc thêm, xóa và tìm kiếm các phần tử.
function main(){
   let m = new Map([
      ['name', 'John'],
      ['age', 30]
   ]);
   console.log(m, typeof m);
}
main()
[ Map { 'name': 'John', 'age': 30 }, 'object' ]
set()
Để thêm phần tử vào Map.
function main(){
   let m = new Map([
      ['name', 'John'],
      ['age', 30]
   ]);
   m.set("address", "New York");
   console.log(m);
}
main()
Map { 'name': 'John', 'age': 30, 'address': 'New York' }
get()
Để lấy ra giá trị của một key.
function main(){
   let m = new Map([
      ['name', 'John'],
      ['age', 30]
   ]);
   console.log(m.get("age"));
}
main()
30
size
Trả về số phần tử trong Map.
function main(){
   let m = new Map([
      ['name', 'John'],
      ['age', 30]
   ]);
   console.log(m.size);
}
main()
2
delete()
Xóa một phần tử trong Map.
clear ()
Xóa tất cả phần tử trong Map.
has()
Trả về true nếu khóa tồn tại trong Map.
foreach()
entries()
keys()
values()
as Keys
groupBy()

kiểm tra kiểu dữ liệu của biến.
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <script>
        var a = 100.12345;
        document.write(typeof a);
        document.write('<br>' + a.constructor);
    </script>
</body>
</html>
number
function Number() { [native code] }