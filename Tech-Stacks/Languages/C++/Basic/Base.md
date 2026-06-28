

---

# Kiểm tra C++ đã được cài vào máy hay chưa
1. g++ --version

# cout
Dùng để xuất dữ liệu ra màn hình.
```c++
#include <bits/stdc++.h>
using namespace std;

int main() {
    cout << "hello world" << endl;
    return 0;
}
```

# comments
//.
Xử lý số
max()
int m = max(1,2);
cout << m;
2
sort()
Dùng để sắp xếp.

Bài tập
Sắp xếp danh sách theo tuổi

input
C++ Data types
    • boolean: 1 byte
    • char: 1 byte
    • short | short int: 2 bytes (số nguyên) 
    • int | signed int: 4 bytes (số nguyên)
    • long | long int: 4 hoặc 8 bytes tùy vào hệ thông (số nguyên)
    • long long | long long int: 8 bytes (số nguyên)
    • float: 4 bytes (số thực)
    • double: 8 bytes (số thực)
C++ Operator
/
Chia lấy phần nguyên
7/2
3

Strings
Để xử lý chuỗi. Cần import <string>.
length()
Để lấy độ dài của một chuỗi.
substr()
Dùng để cắt chuỗi.
string a = "hello";
cout << a.substr(0, 2);
he
// cắt chuỗi từ vị trí start đến end-1
replace()
Thay thế chuỗi con bằng chuỗi con khác.
#include <iostream>
#include <string>
using namespace std;
int main() {
    string text = "hello world";
    text.replace(6, 5, "C++"); 
    cout << text; 
    return 0;
}
// Thay thế "world" bằng "C++"
hello C++
Thay thế ký tự trong chuỗi 
#include <iostream>
#include <string>
using namespace std;
int main() {
	string text = "hello";
	text[0] = 'n';
	cout << text[0];
	return 0;
}
nello
So sánh chuỗi
#include <bits/stdc++.h>
using namespace std;

int main() {
    string a = "Alice";
    string b = "Bob";

    if (a < b) cout << a << " nho hon " << b << endl;
    if (a > b) cout << a << " lon hon " << b << endl;
    if (a == b) cout << a << " bang " << b << endl;
}
C++ Math
C++ Booleans
Câu điều kiện
C++ If…else
C++ Switch
C++ While Loop
C++ For Loop
C++ break/Continue
Arrays
Foreach loop
#include <iostream>
using namespace std;

int main() {
  // Create an array of integers
  int myNumbers[5] = {10, 20, 30, 40, 50};
  
  // Loop through integers
  for (int num : myNumbers) { // có thể thay int bằng auto
    cout << num << "\n";
  }
  return 0;
}
10
20
30
40
50

sizeof()
Đơn vị là bytes. Khác với Java, C++ có thể thay đổi được giá trị phần tử trong mảng nhưng kích thước của mảng không thể thay đổi.
int arr[] = { 2,1,4,3,2,5,1,8,7,6 };
int length = sizeof(arr) / sizeof(arr[0]);
cout << length;
10
Mảng 2 chiều
string letters[2][4] = {
  { "A", "B", "C", "D" },
  { "E", "F", "G", "H" }
};
string letters[2][2][2] = {
  {
    { "A", "B" },
    { "C", "D" }
  },
  {
    { "E", "F" },
    { "G", "H" }
  }
};
string letters[2][4] = {
  { "A", "B", "C", "D" },
  { "E", "F", "G", "H" }
};

cout << letters[0][2];  // Outputs "C"
string letters[2][4] = {
  { "A", "B", "C", "D" },
  { "E", "F", "G", "H" }
};
letters[0][0] = "Z";

cout << letters[0][0];  // Now outputs "Z" instead of "A"
Duyệt phần tử
string letters[2][4] = {
  { "A", "B", "C", "D" },
  { "E", "F", "G", "H" }
};

for (int i = 0; i < 2; i++) {
  for (int j = 0; j < 4; j++) {
    cout << letters[i][j] << "\n";
  }
}
Structures
Là một cách để nhóm nhiều biến liên quan vào một nơi. Mỗi biến trong cấu trúc được gọi là thành viên của cấu trúc.
// Create a structure variable called myStructure
struct {
  int myNum;
  string myString;
} myStructure;

// Assign values to members of myStructure
myStructure.myNum = 1;
myStructure.myString = "Hello World!";

// Print members of myStructure
cout << myStructure.myNum << "\n";
cout << myStructure.myString << "\n";
1
Hello World!
Thường được dùng để biểu diễn dữ liệu dạng danh sách tuyến tính.
C++ Enums
C++ References
C++ Pointers
Con trỏ trong C++ là một biến dùng để lưu địa chỉ của một biến khác trong bộ nhớ. Con trỏ rất mạnh mẽ và linh hoạt, giúp bạn thao tác trực tiếp với bộ nhớ, truyền tham chiếu, tạo mảng động, danh sách liên kết.
Tuy nhiên nếu không sử dụng cẩn thận thì có thể gây lỗi chương trình (như truy cập vào vùng nhớ không hợp lệ).
Cú pháp: <kiểu_dữ_liệu>* <tên>
int main() {
	int a = 10;
	int* p = &a;
	cout << p << ", " << *p;
	return 0;
}
0000001A5091F8C4, 10
C++ Functions
C++ Classes

C++ Define
Là tiền xử lý trong ngôn ngữ C++ cho phép đặt tên cho một hằng số. Nó có thể chứa nhiều kiểu dữ liệu khác nhau.
Cú pháp: #define <name> <value>
Vector
Cần #include <vector>
Cho phép bạn tạo một mảng động. Có nghĩa là mảng này có thể thay đổi kích thước trong quá trình chạy chương trình.
Đặc điểm:
Có thể thay đổi kích thước khi cần thiết.
Truy cập phần tử bằng chỉ số (index) với độ phức tạp O(1).
Thêm xóa phần tử ở cuối vector hiệu quả O(1).
Vector tự động quản lý việc cấp phát và giải phóng bộ nhớ.
Cú pháp:
vector<int> a(3, 4);
for(int x : a) cout << x << " "; // tạo ra 3 số 4

push_back()
Để thêm phần tử vào cuối vetor.
size()
Trả về số lượng phần tử trong vector.
pop_back()
Để xóa phần tử cuối cùng trong vector.
insert()
Để chèn vào vị trí thứ n.
#include <iostream>
    #include <vector>

    int main() {
        std::vector<int> myVector = {1, 2, 4, 5};
        int n = 2; // Vị trí muốn chèn
        int value = 3; // Giá trị muốn chèn

        // Chèn giá trị vào vị trí n
        myVector.insert(myVector.begin() + n, value);

        // In ra vector sau khi chèn
        std::cout << "Vector sau khi chèn: ";
        for (int element : myVector) {
            std::cout << element << " ";
        }
        std::cout << std::endl;

        return 0;
    }
Vector sau khi chèn: 1 2 3 4 5
Erase()
Để xóa phần tử tại vị trí thứ i.
#include <iostream>
    #include <vector>

    int main() {
        std::vector<int> myVector = {1, 2, 3, 4, 5};
        int n = 2; // Vị trí muốn xóa

        // Xóa phần tử tại vị trí n
        myVector.erase(myVector.begin() + n);

        // In ra vector sau khi xóa
        std::cout << "Vector sau khi xóa: ";
        for (int element : myVector) {
            std::cout << element << " ";
        }
        std::cout << std::endl;

        return 0;
    }
Vector sau khi xóa: 1 2 4 5
.begin()
.resize()
.assign()
Khởi tạo lại toàn bộ vector với kích thước và giá trị mình muốn
Cú pháp:
vector<int> v;
v.assign(5, 10); # v = [10, 10, 10, 10, 10]
vector<int> a = {1, 2, 3, 4};
vector<int> b;

b.assign(a.begin(), a.end());
dp.assign(n + 1, vector<int>(s + 1, 0));
C++ setw
setw()
Đặt độ rộng trường xuất thành n ký tự. cần #include <iomanip>
#include <iostream>
#include <iomanip>

int main() {
    std::cout << std::setw(10) << "Tên" << std::setw(5) << "Tuổi" << std::endl;
    std::cout << std::setw(10) << "Alice" << std::setw(5) << 30 << std::endl;
    std::cout << std::setw(10) << "Bob" << std::setw(5) << 25 << std::endl;
    std::cout << std::setw(10) << "Charlie" << std::setw(5) << 35 << std::endl;

    return 0;
}
Tên Tuổi
 Alice 30 
Bob 25 
Charlie 35
Căn chữ sang trái khi sử dụng setw
#include <iostream>
#include <iomanip>
using namespace std;

int main() {
    cout << left << setw(15) << "Tên" 
         << setw(10) << "Tuổi" 
         << endl;

    cout << left << setw(15) << "Nguyễn Văn A" 
         << setw(10) << 20 
         << endl;

    cout << left << setw(15) << "Trần B" 
         << setw(10) << 22 
         << endl;

    return 0;
}
Tên                    Tuổi     
Nguyễn Văn A   20        
Trần B                22        

C++ nullptr
Biểu thị rằng một con trỏ không trỏ tới đâu cả.
int* a = nullptr;


Phần 3: thư viện cstring
Cần #include <cstring>
strcpy()
Để sao chép chuỗi ký tự từ chuỗi này sang chuỗi khác.
Sinh số ngẫu nhiên
rand()
Sinh ra số nguyên không âm [0, RAND_MAX]. RAND_MAX là hằng số tùy mô hình.
Bài tập
Tạo ra 100 số ngẫu nhiên từ 0 -> 100 bằng C++ 
#include <iostream>
#include <cstdlib>
using namespace std;
int main()
{
    for (int i = 0; i < 100; i++) {
        int a = rand()%101;
        cout << a << endl;
    }
    return 0;
}
Sinh số ngẫu nhiên từ min đến max
#include <iostream>
#include <cstdlib>
using namespace std;
int main()
{
    int min, max;
    cout << "Min: "; cin >> min;
    cout << "Max "; cin >> max;
    for (int i = 0; i < 100; i++) {
        int a = min + rand()%(max-min+1);
        cout << a << endl;
    }
    return 0;
}

Sinh ra số thực ngẫu nhiên từ min đến max
#include <bits/stdc++.h>
using namespace std;

int main(){
    srand(time(0)); // khoi tao hat giong ngau nhien
    double min = 10;
    double max = 15;
    for (int i = 0; i<20; i++){
        double randomFloat = min + (((double)rand() / RAND_MAX)*(max-min+1));
        cout << randomFloat << " ";
    }
    
    return 0;
}
11.7022 13.9647 10.4299 10.922 13.8461 12.6833 11.9146 10.277 14.1616 11.1679 10.4442 13.9052 14.1226 13.2625 14.6937 10.1641 14.5086 14.0645 14.0605 13.7891
random_shuffle()

Cú pháp:

#include <algorithm>
#include <iostream>
using namespace std;

int main() {
    int a[5] = {1,2,3,4,5};
    random_shuffle(a, a + 5); // dùng iterators: begin, end
    for (int i = 0; i < 5; i++) cout << a[i] << " ";
    return 0;
}

Shuffle()
#include <bits/stdc++.h>
using namespace std;

int main() {
    vector<string> ten_hang = {"hang1", "hang2", "hang3", "hang4", "hang5", "hang6", "hang7", "hang8"};
    
    // Cần một bộ sinh số ngẫu nhiên
    random_device rd;
    mt19937 g(rd()); // Mersenne Twister 19937
    
    shuffle(ten_hang.begin(), ten_hang.end(), g);
    
    for (auto &x : ten_hang) cout << x << " ";
    return 0;
}



Chương 3: Giải thuật
Bằng đệ quy
Bài tập
Xuất mảng bằng đệ quy
#include <iostream>
#include <string>
using namespace std;

string arr(int li[],int length) {
	// trường hợp mảng rỗng
	if (length == 0) return ""; 
	// trường hợp mảng có 1 phần tử
	if (length == 1) return to_string(li[0]);
	// trường hợp mảng có nhiều phần tử
	else {
		return arr(li, length - 1) + to_string(li[length - 1]);
	}	
}
int main() {
	int list[] = { 1,2,3,4,5 };
	cout << arr(list, sizeof(list) / sizeof(list[0]));
	return 0;
}
12345
Tìm phần tử thứ n trong dãy fibonaci
#include <iostream>
using namespace std;
int fibonaci(int n){// n = 0,1,2,...
    if(n==0 || n==1) return 1;
    return fibonaci(n-1) + fibonaci(n-2);
}
int main(){
    cout << fibonaci(4);
    return 0;
}
5
Tìm phần tử thứ n trong dãy fibonaci có nhớ
#include <iostream>
#include <vector>
using namespace std;

