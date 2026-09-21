- [Display (Cung cấp thông tin)](#display-cung-cấp-thông-tin)
	- [System.out.println() (xuất một nội dung ra màn hình có xuống dòng)](#systemoutprintln-xuất-một-nội-dung-ra-màn-hình-có-xuống-dòng)
	- [System.out.print() (in nội dung không xuống dòng)](#systemoutprint-in-nội-dung-không-xuống-dòng)
	- [System.out.printf() (in nội dung theo một định dạng nào đó)](#systemoutprintf-in-nội-dung-theo-một-định-dạng-nào-đó)
- [variable (biến)](#variable-biến)
	- [public (Instance variable - biến toàn cục)](#public-instance-variable---biến-toàn-cục)
	- [Static variable (Biến static có thể chia sẻ nó ở tất cả mọi thể hiện của lớp)](#static-variable-biến-static-có-thể-chia-sẻ-nó-ở-tất-cả-mọi-thể-hiện-của-lớp)
	- [Boolean](#boolean)
- [Integer (Số nguyên)](#integer-số-nguyên)
	- [parseInt](#parseint)
	- [Float (Số thực)](#float-số-thực)
- [Long](#long)
	- [.parseLong()](#parselong)
- [math](#math)
	- [BigInteger() (dùng để tạo ra một số nguyên cực lớn)](#biginteger-dùng-để-tạo-ra-một-số-nguyên-cực-lớn)
		- [.valueOf() (Tạo ra một đối tượng lớp Integer có giá trị cụ thể)](#valueof-tạo-ra-một-đối-tượng-lớp-integer-có-giá-trị-cụ-thể)
			- [.add() (để cộng 2 số có kiểu dữ liệu BigInteger)](#add-để-cộng-2-số-có-kiểu-dữ-liệu-biginteger)
			- [.subtract() (để trừ 2 số có kiểu dữ liệu BigInteger)](#subtract-để-trừ-2-số-có-kiểu-dữ-liệu-biginteger)
			- [.multiply() (để nhân 2 số có kiểu dữ liệu BigInteger)](#multiply-để-nhân-2-số-có-kiểu-dữ-liệu-biginteger)
			- [.divide() (để chia 2 số có kiễu dữ liệu BigInteger)](#divide-để-chia-2-số-có-kiễu-dữ-liệu-biginteger)
			- [.mod() (để chia lấy dư của 2 số có kiểu dữ liệu BigInteger)](#mod-để-chia-lấy-dư-của-2-số-có-kiểu-dữ-liệu-biginteger)
			- [.compareTo() (để so sánh với một BigInteger khác)](#compareto-để-so-sánh-với-một-biginteger-khác)
			- [.equals() (so sánh 2 đối tượng BigInteger có bằng nhau về giá trị hay không](#equals-so-sánh-2-đối-tượng-biginteger-có-bằng-nhau-về-giá-trị-hay-không)
			- [.intValue() (chuyển đổi một đối tượng BigInteger thành một giá trị nguyên)](#intvalue-chuyển-đổi-một-đối-tượng-biginteger-thành-một-giá-trị-nguyên)
- [Operators](#operators)
	- [++](#)
	- [--](#--)
- [String (Là kiểu chuỗi)](#string-là-kiểu-chuỗi)
	- [int -\> String](#int---string)
	- [Long.toString() (ép từ long -\> String)](#longtostring-ép-từ-long---string)
- [char (Là kiểu ký tự. 2 byte)](#char-là-kiểu-ký-tự-2-byte)
	- [int -\> char](#int---char)
	- [.charAt() (Chỉ chuyển được một ký tự)](#charat-chỉ-chuyển-được-một-ký-tự)
- [Character (Là kiểu đối tượng với kiểu char gốc. lớp này có một số phương thức hữu ích để tao tác với ký tự)](#character-là-kiểu-đối-tượng-với-kiểu-char-gốc-lớp-này-có-một-số-phương-thức-hữu-ích-để-tao-tác-với-ký-tự)
- [Instanceof (Để so sánh variable với kiểu dữ liệu trả về true hoặc false)](#instanceof-để-so-sánh-variable-với-kiểu-dữ-liệu-trả-về-true-hoặc-false)
- [Math (Để xử lý dữ liệu số)](#math-để-xử-lý-dữ-liệu-số)
	- [Math.pow() (Để tính lũy thừa)](#mathpow-để-tính-lũy-thừa)
	- [.Abs() (tính giá trị tuyệt đối kiễu dữ liệu)](#abs-tính-giá-trị-tuyệt-đối-kiễu-dữ-liệu)
	- [.Acos() (tính acos của góc)](#acos-tính-acos-của-góc)
	- [.addExact() (tính tổng các đối số của nó, ném ra một ngoại lệ nếu kết quả làm tràn một int)](#addexact-tính-tổng-các-đối-số-của-nó-ném-ra-một-ngoại-lệ-nếu-kết-quả-làm-tràn-một-int)
	- [.Asin() (tính asin của một góc)](#asin-tính-asin-của-một-góc)
	- [Atan() (tính atan của một góc)](#atan-tính-atan-của-một-góc)
	- [Atan2() (tính atan2)](#atan2-tính-atan2)
	- [Cbrt()](#cbrt)
	- [Ceil() (trả về giá trị nguyên nhỏ nhất lớn hơn hoặc bằng đối)](#ceil-trả-về-giá-trị-nguyên-nhỏ-nhất-lớn-hơn-hoặc-bằng-đối)
	- [copySign()](#copysign)
	- [Cos() (tính cosin của một góc)](#cos-tính-cosin-của-một-góc)
	- [Coah()](#coah)
	- [decrementExact()](#decrementexact)
	- [Exp()](#exp)
	- [Expml()](#expml)
	- [Floor() (trả về giá trị nguyên lớn nhỏ hơn hoặc bằng đối số)](#floor-trả-về-giá-trị-nguyên-lớn-nhỏ-hơn-hoặc-bằng-đối-số)
	- [floorDiv() (trả về giá trị lớn nhất nhỏ hơn hoặc bằng thương đại số)](#floordiv-trả-về-giá-trị-lớn-nhất-nhỏ-hơn-hoặc-bằng-thương-đại-số)
	- [floorMod()](#floormod)
	- [getExpoment()](#getexpoment)
	- [hypot()](#hypot)
	- [IEEErementExact()](#ieeerementexact)
	- [incrementExact()](#incrementexact)
	- [Log() (trả về logarit cơ số e)](#log-trả-về-logarit-cơ-số-e)
	- [Log10() (trả về logarit cơ số 10)](#log10-trả-về-logarit-cơ-số-10)
	- [Log1p() (trả về logarit tự nhiên của tổng dối số và 1)](#log1p-trả-về-logarit-tự-nhiên-của-tổng-dối-số-và-1)
	- [Max() (tìm giá trị lớn hơn)](#max-tìm-giá-trị-lớn-hơn)
	- [Min() (tìm giá trị nhỏ hơn)](#min-tìm-giá-trị-nhỏ-hơn)
	- [multiplyExact()](#multiplyexact)
	- [negateExact()](#negateexact)
	- [NextAfter()](#nextafter)
	- [NextDown()](#nextdown)
	- [NextUp()](#nextup)
	- [Round() (làm tròn và trả về số double)](#round-làm-tròn-và-trả-về-số-double)
	- [Scalb()](#scalb)
	- [Signum](#signum)
	- [Sin](#sin)
	- [Sqrt](#sqrt)
	- [SubtractExact](#subtractexact)
	- [Tan](#tan)
	- [Tanh](#tanh)
	- [toDegree](#todegree)
	- [toIntExact](#tointexact)
	- [ToRadians()](#toradians)
	- [Ulp()](#ulp)
	- [Random](#random)
		- [Math.random() (Để sinh ra 1 số thực ngẫu nhiên từ 0 -\> 1)](#mathrandom-để-sinh-ra-1-số-thực-ngẫu-nhiên-từ-0---1)
- [Random (Để sinh ra số ngẫu nhiên)](#random-để-sinh-ra-số-ngẫu-nhiên)
	- [random.nextInt() (Để sinh ra số ngẫu nhiên từ 0 đến bound)](#randomnextint-để-sinh-ra-số-ngẫu-nhiên-từ-0-đến-bound)
- [If … Else (Là cấu trúc lệnh điều kiện)](#if--else-là-cấu-trúc-lệnh-điều-kiện)
- [Ternary Operator (toán tử 3 ngôi Là cấu trúc câu điều kiện sử dụng cú pháp khác)](#ternary-operator-toán-tử-3-ngôi-là-cấu-trúc-câu-điều-kiện-sử-dụng-cú-pháp-khác)
- [Switch ... case (Là cấu trúc câu điều kiện)](#switch--case-là-cấu-trúc-câu-điều-kiện)
- [Loop](#loop)
	- [While loop (Là cấu trúc lặp không có giới hạn lần lặp)](#while-loop-là-cấu-trúc-lặp-không-có-giới-hạn-lần-lặp)
	- [For loop (Để lặp lại một khổi mã với một số lần nhất định)](#for-loop-để-lặp-lại-một-khổi-mã-với-một-số-lần-nhất-định)
	- [Break (Để thoát khỏi vòng lặp)](#break-để-thoát-khỏi-vòng-lặp)
	- [Continue (Để chuyển sang một vòng lặp tiếp theo)](#continue-để-chuyển-sang-một-vòng-lặp-tiếp-theo)
	- [For-each loop (Là cấu trúc lặp duyệt qua phần tử. Thích hợp cho Array, String, …)](#for-each-loop-là-cấu-trúc-lặp-duyệt-qua-phần-tử-thích-hợp-cho-array-string-)
	- [Labelled for loop (Là cấu trúc lặp được gán nhãn. Thích hợp trong vòng lặp lồng nhau)](#labelled-for-loop-là-cấu-trúc-lặp-được-gán-nhãn-thích-hợp-trong-vòng-lặp-lồng-nhau)
	- [Do-while loop (Là cấu trúc lặp không có giới hạn lần lặp. và được lặp ít nhất một lần)](#do-while-loop-là-cấu-trúc-lặp-không-có-giới-hạn-lần-lặp-và-được-lặp-ít-nhất-một-lần)
- [Arrays (Dùng để lưu trữ có các thành phần dữ liệu cùng kiểu)](#arrays-dùng-để-lưu-trữ-có-các-thành-phần-dữ-liệu-cùng-kiểu)
	- [length (Xác định số phần tử có trong mảng)](#length-xác-định-số-phần-tử-có-trong-mảng)
- [Object](#object)
- [ArrayList (ArrayList được sử dụng như một mảng động để lưu trữ phần tử)](#arraylist-arraylist-được-sử-dụng-như-một-mảng-động-để-lưu-trữ-phần-tử)
	- [size() (Trả về số lượng phần tử có trong ArrayList)](#size-trả-về-số-lượng-phần-tử-có-trong-arraylist)
	- [add() (Nó được sử dụng để nối thêm phần tử được chỉ định vào cuối hoặc một vị trí bất kì trong một danh sách)](#add-nó-được-sử-dụng-để-nối-thêm-phần-tử-được-chỉ-định-vào-cuối-hoặc-một-vị-trí-bất-kì-trong-một-danh-sách)
	- [isEmpty() (để kiểm tra xem một ArrayList có phần tử hay không)](#isempty-để-kiểm-tra-xem-một-arraylist-có-phần-tử-hay-không)
	- [remove() (xóa một phần tử trong ArrayList tham số truyền vào có thể là một đối tượng hoặc một số)](#remove-xóa-một-phần-tử-trong-arraylist-tham-số-truyền-vào-có-thể-là-một-đối-tượng-hoặc-một-số)
	- [removeAll() (xóa hết phần tử có trong ArrayList value)](#removeall-xóa-hết-phần-tử-có-trong-arraylist-value)
	- [contains() (Kiểm tra xem có tồn tại value trong ArrayList hay không)](#contains-kiểm-tra-xem-có-tồn-tại-value-trong-arraylist-hay-không)
	- [set() (Để gán phần tử)](#set-để-gán-phần-tử)
---
# Display (Cung cấp thông tin)
## System.out.println() (xuất một nội dung ra màn hình có xuống dòng)
**Ex**
```java
public class test {
    public static void main(String[] args) {
        System.out.println("hello world!!!");
    }
}
// thang@PhatToNhuLai:~/workspace/test/HEALTH_CARE_WEBSITE$ java test.java
// hello world!!!
```
## System.out.print() (in nội dung không xuống dòng)
## System.out.printf() (in nội dung theo một định dạng nào đó)
# variable (biến)
## public (Instance variable - biến toàn cục)
**Ex**
```java
class Solution {
	public int n = 10; // đây là biến instance

	public void age() {
		n *= 2;
	}

	public static void main(String[] args) {
		Solution object = new Solution(); // khai báo đối tương
		System.out.println(object.n);
		object.age();
		System.out.println(object.n);
	}
}
// 10
// 20
```
## Static variable (Biến static có thể chia sẻ nó ở tất cả mọi thể hiện của lớp)
**Ex**
```java
class Solution {
	public static int n = 10; // đây là biến static
	public static void age() {
		n *= 2;
	}
	public static void main(String[] args) {
		// không cần khai báo đối tượng
		System.out.println(n); // 10
		age();
		System.out.println(n); // 20
	}
}
```
## Boolean
```bash
boolean: 1 bit
```
# Integer (Số nguyên)
```bash
byte: 1 byte
short: 2 byte
int: 4 byte
long: 8 byte
```
## parseInt
**Ex**
```java
int <name> = Integer.parseInt(<variable>);
class Person{
	public static void main(String[] args) {
		String a = "200";
		int b = Integer.parseInt(a);
		b +=200;
		System.out.println(b); // 400
	}
} 
```
## Float (Số thực)
```bash
float: 4 byte
double: 8 byte
```
# Long
## .parseLong()
**Syn**
```java
long <name> = Long.parseLong(<variable>);
class Person{
	public static void main(String[] args) {
		String a = "200";
		long b = Long.parseLong(a);
		b +=200;
		System.out.println(b); // 400
	}
}
```
# math
## BigInteger() (dùng để tạo ra một số nguyên cực lớn)
**Syn**
```bash
import java.math.BigInteger

BigInteger name = new BigInteger();
```
### .valueOf() (Tạo ra một đối tượng lớp Integer có giá trị cụ thể)
#### .add() (để cộng 2 số có kiểu dữ liệu BigInteger)
**Syn**
```bash
<name1>.add(<name2>);
```
#### .subtract() (để trừ 2 số có kiểu dữ liệu BigInteger)
#### .multiply() (để nhân 2 số có kiểu dữ liệu BigInteger)
#### .divide() (để chia 2 số có kiễu dữ liệu BigInteger)
#### .mod() (để chia lấy dư của 2 số có kiểu dữ liệu BigInteger)
#### .compareTo() (để so sánh với một BigInteger khác)
```bash 
Trả về -1 nếu bé hơn BigInteger được so sánh, 0 nếu bằng và 1 nếu lớn hơn.
```
#### .equals() (so sánh 2 đối tượng BigInteger có bằng nhau về giá trị hay không
```bash
Nó so sánh giá trị tuyệt đối. trả về true nếu bằng và false nếu không bằng.
```
#### .intValue() (chuyển đổi một đối tượng BigInteger thành một giá trị nguyên) 
```bash
phương thức này lấy 32 bit ý nghĩa nhất của Integer và chuyển chúng thành số nguyên nếu giá trị của BigInteger quá lớn, các bit cao sẽ bị bỏ đi dẫn đến mất mát dữ liệu
```
# Operators
## ++ 
**Ex**
```java
class Solution{
	public static void main(String[] args) {
		int a = 10;
		System.out.println(a++);
		System.out.println(++a);
	}
}
// 10
// 12
```
## --
**Ex**
```java
class Solution{
	public static void main(String[] args) {
		int a = 10;
		System.out.println(a--);
		System.out.println(--a);
	}
}
// 10 
// 8
```
# String (Là kiểu chuỗi)
## int -> String
**Syn**
```bash
String <name> = String.valueOf(<variable>);
String <name> = Integer.toString(<variable>);
```
**Ex**
```python
class Person{
	public static void main(String[] args) {
		int a = 10;
		String s = String.valueOf(a);
		String t = Integer.toString(a);
		System.out.println(s + 10); // 20
		System.out.println(t+10); // 20
	}
}
```
## Long.toString() (ép từ long -> String)
**Syn**
```bash
String <name> = String.valueOf(<variable>);
String <name> = Long.toString(<variable>);
```
**Ex**
```java
class Person{
	public static void main(String[] args) {
		int a = 10;
		String s = String.valueOf(a);
		String t = Long.toString(a);
		System.out.println(s + 10); // 1010
		System.out.println(t+10); // 1010
	}
}
```
toUpperCase()
Trả về kí tự viết hoa hoặc trả về chuỗi in hoa hết.
Cú pháp:
<variable>.toUpperCase();
Ví dụ về toUpperCase
public class Chuoi {
	public static void main(String[] args) {
		String a = "Le Duc Thang";
		System.out.println(a.toUpperCase());
	}
}
LE DUC THANG
Thuật toán viết hoa hết chuỗi nhập từ bàn phím (không viết hoa được chữ có dấu)
import java.util.Scanner;
class Solution {
	public static char UpperCase(char a){
		if(a >= 'a' && a<='z') { // có thể viết cách khác: a >= 97 && a <= 122
			return (char) (a-32);
		}
		return a;
	}	
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		String a = sc.nextLine();
		String b = "";
		for(int i = 0; i < a.length(); i++) {
			b += UpperCase(a.charAt(i));
		}
		System.out.println(b);
	}	
}

Thuật toán chuyển ký tự in thường thành in hoa
import java.util.Scanner;
class Solution {
             public static char UpperCase(char a){
		if(a >= 'a' && a<='z') { // có thể viết cách khác: a >= 97 && a <= 122
			return (char) (a-32);
		}
		return a;
	}	
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		while(true) {
			String a = sc.next();
			System.out.println(UpperCase(a));
		}
	}	
}
Input: a
Result: A
Thuật toán viết hoa kí tự đầu của chữ trong một chuỗi
import java.util.Scanner;
class Solution {
	public static char change(char a){
		if(a >= 'a' && a<='z') {
			return (char) (a-32);
		}
		return a;
	}	
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		String input = sc.nextLine();
		if(input.length()>0) {
			input = change(input.charAt(0))+input.substring(1);
		}
		StringBuilder result = new StringBuilder(input);
		for(int i = 1; i < result.length(); i++)
			if(result.charAt(i-1)==' ' && result.charAt(i)>='a'&& result.charAt(i)<='z') {
				result.setCharAt(i, change(result.charAt(i)));
		}
		System.out.println(result.toString());
	}	
}

toLowerCase()
Chuyển chuỗi thành in thường.
public class Chuoi {
	public static void main(String[] args) {
		String a = "Le Duc Thang";
		System.out.println(a.toLowerCase());
	}
}

indexOf()
Để tìm kiếm chuỗi trong một chuỗi nào đó. Trả về số dương nếu có, trả về âm nếu không. Có thể có 1 giá trị trong ngoặc hoặc 2, hoặc nhiều hơn
Cú pháp:
    • a.indexOf(b) – tìm b trong a;
    • …
class Solution {
	public static void main(String args[]) {
		String a = "bfgrui";
		String b = "g";
		System.out.println(a.indexOf(b));
	}
}
2

class Solution {
	public static void main(String args[]) {
		String a = "bfgrui";
		String b = "g";
		System.out.println(a.indexOf(b,3));
	}
}
-1
equals()
Để so sánh chuỗi, phân biệt viết thường và viết hoa.
public class Chuoi {
	public static void main(String[] args) {
		String a = "le duc thang";
		String b = "Le duc thang";
		String c = "le duc thang";
		System.out.println(a.equals(b));             		              System.out.println(a.equals(c));
}
false
true
1.  Find the index of the First Occurrence in a String
class Solution {
    public int strStr(String haystack, String needle) {
        if(needle.length() == 0) return  0;
        if(haystack.indexOf(needle) < 0) return -1;
        if(haystack.length() == needle.length()){
            if(haystack.equals(needle)) return 0;
        }
        for(int i = 0; i <= haystack.length()-needle.length(); i++){
            if(haystack.substring(i, i+needle.length()).equals(needle)) return i;
        }
        return -1;
    }
}

equalsIgnoreCase()
So sách chuỗi và không biệt chữ hoa và chữ thường.
public class Chuoi {
	public static void main(String[] args) {
		String a = "le duc thang";
		String b = "Le duc thang";
		String c = "le duc thang";
		System.out.println(a.equalsIgnoreCase(b));		
System.out.println(a.equalsIgnoreCase(c));
}
True
True

==
Để so sánh chuỗi. Phân biệt chữ hoa và chữ thường.
public class Solution{	
	public static void main(String[] args) {
		String a = "le duc thang";
		String b = "le duc thang";
		if(a == b) System.out.println("giống nhau");		
	}
}
giống nhau
substring()
Để cắt chuỗi con hoặc lấy ra một đoạn chuỗi từ vị trí chỉ định.
Cú pháp:
    • <variable>.substring(int startIndex)
    • <variable>.substring(int startIndex, int endIndex)
public class Chuoi {
	public static void main(String[] args) {
		String a = "Le Duc Thang";
		System.out.println(a.substring(3,6));
	}
}
Duc – tức là nó sẽ lấy từ 3 đến 6-1
14. Longest Common Prefix
class Solution {
    public String longestCommonPrefix(String[] strs) {
        if(strs.length == 0) return "";
        String s = strs[0];
        for(int i = 0; i < s.length(); i++){
            for(int j = 1; j < strs.length; j++){
                if(i >= strs[j].length() || s.charAt(i) != strs[j].charAt(i)) return s.substring(0, i);
            }
        }
        return s;
    }
}


trim()
Xóa khoản trắng dư thừa ở đầu chuỗi.
public class Chuoi {
	public static void main(String[] args) {
		String a = "   Le Duc Thang   ";
		System.out.println(a.trim());
	}
}

split(String regex)
Dùng để tách chuỗi này theo biểu thức chính quy và trả về mảng chuỗi.
Cú pháp:
    • <variable>.split(String regex)
    • <variable>.split(String regex, int limit)
Tách chữ trong một chuỗi
public class Solution {
    public static void main(String[] args) {
       String s = "he is is";
       String [] words = s.split(" ");
       for (String string : words) {
		System.out.println(string);
	}
    }
}

58. Length of Last Word
class Solution {
    public int lengthOfLastWord(String s) {
        s = s.trim();
        String [] text = s.split(" ");
        return text[text.length-1].length();
    }
}

compareTo()
Dùng để so sánh chuỗi theo bảng chữ cái. Nó chỉ có thể so sánh được 2 chuỗi với nhau. Thường dùng compareTo cho bài toán sắp xếp.
getChars(…)
Lấy nhiều ký tự nhưng phải gán vào một mảng vì nó xuất ra theo kiêu mảng.
public class Chuoi {
	public static void main(String[] args) {
		String a = "Hello Wolrd!!";
		char[] charArr = new char[10];
		a.getChars(6, 11, charArr, 0);
		System.out.println(charArr); // cách 1 để xuất ra màn hình
		for(char value : charArr) { // cách 2 để xuất ra màn hình
			System.out.print(value);
		}
	}
}

Getbytes()
Lấy giá trị trong bang mã ascii theo hệ cơ số 10.
isEmpty()
Nếu chuỗi trống trả về true, ngược lại trả về false.
regionMatches()
So sánh một đoạn chuỗi.
public class Chuoi {
	public static void main(String[] args) {
		String a = "le duc thang";
		String b = "thang";
		System.out.println(a.regionMatches(7,b,0,5)); // so sánh 5 kí tự từ kí tự thứ 7 của a với kí tự thứ 0 của b
	}
}

startsWith()
kiểm tra chuỗi bắt đầu bằng một chuỗi hay một ký tự nào đó không.
public class Chuoi {
	public static void main(String[] args) {
		String a = "le duc thang";
		System.out.println(a.startsWith("le")); 
		System.out.println(a.startsWith("duc"));
	}
}
True
False

endWith()
kiểu tra chuỗi có kết thúc bằng một chuỗi hay một ký tự nào đó không.
public class Chuoi {
	public static void main(String[] args) {
		String a = "le duc thang";
		System.out.println(a.startsWith("thang"));		              System.out.println(a.startsWith("duc")); 
	}
}
True
False

lastIndexOf()
Tìm kiếm chuỗi từ bên phải sang bên trái.
concat()
Dùng để nối chuỗi.
public class Chuoi {
	public static void main(String[] args) {
		String a = "Việt";
		String b = "Nam";
		System.out.println(a.concat(b));
		System.out.println(a+b);
	}
}


contains()
Để tìm kiếm chuỗi kí tự trong một chuỗi. kiểu trả về là true hoặc false.
class Solution {	
	public static void main(String[] args) {
		String a = "aa";
		String b ="aab";
		System.out.println(a.contains(b)); // tìm kiếm b trong a
	}
}
false
replace()
thay thế một kí tự hoặc một chuỗi vào chuỗi đã cho.
public class Chuoi {
	public static void main(String[] args) {
		String a = "le duc thang";
		System.out.println(a.replace("le", "nguyen"));
	}
}

replaceAll()
Để thay thế nhưng không thay thế biến ban đầu.
Public char[] toCharArray()
Được sử dụng để đổi chuỗi thành mảng kí tự. nó trả nề một mảng ký tự có độ dài tương đương độ dài của chuỗi.
class Solution {
	public static void main(String args[]) {
		String s1 = "hello";
		char[] ch = s1.toCharArray();
		for (int i = 0; i < ch.length; i++) {
			System.out.println(ch[i]);
		}
	}
}
h
e
l
l
o
Đếm sô lần xuất hiện của các ký tự trong một chuỗi
import java.util.Scanner;
class Solution {
	public static void main(String args[]) {
		int[] count = new int[26];
		Scanner sc = new Scanner(System.in);
		String text = sc.next();
		for(char c : text.toCharArray()) {
			count[c-'a']++;
		}
		for(int i = 0; i < count.length; i++) {
			if(count[i]!=0) {
				System.out.println((char)(i+'a') + " - " + count[i]);
			}
		}
	}
}
thanggg
a - 1
g - 3
h - 1
n - 1
t - 1

Java regex / regular expression (biểu thức chính quy)
Là một API để định nghĩa một mẫu để tìm kiếm hoặc thao tác với chuỗi. Nó được sử dụng rộng rãi để xác định ràng buộc trên các chuỗi như xác thực mật khẩu, email, kiểu dữ liệu datetime, …
Java regex API cung cấp 1 interface và 3 lớp trong gói java.util.regex
- interface MathResult
- lớp Matcher
- lớp Pattern
- lớp PatternSyntaxException
Quy tắc viết regular expression
    • . – so khớp với bất kỳ ký tự đơn nào
    • ^ - so khớp phần đầu của chuỗi hay dòng
    • $ - so khớp phần cuối của chuỗi hay dòng
    • (…) – so khớp các nhóm kí tự bên trong
    • […] – so khớp bất kỳ kí tự đơn nào trong dấu ngoặc vuông
    • [^…] – so khớp bất kì kí tự đơn nào ngoại trừ các kí tự trong dáu ngoặc vuông
    • [m-n] – so khớp từ ký tự m đến ký tự n theo thứ tự trong ASCII
    • XY – so khớp với X theo sau là Y, ví dụ[a-e][i-u]
    • X|Y – so khớp với X hoặc Y
    • \d – so khớp với ký tự là chữ số, viết tắt của [0-9]
    • \D – so khớp với ký tự không phải là chữ số, viết tắt là [^0-9]
    • \s – so khớp với bất kì kí tự nào (dấu cách, tab, xuông dòng) viết tắt của [\t\n\x0B\f\r]
    • \S – so khớp với bất kỳ ký tự không phải kí tự trống, viết tắt của [^\s]
    • \w – so khớp với bất kỳ ký tự nào là chữ cái và số [a-zA-z0-9] và dấu gạch dưới
    • \W – so khớp với bất kỳ ký tự nào không phải chữ cái và số, viết tắt của [^\w]
    • \b – ranh giới của một từ
    • \B – không phải ranh giới của một từ
    • \A – so khớp phần đầu của đầu vào
    • \G – so khớp phần cuối của đầu vào
    • X* - so khớp với 0 hoặc nhiều sự xuất hiện của X, viết gọn cho X{0,}
    • X+ - so khớp với 1 hoặc nhiều sự xuất hiện của X, viết gọn cho X{1,}
    • X? – so khớp 0 hoặc 1 sự xuất hiện của X, viết gọn cho X{0,1}
    • X{n} – so khớp chính xác n lần xuất hiện của X
    • X{n,m} – so khớp với ít nhất n và nhiều nhất m lần xuất hiện của X
Lớp Pattern – Matcher
public static pattern compile(String regex)
Định dạng regex cho Pattern.
Cú pháp:
Pattern name = Pattern.compile(“<định dạng>”);
Matcher matcher(CharSequence input)
Tạo một matcher để khớp với đầu vào đã cho với mẫu.
Cú pháp:
Matcher matcher = patternName.matcher(nameStr)
- patternName: là tên đã tạo ra đối tượng pattern
- nameStr: tên của chuỗi
boolean matches()
kiểm tra xem biểu thức chính quy có khớp với mẫu hay không, không cần import thư viện.

public class Solution{
	 public static void main(String[] args) {
		 String str = "hello";
		 // do chuỗi này không phải có độ dài là 1 kí tự bất kì nên kết quả trả về là false
		 System.out.println(str.matches("."));
		 // .* là chuỗi có độ dài bất kì, các kí tự cos thể lặp lại nhiều lần
		 System.out.println(str.matches(".*"));
	 }
}
Bài tập kết hợp pattern-Matcher-Matches
Kiểm tra xem email nhập vào có đúng định dạng hay không, trả về true hoặc false
import java.util.Scanner;
import java.util.regex.Matcher;
import java.util.regex.Pattern;

public class Solution {
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		System.out.print("Email: ");
		String email = sc.nextLine();
		// case 1
		System.out.println(email.matches("\\w{1,}(@gmail.com)"));
		// case 2
		Pattern patternName = Pattern.compile("\\w{1,}(@gmail.com)");
		Matcher matcherName = patternName.matcher(email);
		System.out.println(matcherName.matches());
	}
}


Dùng regex kiểm tra xem số nhập vào có phải số thuộc từ 0 đến 199 hay không

import java.util.Scanner;
import java.util.regex.Matcher;
import java.util.regex.Pattern;

public class Solution {
	public static void main(String[] args) {
		while (true) {
			Scanner sc = new Scanner(System.in);
			int a = sc.nextInt();
			// tạo ra chuỗi vì matcher không dùng được cho số
			String s = a + "";
			Pattern patternName = Pattern.compile("[0-1]?[0-9]?[0-9]");
			Matcher matcher = patternName.matcher(s);
			System.out.println(matcher.matches());
		}
	}
}
Dùng regex kiểm tra xem số nhập vào có phải số từ 0-255 hay không

import java.util.Scanner;
import java.util.regex.Matcher;
import java.util.regex.Pattern;

public class Solution {
	public static void main(String[] args) {
		while (true) {
			Scanner sc = new Scanner(System.in);
			int a = sc.nextInt();
			// tạo ra chuỗi vì matcher không dùng được cho số
			String s = a + "";
			Pattern patternName = Pattern.compile("([0-1]?[0-9]?[0-9])|(2[0-4][0-9])|(25[0-5])");
			Matcher matcher = patternName.matcher(s);
			System.out.println(matcher.matches());
		}
	}
}
Dùng regex kiểm tra xem một chuỗi nhập vào có phải một IP hay không, trả về true false
import java.util.regex.Matcher;
import java.util.regex.Pattern;
import java.util.Scanner;

class Solution{

    public static void main(String[] args){
        Scanner in = new Scanner(System.in);
        while(in.hasNext()){
            String IP = in.next();
            System.out.println(IP.matches(new MyRegex().pattern));
        }

    }
}

class MyRegex{
    public String pattern;
    MyRegex(){
        pattern = Pattern.compile("^([0-1]?[0-9]?[0-9]|2[0-4][0-9]|25[0-5])\\.([0-1]?[0-9]?[0-9]|2[0-4][0-9]|25[0-5])\\.([0-1]?[0-9]?[0-9]|2[0-4][0-9]|25[0-5])\\.([0-1]?[0-9]?[0-9]|2[0-4][0-9]|25[0-5])$").toString();
    }
    
}
# char (Là kiểu ký tự. 2 byte)
## int -> char
**Syn**
```bash
(char) variable_int;
```
## .charAt() (Chỉ chuyển được một ký tự)
**Syn**
```bash
<Variable>.charAt(0);
```
# Character (Là kiểu đối tượng với kiểu char gốc. lớp này có một số phương thức hữu ích để tao tác với ký tự)
# Instanceof (Để so sánh variable với kiểu dữ liệu trả về true hoặc false)
# Math (Để xử lý dữ liệu số)
## Math.pow() (Để tính lũy thừa)
## .Abs() (tính giá trị tuyệt đối kiễu dữ liệu)
## .Acos() (tính acos của góc)
## .addExact() (tính tổng các đối số của nó, ném ra một ngoại lệ nếu kết quả làm tràn một int)
## .Asin() (tính asin của một góc)
## Atan() (tính atan của một góc)
## Atan2() (tính atan2) 
## Cbrt()
## Ceil() (trả về giá trị nguyên nhỏ nhất lớn hơn hoặc bằng đối)
## copySign()
## Cos() (tính cosin của một góc)
## Coah()
## decrementExact()
## Exp()
## Expml()
## Floor() (trả về giá trị nguyên lớn nhỏ hơn hoặc bằng đối số)
## floorDiv() (trả về giá trị lớn nhất nhỏ hơn hoặc bằng thương đại số)
## floorMod()
## getExpoment()
## hypot()
## IEEErementExact()
## incrementExact()
## Log() (trả về logarit cơ số e)
## Log10() (trả về logarit cơ số 10)
## Log1p() (trả về logarit tự nhiên của tổng dối số và 1)
## Max() (tìm giá trị lớn hơn)
## Min() (tìm giá trị nhỏ hơn)
## multiplyExact()
## negateExact()
## NextAfter()
## NextDown()
## NextUp()
## Round() (làm tròn và trả về số double)
## Scalb()
## Signum
## Sin
## Sqrt
## SubtractExact
## Tan
## Tanh
## toDegree
## toIntExact
## ToRadians()
## Ulp()
## Random
### Math.random() (Để sinh ra 1 số thực ngẫu nhiên từ 0 -> 1)
**Ex: Thuật toán tạo ra 100 số ngẫu hiên từ 0 -> 100 bằng java**
```java
class Solution {	
	public static void main(String[] args) {
		for(int i = 0; i < 101; i++) {
			int a = (int)(Math.random()*101);
			System.out.print(a + " ");
		}
	}
}
```
**Ex2: Thuật toán trò chơi trúng thưởng với xác suất 2%**
```java
class Solution {
	
	public static void main(String[] args) {
		for(int i = 0; i < 101; i++) {
			double a = Math.random();
			System.out.print((a<0.02)?"bạn đã trúng thưởng":"rất tiếc, bạn không trúng thưởng");
			System.out.println();
		}
	}
}
```
# Random (Để sinh ra số ngẫu nhiên)
```bash
Cần import java.util.Random;
```
## random.nextInt() (Để sinh ra số ngẫu nhiên từ 0 đến bound)
# If … Else (Là cấu trúc lệnh điều kiện)
# Ternary Operator (toán tử 3 ngôi Là cấu trúc câu điều kiện sử dụng cú pháp khác)
# Switch ... case (Là cấu trúc câu điều kiện)
**Syn**
```bash
switch(expression){
case value1:
// code
break;
case valse2:
// code
break;
…
}
```
# Loop
## While loop (Là cấu trúc lặp không có giới hạn lần lặp)
## For loop (Để lặp lại một khổi mã với một số lần nhất định)
**Ex**
```java
class Solution{

	public static void main(String[] args) {
		for(int i = 0; i < 4; i++) {
			aa:
			for(int j = 0; j < 4; j++) {
				if(j==2) continue aa;
				System.out.print(i + " " + j + "\n");
			}
		}
		
	}
}
// 0 0
// 0 1
// 0 3
// 1 0
// 1 1
// 1 3
// 2 0
// 2 1
// 2 3
// 3 0
// 3 1
// 3 3
```
## Break (Để thoát khỏi vòng lặp)
## Continue (Để chuyển sang một vòng lặp tiếp theo)
## For-each loop (Là cấu trúc lặp duyệt qua phần tử. Thích hợp cho Array, String, …)
## Labelled for loop (Là cấu trúc lặp được gán nhãn. Thích hợp trong vòng lặp lồng nhau)
## Do-while loop (Là cấu trúc lặp không có giới hạn lần lặp. và được lặp ít nhất một lần)
**Syn**
```bash
do {
      // code;
} while();
```
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
# Object
**Ex: Quản lý danh sách sinh viên**
```java
class student{
	String name, room, sex;
	student(String name, String room, String sex){
		this.name = name;
		this.room = room;
		this.sex = sex;
	}
	@Override
	public String toString() {
		return "student [name=" + name + ", room=" + room + ", sex=" + sex + "]";
	}
}
public class Solution{
	public static void main(String[] args) {
		student [] list = new student[2];
		student sv1 = new student("JSON", "12A1", "male");
		student sv2 = new student("MICK", "12A1", "female");
		list[0] = sv1;
		list[1] = sv2;
		for (student student : list) {
			System.out.println(student);
		}
	}
}
// student [name=JSON, room=12A1, sex=male]
// student [name=MICK, room=12A1, sex=female]
```
# ArrayList (ArrayList được sử dụng như một mảng động để lưu trữ phần tử)
```bash
Cần import java.util.ArrayList

Lưu ý:
- có thể chứa các phần tử trùng lặp
- Duy trì thứ thự các phần tử được thêm vào
- ArrayList là không đồng bộ (non-synchronized)
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
Static boolean matches(String regex, CharSequence input)
Nó biên dịch biểu thức chính quy và tìm kiếm các chuỗi con từ chuỗi input phù hợp với mẫu regex
string[] split(CharSequence input)
Chia chuoix input đã cho thành các mảng các kết quả trùng khớp với mẫu đã cho
String pattern()
Trả về mẫu regex
HTTP client API


boolean find()
tìm biểu thức khớp với mẫu
String group()
Trả về chuỗi con phù hợp
int start()
Trả về vị trí bắt đầu của chuỗi con phù hợp
int end()
Trả về vị trí kết thúc của chuỗi con phù hợp
Pattern.CASE_INSENSITIVE
Là một flag được sử dụng trong biểu thức chính quy để so sánh không phân biệt chữ hoa chữ thường.
Để sử dụng flag này cần kết hợp với phương thức compile() của lớp Pattern khi tạo biểu thức chính quy.

import java.util.regex.Pattern;
import java.util.regex.Matcher;

public class CaseInsensitiveExample {
    public static void main(String[] args) {
        String text = "I love Java programming. JAVA is fun!";
        String regex = "java";

        // Tạo Pattern với flag CASE_INSENSITIVE
        Pattern pattern = Pattern.compile(regex, Pattern.CASE_INSENSITIVE);
        Matcher matcher = pattern.matcher(text);

        // Tìm và in ra tất cả các kết quả khớp
        while (matcher.find()) {
            System.out.println("Found match: " + matcher.group());
        }
    }
}
Bài tập find – group – start – end - …
Tìm xem một chuỗi cho trước cho định dạng ngày tháng năm hay không, có thì xuất định dạng đó ra màn hình

import java.util.Scanner;
import java.util.regex.Matcher;
import java.util.regex.Pattern;

public class Solution {
	public static void main(String[] args) {
		String text = "17-07-2005 is my birthday, 02/08/2003 is not my birthday";
		Pattern patternName = Pattern.compile("\\d{1,2}[-|/]\\d{1,2}[-|/]\\d{4}");
		Matcher matcher = patternName.matcher(text);
		while(matcher.find()) {
			// case 1
			System.out.println(text.substring(matcher.start(), matcher.end()));
			// case 2
			System.out.println(matcher.group());
		}
	}
}
Tìm các chữ bắt đầu bằng một kí tự m trong chuỗi “My name is Thang head moi, is very very lucky”

import java.util.regex.Matcher;
import java.util.regex.Pattern;

class Solution{
	public static void main(String[] args) {
		String text = "My name is Thang head moi, is very very lucky";
		Pattern partternName = Pattern.compile("\\b(m)([a-z]*)", Pattern.CASE_INSENSITIVE);
		Matcher matcher = partternName.matcher(text);
		while(matcher.find()) {
			System.out.println(matcher.group());
		}
	}
}
Tìm các chữ kết thúc bằng một kí tự y trong chuỗi “My name is Thang head moi, is very very lucky”

import java.util.regex.Matcher;
import java.util.regex.Pattern;

class Solution{
	public static void main(String[] args) {
		String text = "My name is Thang head moi, is very very lucky";
		Pattern partternName = Pattern.compile("([a-z]*)(y)\\b", Pattern.CASE_INSENSITIVE);
		Matcher matcher = partternName.matcher(text);
		while(matcher.find()) {
			System.out.println(matcher.group());
		}
	}
}
import java.util.Scanner;
import java.util.regex.Matcher;
import java.util.regex.Pattern;

public class DuplicateWords
{
    public static void main(String[] args){

        String pattern = "(\\s|^)([a-z]+)(\\s+\\2)+(?=(?:\\s|$))";
        Pattern r = Pattern.compile(pattern, Pattern.CASE_INSENSITIVE);

        Scanner in = new Scanner(System.in);
        int testCases = Integer.parseInt(in.nextLine());
        while(testCases>0){
            String input = in.nextLine();
            Matcher m = r.matcher(input);
            boolean findMatch = true;
            while(m.find( )){
                input = input.replaceAll(m.group(), m.group(1) + m.group(2)).replace("Rana is the best", "Rana is the the best");
                findMatch = false;
            }
            System.out.println(input);
            testCases--;
        }
    }
}

import java.util.Scanner;
import java.util.regex.Matcher;
import java.util.regex.Pattern;

public class DuplicateWords
{
    public static void main(String[] args){

        String pattern = "(\\b\\w+\\b)(\\s*\\1\\b)+";
        Pattern r = Pattern.compile(pattern, Pattern.CASE_INSENSITIVE);

        Scanner in = new Scanner(System.in);
        int testCases = Integer.parseInt(in.nextLine());
        while(testCases>0){
            String input = in.nextLine();
            Matcher m = r.matcher(input);
            boolean findMatch = true;
            while(m.find( )){
                input = input.replaceAll(m.group(), m.group(1));
                findMatch = false;
            }
            System.out.println(input);
            testCases--;
        }
    }
}
Sử dụng regex định dạng một username đúng là các kí tự chữ hoa, chữ thường, số (không được ở đầu) và dấu gạch dưới (không được ở đầu), không có các kí tự đặc biệt khác.

import java.util.Scanner;
import java.util.regex.Matcher;
import java.util.regex.Pattern;

class Solution{
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int testCase = sc.nextInt(); sc.nextLine();
        Pattern pattern = Pattern.compile("[a-z | A-Z](\\w){7,29}", Pattern.CASE_INSENSITIVE);
        while(testCase != 0) {
            String user = sc.nextLine();            
            Matcher matcher = pattern.matcher(user);
            if(matcher.matches()) {
                System.out.println("Valid");
            } else {
                System.out.println("Invalid");
            }
            testCase--;
        }
    }
}

boolean find(int start)
tìm biểu thức tiếp theo khớp với mẫu từ số bắt đầu đã cho
int groupCount()
Trả về tổng số các chuỗi con phù hợp
    • Character.toUpperCase(char variable);
public static String FirstUpperCase(String letter){
	char first = letter.charAt(0);
	if(!Character.isUpperCase(first)) {
		first = Character.toUpperCase(first);
		return letter.replace(letter.charAt(0), first);
	} return letter;
}

Boolean isUpperCase(char value)
kiểm tra xem ký tự truyền vào là viết hoa không. 
Cú pháp:
Character.isUpperCase(‘’);
StringBuilder
Là một đối tượng, cho phép theo tác với với chuỗi. khác với String, StringBuiler cho phép thay đổi nội dung của chuỗi mà không tạo ra các đối tượng mới, giúp tiết kiệm bộ nhớ và tăng hiệu suất khi thực hiện nhiều thao tác nối chuỗi.
Khởi tạo
Để tạo ra đối tượng StringBuilder.
Cú pháp:
    • StringBuilder <name> = new StringBuilder(); tạo ra một builder chuỗi với dung lượng ban đầu là 16
    • StringBuilder <name> = new StringBuilder(String str); tạo ra một builder chuỗi với chuỗi cụ thể
    • StringBuilder <name> = new StringBuilder(int capacity); tạo ra một builder chuỗi với dung lượng  được chỉ định như độ dài chuỗi.
append()
Được sử dụng để nối thêm các chuỗi được chỉ định với chuỗi này.
Cú pháp:
    • <variable>.append(String s)
    • …
insert()
Để chèn chuỗi chỉ định với chuỗi này tại vị trí quy định.
Cú pháp:
<variable>.insert(int offset, String s)
replace()
Để thay thế chuỗi từ vị trí nhất định.
Cú pháp:
Replace(int startIndex, int endIndex, String str)
delete()
Để xóa chuỗi từ vị trí nhất định.
Cú pháp:
<variable>.delete(int startIndex, int endIndex)
reverse()
Để đảo được chuỗi.
Cú pháp:
<variable>.reverse()
capacity()
Để trả về dung lượng hiện tại của chuỗi.
Cú pháp:
<variable>.capacity()
Ensure()
Để đảm bảo dung lượng ít nhất bằng mức tối thiểu nhất định.
Cú pháp:
ensureCapacity(int minimumCapacity)
charAt()
Để trả về ký tự tại vị trí quy định.
Cú pháp:
<variable>.charAt(int index)
length()
Để trả về chiều dài của chuỗi nghĩa là tổng số ký tự.
Cú pháp:
<variable>.length()
substring()
Để trả về chuỗi con tại một vị trí nào đó.
Cú pháp:
    • <variable>.substring(int beginIndex)
    • <variable>.substring(int beginIndex, int endIndex)
StringBuffer

Static {}
Là khối khởi tạo tĩnh tring java. Mã bên trong khối lệnh được thực thi tự động khi lớp được tải lần đầu tiên, trước cả bất kì đối tượng nào của lớp đó được tạo ra.
Đặc điểm:
Chỉ được thực thi một lần duy nhất.
Không cần tạo đối tượng của lớp để truy cập đến khối khởi tạo tĩnh.
Thường được khởi tạo biến static, thực hiện các tác vụ khởi tạo ban đầu cho lớp, chẳng hạn như kết nối cơ sở dữ liệu, tải tài nguyên.
Thực hiện các kiểm tra hợp lệ trước khi sử dụng lớp.
import java.io.*;
import java.util.*;
import java.text.*;
import java.math.*;
import java.util.regex.*;
public class Solution {
	static boolean flag;
	static int B, H;
	private static final Scanner SR = new Scanner(System.in);
	static {
		B = SR.nextInt();
		H = SR.nextInt();
		if (B > 0 && H > 0) {
			flag = true;
		} else {
			System.out.println("java.lang.Exception: Breadth and height must be positive");
		}
	}
	public static void main(String[] args) {
		if (flag) {
			int area = B * H;
			System.out.print(area);
		}
	}// end of main
}// end of class



getClass().getName()
có thể dùng kể kiểm tra kiểu dữ liệu của một biến hay một đối tượng

public class Main {
	public static void main(String[] args) {
		Object a = new Object();
		int b = 1;
		String c="";
		Integer d=1;
		int[] e= new int[] {1,2};
		System.out.println(a.getClass().getName());
		System.out.println(c.getClass().getName());
		System.out.println(d.getClass().getName());
		System.out.println(e.getClass().getName());
	}
}
java.lang.Object
java.lang.String
java.lang.Integer
[I
String.format()
Để định dạng dữ liệu trước khi xuất
Ví dụ: cho số nguyên n = 5 in ra số nguyên n = 005;
package Content;

public class Run_01 {
    public static void main(String[] args) {
        int n = 5;
        System.out.println("0" + "0" + n); // không đúng với bản chất bài toán;
        // CÁCH 1
        String str = String.format("%03d", n);
        System.out.println(str);
        // CÁCH 2
        System.out.printf("%03d", n);
    }
}
Decimalformat
Dùng để dịnh dạng số theo cách mà ta chỉ định
Cần import java.text.Decimalformat;
Tạo một DecimalFormat
Format(kiểu_dữ_liệu <tên>)
Phương thúc này trả về kết quả có giá trị String ứng với <tên> sau khi định dạng
Ví dụ:
package Content;
import java.text.DecimalFormat;
public class Run_01 {
    public static void main(String[] args) {
        int n = 5;
        System.out.println("0" + "0" + n); // không đúng với bản chất bài toán;
        // CÁCH 1
        String str = String.format("%03d", n);
        System.out.println(str);
        // CÁCH 2
        System.out.printf("%03d\n", n);
	  // CÁCH 3
        DecimalFormat s = new DecimalFormat("000");
        String m = s.format(n);
        System.out.println(m);
    }
}


Cách kiểm tra và xử lý lỗi biên dịch

OOP (Lập trình hướng đối tượng)
Đối tượng có nghĩa là một thực thể (có trạng thái và hành vi) trong thế giới thực như bút, ghế, … Lập trình hướng đối tượng là một phương pháp lập hoặc mô hình để thiết kế chương trình bằng cách sử dụng các lớp và đối tượng.
Đối tượng có thể là vật lý hoặc logic.
Các đối tượng có thể giao tiếp mà không cần biết chi tiết về dữ liệu hoặc mã của nhau. Điều kiện cần duy nhất là loại tin nhắn được chấp nhận và loại phản hồi được trả về bởi các đối tượng.

Ví dụ: Chó là một loại đối tượng, nó có các trạng thái như màu sắc, tên, giống, … cũng như các hành vi như vẫy đuôi, sủa, ăn, …
Class
Lớp được định nghĩa là mọt bản thiết kế mà từ đó bạn có thể tạo ra một đối tượng riêng lẻ. Lớp không chiếm bất kỳ không gian nào.
Inheritance (kế thừa)
Khi một đối tượng có tất cả các thuộc tính và hành vi của đối tượng cha, thì được gọi là kế thừa. Nó cung cấp khả năng tái sử dụng mã. Nó được sử dụng để đạt được đa hình thời gian chạy.
Ý tưởng đằng sau kế thừa trong Java là tạo ra lớp mới được xây dựng dựa trên các lớp hiện có. Chúng ta có thể sử dụng lại các phương thức hiện có và trường của lớp cha. Tuy nhiên, cũng có thể thêm các phương thức và trường mới và lớp hiện tại của bạn.
Kế thừa biểu thị mối quan hệ IS-A được gọi là mối quan hệ cha – con.

Overloadiing (Nạp chồng phương thức) 
Khi một lớp có 2 hay nhiều phương thức cùng tên nhưng khác nhau về tham số, nó được biết đến như là phương thức overloading. Nó khác với overriding một phương thức có một phương thức khác cùng tên, kiểu, số tham số, …
2 cách để nạp chồng phương thức:
    • Bằng việc thay đổi số tham số.
    • Bằng việc thay đổi kiểu dữ liệu.
Trong java nạp chồng phương thức không thể thay đổi kiểu trả về của phương thức.
public class MathOperations {  
    public int add(int a, int b) {  
        return a + b;  
    }  
    public double add(double a, double b, double c) {  
        return a + b + c;  
    }  
}  

Overriding (ghi đè phương thức)
Để định nghĩa lại một phương thức đã có mặt ở lớp cha.
class Vehicle{    
  void run(){System.out.println("Vehicle is running");}    
}    
class Bike2 extends Vehicle{    
  void run(){System.out.println("Bike is running safely");}    
  public static void main(String args[]){    
  Bike2 obj = new Bike2();//creating object    
  obj.run();
  }    
}   

Extends
Một đối tượng thu được tất cả tất cả thuộc tính và hành vi của đối tượng cha. Ý tưởng đằng sau tính kế thừa là bạn có thể tạo một lớp mới mà được xây dụng dựa trên các lớp đang tồn tại. khi bạn kế thừa từ một lớp đang tồn tại bạn có thể tái sử dụng các phương thức và các trường hợp của cha, bạn có thể bổ sung thêm các phương thức và các trường khác. Tính kế thừa biểu diễn mối quan hệ IS-A.
Ta sử dụng từ khóa extends của lớp con để kế thừa các thuộc tính của lớp cha trừ các thuộc tính private của lớp cha.
Cú pháp:
Class <ten_con> extends <tên_cha>{…}
Super Keyword
Từ khóa super trong java là một biến tham chiếu được sử dụng để tham chiếu đến đối tượng lớp cha trực tiếp.
Bất cứ khi nào bạn tạo thể hiện cho lớp con, một thể hiện của lớp cha được tạo ra một các ngầm định và được tham chiếu bằng biến super.
class Animal{  
    String color="white";  
}  
class Dog extends Animal{  
    String color="black";  
    void printColor(){  
        System.out.println(color);//prints color of Dog class  
        System.out.println(super.color);//prints color of Animal class  
    }  
}  
class TestSuper1{  
    public static void main(String args[]){  
    Dog d=new Dog();  
    d.printColor();  
    }
}  


public class SieuNhan {
	private String ten, tuoi;
	
	public SieuNhan(String ten, String tuoi) {
		this.ten = ten;
		this.tuoi = tuoi;
	}

	void out() {
		System.out.println(ten+" - "+tuoi);
	}
}
package jse;

public class SieuNhanXanh extends SieuNhan{
	private String mau, trangBi;

	public SieuNhanXanh(String ten, String tuoi, String mau, String trangBi) {
		super(ten, tuoi);
		this.mau = mau;
		this.trangBi = trangBi;
	}
	
}
package jse;
public class Main {
	public static void main(String[] args) {
		SieuNhanXanh sn =new SieuNhanXanh("AI", "19" ,"Xanh", "Kiem");
		sn.out();
	}
}

public class SieuNhan {
	private String ten, tuoi;
	
	public SieuNhan(String ten, String tuoi) {
		this.ten = ten;
		this.tuoi = tuoi;
	}

	void out() {
		System.out.println(ten+" - "+tuoi);
	}
}
package jse;

public class SieuNhanXanh extends SieuNhan{
	private String mau, trangBi;

	public SieuNhanXanh(String mau, String trangBi) {
		super("sieu nhan xanh", "19");
		this.mau = mau;
		this.trangBi = trangBi;
	}
	
}
package jse;

public class Main {
	public static void main(String[] args) {
		SieuNhanXanh sn =new SieuNhanXanh("Xanh", "Kiem");
		sn.out();
	}
}
Access modifier
Để kiểm soát mức độ mức độ truy cập vào các thành phần (biến, phương thức) của một lớp. Java cung cấp bốn loại access modifier chính: public, protected, default, private. Việc sử dụng access modifier thích hợp là rất quan trọng để bảo đảm tính bảo mất, tính bảo trì và tính linh hoạt của mã.
Access Modifier
Phạm vi truy cập
public
Toàn bộ chương trình
protected
Chỉ trong cùng package hoặc lớp con
default (gói)
Chỉ trong cùng package
private
Chỉ trong cùng lớp
Quy tắc:
- một lớp chỉ có thể có một access modifier duy nhất. nếu không có từ khóa nào được sử dụng, mặc định là default
- các phương thức và biến trong cùng một lớp có các access modifier khác nhau	
- các lớp con có thể truy cập vào các thành phần có mức truy cấp là private của lớp cha
- các lớp không liên quan không thể truy cập vào các thành phần có mức độ truy cập là default hoặc protected của lớp
- các lớp không liên quan không thể truy cập vào các thành phần có mức truy cập là private của lớp.
Enum
Enum là một từ khóa trong java, là một kiểu dữ liệu đặc biệt đại diện cho hằng số cố định
Enum có thể chứ các trường, phương thức và constructor.
Bởi vì các giá trị của enum là các hằng số, nên tên của các trường kiểu enum thường là các chữ cái hoa.
Cú pháp:
Enum tên{…}
equals
Dùng để so sánh kiểu dữ liệu không phải nguyên thủy
Cú pháp:
Public boolean equals(Object obj){
	if(this == obj) return true;
	if(this == null) return fault;
	if(this.getClass() != obj.getClass()) return fault;
	MyDate other = (MyDate) obj;
	if(this.day != other.day) return fault;
	if(this.month != other.month) return fault;
	if(this.year != other.year) return fault;
	Return true;
}
getName()
là một phương thức để lấy ra tên của một đối tượng cụ thể. Tên này thường là chuỗi ký tự String dùng để xác định hoặc phân biệt đối tượng đó với các đối tượng khác trong chương trình
garbage Collection
có nghĩa là các đối tượng không còn được tham chiếu nữa. để thực hiện quá trình tự động khôi phục bộ nhớ không được sử dụng tại runtime một cách tự động. đó là một cách để phá hủy đối tượng không sử dụng nữa
ưu điểm:
loại bỏ các đối tượng không được tham chiếu từ bộ nhớ heap. Nó được thực hiện tự động bởi trình thu gom rác.
Trường hộp đối tượng không được tham chiếu:
- gán bởi giá trị null
- gán đối tượng đến một tham chiếu khác
- bởi một đối tượng annonymous
finalize();
được gọi mỗi lần trước khi đối tượng được thu gom rác. Có thể được thực hiện để sử lý dọn dẹp
cú pháp:
protected void finalize(){}
gc();
được sử dụng để gọi bộ thu gom rác để thực hiện quá trình dọn dẹp. phương thức gc() được cài đặt trong System và Runtime.
Giải thích code
protected void finalize() throws Throwable{
	Person.count--;
}
Throwable: phương thức finalize có thể ném ra một ngoại lệ throwable. Một ngoại lệ được ném ra từ phương thức finalize() nó sẽ bị GC bỏ qua, và đối tượng vẫn không được thu hồi như mong đợi
class Person {
    static int count = 0;

    // Constructor
    public Person() {
        count++; // Tăng biến đếm khi có đối tượng mới được tạo ra
    }

    // Phương thức finalize
    protected void finalize() throws Throwable {
        count--; // Giảm biến đếm khi đối tượng bị thu hồi
        super.finalize(); // Gọi finalize của lớp cha
    }
    
    // Phương thức để lấy số lượng đối tượng Person
    public static int getCount() {
        return count;
    }
}

public class Main {
    public static void main(String[] args) {
        System.out.println("Số đối tượng Person hiện tại: " + Person.getCount()); // 0
        
        Person p1 = new Person();
        Person p2 = new Person();
        
        System.out.println("Số đối tượng Person hiện tại: " + Person.getCount()); // 2
        
        p1 = null; // Đánh dấu p1 để được thu hồi bộ nhớ
        p2 = null; // Đánh dấu p2 để được thu hồi bộ nhớ
        
        // Gọi Garbage Collector
        System.gc();
        
        // Chờ một chút để GC có thời gian chạy
        try {
            Thread.sleep(1000); 
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        
        System.out.println("Số đối tượng Person hiện tại: " + Person.getCount()); // 0 (nếu GC đã chạy)
    }
}
PoLymorphinsm (đa hình)
Nếu một tác vụ thực hiện theo nhiều các khác nhau thì được goi là đa hình.
Ví dụ: Thuyết phục khách hàng theo nhiều cách khác nhau. 
Abstract (trừu tượng)
Ẩn triển khai nội bộ và chỉ hiện thị chức năng cho người dùng thì được gọi là trừu tượng.
Chúng cung cấp bane thiết kế để các nhóm khác làm theo và một số phương thức vẫn chưa được xác định. Giúp tạo ra cơ sở mã tốt và có thể mở rộng
Ví dụ: Trong một cuộc điện thoại, chúng ta không biết quá trình xử lý nội bộ.
Java sử dụng abstract (0 ->100) và interface (100) để đạt được trừu tượng.
Cú pháp:
abstract class <name> { }
Interface (giao diện)
Là một bản thiết kế của một lớp, nó chỉ có các hằng số tĩnh và phương thức trừu tượng. interface là một kĩ thuật để thu được tính trừu tượng hoàn toàn và đa kế thừa trong java. Interface cũng biểu diễn mối qua hệ IS-A. nó không thể được khởi tạo giống như lớp trừu tượng.
Các trường của interface là public, static, final theo mặc định và tất cả các phương thức là public.
Interface không phải là một lớp. lớp mô tả thuộc tính và hành vi của một đối tượng. interface chứa các hành vi mà một class triển khai.
Trừ khi một lớp triển khai interface là một lớp trừu tượng abstract còn lại tất cả các phương thức của interface cần được định nghĩa trong class
Điểm khác biệt với class
    • Không chứa hàm constructor.
    • Phương thức đều là abstract.
    • Không thể kế thừa từ một lớp và nó được triển khai từ một lớp.
    • Một interface có thể kế thừa từ một interface khác.

Sự khác biệt giữa abstract và interface
    • Abstract có thể có các phương thức trừu tượng hoặc không trừu tượng.
    • Abstract không hỗ trợ đa kế thừa.
    • Abstract có thể có các biến final, non-final, static, non-static.
    • Abstract có thể triển khai thành interface.
    • …
    • Interface chỉ có thể có phương thức trừu tượng.
    • Interface hỗ trợ đa kế thừa.
    • Interface chỉ có các biến final và static.
    • Interface không thể triển khai thành abstract.
    • …

Encapsulation (Đóng gói)
Liên kết (hoặc gói) mã và dữ liệu với nhau thành một đơn vị duy nhất được gọi là đóng gói.
Ví dụ: Java bean là lớp được đóng gói hoàn toàn vì tất cả dữ liệu đều riêng tư ở đây.
Constructor
Khởi tạo một đối tượng khi nó được tạo. nó có cùng tên với lớp của nó. tuy nhiên, các constructor không có kiểu trả về rõ ràng.
Constructor có thể có tham số hoặc không có tham số.
Tạo một đối tượng người dùng có tên, tuổi. Tạo người 2 người dùng là Thanh, Minh có 2 thông tin là tên, tuổi.
class User{
	String name;
	int age;
	User(){}
	User(String name, int age){
		this.name = name;
		this.age = age;
	}
}
public class Solution{	
	public static void main(String[] args) {
		// Object 1
		User Thanh = new User();
		Thanh.name = "Nguyen Thi Thanh";
		Thanh.age = 32;
		// Object 2
		User Minh = new User("Hoàng Văn Minh", 28);
		System.out.println(Thanh.name + " " + Thanh.age);
		System.out.println(Minh.name + " " + Minh.age);
	}
}
Nguyen Thi Thanh 32
Hoàng Văn Minh 28

Lỗi hay gặp:
class User{
	String name;
	int age;
	User(){}
	User(String name, int age){
		this.name = name;
		this.age = age;
	}
}
public class Solution{	
	public static void main(String[] args) {
		// Object 1
		User Thanh = new User();
		System.out.println(Thanh.name + " " + Thanh.age);
	}
}
Null 0
toString()
In kết quả ra màn hình dưới dạng chuỗi. kiểu dữ kiệu là một String.
import java.util.Scanner;
class Person{
	private String name;
	private int age;
	private String address;
	public static Scanner sc = new Scanner(System.in);
	public Person() {
		this.name = sc.nextLine();
		this.age = sc.nextInt();
		sc.nextLine();
		this.address = sc.nextLine();
	}
	public String toString() {
		return this.name + " " + this.age + " " + this.address;
	}
}
public class Main{
	public static void main(String[] args) {
		Person SinhVien1 = new Person();
		System.out.println(SinhVien1.toString());
	}
}
line1: le duc thang
line2: 19
line3: phu da
le duc thang 19 phu da
 

Getter và setter
Là 2 phương thức sử dụng để cập nhật và lấy ra giá trị thuộc tính, đặc biệt dành cho các thuộc tính ở phạm vi private. 
Việc sử dụng set và get cần thiết trong việc kiểm soát những thuộc tính quan trọng mà ta thường sử dụng và yêu cầu giá trị chính xác. 
Cú pháp:
Setter:
public void setter (<tham số giá trị mới>){
	This.<tên thuộc tính> = <tham số giá trị mới>;
}
Getter: 
<kiểu dữ liệu thuộc tính> getter (){
	Return this.<tên thuộc tính>;
}
public class Person {	
	public String name;
	private int age;
	public float height;	
	public Person(String name, int age, float height) {
		this.name = name;
		this.age = age;
		this.height = height;
	}
	public void setAge(int age) {
		if (age>=0 && age<=100 ) {
			this.age = age;
		}
	}	
	public int getAge() {
		return this.age;
	}
	public void getInfo() {
		System.out.println("Name:"+this.name);
		System.out.println("Age:"+this.age);
		System.out.println("Height:"+this.height);
	}	
}


Mickey
public class SinhVien {
	private String hoTen, lop;
	private int namSinh, tuoi;
	public SinhVien() {
		
	}
	public SinhVien(String hoTen, int namSinh, int tuoi, String lop) {
		this.hoTen = hoTen;
		this.lop = lop;
		this.namSinh = namSinh;
		this.tuoi = tuoi;
	}
	public String getHoTen() {
		return hoTen;
	}
	public String getLop() {
		return lop;
	}
	public int getNamSinh() {
		return namSinh;
	}
	public int getTuoi() {
		return tuoi;
	}
	public void setHoTen(String hoTen) {
		this.hoTen = hoTen;
	}
	public void setLop(String lop) {
		this.lop = lop;
	}
	public void setNamSinh(int namSinh) {
		this.namSinh = namSinh;
	}
	public void setTuoi(int tuoi) {
		this.tuoi = tuoi;
	}
	
}
class Solution{
	public static void main(String[] args) {
		SinhVien sv1 = new SinhVien("Micky", 2005, 18, "12a1");
		System.out.println(sv1.getHoTen());
	}
}

In danh sách các đôi tượng nhập từ bàn phím của lớp sinh viên có thuộc tính gồm họ và tên, tuổi, địa chỉ.
Code 1:
import java.util.Scanner;
class Person{
	private String name;
	private int age;
	private String address;
	public Person() {
	}
	public Person(String name, int age, String address) {
		this.name = name;
		this.age = age;
		this.address = address;
	}
	
	public String getName() {
		return name;
	}
	public int getAge() {
		return age;
	}
	public String getAddress() {
		return address;
	}
	public void setName(String name) {
		this.name = name;
	}
	public void setAge(int age) {
		this.age = age;
	}
	public void setAddress(String address) {
		this.address = address;
	}
	public String toString() {
		return this.name + " " + this.age + " " + this.address;
	}
}
import java.util.Scanner;
public class SinhVien {
	private Person[] sinhVien;
	Scanner sc = new Scanner(System.in);
	public Person[] EnterListArr() {
		System.out.print("The number element in student list: "); int n = sc.nextInt(); sc.nextLine();
		sinhVien = new Person[n];
		for(int i = 0; i < n; i++) {	
			String name = sc.nextLine();
			name = String.format("%-30s", name);
			int age = sc.nextInt();
			sc.nextLine();
			String address = sc.nextLine();
			address = String.format("%30s", address);
			sinhVien[i] = new Person(name, age, address);
		}
		return sinhVien;
	}
	public void PrintListArr(Person[] person) {
		for(Person value : person) {
			System.out.println(value);
		}
	}	
	public static void main(String[] args) {
		SinhVien sinhVien = new SinhVien();
		sinhVien.EnterListArr();
		sinhVien.PrintListArr(sinhVien.sinhVien);
	}
}

Code 2:
import java.util.Scanner;
class Person{
	private String name;
	private int age;
	private String address;
	public Person() {
	}
	public Person(String name, int age, String address) {
		this.name = name;
		this.age = age;
		this.address = address;
	}	
	public String getName() {
		return name;
	}
	public int getAge() {
		return age;
	}
	public String getAddress() {
		return address;
	}
	public void setName(String name) {
		this.name = name;
	}
	public void setAge(int age) {
		this.age = age;
	}
	public void setAddress(String address) {
		this.address = address;
	}
	public String toString() {
		return this.name + " " + this.age + " " + this.address;
	}
}
import java.util.Scanner;
public class SinhVien {
	private Person[] sinhVien;
	Scanner sc = new Scanner(System.in);
	public Person[] EnterListArr() {
		System.out.print("The number element in student list: "); int n = sc.nextInt(); sc.nextLine();
		sinhVien = new Person[n];
		for(int i = 0; i < n; i++) {	
			String name = sc.nextLine();
			int age = sc.nextInt();
			sc.nextLine();
			String address = sc.nextLine();
			sinhVien[i] = new Person(name, age, address);
		}
		return sinhVien;
	}

	public void PrintListArr(Person[] person) {
		for(Person value : person) {
			System.out.printf("%-30s%-30d%-30s\n",value.getName(), value.getAge(), value.getAddress());
		}
	}
	
	public static void main(String[] args) {
		SinhVien sinhVien = new SinhVien();
		sinhVien.EnterListArr();
		sinhVien.PrintListArr(sinhVien.sinhVien);
	}
}

Code 3:
import java.util.Scanner;
class Person{
	private String name;
	private int age;
	private String address;
	public Person() {
	}
	public Person(String name, int age, String address) {
		this.name = name;
		this.age = age;
		this.address = address;
	}
	
	public String getName() {
		return name;
	}
	public int getAge() {
		return age;
	}
	public String getAddress() {
		return address;
	}
	public void setName(String name) {
		this.name = name;
	}
	public void setAge(int age) {
		this.age = age;
	}
	public void setAddress(String address) {
		this.address = address;
	}
	public String toString() {
		return this.name + " " + this.age + " " + this.address;
	}
	
	public Person[] EnterListArr(Person[] sinhVien)  {
		System.out.print("The number element in student list: "); int n = sc.nextInt(); sc.nextLine();
		sinhVien = new Person[n];
		for(int i = 0; i < n; i++) {	
			String name = sc.nextLine();
			int age = sc.nextInt();
			sc.nextLine();
			String address = sc.nextLine();
			sinhVien[i] = new Person(name, age, address);
		}
		return sinhVien;
	}
	public void PrintListArr(Person[] person) {
		for(Person value : person) {
			System.out.printf("%-30s%-30d%-30s\n",value.getName(), value.getAge(), value.getAddress());
		}
	}
}
import java.util.Scanner;
public class SinhVien {
	private static Person[] SV;
	public static void main(String[] args) {
		Person SinhVien = new Person();
		SV = SinhVien.EnterListArr(SV);
		SinhVien.PrintListArr(SV);
	}
}

Instance intializer block
Khối này sẽ thực thi mỗi khi đối tượng của lớp được tạo.
class Display{
	{System.out.println("Hello World");}
}
public class Solution{	
	public static void main(String[] args) {
		Display display = new Display();
	}
}
Hello world
Object class
Theo mặc định, lớp object là lớp cha của tất cả các lớp trong java. Object có lợi thế nếu muốn tham chiếu bất kỳ đối tượng nào mà bạn không biết loại.

getClass()
Để trả về tên Class của một object nào đó.
class Person{
	public static void main(String[] args) {
		Person b = new Person();
		String c = new String();
		System.out.println(b.getClass());
		System.out.println(c.getClass());
	}
}

hashCode()
Trả về giá trị mã băm cho tập hợp này.
notify()
equals()
Object clone() throws CloneNotSupportedException
toString()
notifyAll()
wait(long timeout) throws InterruptedException
wait() throws InterruptedException
finalized() throws Throwable
Object Cloning

Bài tập OOP
import java.util.Scanner;
public class PhanSo {
    private int tuSo;
    private int mauSo;

    // Constructor
    public PhanSo(int tuSo, int mauSo) {
        this.tuSo = tuSo;
        this.mauSo = mauSo;
    }

    // Getter và Setter
    public int getTuSo() {
        return tuSo;
    }

    public int getMauSo() {
        return mauSo;
    }

    // Tìm ước chung lớn nhất
    private int ucln(int a, int b) {
        while (b != 0) {
            int temp = a % b;
            a = b;
            b = temp;
        }
        return a;
    }

    // Rút gọn phân số
    private void rutGon() {
        int ucln = ucln(tuSo, mauSo);
        tuSo /= ucln;
        mauSo /= ucln;
    }

    // Các phép toán
    public PhanSo cong(PhanSo ps) {
        int tu = tuSo * ps.mauSo + ps.tuSo * mauSo;
        int mau = mauSo * ps.mauSo;
        return new PhanSo(tu, mau);
    }

    public PhanSo tru(PhanSo ps) {
        int tu = tuSo * ps.mauSo - ps.tuSo * mauSo;
        int mau = mauSo * ps.mauSo;
        return new PhanSo(tu, mau);
    }

    public PhanSo nhan(PhanSo ps) {
        int tu = tuSo * ps.tuSo;
        int mau = mauSo * ps.mauSo;
        return new PhanSo(tu, mau);
    }

    public PhanSo chia(PhanSo ps) {
        if (ps.tuSo == 0) {
            throw new IllegalArgumentException("Không thể chia cho 0");
        }
        int tu = tuSo * ps.mauSo;
        int mau = mauSo * ps.tuSo;
        return new PhanSo(tu, mau);
    }

    // Kiểm tra phân số có tối giản hay không
    public boolean laPhanSoToiGian() {
        return ucln(tuSo, mauSo) == 1;
    }

    // In phân số
    @Override
    public String toString() {
        return tuSo + "/" + mauSo;
    }
}
package RunMain;
import PhanSo.*;
import java.util.Scanner;
public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.print("Nhập số lượng phân số: ");
        int n = scanner.nextInt();

        PhanSo[] phanSos = new PhanSo[n];

//        for (int i = 0; i < n; i++) {
//            System.out.print("Nhập tử số của phân số thứ " + (i + 1) + ": ");
//            int tu = scanner.nextInt();
//            System.out.print("Nhập mẫu số của phân số thứ " + (i + 1) + ": ");
//            int mau = scanner.nextInt();
//            phanSos[i] = new PhanSo(tu, mau);
//        }
        phanSos[0] = new PhanSo(3,2);
        System.out.println("Các phân số đã nhập dưới dạng tối giản:");
        for (PhanSo ps : phanSos) {
            System.out.println(ps);
        }

    }
}
Xử lý ngoại tệ

Error
Là lỗi không thể chữa được các tình huống nghiêm trọng. ví dụ: OutOfMemoryError, VirtualMachineError, … 
Exception 
Là một tình trạng bất thường. ngoại lệ là một sự kiện làm gián đoạn luồng bình thường của chương trình. Nó là một đối tượng được ném ra tại runtime. Ngoại lệ này có thể xử lý được
Throw
Được sử dụng để ném ra một ngoại lệ cụ thể.
Chúng ta có thể ném ra 1 trong 2 ngoại lệ checked hoặc unchecked. Chủ yếu được sử dụng để ném ra ngoại lệ tùy chỉnh (ngoại lệ do người dùng tự định nghĩa).
Cú pháp:
    • throw exception;
    • throw new IOException(“…”);
Throws
Checked exception (ngoại lệ kiểm tra) là các loại ngoại lệ mà trình biên dịch yêu cầu phải xử lý hoặc khai báo thông qua từ khóa throws.

Thường là các tình huống mà chương trình không thể kiểm soát được, như đọc/ghi, kết nối mạng, hoặc thao tác với cơ sở dữ liệu.

Được sử dụng để khai báo một ngoại lệ, nó thể hiện thông tin cho lập trình viên rằng có thể xảy ra một ngoại lệ, vì vậy nó tốt hơn cho các lập trình viên để cung cấp các mã xử lý ngoại lệ để duy trì luồng bình thường của chương trình.

Exception Handing chủ yếu được sử dụng để xử lý ngoại lệ checked. Nếu xảy ra bất kỳ ngoại lệ unchecked như nullPointerException đó là lỗi của lập trình viên mà anh ta không thực hiện kiểm tra trước khi code được sử dụng.

Cú pháp:
Return_type method_name() throws exception_class_name{ … }
Checked Exception
Là các loại ngoại lệ mà trình biên dịch phải yêu cầu phải xử lý khoặc khai báo thông qua từ kháo throws. Thường là các tình huống mà chương trình không thể kiểm soát hoặc dự đoán được, như đọc ghi tệp tin, kết nối mạng, hoặc thao tác với cơ sở dữ liệu. mục tieeuuu của việc yêu cầu xử lý checked exception là để đảm bảo rằng các tình huống không mong muốn sẽ được xử lý một cách an toàn, tránh gây ra các vấn đề không mong muốn cho người sử dụng cuối.
ParseException
Là một ngoại lệ Exception được sử dụng để báo cáo lỗi khi không thể phân tích (parse) theo định dạng một chuỗi mà nó mong đợi. ngoại lệ này thường được sử dụng trong các tình huống liên quan đến việc chuyển đổi chuỗi thành các kiểu các, chẳng hạn như ngày giờ, số, hoặc bất kỳ loại dữ liệu nào cần parsing.
Ví dụ: nếu bạn đang sử dụng lớp SimpleDateFormat để phân tích một chuỗi thành một đối tượng date và chuoix đó không phù hợp với định dạng chỉ định thì một parseException sẽ được ném ra 
Unchecked Exception
Là các loại ngoại lệ mà trình biên dịch không yêu cầu phả xử lý hoặc khai báo. Thường là các lỗi logic hoặc tình huống không mong muốn trong quá trình thực thii chương trình. Có thể hoặc không xử lý những ngoại lệ này, tùy thuộc vào yeeuu cầ cụ thể của uungs dụng
NullPointerException
Dùng để xử lý khi thực hiện một hoạt động trên một đối tượng mà thực sự không tồn tại, có giá trị null.

Ví dụ:

class test{
	public static void main(String[] args) {
		try {
			int[] n = null;
			System.out.println(n.length);
		} catch(NullPointerException e) {
			System.out.println("Lỗi null");
		}
	}
}
ArrayIndexONutOfBoundsException
Xảy ra khhi truy cập phần tử mảng ở một chỉ mục nằm ngoài phạm vi của mảng

Ví dụ: 

public static void main(String[] args) { 
try { int[] numbers = {1, 2, 3}; 
System.out.println(numbers[4]);
} catch (ArrayIndexOutOfBoundsException e) { 
System.out.println("Lỗi: Phần tử không tồn tại trong mảng.");}
}
NumberFormatException
Xảy ra khii chuyển đổi một chuỗi thành một số, nhưng chuỗi không thể chuyển thành một số hợp lệ

Ví dụ:

import java.util.Scanner;

class test{
	public static void main(String[] args) {
		
		try {
			String a = "aa";
			int b = Integer.parseInt(a);
			System.out.println(a);
		} catch (NumberFormatException e) {
			System.out.println("Lỗi: " + e.getMessage());
		}
	}
}

ArithmeticException
Xảy ra khi một phép toán số học không hợp lệ

Ví dụ:

public class Main {
	
	public static void main(String[] args) {
		try {
			int a = 50/0;
			System.out.println(a);
		} 
		catch (ArithmeticException e) {
			System.out.println("running!!");
		}
		finally {
			System.out.println("running!!");
		}
	}
}
ClassCastExeption
Xảy ra khi chúng ta cố gắng chuyển đổi một đối tượng thành một lớp mà không thể chuyển đổi được
IllegalArgumentException()
Xảy ra khi một phương thức nhận một đối số không hợp lệ

Ví dụ:

import java.util.Scanner;

class test{
	public static void main(String[] args) {
		try {
			Scanner sc = new Scanner(System.in);
			int age = sc.nextInt();
			if (age < 0) {
				throw new IllegalArgumentException("Tuổi không được âm");
			}
		} catch (IllegalArgumentException e) {
			System.out.println("Lỗi: " + e.getMessage());
		}
	}
}
InputMismatchException
Dùng để xử lý khi nhập sai hoặc làm việc sai với kiểu dữ liệu.

Ví dụ:

import java.util.InputMismatchException;
import java.util.Scanner;

class test{
	public static void main(String[] args) {
		try {
			Scanner sc = new Scanner(System.in);
			double a = sc.nextDouble();
			System.out.println(a);
		} catch(InputMismatchException e) {
			System.out.println("Bạn đã nhập sai dữ liệu:" + " " + e);
		}
	}
}
PatternSyntaxException
Dùng để cho ta biết lỗi cú pháp trong biểu thức chính quy
Yêu cầu người dùng nhập vào một biểu thức chính quy, nếu biểu thức chính quy đó hợp lệ thì in ra Valid, ngược lại in ra Invalid

import java.util.Scanner;
import java.util.regex.*;

public class Solution
{
    public static void main(String[] args){
            Scanner in = new Scanner(System.in);
            int testCases = Integer.parseInt(in.nextLine());
            while(testCases>0){
                try{
                    String pattern = in.nextLine();
                    Pattern PatternName = Pattern.compile(pattern);
                    System.out.println("Valid");
                }catch(PatternSyntaxException e){
                    System.out.println("Invalid");
                }             
                testCases--; 
            }
        } 
        
}
Exception Handling
Xử lý ngoại lệ là một cơ chế xử lý các lỗi runtime như ClassNotFound, IO, SQL, Remote, …
Lợi thế cốt lõi của việc xử lý ngoại lệ là duy trì luồng bình thường của ứng dụng. Ngoại lệ thường làm gián đoạn luồng bình thường của ứng dụng đó.
try-catch-finally
    • try: Được sử dụng để chứa một đoạn code có thể xảy ra ngoại lệ. nó phải được khai báo trong phương thức.
    • Sau một khối lệnh try bạn phải khai báo khối lệnh catch hoặc finally hoặc cả 2.
    • catch: Được sử dụng để xử lý các exception. Nó phải được sử dụng sau khối try. bạn có thể sử dụng nhiều khối catch với một khối try duy nhất.
    • finally: Code trong này luôn được thực thi
Cú pháp:
try{
// code nghi ngờ có ngoại lệ
} catch(exception_class_Name ref){
// code xử lý ngoại lệ
} finally {
	// code trong khối này luôn được thực thi
}
Locale
Cần import java.util.Locale;
Để chỉ định quốc gia và ngôn ngữ. thao tác này sẽ hiển thị các cài đặt liên quan khác, chẳng hạn như hiển thị ngày và giờ. Máy ảo Java (JVM) lấy các cài đặt vùng từ hệ điều hành. Tuy nhiên ngôn ngữ mặc định trong Java có thể được thay đổi bằng một phương thực đặt biết nếu cần.
Country
Language Code
Country Code
English
en
EN
Germany
de
DE
China
zh
CN
Czech Republic
cs
CZ
Netherlands
nl
AN
France
fr
FR
Italy
it
IT
Japan
ja
JP
Korea
ko
KR
Russia
ru
RU
Spain
es
ES
Bulgaria
bg
BG
Canada
ca
CA
Croatia
hr
HR
Denmark
da
DK
Finland
fi
FI
Greece
el
GR
Hungary
hu
HU
Indonesia
in
ID, IN
Latvia
lv
LV
Lithuania
lt
LT
Norway
nb
NO
Portugal
pt
PT
Romania
ro
RO
Serbia
sr
RS
Slovakia
sk
SK
Slovenia
sl
SI
Sweden
sv
SE
Thailand
th
TH
Turkey
tr
TR
Ukraine
uk
UA
Vietnam
vi
VN

Ví dụ:
// cài đặt quốc gia Mỹ và ngôn ngữ Mỹ;
package Content;
import java.util.Locale;
public class Run_01{
	public static void main(String[] args) {
		Locale vNlanguage = Locale.US;
		System.out.println(vNlanguage);
		Locale vNlanguage1 = new Locale("en", "US");
		System.out.println(vNlanguage1);
	}
		
}
Locale.getDefault();
Dùng để xem ngôn ngữ hiện tại mà bạn đang sử dụng.
package RunMain;
import java.util.Locale;
public class Main {
	@SuppressWarnings("deprecation")
	public static void main(String[] args) {
		Locale current = Locale.getDefault();// en_US
		System.out.println(current);
		current = new Locale("vi", "VN");
		System.out.println(current); // vi_VN
		System.out.println(Locale.getDefault()); // en_US
	}
}
}
Locale.setDeafault();
Dùng để thay đổi ngôn ngữ mặc định của phiên bản
package RunMain;
import java.util.Locale;
public class Main {
	@SuppressWarnings("deprecation")
	public static void main(String[] args) {
		System.out.println(Locale.getDefault());// en_US
		Locale.setDefault(Locale.KOREA);
		System.out.println(Locale.getDefault()); // ko_KR

	}
}
GetDisplayLanguage()
Trả về tên ngôn ngữ đang sử dụng
Ví dụ:
// xem ngôn ngữ của Locale
package Content;
import java.util.Locale;
public class Run_01{
	public static void main(String[] args) {
		Locale.setDefault(Locale.CHINA);
		Locale current = Locale.getDefault();
		System.out.println(current.getDisplayLanguage());
	}
		
}
getDisplayCountry()
trả về tên quốc gia đang sử dụng
getlanguage()
trả về mã ngôn ngữ đang sử dụng
getCountry()
trả về mã quốc gia đang sử dụng
getProperty()


NumberFormat
Được dùng để định dạng số theo một số quốc gia, khu vực cụ thể. Ngoài ra còn được dùng để xử lý với số chẳng hạn như làm tròn số, chuyển đổi kiểu dữ liệu số, …
Cần import java.text.NumberFormat;
Cú pháp:
NumberFormat <tên> = NumberFormat.getInstance();
Để tạo một Numberformat để định dạng số của khu vực hiện tại của máy ảo JVM
Format()
Phương thức này sẽ trả kết quả có kiểu dữ liệu là chuỗi ứng với số sau khi định dạng
Cú pháp:
format(kiểu_dữ_liệu <tên>);
package RunMain;
import java.util.Locale;
import java.text.NumberFormat;
public class Main {
	@SuppressWarnings("deprecation")
	public static void main(String[] args) {
		Locale americanLocale = new Locale("en", "US"); // tạo ra một trường sử dụng định dang số của Hoa kỳ
		NumberFormat american = NumberFormat.getInstance(americanLocale);// tạo ra một trường để làm việc với số của Hoa kỳ
		double d1 = 12000.34567;
		String str1 = american.format(d1); // format() luôn trả về kiểu String
		System.out.println(str1); // kết quả: 12,000.346
		
		Locale vietNamLocale = new Locale("vi", "VN");
		NumberFormat vietNamese = NumberFormat.getInstance(vietNamLocale);
		String str2 = vietNamese.format(d1);
		System.out.println(str2); // 12.000,346
		
		Locale enlishLocale = new Locale("en", "EN");
		NumberFormat england = NumberFormat.getInstance();
		String str3 = england.format(d1);
		System.out.println(str3); // 12,000.346
	}
}
getCurrencyInstance()
để định dạng tiền tệ 
cần import java.util.Currency;
public String CurrencyDefault(double number) {
		@SuppressWarnings("deprecation")
		Locale america = new Locale("en", "US");
		NumberFormat currencyDefault = NumberFormat.getCurrencyInstance(america);
		String str = currencyDefault.format(number);
		return str;
	}
setCurrencyInstance()
để thay đổi từ kiểu đơn vị tiền tệ quốc gia, khu vực này sang kiểu đơn vị tiền tệ của quốc gia, khu vực khác
public interface List<E> extends Collection<E>
Là một interface trong java. Nó chứa các phương thức để chèn và xóa dựa trên chỉ số index. Nó đại diện một danh sách các phần tử có thứ tự, có thể chứa các phần tử trùng lặp, mỗi phần tử trong list có một chỉ số duy nhất bắt đầu từ 0.
size(int value)
Dùng để trả về số lượng có trong List<>
object get(int index)
Dùng để trả về giá trị của phần tử ở vị trí thứ index trong List<>
Linked Structure
Là cấu trúc dạng xâu.
Xây dựng một danh sách dạng xâu và in ra màn hình
JSon 20 London
Mickey 12 USA
Author 19 VietNam
class Person{
	private String name;
	private int age;
	private String address;
	private Person next = null;
	Person(String name, int age, String address){
		this.name = name;
		this.age = age;
		this.address = address;
	}
	public Person getNext() {
		return this.next;
	}
	public void setNext(Person next) {
		this.next = next;
	}
	@Override
	public String toString() {
		return name + " " + age + " " + address;
	}
}
public class Solution{
	public static void main(String[] args) {
		Person person1 = new Person("JSon", 20, "London");
		Person person2 = new Person("Mickey", 12, "USA");
		Person person3 = new Person("Author", 19, "VietNam");
		person1.setNext(person2);
		person2.setNext(person3);
		Person temp = person1;
		while(true) {
			System.out.println(temp.toString());
			temp = temp.getNext();
			if (temp == null){
				break;
			}
		}
	}	
}


Linked list
    • Là danh sách liên kết. là moọt tập hợp các nút (nodes) kết hợp với nhau để tạo thành một thứ tự tuyến tính. 
    • Mỗi nút là một đối tượng lưu trữ một tham chiếu đến một phần tử và một tham chiếu, gọi là next, đến một nút khác.
    • Tham chiếu ‘next’ bên trong một nút có thể được xem như một liên kết hoặc con trỏ đến một nút khác. 
    • Nút đầu tiên của một danh sách liên kết thường được gọi là đầu của danh sách.
Liên kết đơn – singly linked list:

Liên kết vòng – Circular linked list:

Liên kết kép – Doubly linked list:

    • Vấn đề với các đối tượng tự tham chiếu là chúng biết rằng chúng là một phần của danh sách.
    • Một cách tiếp cận tốt hơn là quản lý một danh sách riêng các nút cũng tham chiếu đến các đối tượng được lưu trữ trong danh sách.
    • Danh sách vẫn được quản lý bằng cách sử dụng cách kĩ thuật tương tự.
    • Các đối tượng lưu trữ trong danh sách không cần phải có bất kì triển khai đặc biệt nào để trở thành một phần của danh sách.
    • Một tập hợp danh sách tổng quát có thể được sử dụng để lưu trữ bất kì loại đối tượng nào.
Tạo ra Node trong linked list
Le Duc Thang VietNam
Nguyen Van A VietNam
JSon Ba Lan
class Person{
	private String name;
	private String address;
	Person(String name, String address){
		this.name = name;
		this.address = address;
	}
	@Override
	public String toString() {
		return name + " " + address;
	}	
}
class Node<T>{
	private T data;
	private Node<T> next;
	public T getData() {
		return data; 
	}
	public void setData(T data) {
		this.data = data;
	}
	public Node<T> getNext(){
		return next;
	}
	public void setNext(Node<T> next){
		this.next = next;
	}
}
class Solution{
	public static void main(String[] args) {
		Person p1 = new Person("Le Duc Thang", "VietNam");
		Person p2 = new Person("Nguyen Van A", "VietNam");
		Person p3 = new Person("JSon", "Ba Lan");
		
		Node<Person> Node1 = new Node<Person>();
		Node<Person> Node2 = new Node<Person>();
		Node<Person> Node3 = new Node<Person>();
		
		Node1.setData(p1);
		Node2.setData(p2);
		Node3.setData(p3);
		
		Node1.setNext(Node2);
		Node2.setNext(Node3);
		
		Node<Person> Head = Node1;
		while(true) {
			System.out.println(Head.getData());
			Head = Head.getNext();
			if(Head == null) break;
		}
	}
}

Xây dựng danh sách liên kết (Linked List)
import java.io.IOException;

class Node<T>{
	private T data;
	private Node<T> next;
	Node(){}
	Node(T data, Node<T> next){
		this.data = data;
		this.next = next;
	}
	public T getData() {
		return data;
	}
	public Node<T> getNext() {
		return next;
	}
	public void setData(T data) {
		this.data = data;
	}
	public void setNext(Node<T> next) {
		this.next = next;
	}
}
class LinkedList<T>{
	private Node<T> head;
	LinkedList(){
		this.head = null;
	}
	public void print() {
		Node<T> temp = head;
		while(temp != null) {
			System.out.println(temp.getData());
			temp = temp.getNext();
		}
	}
	public void addFirst(T item) {
		Node<T> newNode = new Node<T>(item, this.head);
		this.head = newNode;
	}
	public void addLast(T item) {
		if(this.head == null) addFirst(item);
		else {
			Node<T> newNode = new Node<T>(item, null);
			Node<T> temp = this.head;
			while(temp.getNext() != null) {
				temp = temp.getNext();
			}
			temp.setNext(newNode);
		}
	}
	public void insertAfter(T key, T toInsert) {
		Node<T> temp = head;
		while(temp != null && !temp.getData().equals(key)) {
			temp = temp.getNext();
		}
		if(temp != null) {
			Node<T> newNode = new Node<T>();
			newNode.setData(toInsert);
			newNode.setNext(temp.getNext());
			temp.setNext(newNode);
		}
	}
		public void remove(T item) {
			if(head == null) throw new RuntimeException("Can not delete");
			if(head.getData().equals(item)) {
				this.head = head.getNext();
				return;
			}
			Node<T> prev = null;
			Node<T> cur = head;
			while(cur != null && !cur.getData().equals(item)) {
				prev = cur;
				cur = cur.getNext();
			}
			if(cur == null) throw new RuntimeException("Can not delete");
			prev.setNext(cur.getNext());
		}
}
public class Solution{
	public static void main(String[] args) {
		LinkedList<String> ll = new LinkedList<String>();
		ll.addFirst("Le Duc Thang");
		ll.addFirst("Nguyen Quang Anh");
		ll.addLast("Json");
		ll.print();
		ll.remove("Le Duc Thang");
		ll.print();
	}
}

Iterator
Là một interface được sử dụng để thay thế Enumerations trong java Collection Framework
Sử dụng iterface để
- duyệt các phần tử từ đầu đến cuối của một collection
- iterator cho phép xóa phần tử khi lặp một collection
public boolean hasNext()
trả về true nếu iterator còn phần tử kế tiếp phần tử đang duyệt. hasNext() được thiết kế chủ yếu dành cho Scanner, thường được sử dụng để đọc dữ liệu từ file ra.

ví dụ: nhập vào sau đó chương trình xuất ra ngay và không có điểm dừng (cứ nhập vào là lại xuất ra màn hình)

import java.util.*;
public class Run_01 {
	public static void main(String args[]) {
		Scanner input = new Scanner(System.in);
        	int lines = 1;
        
        	while (true){
            		String line = input.nextLine();
            		System.out.println(lines + " " + line);
            		lines++;
            		if (!input.hasNext()){
                		break;
            		}
	 	}
}
}
next()
Nó trả về phần tử hiện tại và di chuyển con trỏ đến phần tử tiếp theo
Set
Là một tập hợp có cùng kiểu dữ liệu.
Là một interface kế thừa collection interface trong java. Set là một Collection không thể chứa các phần trử trùng lặp.
Cần import java.util.Set
Set được triển khai bởi Hashset, LinkedHashset, Treeset hoặc EnumSet
- HashSet: lưu trữ các phần tử của nó trong bảng băm, là cách thực hiện tốt nhất, tuy nhiên nó không đảm bảo về thứ tự các phần tử được chèn vào.
- TreeSet: lưu trữ các phần tử cua nó trong một cây, sắp xếp các phần tử của nó dựa trên các giá trị của chúng, về cơ bản là chậm hơn HashSet
- LinkedHashSet: được triển khai dưới dạng bảng băm với có cấu trúc dữ liệu danh sách liên kết, sắp xếp các phần tử của nó dựa trên thứ tự chúng được chèn vào tập hợp (thứ tự chèn)
- enumSet: là một cài đặt chuyên biệt để sử dụng với các kiểu enum
Vì set là một giao diện interface nên cần khởi tạo một triển khai cụ thể để sử dụng nó
Khai báo một set
Set<kiểu_dữ_liệu> tên = new HashSet<kiểu_dữ_liệu>;
Set<kiểu_dữ_liệu> tên = new LinkedHashSet<kiểu_dữ_liệu>;
Set<kiểu_dữ_liệu> tên = new TreeSet<kiểu_dữ_liệu>;
Set<kiểu_dữ_liệu> tên = new EnumSet<kiểu_dữ_liệu>;
Duyệt phần tử trong set
Có thể sử dụng vòng lặp iterator hoặc for-each để duyệt phần tử trong set
add(E e)
Để thêm một giá trị nào đó vào set
addAll()
thêm tất cả các phần tử được chỉ định vào tập hợp này nếu chúng chưa có mặt (thao tác tùy chọn)
remove()
Xóa một phần tử khỏi set
removeAll(Collection<?> c)
xóa bỏ tập hợp này tất cả các phần tử có trong tập hợp này được xác định
clear()
Xóa tất cả các phần tử khỏi tập hợp
contains(Object o)
Trả về true nếu tập hợp này chứa phần tử được chỉ định
containsAll(Collection<?> c)
trả về true nếu tập hợp này chứa tất cả các phần tử của tập hợp chỉ định
equals(Object o)
so sánh đối tượng được chỉ đinh với tập hợp này cho bằng nhau
isEmpty()
trả về true nếu tập hợp này không chứa phần tử nào
iterator()
trả về một trình lặp trên các phần tử của tập hợp này
retainAll(Collection<?> c)
chỉ giữ lại các phần tử trong tập hợp này có trong tập hợp được chỉ định
size()
trả về số phần tử trong tập hợp này
spliterator()
tạo một Spliterator trên các phần tử trông tập hợp này
toArray()
trả về một mảng chứa tất cả các phần tử trong tập hợp này
toArray(T[] a)
trả về một mảng chứa tất cả các phần tử trong tập hợp này; kiểu thời gian chạy của mảng được trả về là kiểu của mảng được chỉ định
bài tập

Map
Được sử dụng để truy xuất dữ liệu theo cặp key value. Mỗi cặp key value được gọi là một mục nhập (entry). Map trong java chỉ chứa các cặp key duy nhất. map hữu ích trong việc tìm kiếm, cập nhật hoặc xóa các phần tử dựa vào các key.
Map.Entry
Entry là một interface con của Map. Vì vậy, có thể truuy cập nó bằng Map.Entry. có cung cấp các phương thức để truy xuất các key và value.
Object getKey()
Dùng để lấy key
Object getValue()
Dùng để lấy value
Collection
Collection và collections trong java là 2 khái niệm khác nhau
Collection là một root interface trog hệ thống cấp bậc Collection. Java collection cung cấp nhiều interface (set, List, Queue, Deque vv) và các lớp (ArrayList, Vector, LinkedList, PriorityQueue, HashSet, LinkedHashSet, TreeSet, vv)

Collections
Comparable
Được dùng để sắp xếp các đối tượng của lớp do người dùng tự định nghĩa ra. Giao diện này chỉ chứa một phương thức có tên là compareTo(Object).
public int compareTo(Object obj)
cần implements comparable<…>. Nó dùng để so sánh đối tượng hiện tại với đối tượng được chỉ định.

có thể sử dụng để sắp xếp: 
- đối tượng String
- Các đối tuongj lớp wrapper
- Các đối tượng do người dùng tạo ra

Collections cung cấp phương thức sort() để phân sắp xếp các phần tử của List.
sort()
Để sắp xếp các phần tử của list.
Bài tập
Sử dụng Compararble, sort() để sắp xếp một danh sách dựa vào tên của sinh viên đó

class Student implements Comparable<Student> {
    private int id;
    private String name;
    private int age;
    private String address;
 
    public Student() {
    }
 
    public Student(int id, String name, int age, String address) {
        super();
        this.id = id;
        this.name = name;
        this.age = age;
        this.address = address;
    }
 
    // getter & setter
     
    @Override
    public String toString() {
        return "Student@id=" + id + ",name=" + name 
                + ",age=" + age + ",address=" + address;
    }
 
    @Override
    public int compareTo(Student student) {
        // sort student's name by ASC
        return this.getName().compareTo(student.getName());
    }
}


 
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;
 
public class ComparableExample {
    public static void main(String[] args) {
        // create list students
        List<Student> listStudents = new ArrayList<Student>();
        // add students to list
        listStudents.add(new Student(1, "Vinh", 19, "Hanoi"));
        listStudents.add(new Student(2, "Hoa", 19, "Hanoi"));
        listStudents.add(new Student(3, "Phu", 20, "Hanoi"));
        listStudents.add(new Student(4, "Quy", 22, "Hanoi"));
        // sort list student
        Collections.sort(listStudents);
        // show list students
        for (Student student : listStudents) {
            System.out.println(student.toString());
        }
    }
}
Sử dụng Compararble, sort() để sắp xếp một danh sách dựa vào tên của sinh viên đó theo thứ tự giảm dần

import java.util.*;
class SinhVien implements Comparable<SinhVien>{
	private String fullName;
	private int age;
	private String address;
	
	public SinhVien() {}
	public SinhVien(String fullName, int age, String address) {
		this.fullName = fullName;
		this.age = age;
		this.address = address;
	}
	public String getFullName() {
		return fullName;
	}
	public void setFullName(String fullName) {
		this.fullName = fullName;
	}
	@Override
	public String toString() {
		return "SinhVien [fullName=" + fullName + ", age=" + age + ", address=" + address + "]";
	}
	@Override
	public int compareTo(SinhVien o) {
		return this.getFullName().compareToIgnoreCase(o.getFullName());
	}
}
public class test { 
	public static ArrayList<SinhVien> arr = new ArrayList<SinhVien>();
	public static void main(String[] args) { 
		arr.add(new SinhVien("Le duc thang", 19, "phu da"));
		arr.add(new SinhVien("Tran Ngoc Anh", 19, "phu da"));
		arr.add(new SinhVien("Dao gia Thi", 19, "phu da"));
		arr.add(new SinhVien("Ninh Van Quyen", 19, "phu da"));
		arr.add(new SinhVien("Nguyen The Anh", 19, "phu da"));
		Collections.sort(arr, Collections.reverseOrder());
		for (SinhVien string : arr) {
			System.out.println(string);
		}
	}
}

compare()
cần implements comparator<>. Comparator chỉ chứa một phương thức là compareTo(Object)
so sách >, <, = của chuỗi theo thứ tự từ điển hoặc là đối tượng giá trị trả về là một con số âm bằng 0 hoặc dương. Thường sử dụng cho bài toán sắp xếp
https://www.youtube.com/watch?v=xWRGSp7BsP0
swap()
trong java, phương thức này đưuọc sử dụng để hoác đổi hai phần tử trong một danh sách. Phương thức này nằm trong lớp collections thường được sử dụng để sắp xếp hoặc thực hiện các thao tác trên danh sách.
Cú pháp:
Collections.swap(tên_danh_sách, vị_trí_1, vị_trí_2)
Bài tập
/* Viết hàm nhập vào một số thực dương, trả về số thực đã làm tròn đến hàng thứ 2 */
package Content;
import java.util.Scanner;
class Run_01 {
	public static void main(String[] agrs) {
		Scanner sr = new Scanner(System.in);
		float t, tOld, tNew, R;
		int nOld, nNew;
		t = sr.nextFloat();
		tOld = t*1000; tNew = t*100;
		nOld = (int) tOld; nNew = (int) tNew;
		R = (float) nNew/100;
		if( R > 0) {
			if((tOld%10) < 5) {
			System.out.println(R);
		}
		else {
			nNew++;
			R = (float) nNew/100;
			System.out.println(R);
		}
		}
		else {
			System.out.println("Number error");
		}
	}
}
/* tạo một lớp đối tượng họ và tên, địa chỉ, tuổi sau đó in ra màn hình */
package bai1;
public class content{
	public String hVT;
	public String dC;
	public byte t;
	
	public content(String hVT, String dC, byte t) {
		this.hVT = hVT;
		this.dC = dC;
		this.t = t;
	}
	
	public static void main(String[] args) {
		content s = new content("Le Duc Thang", "Phu Da", (byte)20);
		System.out.println(s.hVT);
	}
}
class KhachHang {
    private String hoTen;
    private int soNha;
    private String maCongTo;

    // Constructor
    public KhachHang(String hoTen, int soNha, String maCongTo) {
        this.hoTen = hoTen;
        this.soNha = soNha;
        this.maCongTo = maCongTo;
    }

    // Getter và setter
    // ... (bạn tự thêm)

    // Phương thức hiển thị thông tin khách hàng
    public void hienThiThongTin() {
        System.out.println("Họ tên: " + hoTen);
        System.out.println("Số nhà: " + soNha);
        System.out.println("Mã công tơ: " + maCongTo);
    }
}
class BienLai {
    private KhachHang khachHang;
    private int chiSoCu;
    private int chiSoMoi;
    private double tienPhaiTra;

    // Constructor
    public BienLai(KhachHang khachHang, int chiSoCu, int chiSoMoi) {
        this.khachHang = khachHang;
        this.chiSoCu = chiSoCu;
        this.chiSoMoi = chiSoMoi;
        this.tienPhaiTra = tinhTienPhaiTra();
    }

    // Phương thức tính tiền phải trả
    private double tinhTienPhaiTra() {
        return (chiSoMoi - chiSoCu) * 850000;
    }

    // Phương thức hiển thị thông tin biên lai
    public void hienThiThongTin() {
        khachHang.hienThiThongTin();
        System.out.println("Chỉ số cũ: " + chiSoCu);
        System.out.println("Chỉ số mới: " + chiSoMoi);
        System.out.println("Tiền phải trả: " + tienPhaiTra);
    }
}
import java.util.Scanner;

public class QuanLyTienDien {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.print("Nhập số lượng khách hàng: ");
        int n = scanner.nextInt();

        BienLai[] bienLais = new BienLai[n];

        for (int i = 0; i < n; i++) {
            System.out.println("Nhập thông tin khách hàng thứ " + (i + 1));
            System.out.print("Họ tên: ");
            String hoTen = scanner.next();
            System.out.print("Số nhà: ");
            int soNha = scanner.nextInt();
            System.out.print("Mã công tơ: ");
            String maCongTo = scanner.next();
            System.out.print("Chỉ số cũ: ");
            int chiSoCu = scanner.nextInt();
            System.out.print("Chỉ số mới: ");
            int chiSoMoi = scanner.nextInt();

            KhachHang khachHang = new KhachHang(hoTen, soNha, maCongTo);
            BienLai bienLai = new BienLai(khachHang, chiSoCu, chiSoMoi);
            bienLais[i] = bienLai;
        }

        // Hiển thị thông tin các biên lai
        for (BienLai bienLai : bienLais) {
            bienLai.hienThiThongTin();
            System.out.println("------------------------");
        }
    }
}
Lambda
Là một phương thức không có tên hay một phương thức nặc danh. Biểu thức lambda không tự thực thi mà thay vào đó suwr dụng để thực thi một phương thức đưuọc định nghĩa một functional interface.
Xử lí thời gian
Java.util.Date
Để biểu diễn ngày và giờ (date và time). Nó cung cấp các constructor và phương thức để xử lý date và time trong java. Nó implements các giao diện Serializable, cloneable và Comparable<Date>. Nó được kế thừa bởi các lớp java.sql.Date, java.sql.Time và java.sql.TimeStamp
Sau khi Calendar ra đời, hầu hết các constructor và phương thức của lớp java.util.Date đã đưuọc khuyến cáo không dùng nữa
System.currentTimeMillis()
Đưa ra màn hình thời gian tính bằng mili giây
package chuoi;

public class Chuoi {
	public static void main(String[] args) {
		long time1 = System.currentTimeMillis();
		for(int i = 0; i < 100; i++) {
			System.out.println("Hello world!!");
		}
		long time2 = System.currentTimeMillis();
		System.out.println(time2-time1); // chạy vòng for 100 lần tốn 2 mls
	}
}
timeUnit()
quy đổi thời gian. Có kiểu dữ liệu là long
cần import java.util.concurrent.TimeUnit
package chuoi;

import java.util.concurrent.TimeUnit;

public class Chuoi {
	public static void main(String[] args) {
		System.out.println(TimeUnit.HOURS.toMinutes(1)); // 1 giờ = 60 phút
	}
}
Date
Lấy ra thời gian hiện tại có trong hệ thống
Cần import java.util.Date
package chuoi;

import java.util.Date;

public class Chuoi {
	public static void main(String[] args) {
		Date date = new Date();
		Date date2 = new Date(System.currentTimeMillis());
		System.out.println(date); // Sun Oct 20 20:54:52 ICT 2024
		System.out.println(date2); // Sun Oct 20 20:54:52 ICT 2024
	}
}
Calendar
là một lớp trừu tượng abstract cung cấp phương thức chuyển đổi ngày giữa một thời điểm cụ thể theo thời gian và một tập hợp các trường của calender như MONTH, YEAR, HOUR, … nó kế thừa lớp Object và implements giao diện Comparable.
Cần import java.util.Calender;
Phương thức
Mô tả
abstract void add(int field, int amount)
Nó được sử dụng để thêm hoặc trừ số lượng thời gian nhất định vào trường calendar đã cho, dựa trên các quy tắc của calendar.
int get(int field)
Nó được sử dụng để trả lại giá trị của trường calendar đã cho.
abstract int getMaximum(int field)
Nó được sử dụng để trả về giá trị MAX cho trường calendar đã cho của thể hiện Calendar hiện tại.
abstract int getMinimum(int field)
Nó được sử dụng để trả về giá trị MIN cho trường calendar đã cho của thể hiện Calendar hiện tại.
void set(int field, int value)
Nó được sử dụng để thiết lập trường cho trước vói giá trị đã cho.
void setTime(Date date)
Nó được sử dụng để thiết lập time của Calendar với Date đã cho.
Date getTime()
Nó được sử dụng để trả về đối tượng Date biểu diễn giá trị time của Calendar.
Calendar.getInstance()
Dùng để kai báo thời gian hiện tại trên hệ thống
Cú pháp:
Calendar ten = Calendar.getInstace();

package core;

import java.util.Calendar;

public class Main {
	public static void main(String[] args) {
		Calendar calendar = Calendar.getInstance();
		System.out.println(calendar); // nó sẽ in dưới dang list tất cả thuộc tính mà Calendar đang có
	}
}

Date getTime()
Dùng để lấy đầy đủ thời gian trên hệ thống, có thể đưa ra màn hình.
Cú pháp:
Ten.getTime();

Ví đụ:
import java.util.Calendar;

public class Main {
	public static void main(String[] args) {
		Calendar calendar = Calendar.getInstance();
		System.out.println(calendar.getTime()); 
	}
}
/*kết quả
 * Fri Nov 15 09:12:38 ICT 2024
 * kết quả này có thể thay đổi tùy thuộc vào thời gian
 * kết quả này là đúng với thời ggina khi nó in ra màn hình
 * */

package chuoi;

import java.util.Calendar;

public class Chuoi {
	public static void main(String[] args) {
		Calendar time = Calendar.getInstance();
		System.out.println(time.getTime()); // trả về thời gian 
		time.add(Calendar.HOUR, 30);
		System.out.println(time.getTime()); // trả về thời gian 30 giờ sau
	}
}
Lấy ngày trong Calendar

import java.util.Calendar;

public class Main {
	public static void main(String[] args) {
		Calendar calendar = Calendar.getInstance();
		// ví dụ hôm nay là ngày 15/11/2024
		System.out.println(calendar.get(Calendar.DATE)); // 15
		System.out.println(calendar.get(Calendar.DAY_OF_MONTH)); //	15
		System.out.println(calendar.get(Calendar.DAY_OF_WEEK)); // 6 (thứ 6)
		System.out.println(calendar.get(Calendar.DAY_OF_WEEK_IN_MONTH)); // 3
		System.out.println(calendar.get(Calendar.DAY_OF_YEAR)); // 320 (320/365)
	}
}
Lấy tháng trong Calendar

import java.util.Calendar;

public class Main {
	public static void main(String[] args) {
		Calendar calendar = Calendar.getInstance();
		// ví dụ hôm nay là ngày 15/11/2024
		System.out.println(calendar.get(Calendar.MONTH)); // 10
		// kết quả trên là sai với ta mong muốn nên phải cộng thêm 1. code đúng để lấy tháng là
		System.out.println(calendar.get(Calendar.MONTH)+1); // 11
	}
}
Lấy năm trong Calendar

import java.util.Calendar;

public class Main {
	public static void main(String[] args) {
		Calendar calendar = Calendar.getInstance();
		// ví dụ hôm nay là ngày 15/11/2024
		System.out.println(calendar.get(Calendar.YEAR)); // 2024
	}
}
LocalDate
là một immulable class đại diện cho ngày tháng năm không co múi giờ
cần import java.time.LocalDate;
LocalDate.now()
Lấy ra giá trị ngày có trong hệ thống

import java.time.LocalDate;

public class Chuoi {
	public static void main(String[] args) {
		LocalDate time = LocalDate.now();
		System.out.println(time); // 2024-10-20
	}
}
LocalDate.of()
Trả về giá trị ngày khi ta truyền dữ liệu ngày tháng năm vào

import java.time.LocalDate;

public class Chuoi {
	public static void main(String[] args) {
		LocalDate time = LocalDate.of(2024, 1, 1);
		System.out.println(time); // trả về 2024-01-01
	}
}
Lấy ngày trong LocalDate

import java.time.LocalDate;

public class Main {
	public static void main(String[] args) {
		LocalDate lDate = LocalDate.now();
		System.out.println(lDate.getDayOfMonth()); // 15
		System.out.println(lDate.getDayOfWeek()); // FRIDAY
		System.out.println(lDate.getDayOfYear()); // 320
	}
}
Lấy tháng trong LocalDate

import java.time.LocalDate;

public class Main {
	public static void main(String[] args) {
		LocalDate lDate = LocalDate.now();
		System.out.println(lDate.getMonth()); // NOVEMBER
		System.out.println(lDate.getMonthValue()); // 11
	}
}
Lấy năm trong LocalDate

import java.time.LocalDate;

public class Main {
	public static void main(String[] args) {
		LocalDate lDate = LocalDate.now();
		System.out.println(lDate.getYear()); // 2024
	}
}

package chuoi;

import java.time.LocalDate;

public class Chuoi {
	public static void main(String[] args) {
		LocalDate time = LocalDate.now();
		System.out.println(time);
		System.out.println(time.getDayOfMonth()); // trả về ngày theo tháng 20/30
		System.out.println(time.getDayOfYear()); // trả về ngày theo năm 294/365
		System.out.println(time.getDayOfWeek()); // trả về ngày theo tuần SUNDAY
		System.out.println(time.getMonth()); // trả về tháng OCTOBER
		System.out.println(time.getYear()); // trả về năm 2024
		System.out.println(time.getMonthValue()); // trả về giá trị số của tháng 10
		System.out.println(time.getChronology()); // trả về tên của hệ thống lịch đang được sử dụng ISO
		System.out.println(time.getEra()); // trả về thông tin về kỉ nguyên CE (công nguyên)
	}
}
chuyển từ String sang LocalDate

import java.time.LocalDate;
import java.time.format.DateTimeFormatter;

// Driver Class
public class StringToLocalDateExampleOne {
    // Main Function
      public static void main(String[] args) {
        // Example String representing a date
        String dateString = "2024-01-20";

        // Parse the String to LocalDate using the formatter
        LocalDate localDate = LocalDate.parse(dateString);

        // Output the type of the dateString variable
        System.out.println("Type of dateString: " + dateString.getClass().getName());
        System.out.println("Type of localDate: " + localDate.getClass().getName());
      
        // Output the LocalDate
        System.out.println("Parsed LocalDate: " + localDate);
    }
}

Convert LocalDate sang String
Cộng, trừ ngày trong LocalDate 
plus()

import java.time.LocalDate;

public class Chuoi {
	public static void main(String[] args) {
		LocalDate date = LocalDate.now();
		System.out.println(date); // trả về ngày hiện tại - 2024-10-21
		System.out.println(date.plusDays(12)); // trả về ngày khi cộng thêm 12 ngày - 2024-11-02
	}
}
minus()

import java.time.LocalDate;

public class Chuoi {
	public static void main(String[] args) {
		LocalDate date = LocalDate.now();
		System.out.println(date); // trả về ngày hiện tại - 2024-10-21
		System.out.println(date.minusDays(12)); // trả về ngày khi trừ đi 12 ngày - 2024-10-09
	}
}
isEqual(LocalDate other)
isAfter(LocalDate other)
isBefore(LocalDate other)
compareTo(LocalDate other)
isLeapYear()
SimpleDateFormat
Có 2 lớp để định dạng ngày trong java: DateFormat và SimpleDateFormat
Cần import java.text.SimpleDateFormat – cung cấp các định dạng và phân tích ngày tháng và thời gian trong java. SimpleDateFormat kế thừa lớp java.text.DateFormat
Kí hiệu trong định dạng:
- EE: viết tắt của thứ (Mon)
- EEEE: viết đầy đủ của thứ (Monday)
- HH: định dạng giờ
- n…HH: thêm n số không vào định dạng giờ
- m hoặc mm: dịnh dạng phút
- n…mm: thêm n số không vào định dạng phút
- s hoặc ss: định dạng giây
- n…ss: thêm n số không vào định dạng giây
- dd: định dạng ngày theo tháng (21/30)
- DD: định dạng ngày theo năm (295/365)
- MM: định dạng tháng theo số
- MMMM: định dạng tháng theo chữ
- y hoặc yyyy: định dạng năm đầy đủ
- YY: đưa ra 2 số đầu của năm (20 của 2024)
- z hoặc zz: địng dạng tên của lịch trên hệ thống đang được sử dụng
- zzzz: định dạng tê đầy đủ lịch trên hệ thống đang được sử dụng
package chuoi;

import java.text.SimpleDateFormat;
import java.util.Date;
public class Chuoi {
	public static void main(String[] args) {
		Date date = new Date();
		SimpleDateFormat formatter = new SimpleDateFormat();
		System.out.println(formatter.format(date)); // 10/21/24, 4:16 PM
		System.out.println(date); //Mon Oct 21 16:16:12 ICT 2024
	}
}
Format()
Để chuyển một đối tượng date thành một chuỗi ký tự theo định dạng cụ thể
// Định dạng lại thời gian của giờ trên hệ thống JVM
package chuoi;

import java.text.SimpleDateFormat;
import java.util.Date;
import java.util.Calendar;

public class Chuoi {
	public static void main(String[] args) {
		// có thể lấy thời gian hiện tại trên hệ thống bằng 2 cách sau
		Calendar date1 = Calendar.getInstance();
		Date date2 = new Date();
		// xuất thời gian trên hệ thống bằng 2 cách sau
		System.out.println(date1.getTime());
		System.out.println(date2);
		
		SimpleDateFormat formatter = new SimpleDateFormat("EEEE, dd/MM/YYYY, H:m:s, zzzz");
		String date3 = formatter.format(date2);
		System.out.println(date3);
	}
}
/*
    Mon Oct 21 16:54:29 ICT 2024
	Mon Oct 21 16:54:29 ICT 2024
	Monday, 21/10/2024, 16:54:29, Indochina Time
 *  */
ChronoUnit
Là một enum thi hành interface TemporalUnit,nó cung cấp cacss đơn vị tính tiêu chuẩn được sử dụng trong Java Date Time API về cơ bản các đơn vị tính này là đủ để sử dụng, tuy nhiên nếu muốn có một đươn vị tính tùy biến hãy lột lớp thi hành interface
Cần import java.time.temporal.ChronoUnit
long between(LocalDate1, LocalDate1)
để tính khoảng thời gian giữa LocalDate1 và LocalDate2 có thể là ngày, tháng, năm

ví dụ:
import java.time.LocalDate;
import java.time.temporal.ChronoUnit;
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Nhập ngày cần kiểm tra (dưới dạng yyyy-MM-dd)
        System.out.print("Nhập ngày (yyyy-MM-dd): ");
        String inputDate = scanner.nextLine();

        // Chuyển đổi chuỗi nhập vào thành đối tượng LocalDate
        LocalDate enteredDate = LocalDate.parse(inputDate);

        // Lấy ngày hiện tại
        LocalDate currentDate = LocalDate.now();

        // Tính số ngày khác biệt
        long daysDifference = ChronoUnit.DAYS.between(enteredDate, currentDate);
        System.out.println(daysDifference);
        // Kiểm tra và in kết quả
        if (daysDifference < 10) {
            System.out.println("Lỗi: Ngày nhập vào nhỏ hơn 10 ngày so với hiện tại!");
        } else {
            System.out.println("Ngày nhập vào hợp lệ.");
        }
    }
}

Cách để bỏ qua lời cảnh báo
Khi hiện cảnh báo
The constructor Locale(String, String) is deprecated since version 19 -> @SuppressWarnings(“deprecation”)
The value of the local variable currencyEngland is not used -> @SuppressWarnings(“unused”)
Stack
Là cấu trúc last in first out.
Cần import java.util.Stack;
Cú pháp:
Stack<dataType> <name> = new Stack<dataType >();
push()
Đưa giá trị vào stack.
import java.util.Stack;
import java.util.Scanner;
public class test { 
	public static void main(String[] args) { 
		Scanner sc = new Scanner(System.in);
		Stack<String> stackChuoi = new Stack<String>();
		stackChuoi.push("Chuoi");
		stackChuoi.push("String");
	}
}

pop()
Lấy giá trị ra và xóa khỏi stack.
import java.util.Stack;
import java.util.Scanner;
public class test { 
	public static void main(String[] args) { 
		Scanner sc = new Scanner(System.in);
		Stack<String> stackChuoi = new Stack<String>();
		String s = sc.nextLine();
		for(int i = 0; i < s.length(); i++) {
			stackChuoi.push(s.charAt(i)+"");
		}
		System.out.println("Chuoi bi dao: ");
		for(int i = 0; i < s.length(); i++) {
			System.out.print(stackChuoi.pop());
		}
	}
}

peek()
Lấy giá trị ra nhưng không xóa khỏi stack.
clear()
Xóa tất cả phần tủ trong stack.
contains()
Xác định giá trị có tồn tại trong stack hay không.
size()
lấy ra độ lớn của stack.
isEmpty()
kiểm tra xem stack đó có trống không trả về true, false
Chuyển số thập phân sang số nhị phân
package core;
import java.util.Stack;
import java.util.Scanner;
public class test { 
	public static void main(String[] args) { 
		Scanner sc = new Scanner(System.in);
		Stack<String> stack = new Stack<String>();
		int x = sc.nextInt();
		while(x > 0) {
			int soDu = x%2;
			stack.push(soDu+"");
			x = x/2;
		}
		int n = stack.size();
		for(int i = 0; i < n; i++) {
			System.out.print(stack.pop());
		}
	}	
}
ép
Nhập vào 2 chuỗi, kiểm tra xem chuỗi 2 có phải là đảo ngược của chuỗi 1 hay không. Biết rằng không quan tâm đến kí tự hoa hay thường. ví dụ CAT -> TAC, CAT, act, …

import java.util.Scanner;

public class Solution {

    static boolean Stack(String a, String b){
        java.util.Stack<String> doi = new java.util.Stack<String>();
        String s = "";
        for(int i = 0; i < a.length(); i++){
            doi.push(a.charAt(i)+"");
        }
        for(int i = 0; i < a.length(); i++){
            s += doi.pop();
        }
        if(b.equalsIgnoreCase(s)){
            return true;
        } else{
            return false;
        }
    }
    
    static boolean Change(String a, String b){
        char[] arr = new char[a.length()];
        char[] brr = new char[b.length()];
        arr = a.toCharArray();
        brr = b.toCharArray();
        java.util.Arrays.sort(arr);
        java.util.Arrays.sort(brr);
        if(arr.length == brr.length){
            for(int i = 0; i<a.length();i++){
                if(Character.toUpperCase(arr[i]) != Character.toUpperCase(brr[i])){
                    return false;
                }
            }
            return true;
        }
        else{
            return false;
        }
        
    }
    static boolean isAnagram(String a, String b) {
        if(a.equalsIgnoreCase(b)){
            return true;
        }
        if(Stack(a, b)){
            return true;
        }
        if(Change(a, b)){
            return true;
        }
        return false;
    }

    public static void main(String[] args) {
    
        Scanner scan = new Scanner(System.in);
        String a = scan.next();
        String b = scan.next();
        scan.close();
        boolean ret = isAnagram(a, b);
        System.out.println( (ret) ? "Anagrams" : "Not Anagrams" );
    }
}
Queue
First in, first out dữ liệu vào trước thì lấy ra trước
PriorityQueue
là hàng đợi ưu tiên, nó lưu trữ các phần tử theo trật tự tự nhiên của phần tử nếu các phần tử được so sánh với nhau hoặc một bộ so sánh Comparator được cung cấp cho priorityQueue
add(e)
chèn phần tử đã chỉ định vào hàng đợi. nếu tác vụ thanhhf công, trả về true. Nếu không nó sẽ ném ra một ngoại lệ
offer()
chèn phần tử đã chỉ định vào hàng đợi. nếu tác vụ thành công trả về true, nếu không nố sẽ trả về false.
remove()
Trả về và xóa phần đầu của hàng đợi. ném ra một ngoại lệ hàng đợi trống
poll()
trả về và loại bỏ phần đầu của hàng đợi. trả về null nếu hàng đợi trống
element()
trả về phần đầu của hàng đợi. ném ra một ngoại lệ nếu hàng đợi trống
peek()
trả về đầu của hàng đợi. trả về null nếu hàng đợi trống

Deque
là hàng đợi 2 đầu, bạn có thể thêm một phần tử vào một trong 2 đầu và lấy chúng từ một trong 2 đầu. làm cho nó có tính linh hoạt hơn
Generic
Khái niệm này được đưa vào kể từ java 5. Được hiểu là tham số hóa kiểu dữ liệu. để lập trình viên có thể dễ bắt lỗi các kiểu đữ liệu không hợp lệ, đồng thời giúp dễ dàng hơn cho việc tạo và sử dụng các class, interface, method với nhiều kiểu dữ liệu khác nhau.
package core;

import java.util.ArrayList;

class Box<type> {
	private type value;

	public Box(type value) {
		this.value = value;
	}

	public type getValue() {
		return value;
	}

	public void setValue(type value) {
		this.value = value;
	}

}

public class test {
	public static void main(String[] args) {
		// truyền một số nguyên vào đối tượng Box
		Box value1 = new Box(15);
		// truyền một số thực vào đối tượng Box
		Box value2 = new Box(15.45);
		// truyền một chuỗi vào đối tượng Box
		Box value3 = new Box("Welcome to java");
		// truyền mộ mảng vào đối tượng Box
		ArrayList<String> list = new ArrayList<String>();
		list.add("Hello");
		list.add("Hi");
		list.add("How do you do today");
		Box value4 = new Box(list);
		// Xuất
		System.out.println(
				value1.getValue() + " " + value2.getValue() + " " + value3.getValue() + " " + value4.getValue());
	}
}
/*
 * Kết quả
 * 15 15.45 Welcome to java [Hello, Hi, How do you do today]
 * */
Tập tin và thư mục
Cần import java.io.File;
Khai báo
Cú pháp:
File ten_bien = new File(“đường dẫn”);
exists()
Để kiểm tra một folder có tồn tại hay không
Cú pháp: ten.exists();
mkdir()
tạo ra một thư mục
cú pháp: ten.mkdir();
mkdirs()
tạo nhiều thư mục cùng một lúc
cú pháp: ten.mkdirs();
createNewFile()
tạo ra một file nhưng có ngoại lệ phải bọc try catch
cú pháp:
tên.createNewFile();
canExecute()
kiểm tra xem file có thực thi được hay không
cú pháp:
ten_file.canExecute()
canRead()
kiểm tra xem file có thể đọc được hay không
cú pháp:
ten_file.canRead();
canWrite()
kiểm tra file có thể ghi được hay không
cú pháp:
ten_file.canWrite();
getAbsoluteFile()
getAbsolutePath()
in ra đường dẫn
cú pháp:
ten_file.getAbsolutePath();
getName()
in ra tên
cú pháp:
ten_file.getName();

boolean isDirectory()
kiểm tra là thư mục hay là tập tin
cú pháp:
ten_file.isDirectory();
boolean isFile()
kiểm tra là thư mục hay là tập tin
cú pháp:
ten_file.isFile ();
String[] list()
In danh sách các file con
String[] list(FilenameFilter filter)
File[] listFiles()
In danh sách các file con
cú pháp:
File[] ten = ten_file.listFiles();
Xuất bằng vòng lặp
boolean delete()
Xóa đi một file hoặc folder rỗng
boolean deleteOnExit()
delectIfExists
Path
toPath()
renameTo()
thay đổi tên file
move()
để thay đổi tên file hoặc di chuyển file từ thư mục này sang thuw mục khác. Phương thức này phải ném ra ngoại lệ 
copy()
để copy file, chỉ copy được folder bên ngoài không copy được các file, folder con bên trong
PrintWriter
println()
để ghi dữ liệu ra file hoạc chương trình cosole
flush()
để đẩy dữ liệu vào file
close()
để đóng file
bufferedReader
dùng để đọc dữ liệu từ file lên chương trình. Phải ném ra một ngoại lệ
public class Solution {
    public static void main(String[] args) throws IOException {
        BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bufferedWriter = new BufferedWriter(new FileWriter(System.getenv("OUTPUT_PATH")));

        String[] firstMultipleInput = bufferedReader.readLine().replaceAll("\\s+$", "").split(" ");

        int month = Integer.parseInt(firstMultipleInput[0]);

        int day = Integer.parseInt(firstMultipleInput[1]);

        int year = Integer.parseInt(firstMultipleInput[2]);

        String res = Result.findDay(month, day, year);

        bufferedWriter.write(res);
        bufferedWriter.newLine();

        bufferedReader.close();
        bufferedWriter.close();
    }
}
readLine()
đọc nội dung trong file từng dòng một
readAllLines()
đọc dữ liệu trong một file. Dạng này chỉ nên đọc file có dung lượng nhỏ vì tiêu tốn rất nhiều RAM
OutputSream
dùng để ghi dữ liệu vào tập tin. Phải implements Serializale. Ném ra một ngoại lệ
ObjectOutputStream
writeObject()
Inputstream
ObjectInputStream
readObject()
ZipOutputStream
ZipEntry
zipOut
Assertion
Là một cơ chế kieemr tra trong quá trình phát triển phần mềm, giúp đảm bảo rằng mã của bạn hoạt động đúng như mong đợi. nó cho phép bạn đặt các điều kiện mà bạn tin rằng luôn đúng trong chương trình của mình. Nếu điều kiện này sa, một ngoại lệ sẽ được ném ra, giúp bạn nhanh chóng xác định và sửa lỗi.
    • giúp phát hiện lỗi ngay trong quá trình phát triển, thay vì để chúng gây ra sự cố khi chương trình chạy trong môi trường sản xuất
    • bằng cách kiểm tra giả dduinhjjj bằng dữ liệu đầu vào và trạng thái của chương trình, nó giúp bảo dảm rằng mã của bạn hoạt động một cách đáng tin cậy
    • đóng vai trò như một tài liệu, mô tả các điều kiện tiên quyết và hậu quả của các đoạn mã
Cú pháp:
    • assert <điều kiện>
    • assert <điều kiện> : <thông báo>
Cách bật Assertion:
B1: chuột phải vào code chọn run as, chọn run configuration
B2: chọn argument, ở VM ghi –ea
B3: bấm apply và run
class Solution {
	public static void main(String args[]) {
		int a = 18;
		assert a>20 : "phải lớn hơn 20";
		System.out.println(a);	
	}
}
Nếu không bật thì kết quả là 18
Nếu bật thì một ngoại lệ được ném ra

Lập trình giao diện
java khác ngôn ngữ là có thể chạy được trên đa nền tảng
các thư viện hỗ trợ:
- java.awt.*;
- javax.swing.*;
Tìm hiểu của sổ chương trình Jframe
JFrame
Tạo ra một giao diện JFrame
setVisible()
để hiển thị ra một giao diện. bên trong ngoặc chuyền giá trị true là hiển thị. Ngược lại là không hiển thị
setSize(x,y)
để thiết lập kích thước cho giao diện, x là chiều dọc ngang, y là chiều dọc
setTitle()
để thiết lập tiêu đề cho giao diện
setDefaultCloseOperation()
để thiết lập khi đóng của sổ Jframe
setLocation(x,y);
gắn vị trí hiển thị
các thành phần và bố cục chương trình giao diện
FlowLayout
setLayout()
JButton
Tạo ra cái nút bấm
add()
jpanel và cấu hình look and feel
JPanel
Là một class trong java, nó là một vật chứa, có thể chứa các thành phần khác trong một chương trình
Mô hình MVC và cách xử lý JButton
counterModel
lastButtonModel()
setForeground(Color c)
setBackground(Color c)
setOpaque(boolean)
jtextfield
jtextarea
jscrollpane
Scanner
Phải thêm thư viện: import java.util.Scanner;
Phương thức
Mô tả
nextBoolean()
Đọc một giá trị boolean từ bàn phím
nextByte()
Đọc một giá trị byte từ bàn phím
nextDouble()
Đọc một giá trị double từ bàn phím
nextFloat()
Đọc một giá trị float từ bàn phím
nextInt()
Đọc một giá trị int từ bàn phím
nextLong()
Đọc một giá trị long từ bàn phím
nextShort()
Đọc một giá trị short từ bàn phím
nextline()
Đọc một giá trị String từ bàn phím
Ví Dụ:
Scanner sc = new Scanner(System.in);
System.out.println(“…”);
String nhap = sc.nextLine();
Comment
// -  ghi chú trên một dòng
/* ghi chú trên nhiều dòng */
/** chú thích để tạo tài liệu javadoc */
final 
Xác định một biến không thể thay đổi được.
Cú pháp:
final <dataType> <name> = value;
class Solution{
	public static void main(String[] args) {
		final int a = 10;
		a = 12; // Có thông báo lỗi
		System.out.println(a);
	}
}