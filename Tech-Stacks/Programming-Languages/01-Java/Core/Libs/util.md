- [List](#list)
- [ArrayList (được sử dụng như một mảng động để lưu trữ phần tử)](#arraylist-được-sử-dụng-như-một-mảng-động-để-lưu-trữ-phần-tử)
  - [size() (Trả về số lượng phần tử có trong ArrayList)](#size-trả-về-số-lượng-phần-tử-có-trong-arraylist)
  - [add() (Nó được sử dụng để nối thêm phần tử được chỉ định vào cuối hoặc một vị trí bất kì trong một danh sách)](#add-nó-được-sử-dụng-để-nối-thêm-phần-tử-được-chỉ-định-vào-cuối-hoặc-một-vị-trí-bất-kì-trong-một-danh-sách)
  - [isEmpty() (để kiểm tra xem một ArrayList có phần tử hay không)](#isempty-để-kiểm-tra-xem-một-arraylist-có-phần-tử-hay-không)
  - [remove() (xóa một phần tử trong ArrayList tham số truyền vào có thể là một đối tượng hoặc một số)](#remove-xóa-một-phần-tử-trong-arraylist-tham-số-truyền-vào-có-thể-là-một-đối-tượng-hoặc-một-số)
  - [removeAll() (xóa hết phần tử có trong ArrayList value)](#removeall-xóa-hết-phần-tử-có-trong-arraylist-value)
  - [contains() (Kiểm tra xem có tồn tại value trong ArrayList hay không)](#contains-kiểm-tra-xem-có-tồn-tại-value-trong-arraylist-hay-không)
  - [set() (Để gán phần tử)](#set-để-gán-phần-tử)
---
# List
# ArrayList (được sử dụng như một mảng động để lưu trữ phần tử)
```bash
Cần import java.util.ArrayList

Lưu ý:
- có thể chứa các phần tử trùng lặp
- Duy trì thứ thự các phần tử được thêm vào
- cho phép truy cập ngẫu nhiên vì nó lưu trữ dữ liệu chỉ mục
- Thao tác chậm vì cần nhiều sự dịch chuyển nếu bất kỳ phần nào bị xóa khỏi danh sách.
```
**Syn**
```bash
ArrayList list = new ArrayList(); // non-generric – kiểu cũ
ArrayList<String> list = new ArrayList<String>() // generic – kiểu mới
```
## size() (Trả về số lượng phần tử có trong ArrayList)
## add() (Nó được sử dụng để nối thêm phần tử được chỉ định vào cuối hoặc một vị trí bất kì trong một danh sách)
**Ex**
```java
import java.util.ArrayList;
public class SinhVien {
	public static void main(String[] args) {
		ArrayList<String> list = new ArrayList<String>();
		list.add("le duc thang");
		list.add("le khanh toan");
		System.out.println(list);
	}
}
// [le duc thang, le khanh toan]
```
**Ex2**
```java
import java.util.ArrayList;
public class SinhVien {
	public static void main(String[] args) {
		ArrayList<String> list = new ArrayList<String>();
		list.add("le duc thang");
		list.add("le khanh toan");
		System.out.println(list);
		list.add(1, "nguyen minh duc");
		System.out.println(list);
	}
}
// * [le duc thang, le khanh toan]
// * [le duc thang, nguyen minh duc, le khanh toan]
```
## isEmpty() (để kiểm tra xem một ArrayList có phần tử hay không)
## remove() (xóa một phần tử trong ArrayList tham số truyền vào có thể là một đối tượng hoặc một số)
## removeAll() (xóa hết phần tử có trong ArrayList value)
## contains() (Kiểm tra xem có tồn tại value trong ArrayList hay không)
## set() (Để gán phần tử)