// Hàm đệ quy có nhớ
long long fib(int n, vector<long long> &memo) {
    // Trường hợp cơ sở
    if (n <= 1) return n;

    // Nếu đã tính rồi, trả về ngay
    if (memo[n] != -1) return memo[n];

    // Ngược lại, tính và lưu lại
    memo[n] = fib(n - 1, memo) + fib(n - 2, memo);
    return memo[n];
}

int main() {
    int n;
    cout << "Nhap n: ";
    cin >> n;

    // Khởi tạo mảng nhớ, gán -1 (chưa tính)
    vector<long long> memo(n + 1, -1);

    cout << "So Fibonacci thu " << n << " la: " << fib(n, memo);
    return 0;
}
Bài toán tháp hà nội
void chuyen(int n, string a, string b) {
	cout << "\n chuyen coc " << n << " tu coc " << a << " sang coc " << b;
}

void thapHN(int n, string a, string b, string c) {
	if (n == 1) chuyen(n, a, c);
	else {
		thapHN(n - 1, a, c, b);
		chuyen(n, a, c);
		thapHN(n - 1, b, a, c);
	}
}
thapHN(3, "a", "b", "c");
void thapHN(int n, string a, string b, string c) {
	if (n == 1) cout << "chuyen 1 dia tu" << a << "sang" << c << endl;
	else {
		thapHN(n - 1, a, c, b);
		cout << "chuyen 1 dia tu " << a << " sang" << c << endl;
		thapHN(n - 1, b, a, c);
	}
}

Giải thuật sinh
Bài tập
Sinh ra dãy nhị phân có n phần tử
void first_config(int x[], int n){ // khởi tạo cấu hình đầu tiên
    for (int i = 1; i<=n; i+=1){
        x[i] = 0;
    }
}

void generation(int x[], int n, int &ok){
    int i = n;
    while(i>=1 && x[i] == 1){
        x[i] = 0;
        i -= 1;
    }
    if(i == 0){
        ok = 0; // điều kiện dừng, tức cấu hình cuối
    }
    else{
        x[i] = 1;
    }
}

int main(){
    int n = 3;
    int x[n+1];
    int ok = 1;
    first_config(x,n); 

    while(ok){
        for(int i = 1; i <= n; i+=1){
            cout << x[i];
        }
        cout << endl;
        generation(x, n, ok);
    }
    return 0;
}
000
001
010
011
100
101
110
111
// sử dụng giải thuật sinh
void print(int x[], int n){
    for (int i = 0; i < n; i+=1){
        cout << x[i];
    }
    cout << endl;
}

void sinh_nhi_phan_1(int n){
    int i;
    int x[n] = {0};

    do{
        print(x, n);
        i = n-1;

        while(i>=0 && x[i]==1){
            i-=1;
        }
        if(i>=0){
            x[i] = 1;
            i+=1;
            while(i<n){
                x[i] = 0;
                i+=1;
            }
        }
    } while(i>=0);
}

#include <iostream>
using namespace std;

void first_config(int x[], int n){ // khởi tạo cấu hình đầu tiên
    for (int i = 1; i<=n; i+=1){
        x[i] = 0;
    }
}

void generation(int x[], int n, int &ok){
    int i = n;
    while(i>=1 && x[i] == 1){
        i -= 1;
    }
    if(i == 0){
        ok = 0; // điều kiện dừng, tức cấu hình cuối
    }
    else{
        x[i] = 1;
        i++;
        while (i <= n){
            x[i] = 0;
            i++;
        }
    }
}

int main(){
    int n = 3;
    int x[n+1];
    int ok = 1;
    first_config(x,n); 

    while(ok){
        for(int i = 1; i <= n; i++){
            cout << x[i];
        }
        cout << endl;
        generation(x, n, ok);
    }
    return 0;
}

Sinh tập con tăng dần
#include <iostream>
using namespace std;

void print(int x[], int k){
    for (int i = 1; i <= k; i++){
        cout << x[i];
    }
    cout << endl;
}

void first_config(int x[], int k){
    for (int i = 1; i <= k; i+=1){
        x[i] = i;
    }
}

void next_config(int x[], int n, int k, int &ok){
    int i = k;
    while(i>0 && x[i] == n-k+i){
        i -= 1;
    }
    if(i == 0){
        ok = 0;
    }
    else{
        x[i] += 1;
        i++;
        while(i<=k){
            x[i] = x[i-1]+1;
            i+=1;
        }
    }
}

int main(){
    int n; cin >> n;
    int k; cin >> k;
    int x[n+1];
    first_config(x, k);
    int ok = 1;
    while (ok){
        print(x, k);
        next_config(x, n, k, ok);
    }
    return 0;
}
123
124
125
134
135
145
234
235
245
345
Sinh tập con k = 6, n = 7
#include <bits/stdc++.h>
using namespace std;

void first_config(int x[], int k){
	for (int i = 1; i <= k; i++){
		x[i] = i;
	}
}

void next_config(int x[], int n, int k, int &ok){
	int i = k;
	while (i >= 1 && x[i] == n-k+i) i--;
	if (i == 0) ok = 0;
	else {
		x[i] += 1;
		i++;
		while(i <= k){
			x[i] = x[i-1] + 1;
			i++;
		}
	}
}

int main(){
	int n = 7, k = 6;
	char lable[n+1] = {' ', 'A', 'B', 'C', 'D', 'E', 'F', 'G'};
	int x[k+1];
	int ok = 1;
	first_config(x, k);
	while(ok){
		for (int i = 1; i <= k; i++){
			cout << lable[x[i]] << " ";
		}
		cout << endl;
		next_config(x, n, k, ok);
	}
	return 0;
}

Sinh các chuỗi ký tự chỉ chứa 2 ký tự ‘a’ và ‘b’
#include <iostream>
using namespace std;

void print(char x[], int k){
    for (int i = 1; i <= k; i++){
        cout << x[i];
    }
    cout << endl;
}

void first_config(char x[], int k){
    for(int i=1; i<=k; i++){
        x[i] = 'a';
    }
}

void next_config(char x[], int k, int &ok){
    int i = k;
    while(i>0 && x[i] == 'b'){
        i--;
    }
    if(i == 0){
        ok = 0;
    }
    else{
        x[i] = 'b';
        i++;
        while(i<=k){
            x[i] = 'a';
            i++;
        }
    }
}

int main(){
    int n; cin >> n;
    int k; cin >> k;
    char x[n+1];
    first_config(x, k);
    int ok = 1;
    while (ok){
        print(x, k);
        next_config(x, k, ok);
    }
    return 0;
}
2
2
aa
ab
ba
bb
Sinh 4 sinh viên từ 6 sinh viên cho trước
#include <iostream>
#include <string>
using namespace std;

// Hàm in ra tổ hợp hiện tại
void print(string students[], int x[], int k) {
    for(int i = 1; i <= k; i++) {
        cout << students[x[i]] << " ";
    }
    cout << endl;
}

// Khởi tạo cấu hình đầu tiên: chọn 1,2,...,k
void first_config(int x[], int k) {
    for(int i = 1; i <= k; i++) {
        x[i] = i;
    }
}

// Sinh cấu hình tiếp theo
void next_config(int x[], int n, int k, int &ok) {
    int i = k;
    while(i > 0 && x[i] == n - k + i) {
        i--;
    }
    if(i == 0) {
        ok = 0; // đã hết tổ hợp
    }
    else {
        x[i] += 1;
        i++;
        while(i <= k) {
            x[i] = x[i-1] + 1;
            i++;
        }
    }
}

int main() {
    string students[7] = {"", "Tam", "Toan", "Trang", "Cong", "Trung", "Tu"};
    int n = 6; // tổng số sinh viên
    int k = 4; // số sinh viên chọn
    int x[k+1];
    
    first_config(x, k);
    int ok = 1;

    while(ok) {
        print(students, x, k);
        next_config(x, n, k, ok);
    }

    return 0;
}
Tam Toan Trang Cong 
Tam Toan Trang Trung
Tam Toan Trang Tu
Tam Toan Cong Trung
Tam Toan Cong Tu
Tam Toan Trung Tu
Tam Trang Cong Trung
Tam Trang Cong Tu
Tam Trang Trung Tu
Tam Trang Trung Tu
Tam Trang Trung Tu
Tam Trang Trung Tu
Tam Trang Trung Tu
Tam Trang Trung Tu
Tam Trang Trung Tu
Tam Cong Trung Tu
Toan Trang Cong Trung
Tam Trang Trung Tu
Tam Cong Trung Tu
Tam Cong Trung Tu
Toan Trang Cong Trung
Toan Trang Cong Tu
Toan Trang Trung Tu
Toan Cong Trung Tu
Trang Cong Trung Tu
Sinh hoán vị n phần tử
#include <iostream>
using namespace std;

void first_config(int x[], int n){ // khởi tạo cấu hình đầu tiên
    for (int i = 1; i<=n; i+=1){
        x[i] = i;
    }
}

void next_config(int x[], int n, int &ok){
    int i = n-1;
    while(i>=1 && x[i] > x[i+1]){
        --i;
    }
    if(i == 0){
        ok = 0; // điều kiện dừng, tức cấu hình cuối
    }
    else{
        int j = n;
        while (x[i] > x[j]) --j;
        swap(x[i], x[j]);
        int l = i+1, r = n;
        while (l < r){
            swap(x[l], x[r]);
            ++l;--r;
        }
    }
}

int main(){
    int n = 3;
    int x[n+1];
    int ok = 1;
    first_config(x,n); 

    while(ok){
        for(int i = 1; i <= n; i++){
            cout << x[i];
        }
        cout << endl;
        next_config(x, n, ok);
    }
      
    return 0;
}
1 2 3
1 3 2
1 2 3
1 2 3
1 2 3
1 2 3
1 2 3
1 2 3
1 2 3
1 2 3
1 2 3
1 3 2
2 1 3
2 3 1
3 1 2
3 2 1
Liệt kê tất cả các cách xếp 6 sinh viên vào 6 chiếc ghế được đánh số từ 1 đến 6
#include <iostream>
using namespace std;

void first_config(int x[], int n){ // khởi tạo cấu hình đầu tiên
    for (int i = 1; i<=n; i+=1){
        x[i] = i;
    }
}

void next_config(int x[], int n, int &ok){
    int i = n-1;
    while(i>=1 && x[i] > x[i+1]){
        --i;
    }
    if(i == 0){
        ok = 0; // điều kiện dừng, tức cấu hình cuối
    }
    else{
        int j = n;
        while (x[i] > x[j]) --j;
        swap(x[i], x[j]);
        int l = i+1, r = n;
        while (l < r){
            swap(x[l], x[r]);
            ++l;--r;
        }
    }
}

int main(){
    int n = 6;
    string name[n+1] = {"", "trang", "cong", "trung", "binh", "hoan", "mai"};
    int x[n+1]; // lưu chỉ số
    int ok = 1;
    first_config(x,n); 

    int count = 1;
    while(ok){
        next_config(x, n, ok);
        if (ok) count++;
    }
    cout << count;
    return 0;
}
720
Sắp 4 sinh viên vào 4 ghế có thứ tự
#include <bits/stdc++.h>
using namespace std;

void first_cofig(int x[], int n){
	for (int i = 1; i <= n; i++){
		x[i] = i;
	}
}

void next_cofig(int x[], int n, int &ok){
	int i = n-1;
	while(i >= 1 && x[i] > x[i+1]){
		--i;
	}
	if(i == 0){
		ok = 0;
	}
	else{
		int j = n;
		while (x[i] > x[j]) --j;
		swap(x[i], x[j]);
		int l = i+1, r = n;
		while (l < r){
			swap(x[l], x[r]);
			++l; --r;
		}
	}
}

int main(){
	int n = 4;
	char label[5] = {' ' ,'A', 'B', 'C', 'D'};
	string name[5] = {"", "tung", "cuc", "truc", "mai"};
	int ok = 1;
	int x[5] = {0};
	first_cofig(x, n);
	while(ok){
		for (int i = 1; i <= n; i++){
			cout << name[x[i]] << " - " << label[i] << " ";
		}
		cout << endl;
		next_cofig(x, n, ok);
	}
	return 0;
}
Backtracking (Quay lui) 
Bài tập
Sinh dãy nhị phân có n phần tử
void sinh_nhi_phan_2(int n, string current){
    if (current.length() == n){
        cout << current << endl;
        return;
    }
    string current1 = current+"0";
    string current2 = current+"1";
    sinh_nhi_phan_2(n, current1);
    sinh_nhi_phan_2(n, current2);
}
000
001
010
011
100
101
110
111
#include <iostream>
using namespace std;

void print(int x[], int n){
    for(int i = 1; i <= n; i++){
        cout << x[i];
    }
    cout << endl;
}

void truy(int x[], int index, int n){
    for(int i = 0; i <= 1; i++){
        x[index] = i;
        if(index == n){
            print(x, n);
        }
        else{
            truy(x, index+1, n);
        }
    }
}

