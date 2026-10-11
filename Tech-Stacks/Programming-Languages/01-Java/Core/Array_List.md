- [Arrays (Dùng để lưu trữ có các thành phần dữ liệu cùng kiểu)](#arrays-dùng-để-lưu-trữ-có-các-thành-phần-dữ-liệu-cùng-kiểu)
  - [length (Xác định số phần tử có trong mảng)](#length-xác-định-số-phần-tử-có-trong-mảng)
---
# Arrays (Dùng để lưu trữ có các thành phần dữ liệu cùng kiểu)
**Syn**
```bash
<data type>[] <tên> = new <data type>[<kích_thước>];
<data type> <tên>[] = new <data type>[<kích_thước>];
<data type>[] <tên> = {“”, “”, …};
…
```
## length (Xác định số phần tử có trong mảng)
**Ex**
```java
class Solution{
    public static void main(String[] args) {
       int [] n = {0,1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20};
       System.out.println(n.length); // 21
    }
}
```