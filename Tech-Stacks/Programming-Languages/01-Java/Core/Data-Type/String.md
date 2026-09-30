- [.trim() (Xóa khoản trắng dư thừa ở đầu chuỗi)](#trim-xóa-khoản-trắng-dư-thừa-ở-đầu-chuỗi)
- [isEmpty() (Nếu chuỗi trống trả về true ngược lại trả về false)](#isempty-nếu-chuỗi-trống-trả-về-true-ngược-lại-trả-về-false)
---
## valueOf (ép các kiểu khác sang kiểu chuỗi)
**Syn**
```bash
String <name> = String.valueOf(<variable>);
```
**Ex**
```python
class Person{
	public static void main(String[] args) {
		int a = 10;
		String s = String.valueOf(a);
		System.out.println(s + 10); // 20
		System.out.println(t+10); // 20
	}
}
```
## .toString(ép các kiểu khác sang kiểu chuỗi)
**Syn**
```bash
String <name> = Integer.toString(<variable>);
```
**Ex**
```python
class Person{
	public static void main(String[] args) {
		int a = 10;
		String t = Integer.toString(a);
		System.out.println(s + 10); // 20
		System.out.println(t+10); // 20
	}
}
```
**Ex2: Long -> String**
```java
class Person{
	public static void main(String[] args) {
		int a = 10;
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

# .trim() (Xóa khoản trắng dư thừa ở đầu chuỗi)
**Ex**
```java
public class Chuoi {
	public static void main(String[] args) {
		String a = "   Le Duc Thang   ";
		System.out.println(a.trim());
	}
}
```
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
# isEmpty() (Nếu chuỗi trống trả về true ngược lại trả về false)
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