int main(){
    int n = 3;
    int x[n+1];
    truy(x, 1, 3);
    return 0;
}
000
001
010
011
100
101
110
111
Sinh tổ hợp chập k của n bằng quay lui
#include <iostream>
using namespace std;

void print(int x[], int k){
    for(int i = 1; i <= k; i++){
        cout << x[i];
    }
    cout << endl;
}

void truy(int x[], int index, int n, int k){
    for(int i = x[index-1]+1; i <= n-k+index; i++){
        x[index] = i; 
        if(index == k){
            print(x, k);
        }
        else{
            truy(x, index+1, n, k);
        }
    }
}

int main(){
    int n = 6;
    int k = 3;
    int x[n+1];
    x[0] = 0;
    truy(x, 1, n, k);
    return 0;
}
123
124
125
126
134
135
136
145
146
156
234
235
236
245
246
256
345
346
356
356
356
456
Chia để trị
Bài tập
Tìm giá trị lớn nhất trong mảng bằng chia để trị
int max_value(int x[], int l, int r){
    if (l==r){
        return x[l];
    }
    else{
        int m = (int)((l+r)/2);
        int max_left = max_value(x, l, m);
        int max_right = max_value(x, m+1, r);

        return max(max_left, max_right);
    }
}
Tìm giá trị chẵn nhỏ nhất trong mảng bằng chia để trị
#include <iostream>
#include <climits>
using namespace std;

int min_even_value(int x[], int l, int r){
    if (l == r){
        if (x[l] % 2 == 0) return x[l];
        return INT_MAX;  // nếu không chẵn thì trả về giá trị rất lớn
    }
    int m = (l + r) / 2;
    int min_left = min_even_value(x, l, m);
    int min_right = min_even_value(x, m+1, r);
    return min(min_left, min_right);
}

int main(){
    int a[] = {5, 7, 2, 9, 8, 11};
    int n = sizeof(a)/sizeof(a[0]);
    int result = min_even_value(a, 0, n-1);
    if (result == INT_MAX) cout << "Khong co so chan nao\n";
    else cout << "So chan nho nhat: " << result << endl;
}
So chan nho nhat: 2
Tìm giá trị chẵn lớn nhất trong mảng bằng chia để trị
#include <iostream>
#include <climits>
using namespace std;

int max_even_value(int x[], int l, int r){
    if (l == r){
        if (x[l] % 2 == 0) return x[l];
        return INT_MIN;  // nếu không chẵn thì trả về giá trị rất lớn
    }
    int m = (l + r) / 2;
    int min_left = max_even_value(x, l, m);
    int min_right = max_even_value(x, m+1, r);
    return max(min_left, min_right);
}

int main(){
    int a[] = {1, 2, 5, 7, 9, 8, 11};
    int n = sizeof(a)/sizeof(a[0]);
    int result = max_even_value(a, 0, n-1);
    if (result == INT_MIN) cout << "Khong co so chan nao\n";
    else cout << "So chan long nhat: " << result << endl;
}
Tính tổng các số dương trong mảng
#include <iostream>
using namespace std;

int sum(int x[], int l, int r) {
    if (l == r) {
        if (x[l] > 0) return x[l];
        else return 0;
    } else {
        int m = (l + r) / 2;
        int sum_left = sum(x, l, m);
        int sum_right = sum(x, m+1, r);
        return sum_left + sum_right;
    }
}

int main() {
    int a[] = {5, -2, 7, 0, -3, 4};
    int n = sizeof(a)/sizeof(a[0]);
    cout << "Tong cac so duong = " << sum(a, 0, n-1) << endl;
}
Tong cac so duong = 16   // (5 + 7 + 4)
Thuật toán pow(a, n)
Output = 243
int helper(int a, int n) {
	if (a == 0) return 0;
	if (n == 0) return 1;
	int res = helper(a * a, n / 2);
	if (n % 2 != 0) return a * res;
	else return res;
}

int power(int a, int n) {
	if (n > 0) return helper(a, n);
	else if (n == 0) return 1;
	else if (a == 0) return 0;
	else return 1.0 / helper(a, -1 * n);
}
cout << power(3,5);
Sắp xếp trộn
#include <bits/stdc++.h>
using namespace std;
void merge(int x[], int l, int m, int r){
    int n1 = m-l+1; // số phần tử nhánh trái
    int n2 = r-(m+1)+1; // số phần tử nhánh phải
    int L[n1], R[n2];
    for (int i = 0; i<n1; i++) L[i] = x[l+i]; // lất từ l -> m
    for (int j = 0; j<n2; j++) R[j] = x[m+1+j]; //lấy từ m+1 -> r
    int i = 0, j = 0, k = l;
    while(i<n1 && j<n2){
        if(L[i] <= R[j]) x[k++] = L[i++];
        else x[k++] = R[j++];
    }
    while (i < n1) x[k++] = L[i++];
    while (j < n2) x[k++] = R[j++];
}

void merge_sort(int x[], int l, int r){
    if (l < r){ // nếu mảng có nhiều hơn 1 phần tử thì đệ quy, 1 phần tử thì dừng
        int m = (l+r)/2;
        merge_sort(x, l, m);
        merge_sort(x, m+1, r);
        merge(x, l, m, r);
    }
}

int main(){
    int arr[] = {38, 27, 43, 3, 9, 82, 10};
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << "Mang ban dau: ";
    for (int i = 0; i < n; i++) cout << arr[i] << " ";
    cout << endl;

    merge_sort(arr, 0, n - 1); // gọi merge sort

    cout << "Mang sau khi sap xep: ";
    for (int i = 0; i < n; i++) cout << arr[i] << " ";
    cout << endl;
    return 0;
}

Mang ban dau: 38 27 43 3 9 82 10 
Mang sau khi sap xep: 3 9 10 27 38 43 82
#include <bits/stdc++.h>
using namespace std;

void merge(vector<double> &x, int l, int m, int r){
	vector<double> left(x.begin() + l, x.begin()+m+1); //so phan tu nhanh trai
	vector<double> right(x.begin()+m+1, x.begin()+r+1); // so phan tu nhanh phai
	int i = 0; // index nhanh trai
	int j = 0; // index nhanh phai
	int k = l; // index nhanh chinh
	while (i < left.size() && j < right.size()){
		if (left[i] < right[j]) x[k++] = left[i++];
		else x[k++] = right[j++];
	}
	while (i < left.size()) x[k++] = left[i++];
	while (j < right.size()) x[k++] = right[j++];
}

void merge_sort(vector<double> &x, int l, int r){
	if (l < r){
		int m = (l+r)/2;
		merge_sort(x, l, m);
		merge_sort(x, m+1, r);
		merge(x, l, m, r);
	}
}

int main(){
	int min = 0;
	int max = 50;
	srand(time(0));
	
	vector<double> li;
	int n = 10;
	for (int i = 0; i < n; i++){
		double r = min + ((double)rand()/RAND_MAX)*(max-min);
		li.push_back(r);
	}
	for (int i = 0; i < n; i++){
		cout << li[i] << " ";
	}
	cout << endl;
	merge_sort(li, 0, li.size()-1);
	for (int i = 0; i < n; i++){
		cout << li[i] << " ";
	}
	return 0;
}
Tham lam
Bài tập
Xếp hàng lên xe
Ví dụ 1:
Công ty vận tải A có n chiếc xe tải với các xe có tải trọng khác nhau, xe tải ti
có tải trọng là ki (chở được ki tấn). Công ty A cần vận chuyển m tấn hàng từ một
kho đến địa điểm khác, hỏi công ty cần sử dụng bao nhiêu chiếc xe tải, gồm những
xe nào (cho biết tải trọng của xe được chọn sử dụng) sao cho số xe tải cần sử dụng
là ít nhất.
Cài đặt chương trình giải quyết bài toán (sử dụng chiến lược tham lam)
#include <bits/stdc++.h>
using namespace std;

void arrange_truck(int water[], int n, int res[], int k, int &count){
	for (int i = n-1; i >= 0; i--){
		while (k >= water[i]){
			k -= water[i];
			res[i] += 1;
			count++;
		}
		if(k == 0) break;		
	}
}

void print(int weight[], int res[], int n, int count){
	for (int i = 0; i < n; i++){
		cout << weight[i] << " - " << res[i] << " ";
		if(i < n) cout << ", ";
	}
	cout << endl;
	cout << "sum = " << count << endl;
}

int main(){
	int n = 9;
	int count = 0;
	int weight[n] = {1,2,5,10,20,50,100,200,500}; // tan
	int res[n] = {0,0,0,0,0,0,0,0,0}; // ket qua
	arrange_truck(weight, n, res, 127, count);
	print(weight, res, n, count);
	return 0;
}
Ví dụ 2:
Thùng xe có kích thước k (m^3). Có n kiện hàng khác nhau, kiện hàng k_i có khối lượng m_i (kg) và kích thước k_i (m^3). 
Hỏi xếp được bao nhiêu kiện hàng lên thùng xe, gồm kiện hàng nào, sao cho tổng khối lượng xếp lên xe là lớn nhất
#include <bits/stdc++.h>
using namespace std;

// thông tin 1 kiện hàng
struct Box{
	int weight; // khối lượng (kg)
	int size_m3; // kích thước (m3)
	double w_s; // mật độ (kg/m3)
};

struct LineUp{
	int spaces; // thể tích thùng xe
	int n; // số kiện hàng
	vector<Box> box; // danh sách kiện hàng
	// nhập dữ liệu
	void config(){
		cout << "Kich thuoc thung xe (m3): "; cin >> spaces;
		cout << "Số kiện hàng: "; cin >> n;
		// cấp phát đủ chỗ cho n phần tử
		box.resize(n);
		for (int i = 0; i < n; i++){
			cout << "\nKhoi luong cua hang thu " << i+1 << "(kg): "; cin >> box[i].weight;
			cout << "\nKich thuoc cua hang thu " << i+1 << "(m3): "; cin >> box[i].size_m3;
			box[i].w_s = (double) box[i].weight / box[i].size_m3;
		}
		cout << endl;
	}
	// sắp tăng theo w_s
	void merge(vector<Box>& box, int l, int m, int r) {
		vector<Box> left(box.begin() + l, box.begin() + m + 1); // số phần tử nhánh trái
		vector<Box> right(box.begin() + m + 1, box.begin() + r + 1); // số phần tử nhánh phải
		int i = 0, j = 0, k = l;
		while (i < left.size() && j < right.size()){
			if (left[i].w_s < right[j].w_s) box[k++] = left[i++];
			else box[k++] = right[j++];
		}
		while (i < left.size()) box[k++] = left[i++];
		while (j < right.size()) box[k++] = right[j++];
	}

	void merge_sort(vector<Box> &box, int l, int r){
		if (l < r) {
			int m = (l+r)/2;
			merge_sort(box, l, m);
			merge_sort(box, m+1, r);
			merge(box, l, m, r);
		}
		
	}

	vector<Box> line_up(){
		merge_sort(box, 0, n-1);
		vector<Box> res;
		int remain = spaces; // copy vì không muốn thay đổi kích thước gốc
		for (int i = n-1; i >= 0; i--){
			if (box[i].size_m3 <= remain) {
				res.push_back(box[i]);
				remain -= box[i].size_m3;
			}
		}
		return res;
	}

	void print(vector<Box>& res){
		cout << "\nSo kien hang dua len xe: " << res.size();
		for (int i = 0; i < res.size(); i++){
			cout << "Hang" << i+1 << ": " << res[i].weight << " (kg) " << res[i].size_m3 << " (m3) " << res[i].w_s << " (kg/m3)" << endl;
		}
	}
};

int main(){
    LineUp lu;
    lu.config();
    vector<Box> res = lu.line_up();
    lu.print(res);
	return 0;
}
Đổi tiền
#include <bits/stdc++.h>
using namespace std;

void exchange_money(int money[], int n, int res[], int k){
	for (int i = n-1; i >= 0; i--){
		while (k >= money[i]){
			k -= money[i];
			res[i] += 1;
		}
		if(k == 0) break;		
	}
}

void print(int money[], int res[], int n){
	for (int i = 0; i < n; i++){
		cout << money[i] << " - " << res[i] << " ";
		if(i < n) cout << ", ";
	}
	cout << endl;
}

int main(){
	int n = 9;
	int money[n] = {1,2,5,10,20,50,100,200,500};
	int res[n] = {0,0,0,0,0,0,0,0,0};
	exchange_money(money, n, res, 127);
	print(money, res, n);
	return 0;
}
1 - 0 , 2 - 1 , 5 - 1 , 10 - 0 , 20 - 1 , 50 - 0 , 100 - 1 , 200 - 0 , 500 - 0 ,
Bài toán đổ nước
#include <bits/stdc++.h>
using namespace std;

void pour_water(int water[], int n, int res[], int k){
	for (int i = n-1; i >= 0; i--){
		while (k >= water[i]){
			k -= water[i];
			res[i] += 1;
		}
		if(k == 0) break;		
	}
}

