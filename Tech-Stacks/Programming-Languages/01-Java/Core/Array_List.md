- [Arrays (Dùng để lưu trữ có các thành phần dữ liệu cùng kiểu)](#arrays-dùng-để-lưu-trữ-có-các-thành-phần-dữ-liệu-cùng-kiểu)
  - [length (Xác định số phần tử có trong mảng)](#length-xác-định-số-phần-tử-có-trong-mảng)
- [ArrayList (được sử dụng như một mảng động để lưu trữ phần tử)](#arraylist-được-sử-dụng-như-một-mảng-động-để-lưu-trữ-phần-tử)
  - [size() (Trả về số lượng phần tử có trong ArrayList)](#size-trả-về-số-lượng-phần-tử-có-trong-arraylist)
  - [add() (Nó được sử dụng để nối thêm phần tử được chỉ định vào cuối hoặc một vị trí bất kì trong một danh sách)](#add-nó-được-sử-dụng-để-nối-thêm-phần-tử-được-chỉ-định-vào-cuối-hoặc-một-vị-trí-bất-kì-trong-một-danh-sách)
  - [isEmpty() (để kiểm tra xem một ArrayList có phần tử hay không)](#isempty-để-kiểm-tra-xem-một-arraylist-có-phần-tử-hay-không)
  - [remove() (xóa một phần tử trong ArrayList tham số truyền vào có thể là một đối tượng hoặc một số)](#remove-xóa-một-phần-tử-trong-arraylist-tham-số-truyền-vào-có-thể-là-một-đối-tượng-hoặc-một-số)
  - [removeAll() (xóa hết phần tử có trong ArrayList value)](#removeall-xóa-hết-phần-tử-có-trong-arraylist-value)
  - [contains() (Kiểm tra xem có tồn tại value trong ArrayList hay không)](#contains-kiểm-tra-xem-có-tồn-tại-value-trong-arraylist-hay-không)
  - [set() (Để gán phần tử)](#set-để-gán-phần-tử)
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