void print(int water[], int res[], int n){
	for (int i = 0; i < n; i++){
		cout << water[i] << " - " << res[i] << " ";
		if(i < n) cout << ", ";
	}
	cout << endl;
}

int main(){
	int n = 9;
	int water[n] = {1,2,5,10,20,50,100,200,500};
	int res[n] = {0,0,0,0,0,0,0,0,0};
	pour_water(water, n, res, 127);
	print(water, res, n);
	return 0;
}
1 - 0 , 2 - 1 , 5 - 1 , 10 - 0 , 20 - 1 , 50 - 0 , 100 - 1 , 200 - 0 , 500 - 0
Bài toán ăn trộm
Một kho hàng gồm n gói hàng được ghi số thứ tự từ 1 đến n, gói hàng thứ i
có kích thước si và khối lượng mi (1 ≤ i ≤ n).
Ban đêm một cô chộm lẻn vào kho để lấy trộm hàng, cô chộm mang theo một chiếc
ba lô có kích thước k. Vì nữ nhi sức yếu nên cô chộm chỉ chọn những gói hàng nhẹ
nhàng.
Yêu cầu: Hãy chọn cho cô chộm những gói hàng ưng ý: tổng khối lượng các gói
hàng được chọn là nhỏ nhất và tổng kích thước không vượt quá kích thước của ba
lô.
#include <bits/stdc++.h>
using namespace std;

// thông tin 1 gói hàng
struct Box{
	int weight; // khối lượng (kg)
	int size_m3; // kích thước (m3)
	double w_s; // mật độ (kg/m3)
};

struct Steal{
	int spaces; // kích thước cái túi
	int n; // tổng số hàng trong kho
	int count = 0;
	vector<Box> box; // danh sách kiện hàng trong kho
	// nhập dữ liệu
	void config(){
		cout << "Kich thuoc cai tui (m3): "; cin >> spaces;
		cout << "Tong so kien hang trong kho: "; cin >> n;
		// cấp phát đủ chỗ cho n phần tử
		box.resize(n);
		for (int i = 0; i < n; i++){
			cout << "\nKhoi luong cua hang thu " << i+1 << "(kg): "; cin >> box[i].weight;
			cout << "\nKich thuoc cua hang thu " << i+1 << "(m3): "; cin >> box[i].size_m3;
			box[i].w_s = (double) box[i].weight / box[i].size_m3;
		}
		cout << endl;
	}
	// sắp tăng theo w_s
	void merge(vector<Box>& box, int l, int m, int r) {
		vector<Box> left(box.begin() + l, box.begin() + m + 1); // số phần tử nhánh trái
		vector<Box> right(box.begin() + m + 1, box.begin() + r + 1); // số phần tử nhánh phải
		int i = 0, j = 0, k = l;
		while (i < left.size() && j < right.size()){
			if (left[i].w_s < right[j].w_s) box[k++] = left[i++];
			else box[k++] = right[j++];
		}
		while (i < left.size()) box[k++] = left[i++];
		while (j < right.size()) box[k++] = right[j++];
	}

	void merge_sort(vector<Box> &box, int l, int r){
		if (l < r) {
			int m = (l+r)/2;
			merge_sort(box, l, m);
			merge_sort(box, m+1, r);
			merge(box, l, m, r);
		}
		
	}

	vector<Box> steal(){
		merge_sort(box, 0, n-1);
		vector<Box> res;
		int remain = spaces; // copy vì không muốn thay đổi kích thước gốc
		for (int i = 0; i < n; i++){
			while (box[i].size_m3 <= remain) {
				res.push_back(box[i]);
				remain -= box[i].size_m3;
				count++;
			}
		}
		return res;
	}

	void print(vector<Box> res){
		cout << "\nSo kien hang dua len xe: " << res.size();
		for (int i = 0; i < res.size(); i++){
			cout << "Hang" << i+1 << ": " << res[i].weight << " (kg) " << res[i].size_m3 << " (m3) " << res[i].w_s << " (kg/m3)" << endl;
		}
		cout << endl;
		cout << "Tong so hang da trom: " << count << endl;
	}
};

int main(){
    Steal lu;
    lu.config();
    vector<Box> res = lu.steal();
    lu.print(res);
	return 0;
}

Bài toán lập lịch
// bai toan lap lich
#include <bits/stdc++.h>
using namespace std;

struct Schedude{
	int start_time;
	int end_time;
	void print(){
		cout << start_time << " " << end_time << endl;
	}
};

struct ListSchedule{
	vector<Schedude> sch;
	vector<Schedude> res;
	int n; // so luong
	void config(){
		sch.push_back({0, 9});
		sch.push_back({8, 10});
		sch.push_back({10, 14});
		sch.push_back({15, 20});
		sch.push_back({17, 21});
		sch.push_back({21, 23});
		n = sch.size();
	}
	void print(vector<Schedude> sch){
		for (int i = 0; i < sch.size(); i++){
			sch[i].print();
		}
		cout << endl;
	}
	void arrange_schedule(){
		res.push_back(sch[0]);
		int last_end = sch[0].end_time;
		for (int i = 1; i < n; i++){
			if (sch[i].start_time >= last_end) {
				res.push_back(sch[i]);
				last_end = sch[i].end_time;
			}
			cout << endl;
		}
	}
};

int main(){
	ListSchedule l;
	l.config();
	l.arrange_schedule();
	l.print(l.sch);
	l.print(l.res);
	return 0;
}

Bài toán dùng số tiền p để mua quạt nhiều nhất
Cho một số tiền p và một danh sách d gồm n chiếc quạt bàn khác nhau về giá bán, thông tin về mỗi chiếc quạt bàn gồm: tên hãng sản xuất, màu sắc, giá bán. Viết chương trình thực hiện:
    • Sử dụng một thuật toán được thiết kế theo chiến lược tham lam để cho biết nếu dùng số tiền p thì có thể mua được nhiều nhất bao nhiêu chiếc quạt bàn trong danh sách d, gồm những chiếc quạt nào.
    • Khai báo cấu trúc dữ liệu. Khởi tạo p (0 < p < 1200000), n và danh sách d (5 < n < 12). Hiển thị các kết quả, trong đó mỗi chiếc quạt cần hiển thị tên hãng sản xuất và giá bán.
#include <bits/stdc++.h>
using namespace std;

struct Quat{
    string ten, mau;
    int gia;

    void in(){ cout << ten << " " << mau << " " << gia << endl; }
};

struct DanhSach{
    vector<Quat> ds;
    int n, p;

    void ran(){
        vector<string> ten = {"hang1", "hang2", "hang3", "hang4", "hang5", "hang6", "hang7", "hang8", "hang9", "hang10"};
        vector<string> mau = {"mau1", "mau2", "mau3", "mau4", "mau5", "mau6", "mau7", "mau8", "mau9", "mau10"};
        vector<int> gia = {100, 200, 250, 270, 300, 350, 400, 500, 600, 700};

        random_device rd;
        mt19937 g(rd());
        shuffle(ten.begin(), ten.end(), g);
        shuffle(mau.begin(), mau.end(), g);
        shuffle(gia.begin(), gia.end(), g);

        for(int i = 0; i < n; ++i) ds.push_back({ten[i], mau[i], gia[i]});
    }

    void khoi_tao(){
        do{
            cout << "p: "; cin >> p; // so tien
            cout << "n: "; cin >> n; // so phan tu
            if(!(0 < p && p < 1200000 && 5 < n && n < 12)) cout << "loi\n";
        }while(!(0 < p && p < 1200000 && 5 < n && n < 12));
        ran();
    }

    void sap_tang(){
        sort(ds.begin(), ds.end(), [](const Quat &a, const Quat &b){
            return a.gia < b.gia;
        });
    }

    void tham_lam(){
        int tong = 0;
        vector<Quat> chon;
        for(int i=0; i<n; ++i){
            if(tong + ds[i].gia <= p){
                chon.push_back(ds[i]);
                tong += ds[i].gia;
            }      
        }

        cout << "tong so quat duoc chon khi dung p tien: " << chon.size() << endl;
        cout << "danh sach quat duoc chon:\n";
        for(auto &a : chon) a.in();
    }
};

int main(){
    DanhSach li;
    li.khoi_tao();
    li.sap_tang();
    li.tham_lam();
    return 0;
}
#include <bits/stdc++.h>
using namespace std;

// danh sach n chiec quat
struct Quat {
    string ten_hang;
    string mau_sac;
    int gia;

    void in() {
        cout << ten_hang << " " << mau_sac << " " << gia << endl;
    }
};

struct DanhSach {
    vector<Quat> ds;
    int n; // so luong phan tu trong danh sach
    int p; // mot so tien p

    // Generate unique "ten_hang" for the fans by shuffling
    void random_ten_hang() {
        vector<string> ten_hang = {"hang1", "hang2", "hang3", "hang4", "hang5", "hang6", "hang7", "hang8"};
        random_shuffle(ten_hang.begin(), ten_hang.end());  // Shuffle the list to randomize order
        for (int i = 0; i < n; i++) ds[i].ten_hang = ten_hang[i];  // Pick unique item from shuffled list
    }
    // Generate unique "mau_sac" for the fans by shuffling
    void random_mau_sac() {
        vector<string> mau_sac = {"mau1", "mau2", "mau3", "mau4", "mau5", "mau6", "mau7", "mau8"};
        random_shuffle(mau_sac.begin(), mau_sac.end());  // Shuffle the list to randomize order
        for (int i = 0; i < n; i++) ds[i].mau_sac = mau_sac[i];  // Pick unique item from shuffled list
    }
    // Generate unique "gia" for the fans by shuffling
    void random_gia() {
        vector<int> gia = {100, 200, 250, 270, 300, 350, 400, 500};  // Removed 0 to avoid invalid values
        random_shuffle(gia.begin(), gia.end());  // Shuffle the list to randomize order
        for (int i = 0; i < n; i++) ds[i].gia = gia[i];  // Pick unique item from shuffled list
    }

    // Initialize the fan list (taking input from user and setting up the lists)
    void khoi_tao() {
        // Take valid input for p and n
        do {
            cout << "p: "; cin >> p;
            cout << "n: "; cin >> n;
            if (p < 0 || p > 1200000 || n < 5 || n > 8) // Adjusted n range to avoid exceeding available options
                cout << "loi, yeu cau nhap lai" << endl;
        } while (p < 0 || p > 1200000 || n < 5 || n > 8);  // Restrict n to avoid too many fans

        // Resize the vector `ds` to have `n` elements before assigning values
        ds.resize(n);
        cout << "ds.resize(n) done. n = " << n << endl;

        // Generate unique random fan attributes (name, color, price)
        random_ten_hang();
        random_mau_sac();
        random_gia();
    }

    // Print the list of fans
    void in_ds() {
        // Ensure that the list is not empty
        if (ds.empty()) {
            cout << "Danh sach qua rong!" << endl;
            return;
        }

        for (int i = 0; i < n; i++) {
            ds[i].in();
        }
    }
    
    // sap xep
    void merge(vector<Quat> &ds, int l, int m, int r){
    	vector<Quat> left(ds.begin()+l, ds.begin()+m+1);
    	vector<Quat> right(ds.begin()+m+1, ds.begin()+r+1);
    	int i = 0, j = 0, k = l;
    	while(i < left.size() && j < right.size()){
    		if(left[i].gia < right[j].gia) ds[k++] = left[i++];
    		else ds[k++] = right[j++];
		}
		while(i < left.size()) ds[k++] = left[i++];
		while(j < right.size()) ds[k++] = right[j++];
	}
    void merge_sort(vector<Quat> &ds, int l, int r){
    	if (l < r){
    		int m = (l+r)/2;
    		merge_sort(ds, l, m);
    		merge_sort(ds, m+1, r);
    		merge(ds, l, m, r);
		}
	}
	
	// tham lam
	void tham_lam(){
		merge_sort(ds, 0, n-1);
		int cur = 0;
		int count = 0;
		vector<int> index;
		for (int i = 0; i < n; i++){
			if (cur+ds[i].gia <= p){
				cur += ds[i].gia;
				index.push_back(i);
			}
		}
		// in
		cout<< "danh sach quat duoc lua chon: " << endl;
		cout << "so quat duoc lua chon: " << index.size() << endl;
		for (int i = 0; i < index.size(); i++) ds[index[i]].in();
	}
};

int main() {
    srand(time(0));  // Seed the random number generator to get different results each time
    DanhSach danhSach;

    // Initialize the fan list
    danhSach.khoi_tao();

    // Print the list
    cout << "Danh sach quat truoc khi sap xep: " << endl;
    danhSach.in_ds();

    // Use greedy algorithm to choose fans within budget
    danhSach.tham_lam();

    return 0;
}
#include <bits/stdc++.h>
using namespace std;

struct Quat{
    string tenH;
    string mau;
    int gia;

    void in(){
        cout << tenH << " " << mau << " " << gia << endl;
    }
};

struct DanhSach{
    vector<Quat> ds;
    int n;
    int p;
    
    void ran_ten(){
        vector<string> ten = {"hang1", "hang2", "hang3", "hang4", "hang5", "hang6", "hang7", "hang8", "hang9", "hang10"};
        random_shuffle(ten.begin(), ten.end());
        for (int i = 0; i < n; i++) ds[i].tenH = ten[i];
    }
    void ran_mau(){
        vector<string> mau = {"mau1", "mau2", "mau3", "mau4", "mau5", "mau6", "mau7", "mau8", "mau9", "mau10"};
        random_shuffle(mau.begin(), mau.end());
        for (int i = 0; i < n; i++) ds[i].mau = mau[i];
    }
    void ran_gia(){
        vector<int> gia = {10, 20, 50, 100, 200, 500, 700, 900, 1100, 1200};
        random_shuffle(gia.begin(), gia.end());
        for (int i = 0; i < n; i++) ds[i].gia = gia[i];
    }

    void khoi_tao(){
        do{
            cout << "n: "; cin >> n;
            cout << "p: "; cin >> p;
            if (p <= 0 || p >= 1200000 || n <= 5 || n >= 12) cout << "lỗi, yêu cầu nhập lại";
        } while(p <= 0 || p >= 1200000 || n <= 5 || n >= 12);
        ds.resize(n);
        ran_ten();
        ran_mau();
        ran_gia();
    }

    void in_ds(){
        for (int i = 0; i < n; i++){
            ds[i].in();
        }
    }

    // tham lam
    static bool so_sanh_gia(const Quat &a, const Quat &b) {
        return a.gia < b.gia;
    }

    void sap_xep_tang(){
        sort(ds.begin(), ds.end(), so_sanh_gia);
    }

    void tham_lam(){
        sap_xep_tang();
        vector<int> index;
        int cur = 0;
        for (int i = 0; i < n; i++){
            if (cur + ds[i].gia <= p){
                cur += ds[i].gia;
                index.push_back(i);
            }
        }

        cout << "tong so quat lua chon: " << index.size() << endl;
        for (int i = 0; i < index.size(); i++){
            ds[index[i]].in();
        }
    }
};
int main(){
    DanhSach li;
    li.khoi_tao();
    li.in_ds();
    li.tham_lam();
    return 0;
}
#include <bits/stdc++.h>
using namespace std;

struct Quat{
    string tenH;
    string mau;
    int gia;

    void in(){
        cout << tenH << " " << mau << " " << gia << endl;
    }
};

struct DanhSach{
    vector<Quat> ds;
    int n;
    int p;
    
    void tao_random(){
        random_device rd;
        mt19937 g(rd());
        vector<string> ten = {"hang1","hang2","hang3","hang4","hang5","hang6","hang7","hang8","hang9","hang10"};
        vector<string> mau = {"do","xanh","vang","den","trang","tim","hong","xam","nau","luc"};
        vector<int> gia = {10,20,50,100,200,500,700,900,1100,1200};
        shuffle(ten.begin(), ten.end(), g);
        shuffle(mau.begin(), mau.end(), g);
        shuffle(gia.begin(), gia.end(), g);
        for (int i = 0; i < n; i++) ds.push_back({ten[i], mau[i], gia[i]});
    }

    void khoi_tao(){
        do{
            cout << "n: "; cin >> n;
            cout << "p: "; cin >> p;
            if (p <= 0 || p >= 1200000 || n <= 5 || n >= 12) cout << "lỗi, yêu cầu nhập lại";
        } while(p <= 0 || p >= 1200000 || n <= 5 || n >= 12);
        tao_random();
    }

    void in_ds(){
        for (auto &a : ds) a.in();
    }

    void sap_xep_tang(){
        sort(ds.begin(), ds.end(), [](const Quat &a, const Quat &b){
            return a.gia < b.gia;
        });
    }

    void tham_lam(){        
        vector<int> index;
        int cur = 0;
        for (int i = 0; i < n; i++){
            if (cur + ds[i].gia <= p){
                cur += ds[i].gia;
                index.push_back(i);
            }
        }
        cout << "\nTong tien su dung: " << cur << endl;
        cout << "tong so quat lua chon: " << index.size() << endl;
        for (int i = 0; i < index.size(); i++){
            ds[index[i]].in();
        }
    }
};
int main(){
    DanhSach li;
    li.khoi_tao();
    li.sap_xep_tang();
    li.in_ds();
    li.tham_lam();
    return 0;
}
Bán quạt ít nhất mà dùng đúng số tiền p
Dùng tiền nhiều hơn p để bán ít nhất quạt
Cho một số tiền p và một danh sách d gồm n chiếc quạt bàn khác nhau về giá bán,thông tin về mỗi chiếc quạt bàn gồm: tên hãng sản xuất, màu sắc, giá bán. Viết chương trình thực hiện:
    • Sử dụng một thuật toán được thiết kế theo chiến lược tham lam để cho biết cần bán ít nhất bao nhiêu chiếc quạt bàn trong danh sách d, gồm những chiếc quạt nào để được số tiền lớn hơn p.
    • Khai báo cấu trúc dữ liệu. Khởi tạo p (0 < p < 1200000), n và danh sách d (5 < n < 12). Hiển thị các kết quả, trong đó mỗi chiếc quạt cần hiển thị tên hãng sản xuất và giá bán.
#include <bits/stdc++.h>
using namespace std;

struct Quat{
    string ten, mau;
    int gia;

    void in(){ cout << ten << " " << mau << " " << gia << endl; }
};

struct DanhSach{
    vector<Quat> ds;
    int n, p;

    void ran(){
        vector<string> ten = {"hang1","hang2","hang3","hang4","hang5","hang6","hang7","hang8","hang9","hang10"};
        vector<string> mau = {"do","xanh","vang","den","trang","tim","hong","xam","nau","luc"};
        vector<int> gia = {10,20,50,100,200,500,700,900,1100,1200};

        random_device rd;
        mt19937 g(rd());
        shuffle(ten.begin(), ten.end(), g);
        shuffle(mau.begin(), mau.end(), g);
        shuffle(gia.begin(), gia.end(), g);

        for (int i=0; i<n; ++i) ds.push_back({ten[i], mau[i], gia[i]});
    }

    void khoi_tao(){
        do{
            cout << "p: "; cin >> p;
            cout << "n: "; cin >> n;
            if(!(0<p && p<1200000 && 5<n && n<12)) cout << "yeu cau nhap lai\n";
        }while(!(0<p && p<1200000 && 5<n && n<12));
        ran();
    }

    void sap_giam(){
        sort(ds.begin(), ds.end(), [](const Quat &a, const Quat &b){
            return a.gia > b.gia;
        });
    }

    void tham_lam(){
        int tong = 0;
        vector<Quat> chon;
        for (auto &q : ds){
            if (tong > p) break; // đủ tiền rồi, dừng
            chon.push_back(q);
            tong += q.gia;
        }

        if (tong <= p) {
            cout << "Không thể đạt số tiền lớn hơn p với danh sách hiện tại.\n";
            return;
        }

        cout << "Cần bán ít nhất " << chon.size() << " quạt để được số tiền " << tong << " > " << p << endl;
        for (auto &q : chon) q.in();
    }
};

int main(){
    DanhSach d;
    d.khoi_tao();
    cout << "\n--- Danh sách quạt ---\n";
    for (auto &x : d.ds) x.in();

    cout << "\n--- Kết quả tham lam ---\n";
    d.sap_giam();
    d.tham_lam();
    return 0;
}
Bỏ điện thoại vào túi sao cho giá trị lớn nhất
Cho một chiếc túi có kích thước s (inch) và một danh sách d gồm n chiếc điện thoại khác nhau, thông tin về mỗi điện thoại gồm nhãn hiệu, kích thước màn hình (inch) và giá bán. Viết chương trình thực hiện:
    • Khởi tạo n và danh sách d (5 ≤ n ≤ 10) . Bằng một thuật toán được thiết kế theo chiến lược tham lam hãy cho biết có thể lấy được bao nhiêu chiếc điện thoại bỏ vào túi để được tổng giá bán lớn nhất mà không vượt quá kích thước của túi, cho biết những chiếc điện thoại đã lấy (mỗi điện thoại hiển thị nhãn hiệu, giá bán).
#include <bits/stdc++.h>
using namespace std;

struct DT{
    string ten;
    int kt, gia;
    double ti_le;

    void in(){ cout << ten << " " << kt << " " << gia << " " << ti_le << endl; }
};

struct DS{
    vector<DT> ds;
    int n, s;

    void ran(){
        vector<string> ten = {"hang1", "hang2", "hang3", "hang4", "hang5", "hang6", "hang7", "hang8", "hang9", "hang10"};
        vector<int> kt = {6,4,7,5,1,8,3,2,9,10};
        vector<int> gia = {10,20,30,40,45,60,70,80,90,100};
        
        random_device rd;
        mt19937 g(rd());
        shuffle(ten.begin(), ten.end(), g);
        shuffle(kt.begin(), kt.end(), g);
        shuffle(gia.begin(), gia.end(), g);
        vector<double> ti_le;
        for(int i=0; i<kt.size(); ++i) ti_le.push_back((double)gia[i]/kt[i]);
        for(int i = 0; i < n; ++i) ds.push_back({ten[i], kt[i], gia[i], ti_le[i]});
    }

    void khoi_tao(){
        do{
            cout << "n: "; cin >> n;
            cout << "s: "; cin >> s;
            if(!(5 <= n && n <= 10)) cout << "loi\n";
        }while(!(5 <= n && n <= 10));
        ran();
    }

    void sap_giam(){
        sort(ds.begin(), ds.end(), [](const DT &a, const DT &b){
            return a.ti_le > b.ti_le;
        });
    }

    void tham_lam(){
        int tong_kt = 0, tong_gia = 0;
        vector<DT> chon;
        for(int i = 0; i<n; ++i){
            if(tong_kt+ds[i].kt <= s){
                chon.push_back(ds[i]);
                tong_kt += ds[i].kt;
                tong_gia += ds[i].gia;
            }
        }

        cout << "so dien thoai co the lay: " << chon.size() << endl;
        cout << "Tong kich thuoc su dung: " << tong_kt << " / " << s << " inch" << endl;
        cout << "Tong gia tri: " << tong_gia << endl;
        cout << "danh sach dien thoai duoc lay:\n";
        for(auto &a : chon) a.in();
    }
};

int main(){
    DS li;
    li.khoi_tao();
    li.sap_giam();
    li.tham_lam();
    return 0;
}
Boyer Moore Horspool
Cho một danh sách d gồm n xâu ký tự, mỗi xâu ký tự là một câu tiếng anh có chiều dài không quá 100 ký tự, các xâu ký tự đôi một khác nhau. Cài đặt chương trình thực hiện:
    • Khởi tạo số n và danh sách d (5 ≤ n ≤ 10). Sử dụng chiến lược tham lam thiết kế thuật toán tạo một xâu ký tự mới có chiều dài đúng bằng k từ các xâu ký tự trong danh sách d sao cho số xâu ký tự cần lấy trong danh sách d là ít nhất, hiển thị các xâu ký tự đã lấy trong danh sách d.
    • Ứng dụng thuật toán Boyer Moore Horspool cho biết từ “child” xuất hiện trong bao nhiêu xâu của danh sách d, gồm những xâu nào (in các xâu xuất hiện từ “child”)?
    • Ứng dụng thuật toán Z cho biết xâu d[0] là xâu con của những xâu nào trong danh sách d (không tính d[0]), in các xâu chứa xâu d[0] và số lần xuất hiện d[0] trong mỗi xâu đó.
#include <bits/stdc++.h>
using namespace std;

struct DS {
    vector<string> d;
    int n, k;

    // --- KHỞI TẠO ---
    void khoi_tao() {
        do {
            cout << "Nhap so xau n (5 ≤ n ≤ 10): ";
            cin >> n;
        } while(n < 5 || n > 10);
        cout << "Nhap do dai k: ";
        cin >> k;
        cin.ignore();
        d.resize(n);
        for (int i = 0; i < n; ++i) {
            cout << "Nhap xau thu " << i+1 << ": ";
            getline(cin, d[i]);
        }
    }

    // --- PHẦN 1: THAM LAM ---
    void tham_lam() {
        vector<pair<string,int>> v;
        for (auto &s : d) v.push_back({s, (int)s.size()});
        sort(v.begin(), v.end(), [](auto &a, auto &b){ return a.second > b.second; });

        vector<string> chon;
        int tong = 0;
        for (auto &x : v) {
            if (tong < k) {
                chon.push_back(x.first);
                tong += x.second;
            } else break;
        }

        cout << "\n==> Xau moi duoc tao co do dai >= " << k << " voi it xau nhat = " << chon.size() << endl;
        cout << "Cac xau duoc chon:\n";
        for (auto &x : chon) cout << "- " << x << " (" << x.size() << " ky tu)\n";
    }

    // --- PHẦN 2: BOYER–MOORE–HORSPOOL ---
    int BMH_search(const string &text, const string &pattern) {
        int n = text.size(), m = pattern.size();
        if (m > n) return 0;

        unordered_map<char,int> shift;
        for (int i = 0; i < m-1; ++i)
            shift[pattern[i]] = m - i - 1;

        int count = 0;
        int i = 0;
        while (i <= n - m) {
            int j = m - 1;
            while (j >= 0 && pattern[j] == text[i+j]) j--;
            if (j < 0) {
                count++;
                i += m;
            } else {
                i += shift.count(text[i+m-1]) ? shift[text[i+m-1]] : m;
            }
        }
        return count;
    }

    void tim_child_BMH() {
        string pattern = "child";
        int dem = 0;
        cout << "\n==> Tim tu '" << pattern << "' trong cac xau:\n";
        for (auto &x : d) {
            int kq = BMH_search(x, pattern);
            if (kq > 0) {
                cout << "- Xau: \"" << x << "\" (xuat hien " << kq << " lan)\n";
                dem++;
            }
        }
        cout << "=> Co tong cong " << dem << " xau chua tu '" << pattern << "'.\n";
    }

    // --- PHẦN 3: THUẬT TOÁN Z ---
    vector<int> Z_function(const string &s) {
        int n = s.size();
        vector<int> Z(n);
        int l = 0, r = 0;
        for (int i = 1; i < n; i++) {
            if (i <= r)
                Z[i] = min(r - i + 1, Z[i - l]);
            while (i + Z[i] < n && s[Z[i]] == s[i + Z[i]])
                Z[i]++;
            if (i + Z[i] - 1 > r)
                l = i, r = i + Z[i] - 1;
        }
        return Z;
    }

    void tim_xaucon_Z() {
        string pattern = d[0];
        cout << "\n==> Kiem tra xau d[0] la xau con cua nhung xau nao:\n";
        for (int i = 1; i < n; ++i) {
            string combined = pattern + "$" + d[i];
            vector<int> Z = Z_function(combined);
            int len = pattern.size();
            int count = 0;
            for (int z : Z) if (z == len) count++;
            if (count > 0)
                cout << "- " << d[i] << " (xuat hien " << count << " lan)\n";
        }
    }
};

int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);
    DS ds;
    ds.khoi_tao();
    ds.tham_lam();
    ds.tim_child_BMH();
    ds.tim_xaucon_Z();
}

#include <bits/stdc++.h>
using namespace std;

struct Q{
    string qua;
    int gia, khoi_luong;
    double ti_le;
    void in(){ cout << qua << " " << gia << " " << khoi_luong << " " << ti_le << endl; }
};

struct DS{
    vector<Q> ds;
    int n, w;

    void ran(){
        vector<string> qua = {"qua1", "qua2" ,"qua3","qua4","qua5"};
        vector<int> khoi_luong = {5, 1 ,3,7,2};
        vector<int> gia = {7,4,6,1,8};
        vector<double> ti_le;
        
        random_device rd;
        mt19937 g(rd());
        shuffle(qua.begin(), qua.end(), g);
        shuffle(gia.begin(), gia.end(), g);
        shuffle(khoi_luong.begin(), khoi_luong.end(), g);
        for(int i=0; i<gia.size();++i) ti_le.push_back((double)gia[i]/khoi_luong[i]);

        for(int i=0; i<n; ++i) ds.push_back({qua[i], gia[i], khoi_luong[i], ti_le[i]});
    }

    void khoi_tao(){
        do{
            cout << "n: "; cin >> n;
            cout << "w: "; cin >> w;
            if(!(0<= n && n <= 5)) cout << "yeu cau nhap lai\n";
        }while(!(0<= n && n <= 5));
        ran();
    }

    void sap_giam(){
        sort(ds.begin(), ds.end(), [](const Q &a, const Q &b){
            return a.ti_le > b.ti_le;
        });
    }

    void tham_lam(){
        vector<Q> chon;
        int tong = 0, kl = 0;

        for(int i=0; i<n;++i){
            if(kl+ds[i].khoi_luong <= w){
                chon.push_back(ds[i]);
                kl += ds[i].khoi_luong;
                tong += ds[i].gia;
            }
        }

        cout << "tong gia lon nhat: " << tong << endl;
        cout << "so phan qua chon duoc: " << chon.size() << endl;
        cout << "tong khoi luong cac phan qua: " << kl << endl;
        cout << "danh sach qua:\n";
        for(auto &a : chon) a.in();  
    }
};

int main(){
    DS ds;
    ds.khoi_tao();
    ds.sap_giam();
    ds.tham_lam();
    return 0;
}

Xếp lịch hỗi thảo
Chủ nhật tuần sau Nhà trường tổ chức n hội thảo về n chủ đề khác nhau, thông tin về mỗi hội thảo gồm: chủ đề (ví dụ: tìm kiếm việc làm, nâng cao kỹ năng mềm,...), thời gian bắt đầu, thời gian kết thúc. Thiết kế thuật toán cho biết một sinh viên có thể tham dự được nhiều nhất bao nhiêu hội thảo, gồm những hội thảo nào. Khởi tạo n, danh sách n hội thảo, sử dụng thuật toán trên để cho biết số lượng hội thảo và thông tin các hội thảo mà sinh viên có thể tham gia.
#include <bits/stdc++.h>
using namespace std;

struct HT{
    string ten;
    int bd, kt;
    void in(){ cout << ten << " " << bd << " " << kt << " " << endl; }
};

struct DS{
    vector<HT> ds;
    int n;

    void ran(){
        vector<string> ten = {"ten1", "ten2" ,"ten3","ten4","ten5"};
        vector<int> bd = {3,4,6,11,10};
        vector<int> kt = {5,6,9,12,14};

        for(int i=0; i<n; ++i) ds.push_back({ten[i], bd[i], kt[i]});
    }

    void khoi_tao(){
        do{
            cout << "n: "; cin >> n;
            if(!(0< n && n <= 5)) cout << "yeu cau nhap lai\n";
        }while(!(0< n && n <= 5));
        ran();
    }

    void sap_tang(){
        sort(ds.begin(), ds.end(), [](const HT &a, const HT &b){
            return a.kt < b.kt;
        });
    }

    void tham_lam(){
        vector<HT> chon;
        chon.push_back(ds[0]);
        int luu_kt = ds[0].kt; // lưu tg kết thúc

        for(int i=1; i<n;++i){
            if(ds[i].bd >= luu_kt){
                chon.push_back(ds[i]);
                luu_kt = ds[i].kt;
            }
        }

        cout << "so phan qua chon duoc: " << chon.size() << endl;
        cout << "danh sach qua:\n";
        for(auto &a : chon) a.in();  
    }
};

int main(){
    DS ds;
    ds.khoi_tao();
    ds.sap_tang();
    ds.tham_lam();
    return 0;
}
Dyanamic programming
Bài tập
Dùng số tiền p để mua nhiều quạt nhất
Cho một số tiền p và một danh sách d gồm n chiếc quạt bàn khác nhau về giá bán, thông tin về mỗi chiếc quạt bàn gồm: tên hãng sản xuất, màu sắc, giá bán. Viết chương trình thực hiện:
    • Sử dụng một thuật toán được thiết kế theo quy hoạch để cho biết nếu dùng số tiền p thì có thể mua được nhiều nhất bao nhiêu chiếc quạt bàn trong danh sách d,gồm những chiếc quạt nào.
    • Khai báo cấu trúc dữ liệu. Khởi tạo p (0 < p < 1200000), n và danh sách d (5 < n < 12). Hiển thị các kết quả, trong đó mỗi chiếc quạt cần hiển thị tên hãng sản xuất và giá bán.
#include <bits/stdc++.h>
using namespace std;

struct Quat{
    string ten, mau;
    int gia;

    void in(){ cout << ten << " " << mau << " " << gia << endl; }
};

struct DanhSach{
    vector<Quat> ds;
    int n, p;
    vector<vector<int>> dp;

    void ran(){
        vector<string> ten = {"hang1", "hang2", "hang3", "hang4", "hang5", "hang6", "hang7", "hang8", "hang9", "hang10"};
        vector<string> mau = {"mau1", "mau2", "mau3", "mau4", "mau5", "mau6", "mau7", "mau8", "mau9", "mau10"};
        vector<int> gia = {100, 200, 250, 270, 300, 350, 400, 500, 600, 700};

        random_device rd;
        mt19937 g(rd());
        shuffle(ten.begin(), ten.end(), g);
        shuffle(mau.begin(), mau.end(), g);
        shuffle(gia.begin(), gia.end(), g);

        for(int i = 0; i < n; ++i) ds.push_back({ten[i], mau[i], gia[i]});
    }

    void khoi_tao(){
        do{
            cout << "p: "; cin >> p; // so tien
            cout << "n: "; cin >> n; // so phan tu
            if(!(0 < p && p < 1200000 && 5 < n && n < 12)) cout << "loi\n";
        }while(!(0 < p && p < 1200000 && 5 < n && n < 12));
        ran();
    }

    void quy_hoach_dong(){
        dp.assign(n+1, vector<int>(p+1, 0));

        for(int i=1; i<=n; ++i){
            for(int j=1; j<=p; ++j){
                dp[i][j] = dp[i-1][j]; // khong lay i
                if(j >= ds[i-1].gia) dp[i][j] = max(dp[i][j], dp[i-1][j-ds[i-1].gia]+1); // lay i
            }
        }

        vector<Quat> chon;
        int i=n, j=p;
        while(i > 0 && j > 0){
            if(j >= ds[i-1].gia && dp[i][j] == dp[i-1][j-ds[i-1].gia]+1){
                chon.push_back(ds[i-1]);
                j -= ds[i-1].gia;
            }
            --i;
        }
        reverse(chon.begin(), chon.end());
        
        cout << "tong so quat duoc chon khi dung p tien: " << chon.size() << endl;
        cout << "danh sach quat duoc chon:\n";
        for(auto &a : chon) a.in();
    }
};

int main(){
    DanhSach li;
    li.khoi_tao();
    li.quy_hoach_dong();
    return 0;
}
#include <bits/stdc++.h>
using namespace std;

struct Quat{
    string tenH, mau;
    int gia;

    void in(){
        cout << tenH << " " << mau << " " << gia << endl;
    }
};

struct DanhSach{
    vector<Quat> ds;
    int n, p;
    vector<vector<int>> dp;
    
    void tao_random(){
        random_device rd;
        mt19937 g(rd());
        vector<string> ten = {"hang1","hang2","hang3","hang4","hang5","hang6","hang7","hang8","hang9","hang10"};
        vector<string> mau = {"do","xanh","vang","den","trang","tim","hong","xam","nau","luc"};
        vector<int> gia = {10,20,50,100,200,500,700,900,1100,1200};
        shuffle(ten.begin(), ten.end(), g);
        shuffle(mau.begin(), mau.end(), g);
        shuffle(gia.begin(), gia.end(), g);
        for (int i = 0; i < n; i++) ds.push_back({ten[i], mau[i], gia[i]});
    }

    void khoi_tao(){
        do{
            cout << "n: "; cin >> n;
            cout << "p: "; cin >> p;
            if (p <= 0 || p >= 1200000 || n <= 5 || n >= 12) cout << "lỗi, yêu cầu nhập lại";
        } while(p <= 0 || p >= 1200000 || n <= 5 || n >= 12);
        tao_random();
    }

    void in_ds(){
        for (auto &a : ds) a.in();
    }

    void quy_hoach_dong(){
        dp.assign(n+1, vector<int>(p+1, 0)); // dùng p tiền để mua được n chiếc quat 

        for(int i=1;i<=n;++i){
            for(int j=1; j<=p; ++j){
                if(ds[i-1].gia > j) dp[i][j] = dp[i-1][j];
                else dp[i][j] = max(dp[i-1][j], dp[i-1][j-ds[i-1].gia]+1);
            }
        }

        // truy vết
        vector<Quat> chon;
        int i = n, j = p;
        while(i>0 && j>0){
            if(dp[i][j]!=dp[i-1][j]){
                chon.push_back(ds[i-1]);
                j -= ds[i-1].gia;
            }
            --i;
        }
        reverse(chon.begin(), chon.end());

        cout << "so cai nhieu nhat mua duoc là: " << dp[n][p] << endl;
        for(auto &a : chon) a.in();
    }
};

int main(){
    DanhSach li;
    li.khoi_tao();
    li.in_ds();
    li.quy_hoach_dong();
    return 0;
}
Dùng đúng số tiền p để bán ít nhất quạt
Cho một số tiền p và một danh sách d gồm n chiếc quạt bàn khác nhau về giá bán, thông tin về mỗi chiếc quạt bàn gồm: tên hãng sản xuất, màu sắc, giá bán. Viết chương trình thực hiện:
    • Sử dụng một thuật toán được thiết kế theo chiến lược quy hoạch động để cho biết cần bán ít nhất bao nhiêu chiếc quạt bàn trong danh sách d, gồm những chiếc quạt nào để được số tiền “đúng bằng p”.
    • Khai báo cấu trúc dữ liệu. Khởi tạo p (0 < p < 1200000), n và danh sách d (5 < n < 12). Hiển thị các kết quả, trong đó mỗi chiếc quạt cần hiển thị tên hãng sản xuất và giá bán.
#include <bits/stdc++.h>
using namespace std;

struct Quat{
    string ten, mau;
    int gia;

    void in(){ cout << ten << " " << mau << " " << gia << endl; }
};

struct DanhSach{
    vector<Quat> ds;
    int n, p;
    vector<vector<int>> dp;

    void ran(){
        vector<string> ten = {"hang1", "hang2", "hang3", "hang4", "hang5", "hang6", "hang7", "hang8", "hang9", "hang10"};
        vector<string> mau = {"mau1", "mau2", "mau3", "mau4", "mau5", "mau6", "mau7", "mau8", "mau9", "mau10"};
        vector<int> gia = {100, 200, 250, 270, 300, 350, 400, 500, 600, 700};

        random_device rd;
        mt19937 g(rd());
        shuffle(ten.begin(), ten.end(), g);
        shuffle(mau.begin(), mau.end(), g);
        shuffle(gia.begin(), gia.end(), g);

        for(int i = 0; i < n; ++i) ds.push_back({ten[i], mau[i], gia[i]});
    }

    void khoi_tao(){
        do{
            cout << "p: "; cin >> p; // so tien
            cout << "n: "; cin >> n; // so phan tu
            if(!(0 < p && p < 1200000 && 5 < n && n < 12)) cout << "loi\n";
        }while(!(0 < p && p < 1200000 && 5 < n && n < 12));
        ran();
    }

    void sap_giam(){
        sort(ds.begin(), ds.end(), [](const Quat &a, const Quat &b){
            return a.gia > b.gia;
        });
    }

    void quy_hoach_dong(){
        const int INF = 1e9;
        dp.assign(n+1, vector<int>(p+1, INF));
        dp[0][0] = 0;

        for(int i = 1; i<=n; ++i){
            for(int j=0; j <= p; ++j){
                dp[i][j] = dp[i-1][j];
                if(j >= ds[i-1].gia) dp[i][j] = min(dp[i][j], dp[i-1][j-ds[i-1].gia]+1);
            }
        }

        if(dp[n][p] == INF){
            cout << "khong the ban duoc hang tong dung ban p" << endl; 
            return;
        }

        vector<Quat> chon;
        int i=n, j=p;
        while(i>0 && j>0){
            if(j>= ds[i-1].gia && dp[i][j] == dp[i-1][j-ds[i-1].gia]+1){
                chon.push_back(ds[i-1]);
                j -= ds[i-1].gia;
            }
            --i;
        }

        cout << "tong so quat duoc chon khi dung p tien: " << chon.size() << endl;
        cout << "danh sach quat duoc chon:\n";
        for(auto &a : chon) a.in();      
    }
};

int main(){
    DanhSach li;
    li.khoi_tao();
    li.quy_hoach_dong();
    return 0;
}
Dùng tiền nhiều hơn p để bán ít nhất quạt
Cho một số tiền p và một danh sách d gồm n chiếc quạt bàn khác nhau về giá bán,thông tin về mỗi chiếc quạt bàn gồm: tên hãng sản xuất, màu sắc, giá bán. Viết chương trình thực hiện:
    • Sử dụng một thuật toán được thiết kế theo chiến lược quy hoạch động để cho biết cần bán ít nhất bao nhiêu chiếc quạt bàn trong danh sách d, gồm những chiếc quạt nào để được số tiền lớn hơn p.
    • Khai báo cấu trúc dữ liệu. Khởi tạo p (0 < p < 1200000), n và danh sách d (5 < n < 12). Hiển thị các kết quả, trong đó mỗi chiếc quạt cần hiển thị tên hãng sản xuất và giá bán.
#include <bits/stdc++.h>
using namespace std;

struct Quat{
    string ten, mau;
    int gia;

    void in(){ cout << ten << " " << mau << " " << gia << endl; }
};

struct DanhSach{
    vector<Quat> ds;
    int n, p;
    vector<vector<int>> dp;

    void ran(){
        vector<string> ten = {"hang1", "hang2", "hang3", "hang4", "hang5", "hang6", "hang7", "hang8", "hang9", "hang10"};
        vector<string> mau = {"mau1", "mau2", "mau3", "mau4", "mau5", "mau6", "mau7", "mau8", "mau9", "mau10"};
        vector<int> gia = {100, 200, 250, 270, 300, 350, 400, 500, 600, 700};

        random_device rd;
        mt19937 g(rd());
        shuffle(ten.begin(), ten.end(), g);
        shuffle(mau.begin(), mau.end(), g);
        shuffle(gia.begin(), gia.end(), g);

        for(int i = 0; i < n; ++i) ds.push_back({ten[i], mau[i], gia[i]});
    }

    void khoi_tao(){
        do{
            cout << "p: "; cin >> p; // so tien
            cout << "n: "; cin >> n; // so phan tu
            if(!(0 < p && p < 1200000 && 5 < n && n < 12)) cout << "loi\n";
        }while(!(0 < p && p < 1200000 && 5 < n && n < 12));
        ran();
    }

    void quy_hoach_dong(){
        const int INF = 1e9;

        int tong = 0;
        for(auto &a : ds) tong += a.gia;

        dp.assign(n+1, vector<int>(tong+1, INF));
        dp[0][0] = 0;

        for(int i=1; i<=n; ++i){
            for(int j=0; j<=tong; ++j){
                dp[i][j] = dp[i-1][j];
                if(j >= ds[i-1].gia) dp[i][j] = min(dp[i][j], dp[i-1][j-ds[i-1].gia]+1);
            }
        }

        int tong_nho_nhat = -1;
        for(int j = p+1; j <= tong; ++j){
            if (dp[n][j] != INF){
                tong_nho_nhat = j;
                break;
            }
        }

        if(tong_nho_nhat == -1) {
            cout << "khong the chon duoc quat co tong > p" << endl;
            return;
        }

        vector<Quat> chon;
        int i=n, j=tong_nho_nhat;
        while(i>0 && j>0){
            if(j >= ds[i-1].gia && dp[i][j] == dp[i-1][j-ds[i-1].gia]+1){
                chon.push_back(ds[i-1]);
                j -= ds[i-1].gia;
            }
            --i;
        }
        reverse(chon.begin(), chon.end());

        cout << "tong so quat duoc chon khi dung p tien: " << chon.size() << endl;
        cout << "danh sach quat duoc chon:\n";
        for(auto &a : chon) a.in();      
    }
};

int main(){
    DanhSach li;
    li.khoi_tao();
    li.quy_hoach_dong();
    return 0;
}
Bỏ điện thoại vào túi sao cho giá trị lớn nhất
Cho một chiếc túi có kích thước s (inch) và một danh sách d gồm n chiếc điện thoại
khác nhau, thông tin về mỗi điện thoại gồm nhãn hiệu, kích thước màn hình (inch) và giá bán.
Viết chương trình thực hiện:
- Khởi tạo n và danh sách d (5 ≤ n ≤ 10) .
- Bằng một thuật toán được thiết kế theo chiến lược quy hoạch động hãy cho biết có thể
lấy được bao nhiêu chiếc điện thoại bỏ vào túi để được tổng giá bán lớn nhất mà không
vượt quá kích thước của túi, cho biết những chiếc điện thoại đã lấy (mỗi điện thoại
hiển thị nhãn hiệu, giá bán).
Ví dụ: dp[i][j]: giá bán lớn nhất có thể đạt được khi xét đến i cái điện thoại đầu tiên, với túi có kích thước tối đa là j

0 (j)
1
2
3
…
s
0
0
0
0
0
0
0
1
0
TH1: w[i] > j (nghĩa là điện thoại thứ I không thể bỏ vào túi vì nó quá to)
    • dp[i][j] = dp[i-1][j] (Ta bỏ qua điện thoại i, chỉ dùng kết quả của i-1 điện thoại trước)
TH2: w[i] <= j (nghĩa là điện thoại thứ I có thể bỏ vào túi được khi đó ta có 2 lựa chọn) 
    • Không lấy điện thoại i → giá trị là dp[i-1][j]
    • Lấy điện thoại i → giá trị là dp[i-1][j - w[i]] + v[i] (vì ta lấy điện thoại i, nên dung lượng túi còn lại là j - w[i], và cộng thêm giá trị v[i] của điện thoại này) -> dp[i][j] = max(dp[i-1][j], dp[i-1][j - w[i]] + v[i])
2
0

…
0

n
0


#include <bits/stdc++.h>
using namespace std;

struct DT{
    string ten;
    int kt, gia;
    double ti_le;

    void in(){ cout << ten << " " << kt << " " << gia << " " << ti_le << endl; }
};

struct DS{
    vector<DT> ds;
    int n, s;
    vector<vector<int>> dp;

    void ran(){
        vector<string> ten = {"hang1", "hang2", "hang3", "hang4", "hang5", "hang6", "hang7", "hang8", "hang9", "hang10"};
        vector<int> kt = {6,4,7,5,1,8,3,2,9,10};
        vector<int> gia = {10,20,30,40,45,60,70,80,90,100};
        
        random_device rd;
        mt19937 g(rd());
        shuffle(ten.begin(), ten.end(), g);
        shuffle(kt.begin(), kt.end(), g);
        shuffle(gia.begin(), gia.end(), g);
        vector<double> ti_le;
        for(int i=0; i<kt.size(); ++i) ti_le.push_back((double)gia[i]/kt[i]);
        for(int i = 0; i < n; ++i) ds.push_back({ten[i], kt[i], gia[i], ti_le[i]});
    }

    void khoi_tao(){
        do{
            cout << "n: "; cin >> n;
            cout << "s: "; cin >> s;
            if(!(5 <= n && n <= 10)) cout << "loi\n";
        }while(!(5 <= n && n <= 10));
        ran();
    }

    void quy_hoach_dong(){
        dp.assign(n+1, vector<int>(s+1, 0));

        for(int i = 1; i <= n; ++i){
            for(int j = 1; j <= s; ++j){
                dp[i][j] = dp[i-1][j];
                if(j >= ds[i-1].kt) dp[i][j] = max(dp[i][j], dp[i-1][j-ds[i-1].kt]+ds[i-1].gia);
            }
        }

        vector<DT> chon;
        int i=n, j=s;
        int tong_kt = 0, tong_gia = 0; 
        while(i > 0 && j > 0){
            if(j >= ds[i-1].kt && dp[i][j] == dp[i-1][j-ds[i-1].kt]+ds[i-1].gia){
                chon.push_back(ds[i-1]);
                tong_kt += ds[i-1].kt;
                tong_gia += ds[i-1].gia;
                j -= ds[i-1].kt;
            }
            --i;
        } 
        reverse(chon.begin(), chon.end());

        cout << "so dien thoai co the lay: " << chon.size() << endl;
        cout << "Tong kich thuoc su dung: " << tong_kt << " / " << s << " inch" << endl;
        cout << "Tong gia tri: " << tong_gia << endl;
        cout << "danh sach dien thoai duoc lay:\n";
        for(auto &a : chon) a.in();
    }
};

int main(){
    DS li;
    li.khoi_tao();
    li.quy_hoach_dong();
    return 0;
}
Tìm dãy con có chiều dài lớn nhất
Định nghĩa c là một dãy con của dãy a nếu xóa đi một số phần tử trong a ta được c. Cho 2 dãy số a và b chứa các số nguyên có chiều dài lần lượt là n và m. Viết chương trình thực hiện:
    • Sử dụng chiến lược quy hoạch động thiết kế một thuật toán tìm dãy c là dãy con của cả dãy a và dãy b sao cho dãy c có chiều dài lớn nhất.
    • Khởi tạo n, m, a, b. Tìm c và hiển thị kết quả.
#include <bits/stdc++.h>
using namespace std;

struct DC{
    string a,b;
    int n, m;
    vector<vector<int>> dp;

    void khoi_tao(){
        cout << "a: "; cin >> a;
        cout << "b: "; cin >> b;
        n = a.length();
        m = b.length();
    }

    void quy_hoach_dong(){
        dp.assign(n+1, vector<int>(m+1, 0));

        for(int i=1; i<=n; ++i){
            for(int j=1; j<=m; ++j){
                if(a[i-1] == b[j-1]) dp[i][j] = dp[i-1][j-1]+1;
                else dp[i][j] = max(dp[i-1][j], dp[i][j-1]);
            }
        }

        string chon;
        int i=n, j=m;
        while(i>0 && j>0){
            if(a[i-1] == b[j-1]){
                chon += a[i-1];
                --i; --j;
            }
            else if(dp[i-1][j] > dp[i][j-1]) --i;
            else --j;
        }
        reverse(chon.begin(), chon.end());
        cout << "do dai xau con chung: " << dp[n][m] << endl;
        cout << "xau con chung: \n";
        for(auto &a : chon) cout << a;
    }
};

int main(){
    DC dc;
    dc.khoi_tao();
    dc.quy_hoach_dong();
    return 0;
}
Boyer Moore Horspool
#include <bits/stdc++.h>
using namespace std;

struct BoyerMooreHorspool{
    int n;
    vector<double> a;
    double C;
    string P, Q;

    void config(){
        n = 5;
        a = {1,2,3,4,5};
        C = 10;
        P = "le duc thang";
        Q = "duc";
    }

    void D(){
        double M = 0;
        int D = 0;
        vector<double> take;

        for(int i = 0; i < n; ++i){
            if (M+a[i] <= C){
                M += a[i];
                D++;
                take.push_back(a[i]);
            }
        }
        cout << "D = " << D << endl;
        cout << "M = " << M << endl;
        if(D > 0){
            cout << "các phần tử đã lấy: \n";
            for(double x : take) cout << x << " ";
            cout << endl;
        }
    }

    // tạo shift table xho bmh
    vector<int> build_shift(const string &pattern){
        int m = pattern.size();
        vector<int> shift(256, m);

        for(int i = 0; i < m-1; ++i){
            shift[(unsigned char)pattern[i]] = m-1-i;
        }
        return shift;
    }

    bool BMH(){
        int n = P.size();
        int m = Q.size();

        if(m>n) return false;

        vector<int> shift = build_shift(Q);

        int i = m-1;
        while(i<n){
            int k = 0;
            while(k < m && Q[m-1-k] == P[i-k]) k++;

            if(k==m) return true;
            i+= shift[(unsigned char)P[i]];
        }
        return false;
    }

    void run(){
        config();
        cout << "=== Ket qua tham lam ===\n";
        D();

        cout << "\n=== Boyer Moore Horspool ===\n";
        if(BMH()) 
            cout << "Q la chuoi con cua P\n";
        else
            cout << "Q KHONG phai chuoi con cua P\n";
    }

};

int main(){
    // BoyerMooreHorspool bt;
    // bt.run();

    vector<int> a(256, 4);
    string t = "abc";
    a[t[0]] = 5;
    for(int i = 0; i < a.size(); i++){
        cout << i << " " << a[i] << endl;
    }
    
    return 0;
}

Bài toán fibonaci
Bằng hàm bình thường
Tìm phần tử thứ n trong dãy fibonaci
int fibonaci(int n){// n = 0,1,2,...
    int c = 0;
    if(n<0) return c;   
    else if(n==0 || n==1) return c+1;
    else{
        for(int i = 2; i <= n; i++){
            int a = 1,b = 1;
            int c = a + b;
            a = b;
            b = c;
        }
        return c;
    }
}

Tính tổng giá trị từ đầu đến phần tử thứ n trong dãy fibonaci
int sumFibonaci(int n){
    int sum = 0;
    for(int i = 0; i <= n; i++){
        sum += fibonaci(i);
    }
    return sum;
}

Code tối ưu:
int sumFibonaci(int n){
    if(n<0) return 0;
    int a = 1, b = 1, sum = 2; // F(0) = 1, F(1) = 1
    for(int i = 2; i <= n; i++){
        int c = a + b; // F(2)
        sum += c;
        a = b;
        b = c;
    }
    return sum;
}


Tìm uớc chung lớn nhất
Theo Euclid đệ quy
Output = 18
int UCLN(int a, int b) {
	if (b == 0) return a;
	else return UCLN(b, a % b);
}
cout << UCLN(252, 198);
Theo Euclid
Output = 18
int UCLN(int a, int b) {
	if (b == 0) return a;
	while (b != 0) {
		int temp = a % b;
		a = b;
		b = temp;
	}
	return a;
}
cout << UCLN(252, 198);
Cho số nguyên a = 814 và b = 187. Tìm UCLN của a và b, các số nguyên x, y sao so ax+by = d
Cho số nguyên a = 252 và b = 198. Tìm UCLN của a và b, các số nguyên x, y sao cho ax + by = d
Thuật toán kiểm tra số nguyên tố
#include <iostream>
#include <math.h>
using namespace std;
int main() {
	int n, count = 0;
	cin >> n;
	for (int i = 2; i <= sqrt(n); i++) {
		if (n % i == 0) {
			cout << "false";
			count += 1;
			break;
		}
	}
	if (count == 0) cout << "True";
	return 0;
}
Input: 12
Output: false
Thuật toán tìm giá trị của vị trí thứ n trong dãy fibonacci
Cách làm:
Muốn tìm f(n) thì phải tìm được f(n-1) và f(n-2) vì tổng 2 số liền trước sẽ bằng số sau.
f(n) = f(n-1) + f(n-2)
…
f(4) = f(3) + f(2)
f(3) = f(2) + f(1)
f(2) = f(1) + f(0)
f(1) = 1
f(0) = 0
Giải bình thường
Output = 34
long fibo(int n) {
	if (n == 0) return 0;
	else if (n == 1) return 1;
	else if (n == 2) return 1;
	else {
		int result = 0; // gắn đại giá trị là 0
		int r = 0;
		int l = 1;
		for (int i = 2; i <= n; i++) {
			result = r + l;
			r = l;
			l = result;
		}
		return result ;
	}
}
int main() {
	cout << fibo(9);
	return 0;
}
Giải bằng đệ quy
Output = 34
long fibo(int n) {
	if (n <= 2) return 1;
	else return fibo(n - 1) + fibo(n - 2);
}
int main() {
	cout << fibo(9);
	return 0;
}
Thuật toán tìm Max
Bằng cách chia để trị đệ quy 
int searchMax(int li[], int left, int right) {
	if (left == right) return li[left];
	else {
		int mid = (left + right) / 2;
		int max_left = searchMax(li, left, mid);
		int max_right = searchMax(li, mid+1, right);
		if (max_left < max_right) return max_right;
		else return max_left;
	}
}
int arr[] = { 2,1,4,3,2,5,1,8,7,6 };
int l = 0;
int r = sizeof(arr) / sizeof(arr[0]);
cout << searchMax(arr, l, r);
Thuật toán đếm số lượng chữ số
Bằng đệ quy
int Count(int n, int dem) {
	n = n / 10;
	if (n == 0) return dem+1;
	else {
		return Count(n, dem+1);
	}
}
cout << Count(1234567, 0);v
Giải bằng vòng lặp
int Count(int n) {
    int dem = 0;
    while(n/10 != 0){
        n /= 10;
        dem += 1;
    }
    return dem+1;
}
cout << Count(12345);
    return 0;

5
Thuật toán tìm từ khi các từ được sắp xếp trong từ điển
void SearchDict(char  li[], char key) {
    int length = 10;
    int l = 0, r = 9;    
    while(l <= r){
        int mid = (l+r)/2;
        if(int(li[mid]) == int(key)) {
            cout << "tìm thấy " << key << " trong mảng" << endl;
            return ;
        }
        else if(int(li[mid]) < int(key)) l = mid + 1;
        else if(int(li[mid]) > int(key)) r = mid - 1;
    }
    cout << "không tìm thấy" << endl;
}
int main(){
    char li[10] = {'a', 'c', 'd', 'e', 'g', 'h', 'i', 'k', 'm', 'n'};
    // kiểm tra xem các từ đã được sắp xếp tăng dần hay chưa
    for(int i = 0; i < 10; i++){
        int n = int(li[i]);
        cout << n << " ";
    }
    cout << endl;
    SearchDict(li, 'f');
    return 0;
}

97 99 100 101 103 104 105 107 109 110 
không tìm thấy
Thuật toán tính tổng bằng chia để trị
int Sum_Array(int arr[], int left, int right){
    if(left==right){
        return arr[left];
    } 
    int mid = (left + right)/2;
    int l = Sum_Array(arr, left, mid);
    int r = Sum_Array(arr, mid+1, right);
    return l + r;
}
int main(){
    int li[] = {4,5,3,2,1};
    cout << Sum_Array(li, 0, 4);
    return 0;
}

15

Thuật toán đảo ngược chuỗi
Bằng hàm bình thường
Output: gninrom doog
string reverse(string t) {
	string result = "";
	for (int i = 0; i < t.length(); i++) {
		result = t[i] + result;
	}
	return result;
}
string greet = "good morning";
cout << reverse(greet);
Bằng đệ quy
Output: gninrom doog
string reverse(string t) {
	if (t.length() <= 1) return t;
	else return t[t.length() - 1] + reverse(t.substr(0, t.length()-1));
}
string greet = "good morning";
cout << reverse(greet);
Thuật toán sắp xếp tăng bằng chia để trị
#include <iostream>
using namespace std;

void heaptify(int arr[], int length, int i){
    int largest = i;
    int l = 2*i + 1;
    int r = 2*i + 2;
    if(arr[largest] < arr[l] && l < length) largest = l;
    if(arr[largest] < arr[r] && r < length) largest = r;
    if(largest != i){
        int temp = arr[largest];
        arr[largest] = arr[i];
        arr[i] = temp;
        heaptify(arr,length,largest);
    }
}

void heap_sort(int arr[], int length){ // int *arr
    for(int i = length*1.0/2-1; i > -1; i--){
        heaptify(arr,length,i);
    }
    for(int i = length-1; i > 0; i--){
        int temp = arr[0];
        arr[0] = arr[i];
        arr[i] = temp;
        heaptify(arr, i, 0);
    }
}
int main(){
    int a[] = {9,3,5,4,1,2,7,8};
    int length = sizeof(a)/sizeof(a[0]);
    heap_sort(a,length);
    for(int i = 0; i < length; i++){
        cout << a[i] << " ";
    }
    return 0;
}

1 2 3 4 5 7 8 9
Quản lý danh sách sinh viên bằng struct
#include <iostream>
using namespace std;

void view_config(int x[], int k){
	for(int i=1; i<=k; i+=1){
		cout << x[i];
	}
	cout << endl;
}

void next_config(int x[], int k, int i){
	x[i] += 1;
	i +=1;
	while(i<=k){
		x[i] = x[i-1]+1;
		i +=1;
	}
}

void listing_configs(int k, int n){
	int i,  x[k+1] = {0};
	
	// tao cau hinh dau tien
	for(int i = 1; i <= k; i+=1){
		x[i] = i;
	}
	
	do{
		view_config(x, k); 				// in mot cau hinh ra
		
		i = k;
		while (i>0 && x[i] == n-k+i){
			i -=1;
		}
		if(i>0){
			next_config(x, k, i);
		}
	} while (i>0);
}


void backtrack(int n, int k, int start, int current_set[], int index) {
    // Nếu tập con đã đủ k phần tử, in ra và quay lại
    if (index == k) {
        for (int i = 0; i < k; i++) {
            cout << current_set[i] << " ";
        }
        cout << endl;
        return;
    }

    // Thử các phần tử từ start đến n
    for (int i = start; i <= n; i++) {
        current_set[index] = i;  // Thêm phần tử i vào tập con
        backtrack(n, k, i + 1, current_set, index + 1);  // Tiếp tục tìm kiếm
    }
}

int main(){
//	listing_configs(3,5);

	int n = 5; // Tập hợp từ 1 đến n
    int k = 3; // Độ dài tập con cần tìm
    int current_set[k];  // Mảng để chứa tập con hiện tại
    
    backtrack(n, k, 1, current_set, 0); // Bắt đầu backtracking từ 1
	return 0;
}
#include <iostream>
using namespace std;

void next_config(int x[], int n, int i){ 
	x[i] = 1;
	i++;
	while(i<n){
		x[i] = 0;
		i+=1;
	}
}

void view_config(int x[], int n){
	for (int i=0; i<n; i+=1){
		cout << x[i];
	}
	cout << endl;
}

void listing_configs(int n){
	int i;
	int x[n] = {0}; 
	do {
		view_config(x, n);
		i = n-1;
		while (i>=0 && x[i] == 1){
			i -=1;
		}
		if(i>=0){
			next_config(x, n, i);
		}
	} while(i>=0);
}

void backtracking(int n, string &current){
	
	if (current.length() == n){
		cout << current << endl;
		return;
	}
	string current0 = current+"0";
	string current1 = current+"1";

	backtracking(n, current0);	
	backtracking(n, current1);
}

int main(){
//	int n; cout << "Nhap n: "; cin >> n;	
//	listing_configs(n);
	
	string current = "";
	backtracking(3, current);
	return 0;
}
