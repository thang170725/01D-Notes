- [C Sharp Introduction](#c-sharp-introduction)
- [Console.WriteLine()](#consolewriteline)
- [Data type (kiểu dữ liệu)](#data-type-kiểu-dữ-liệu)
  - [int (số nguyên)](#int-số-nguyên)
  - [double (số thực)](#double-số-thực)
  - [float (số thực)](#float-số-thực)
  - [decimal](#decimal)
  - [bool](#bool)
  - [char (Một ký tự)](#char-một-ký-tự)
  - [string (Chuỗi)](#string-chuỗi)
    - [$ (String interpolation)](#-string-interpolation)
    - [.Trim() (Loại bỏ khoảng trắng ở đầu và cuối chuỗi)](#trim-loại-bỏ-khoảng-trắng-ở-đầu-và-cuối-chuỗi)
  - [var](#var)
    - [ToString() (Chuyển một giá trị hoặc đối tượng thành kiểu chuỗi string)](#tostring-chuyển-một-giá-trị-hoặc-đối-tượng-thành-kiểu-chuỗi-string)
    - [string.IsNullOrEmpty() (Kiểm tra chuỗi có bị null hoặc rỗng hay không)](#stringisnullorempty-kiểm-tra-chuỗi-có-bị-null-hoặc-rỗng-hay-không)
    - [string.IsNullOrWhiteSpace() (Kiểm tra chuỗi có phải null, rỗng hoặc chỉ chứa khoảng trắng hay không)](#stringisnullorwhitespace-kiểm-tra-chuỗi-có-phải-null-rỗng-hoặc-chỉ-chứa-khoảng-trắng-hay-không)
  - [List](#list)
  - [Add()](#add)
    - [Count](#count)
    - [Remove](#remove)
  - [Dictionary](#dictionary)
    - [\[\] (thêm phân tử)](#-thêm-phân-tử)
  - [null](#null)
- [Operator (Toán tử)](#operator-toán-tử)
  - [+ (cộng)](#-cộng)
  - [- (trừ)](#--trừ)
  - [\* (nhân)](#-nhân)
  - [/ (chia)](#-chia)
  - [% (chia lấy dư)](#-chia-lấy-dư)
  - [== (so sánh bằng)](#-so-sánh-bằng)
  - [!= (so sánh khác)](#-so-sánh-khác)
  - [\> (so sánh lớn hơn)](#-so-sánh-lớn-hơn)
  - [\< (so sánh nhỏ hơn)](#-so-sánh-nhỏ-hơn)
  - [\>= (so sánh lớn hơn hoặc bằng)](#-so-sánh-lớn-hơn-hoặc-bằng)
  - [\<= (so sánh nhỏ hơn hoặc bằng)](#-so-sánh-nhỏ-hơn-hoặc-bằng)
  - [\&\&](#)
  - [||](#-1)
  - [!](#-2)
- [Conditional (câu điều kiện)](#conditional-câu-điều-kiện)
  - [if ... else if ... else](#if--else-if--else)
  - [switch ... case (Chọn một nhánh xử lý dựa trên giá trị của một biến)](#switch--case-chọn-một-nhánh-xử-lý-dựa-trên-giá-trị-của-một-biến)
- [Loop (vòng lặp)](#loop-vòng-lặp)
  - [for (lặp lại một đoạn code với số lần xác đinh trước)](#for-lặp-lại-một-đoạn-code-với-số-lần-xác-đinh-trước)
  - [while](#while)
  - [foreach (Duyệt lần lượt từng phần tử trong một tập hợp mà không cần tự quản lý biến chỉ số)](#foreach-duyệt-lần-lượt-từng-phần-tử-trong-một-tập-hợp-mà-không-cần-tự-quản-lý-biến-chỉ-số)
  - [While (Lặp lại code khi điều kiện còn đúng Thường dùng khi chưa biết chính xác cần lặp bao nhiêu lần)](#while-lặp-lại-code-khi-điều-kiện-còn-đúng-thường-dùng-khi-chưa-biết-chính-xác-cần-lặp-bao-nhiêu-lần)
- [Function](#function)
  - [int](#int)
  - [void](#void)
- [Class](#class)
  - [Constructor](#constructor)
- [Exception](#exception)
  - [finally](#finally)
- [Array](#array)
- [C# WinForms](#c-winforms)
  - [MessageBox (thông báo bằng hộp thoại)](#messagebox-thông-báo-bằng-hộp-thoại)
    - [Show()](#show)
  - [.Text (lấy dữ liệu từ TextBox)](#text-lấy-dữ-liệu-từ-textbox)
  - [.Clear() (Xóa toàn bộ nội dung bên trong TextBox)](#clear-xóa-toàn-bộ-nội-dung-bên-trong-textbox)
  - [MessageBoxButtons](#messageboxbuttons)
    - [.OK (Chỉ có nút OK)](#ok-chỉ-có-nút-ok)
    - [YesNo (Có Yes và No)](#yesno-có-yes-và-no)
    - [YesNoCancel (Có Yes, No và Cancel)](#yesnocancel-có-yes-no-và-cancel)
    - [Information (Biểu tượng thông tin)](#information-biểu-tượng-thông-tin)
    - [Warning (Biểu tượng cảnh báo)](#warning-biểu-tượng-cảnh-báo)
    - [Error (Biểu tượng lỗi)](#error-biểu-tượng-lỗi)
    - [Question (Biểu tượng câu hỏi)](#question-biểu-tượng-câu-hỏi)
  - [DialogResult (Lưu kết quả mà người dùng chọn trong hộp thoại MessageBox)](#dialogresult-lưu-kết-quả-mà-người-dùng-chọn-trong-hộp-thoại-messagebox)
  - [.Rows (Truy cập danh sách các dòng trong DataGridView)](#rows-truy-cập-danh-sách-các-dòng-trong-datagridview)
    - [.Cells() (Lấy dữ liệu của một ô cụ thể)](#cells-lấy-dữ-liệu-của-một-ô-cụ-thể)
      - [.Value (Lấy hoặc gán nội dung cho một ô trong DataGridView)](#value-lấy-hoặc-gán-nội-dung-cho-một-ô-trong-datagridview)
    - [.Add() (Thêm dữ liệu mới vào DataGridView)](#add-thêm-dữ-liệu-mới-vào-datagridview)
    - [RemoveAt() (Xóa dòng dựa vào chỉ số dòng)](#removeat-xóa-dòng-dựa-vào-chỉ-số-dòng)
  - [DataGridViewCellEventArgs](#datagridviewcelleventargs)
    - [RowIndex (Xác định người dùng vừa click vào dòng nào)](#rowindex-xác-định-người-dùng-vừa-click-vào-dòng-nào)
    - [SelectedRows (Lấy dòng đang được chọn)](#selectedrows-lấy-dòng-đang-được-chọn)
- [System](#system)
  - [Xml](#xml)
    - [XmlDocument (đại diện cho toàn bộ tài liệu XML)](#xmldocument-đại-diện-cho-toàn-bộ-tài-liệu-xml)
      - [Load()	(Đọc XML từ file)](#loadđọc-xml-từ-file)
      - [Save()	(Lưu XML xuống file)](#savelưu-xml-xuống-file)
      - [CreateElement() (Tạo phần tử XML)](#createelement-tạo-phần-tử-xml)
        - [InnerText (Lấy hoặc gán nội dung văn bản)](#innertext-lấy-hoặc-gán-nội-dung-văn-bản)
        - [InnerXml (Lấy hoặc gán nội dung XML bên trong)](#innerxml-lấy-hoặc-gán-nội-dung-xml-bên-trong)
        - [Attributes (Truy cập các thuộc tính của phần tử)](#attributes-truy-cập-các-thuộc-tính-của-phần-tử)
        - [Name (Lấy tên phần tử)](#name-lấy-tên-phần-tử)
      - [CreateAttribute() (Tạo thuộc tính XML)](#createattribute-tạo-thuộc-tính-xml)
      - [DocumentElement() (Lấy phần tử gốc)](#documentelement-lấy-phần-tử-gốc)
      - [XmlElement (Đại diện cho một phần tử XML)](#xmlelement-đại-diện-cho-một-phần-tử-xml)
      - [XmlAttribute (Tạo và quản lý thuộc tính của phần tử XML)](#xmlattribute-tạo-và-quản-lý-thuộc-tính-của-phần-tử-xml)
    - [XmlNode (Đại diện cho một nút trong tài liệu XML)](#xmlnode-đại-diện-cho-một-nút-trong-tài-liệu-xml)
      - [AppendChild() (Thêm nút con)](#appendchild-thêm-nút-con)
      - [RemoveChild() (Xóa nút con)](#removechild-xóa-nút-con)
      - [ReplaceChild() (Thay nút cũ bằng nút mới)](#replacechild-thay-nút-cũ-bằng-nút-mới)
      - [SelectSingleNode() (Tìm một nút theo XPath)](#selectsinglenode-tìm-một-nút-theo-xpath)
      - [SelectNodes() (Tìm nhiều nút theo XPath)](#selectnodes-tìm-nhiều-nút-theo-xpath)
---
# C Sharp Introduction
**Ứng dụng**
```bash
- Backend
- Web API
- desktop
- game 
- enterprise/Microsoft ecosystem
```
# Console.WriteLine()
**Ex**
```csharp
Console.WriteLine("Hello World"); // Hello World
```
# Data type (kiểu dữ liệu)
## int (số nguyên)
```csharp
int age = 20;
```
## double (số thực)
**Ex**
```csharp
double price = 10.5;

Console.WriteLine(price); // 10.5
```
## float (số thực)
**Ex**
```csharp
float x = 10.5f; // Chú ý chữ f. Nếu không có f, C# mặc định số thập phân là double.
```
## decimal
```bash
Thường dùng khi xử lý tiền:
```
**Ex**
```csharp
decimal money = 100000.5m; // Có m ở cuối.
Console.WriteLine(money);
```
## bool
**Ex**
```csharp
bool active = true;

Console.WriteLine(active); // True
```
## char (Một ký tự)
**Ex**
```csharp
char grade = 'A';
// 'A'    → char
// "A"    → string
```
## string (Chuỗi)
```csharp
string name = "Thang";

Console.WriteLine(name); // Thang
```
### $ (String interpolation)
```csharp
string name = "Thang";
int age = 20;

Console.WriteLine($"Name: {name}, Age: {age}"); // Name: Thang, Age: 20
```
### .Trim() (Loại bỏ khoảng trắng ở đầu và cuối chuỗi)
**Syn**
```bash
tenChuoi.Trim()
```
**Ex**
```csharp
string maNV = txtMaNV.Text.Trim();
```
## var 
**Ex**
```csharp
var age = 20;
var name = "Thang";
var price = 10.5;

// C# tự suy ra kiểu:
// 20       → int
// "Thang"  → string
// 10.5     → double
```
### ToString() (Chuyển một giá trị hoặc đối tượng thành kiểu chuỗi string)
**Syn**
```bash
giaTri.ToString()
```
**Ex**
```csharp
int tuoi = 20;

string s = tuoi.ToString();

MessageBox.Show(s);
```
### string.IsNullOrEmpty() (Kiểm tra chuỗi có bị null hoặc rỗng hay không)
**Syn**
```bash
string.IsNullOrEmpty(chuoi)

- Output:
    + true: Chuỗi là null hoặc rỗng "".
    + false: Chuỗi có dữ liệu.
```
**Ex**
```csharp
private void bt_Them_Click(object sender, EventArgs e)
{
    if (string.IsNullOrEmpty(txtMaNV.Text))
    {
        MessageBox.Show("Vui lòng nhập mã nhân viên!");
        return;
    }

    MessageBox.Show("Đã nhập mã nhân viên!");
}
```
### string.IsNullOrWhiteSpace() (Kiểm tra chuỗi có phải null, rỗng hoặc chỉ chứa khoảng trắng hay không)
**Syn**
```bash
string.IsNullOrWhiteSpace(chuoi)
```
**Ex**
```csharp
string maNV = "     ";

if (string.IsNullOrWhiteSpace(maNV))
{
    MessageBox.Show("Mã nhân viên không được để trống!");
}
```
## List<T>
**Ex**
```csharp
List<int> numbers = new List<int>(); // Nghĩa là: List<int> -> List chứa int

foreach (var number in numbers)
{
    Console.WriteLine(number);
}
// 10
// 30
```
## Add()
```csharp
List<int> numbers = new List<int>()

numbers.Add(10);
numbers.Add(20);
numbers.Add(30);
```
### Count
```csharp
Console.WriteLine(numbers.Count); // 3
```
### Remove
```Csharp
numbers.Remove(20); // [10, 30]
```
## Dictionary
**Syn**
```bash
Dictionary<string, string> data = new Dictionary<string, string>();
```
### [] (thêm phân tử)
**Ex**
```csharp
data["name"] = "Thang";
data["city"] = "Hanoi";

Console.WriteLine(data["name"]); // Thang
```
## null
**Ex**
```csharp
string name = null;

if (name == null)
{
    Console.WriteLine("Name is null");
}

// Name is null
```
# Operator (Toán tử)
## + (cộng)
## - (trừ)
## * (nhân)
## / (chia)
## % (chia lấy dư)
## == (so sánh bằng)
## != (so sánh khác)
## > (so sánh lớn hơn)
## < (so sánh nhỏ hơn)
## >= (so sánh lớn hơn hoặc bằng)
**Ex**
```csharp
int age = 20;

Console.WriteLine(age >= 18); // True
```
## <= (so sánh nhỏ hơn hoặc bằng)
## &&
**Ex**
```csharp
if (age >= 18 && active)
{
    Console.WriteLine("Allowed");
}
```
## ||
```csharp
if (age >= 18 || active)
{
    Console.WriteLine("Allowed");
}
```
## !
```csharp
bool active = true;

if (!active)
{
    Console.WriteLine("Inactive");
}
```
# Conditional (câu điều kiện)
## if ... else if ... else
**Syn**
```bash
if (condition)
{
    // code
}
else if (score >= 5)
{
    Console.WriteLine("Pass");
}
else
{
    // code
}
```
**Ex**
```csharp
int score = 8;

if (score >= 8)
{
    Console.WriteLine("Good");
}
else if (score >= 5)
{
    Console.WriteLine("Pass");
}
else
{
    Console.WriteLine("Fail");
}
// Good
```
## switch ... case (Chọn một nhánh xử lý dựa trên giá trị của một biến)
**Syn**
```bash
switch (biến)
{
    case giá_trị_1:
        // Xử lý
        break;

    case giá_trị_2:
        // Xử lý
        break;

    default:
        // Trường hợp còn lại
        break;
}
```
**Ex**
```csharp
int day = 2;

switch (day)
{
    case 1:
        Console.WriteLine("Monday");
        break;

    case 2:
        Console.WriteLine("Tuesday");
        break;

    default:
        Console.WriteLine("Other");
        break;
}
// Tuesday
```
# Loop (vòng lặp) 
## for (lặp lại một đoạn code với số lần xác đinh trước)
**Syn**
```bash
for (khởi_tạo; điều_kiện; cập_nhật)
{
    // code
}
```
**Ex**
```csharp
for (int i = 0; i < 5; i++)
{
    Console.WriteLine(i);
}
// 0
// 1
// 2
// 3
// 4
```
## while
**Ex**
```csharp
int i = 0;

while (i < 5)
{
    Console.WriteLine(i);
    i++;
}
// 0
// 1
// 2
// 3
// 4
```
## foreach (Duyệt lần lượt từng phần tử trong một tập hợp mà không cần tự quản lý biến chỉ số)
**Syn**
```bash
foreach (kiểu biến in collection)
{
    ...
}
```
**Ex**
```csharp
List<string> names = new List<string>();

names.Add("Thang");
names.Add("An");
names.Add("Binh");

foreach (string name in names)
{
    Console.WriteLine(name);
}
// Thang
// An
// Binh
```
## While (Lặp lại code khi điều kiện còn đúng Thường dùng khi chưa biết chính xác cần lặp bao nhiêu lần)
**Syn**
```bash
while (điều_kiện)
{
    // Code cần lặp
}
```
**Ex**
```csharp
int i = 1;

while (i <= 5)
{
    MessageBox.Show(i.ToString());
    i++;
}
// 1
// 2
// 3
// 4
// 5
```
# Function
## int
```csharp
public int Sum(int a, int b)
{
    return a + b;
}

int result = Sum(10, 20);

Console.WriteLine(result); // 30
```
## void
```csharp
public void SayHello()
{
    Console.WriteLine("Hello");
}

SayHello(); // Hello
```
**Ex2: Parameter**
```csharp
public void SayHello(string name)
{
    Console.WriteLine("Hello " + name);
}

SayHello("Thang"); // Hello Thang
```
# Class
**Ex**
```csharp
public class Student
{
    public string Name { get; set; }
    public int Age { get; set; }
}

Student student = new Student();

student.Name = "Thang";

Console.WriteLine(student.Name); // Thang
```
## Constructor
**Ex**
```csharp
public class Student
{
    public string Name { get; set; }
    public int Age { get; set; }

    public Student(string name, int age)
    {
        Name = name;
        Age = age;
    }
}

Student student = new Student("Thang", 20);

Console.WriteLine(student.Name); // Thang
```
# Exception
**Syn**
```bash
try
{
    // code có thể lỗi
}
catch (Exception ex)
{
    // xử lý lỗi
}
```
**Ex**
```csharp
try
{
    int a = 10;
    int b = 0;

    int result = a / b;
}
catch (Exception ex)
{
    Console.WriteLine(ex.Message);
}
// Attempted to divide by zero.
```
## finally
**Ex**
```csharp
try
{
    Console.WriteLine("Try");
}
catch (Exception ex)
{
    Console.WriteLine("Error");
}
finally
{
    Console.WriteLine("Finally");
}
// finally luôn được chạy sau try/catch.
```
# Array
**Ex**
```csharp
int[] numbers = { 10, 20, 30, 40 };

Console.WriteLine(numbers[0]); // 10
```
# C# WinForms
## MessageBox (thông báo bằng hộp thoại)
**Ex**
```csharp
private void bt_Sua_Click(object sender, EventArgs e)
{
    MessageBox.Show("Bạn vừa bấm nút Sửa!");
}
```
### Show()
**Ex**
```csharp
MessageBox.Show(
    "Bạn có chắc chắn muốn xóa không?", // Nội dung thông báo
    "Xác nhận xóa", // Tiêu đề hộp thoại
    MessageBoxButtons.YesNo, // Hiển thị hai nút Yes và No
    MessageBoxIcon.Question // Hiển thị biểu tượng dấu hỏi
);
```
## .Text (lấy dữ liệu từ TextBox)
**Ex**
```csharp
private void bt_KiemTra_Click(object sender, EventArgs e)
{
    string maNV = txtMaNV.Text;

    MessageBox.Show(maNV);
}
```
**Ex2: Gán dữ liệu vào TextBox**
```csharp
txtMaNV.Text = "NV001";
```
## .Clear() (Xóa toàn bộ nội dung bên trong TextBox)
**Syn**
```bash
tenTextBox.Clear();
```
**Ex**
```csharp
private void bt_XoaTrang_Click(object sender, EventArgs e)
{
    txtMaNV.Clear();
    txtHo.Clear();
    txtTen.Clear();
    txtDiaChi.Clear();
}
```
## MessageBoxButtons
### .OK (Chỉ có nút OK)
### YesNo (Có Yes và No)
### YesNoCancel (Có Yes, No và Cancel)
### Information (Biểu tượng thông tin)
### Warning (Biểu tượng cảnh báo)
### Error (Biểu tượng lỗi)
### Question (Biểu tượng câu hỏi)
## DialogResult (Lưu kết quả mà người dùng chọn trong hộp thoại MessageBox)
**Ex**
```csharp
private void bt_Xoa_Click(object sender, EventArgs e)
{
    DialogResult xacNhan = MessageBox.Show(
        "Bạn có chắc chắn muốn xóa không?",
        "Xác nhận xóa",
        MessageBoxButtons.YesNo,
        MessageBoxIcon.Question
    );

    if (xacNhan == DialogResult.Yes)
    {
        MessageBox.Show("Đã xóa thành công!");
    }
    else
    {
        MessageBox.Show("Bạn đã hủy thao tác!");
    }
}
```
## .Rows (Truy cập danh sách các dòng trong DataGridView)
**Syn**
```bash
table.Rows
```
**Ex**
```csharp
int soDong = table.Rows.Count;

MessageBox.Show(soDong.ToString());
```
### .Cells() (Lấy dữ liệu của một ô cụ thể)
Cú pháp:
table.Rows[chỉ_số_dòng].Cells[chỉ_số_cột].Value


Bạn cần nhớ:
- Rows[0]: Dòng đầu tiên.
- Cells[0]: Cột đầu tiên.
- Chỉ số dòng và cột đều bắt đầu từ 0.
Ví dụ bảng:
Chỉ số cột	0	1	2	3
Tên cột	Mã NV	Họ	Tên	Địa chỉ

Lấy mã nhân viên của dòng đầu tiên:
string maNV = table.Rows[0].Cells[0].Value.ToString();


Nếu dòng đầu tiên chứa NV01 thì:
maNV = "NV01"


Lấy tên nhân viên:
string ten = table.Rows[0].Cells[2].Value.ToString();


Output:
An


Mẹo đi thi: Hãy nhớ công thức:
table.Rows[i].Cells[j].Value


Trong đó:
- i là vị trí dòng.
- j là vị trí cột.
#### .Value (Lấy hoặc gán nội dung cho một ô trong DataGridView)
Cú pháp:
table.Rows[0].Cells[0].Value


Ví dụ lấy dữ liệu:
string maNV = table.Rows[0].Cells[0].Value.ToString();


Ví dụ gán dữ liệu:
table.Rows[0].Cells[0].Value = "NV999";


Kết quả: Mã nhân viên ở dòng đầu tiên thay đổi thành NV999.

Lưu ý: Nếu ô không có dữ liệu, Value có thể là null. Vì vậy, khi chưa chắc chắn có dữ liệu, nên kiểm tra null trước hoặc dùng cách an toàn:
string maNV = table.Rows[0].Cells[0].Value?.ToString() ?? "";
### .Add() (Thêm dữ liệu mới vào DataGridView)
Cú pháp:
table.Rows.Add(giá_trị_cột_1, giá_trị_cột_2, ...);


Ví dụ:
table.Rows.Add("NV04", "Phạm", "Nam", "Hà Nội");


Kết quả:
Mã NV	Họ	Tên	Địa chỉ
NV01	Nguyễn	An	Hà Nội
NV02	Trần	Bình	Đà Nẵng
NV03	Lê	Minh	TP.HCM
NV04	Phạm	Nam	Hà Nội

Lưu ý: Các giá trị truyền vào phải tương ứng với số cột và thứ tự cột của bảng.

Nếu DataGridView được liên kết dữ liệu bằng DataSource, không nên sử dụng Rows.Add() trực tiếp; khi đó cần thêm dữ liệu vào nguồn dữ liệu.
### RemoveAt() (Xóa dòng dựa vào chỉ số dòng)
Cú pháp:
table.Rows.RemoveAt(chỉ_số_dòng);


Ví dụ:
table.Rows.RemoveAt(0);


Kết quả: Xóa dòng đầu tiên trong bảng.

Ban đầu:
Mã NV	Tên
NV01	An
NV02	Bình
NV03	Minh

Sau khi chạy:
table.Rows.RemoveAt(0);


Kết quả:
Mã NV	Tên
NV02	Bình
NV03	Minh

Chú ý: Chỉ số dòng phải hợp lệ. Nếu bảng có dòng trống cuối cùng để nhập dữ liệu, cần tránh xóa nhầm dòng đó.
## DataGridViewCellEventArgs 
### RowIndex (Xác định người dùng vừa click vào dòng nào)
Cú pháp thường dùng trong sự kiện CellClick:
private void table_CellClick(
    object sender,
    DataGridViewCellEventArgs e)
{
    int dongChon = e.RowIndex;
}


Giải thích:
Thành phần	Ý nghĩa
table_CellClick	Sự kiện click vào ô trong bảng
DataGridViewCellEventArgs e	Thông tin về ô được click
e.RowIndex	Chỉ số dòng được click
e.ColumnIndex	Chỉ số cột được click

Ví dụ:
private void table_CellClick(object sender, DataGridViewCellEventArgs e)
{
    int dongChon = e.RowIndex;

    MessageBox.Show(dongChon.ToString());
}


Nếu bạn click vào dòng nhân viên NV02 (dòng thứ 2), kết quả là:
1


Bởi vì chỉ số dòng bắt đầu từ 0.

Chú ý: Khi click vào phần tiêu đề cột, RowIndex có thể bằng -1. Vì vậy cần kiểm tra:
if (e.RowIndex >= 0)
{
    // Xử lý dòng được chọn
}
### SelectedRows (Lấy dòng đang được chọn)
Công dụng: Truy cập những dòng mà người dùng đang chọn.

Cú pháp:
table.SelectedRows


Ví dụ:
if (table.SelectedRows.Count > 0)
{
    string maNV = table.SelectedRows[0].Cells[0].Value.ToString();

    MessageBox.Show(maNV);
}


Giải thích:
- SelectedRows: Danh sách dòng được chọn.
- Count: Số dòng đang được chọn.
- [0]: Dòng được chọn đầu tiên.
- Cells[0]: Ô đầu tiên của dòng.
- Value: Giá trị trong ô.
Phân biệt:
Câu lệnh	Chức năng
e.RowIndex	Lấy dòng vừa được click
SelectedRows	Lấy danh sách dòng đang được chọn

Muốn sử dụng SelectedRows thuận tiện, bạn có thể đặt thuộc tính:
table.SelectionMode = DataGridViewSelectionMode.FullRowSelect;


Khi đó click vào một ô sẽ chọn cả dòng.
# System
## Xml
### XmlDocument (đại diện cho toàn bộ tài liệu XML)
**Syn**
```bash
XmlDocument doc = new XmlDocument();
```
#### Load()	(Đọc XML từ file)
**Ex**
```bash
XmlDocument doc = new XmlDocument();

doc.Load("nhanvien.xml");

MessageBox.Show("Đọc XML thành công!");
```
#### Save()	(Lưu XML xuống file)
#### CreateElement() (Tạo phần tử XML)
##### InnerText (Lấy hoặc gán nội dung văn bản)
**Ex**
```csharp
XmlElement ho = doc.CreateElement("ho");

ho.InnerText = "Nguyen Van";

MessageBox.Show(ho.InnerText); // Nguyen Van
```
##### InnerXml (Lấy hoặc gán nội dung XML bên trong)
##### Attributes (Truy cập các thuộc tính của phần tử)
##### Name (Lấy tên phần tử)
#### CreateAttribute() (Tạo thuộc tính XML)
#### DocumentElement() (Lấy phần tử gốc)
**Ex**
```xml
<ds>
    <nhanvien manv="NV01"/>
</ds>
```
```csharp
XmlElement theGoc = doc.DocumentElement; // theGoc đại diện cho thẻ <ds>.
```
#### XmlElement (Đại diện cho một phần tử XML)
**Syn**
```csharp
XmlElement nhanVien = doc.CreateElement("nhanvien"); // Kết quả tạo ra phần tử: <nhanvien />
```
#### XmlAttribute (Tạo và quản lý thuộc tính của phần tử XML)
**Ex**
```xml
<nhanvien manv="NV01"/>
```
```csharp
XmlAttribute maNV = doc.CreateAttribute("manv"); // Tạo thuộc tính tên manv.

maNV.InnerText = "NV01"; // Gán giá trị thuộc tính.
```
### XmlNode (Đại diện cho một nút trong tài liệu XML)
#### AppendChild() (Thêm nút con)
#### RemoveChild() (Xóa nút con)
#### ReplaceChild() (Thay nút cũ bằng nút mới)
#### SelectSingleNode() (Tìm một nút theo XPath)
#### SelectNodes() (Tìm nhiều nút theo XPath)
SelectSingleNode()
Công dụng: Tìm và lấy một nút XML đầu tiên thỏa mãn điều kiện.

Cú pháp:
XmlNode node = doc.SelectSingleNode("đường_dẫn_XPath");


Ví dụ có file XML:
<ds>
    <nhanvien manv="NV01">
        <hoten>
            <ho>Nguyen</ho>
            <ten>An</ten>
        </hoten>
        <diachi>Ha Noi</diachi>
    </nhanvien>

    <nhanvien manv="NV02">
        <hoten>
            <ho>Tran</ho>
            <ten>Binh</ten>
        </hoten>
        <diachi>Da Nang</diachi>
    </nhanvien>
</ds>


Muốn tìm nhân viên NV01:
XmlNode nv = doc.SelectSingleNode("/ds/nhanvien");


Kết quả: Lấy nhân viên đầu tiên trong danh sách.

Muốn lấy nhân viên có mã NV02:
XmlNode nv = doc.SelectSingleNode(
    "/ds/nhanvien[@manv='NV02']"
);


Kết quả: Lấy nút nhân viên NV02.

Giải thích XPath:
Thành phần	Ý nghĩa
/	Bắt đầu từ nút gốc
ds	Thẻ gốc
nhanvien	Thẻ nhân viên
@manv	Thuộc tính manv
[@manv='NV02']	Điều kiện mã nhân viên bằng NV02

Nếu không tìm thấy, SelectSingleNode() trả về null.

Vì vậy thường phải kiểm tra:
if (nv != null)
{
    MessageBox.Show("Tìm thấy nhân viên!");
}
else
{
    MessageBox.Show("Không tìm thấy!");
}



2. SelectNodes()
Công dụng: Tìm và lấy tất cả các nút thỏa mãn điều kiện.

Khác với SelectSingleNode() chỉ lấy một nút, SelectNodes() lấy danh sách nút.

Cú pháp:
XmlNodeList danhSach = doc.SelectNodes("đường_dẫn_XPath");


Ví dụ:
XmlNodeList danhSach = doc.SelectNodes("/ds/nhanvien");


Kết quả có 2 nhân viên:
- NV01
- NV02
Muốn duyệt danh sách nhân viên
XmlNodeList danhSach = doc.SelectNodes("/ds/nhanvien");

foreach (XmlNode nv in danhSach)
{
    MessageBox.Show(nv.Attributes["manv"].Value);
}


Kết quả:
NV01
NV02


Giải thích:
- SelectNodes(): Lấy danh sách nhân viên.
- foreach: Duyệt từng nhân viên.
- nv: Đại diện cho một nhân viên.
- Attributes["manv"]: Lấy thuộc tính mã nhân viên.
- .Value: Lấy giá trị của thuộc tính.

3. Các cách viết XPath thường gặp
Đây là phần nên ghi nhớ khi đi thi.

Giả sử XML có cấu trúc như ví dụ phía trên.
XPath	Ý nghĩa
/ds	Lấy thẻ gốc ds
/ds/nhanvien	Lấy các nhân viên
/ds/nhanvien[1]	Lấy nhân viên đầu tiên
/ds/nhanvien[2]	Lấy nhân viên thứ hai
/ds/nhanvien[@manv='NV01']	Tìm nhân viên có mã NV01
/ds/nhanvien/hoten	Lấy thẻ họ tên của các nhân viên
/ds/nhanvien/diachi	Lấy các thẻ địa chỉ
/ds/nhanvien[hoten/ten='An']	Tìm nhân viên có tên An

Lưu ý: Trong XPath, chỉ số [1] là phần tử đầu tiên, không phải [0] như chỉ số mảng trong C#.

4. Lấy dữ liệu bên trong thẻ XML
Ví dụ:
<nhanvien manv="NV01">
    <hoten>
        <ho>Nguyen</ho>
        <ten>An</ten>
    </hoten>
    <diachi>Ha Noi</diachi>
</nhanvien>


Cách 1: Dùng SelectSingleNode()
XmlNode nv = doc.SelectSingleNode(
    "/ds/nhanvien[@manv='NV01']"
);

if (nv != null)
{
    string diaChi = nv.SelectSingleNode("diachi").InnerText;

    MessageBox.Show(diaChi);
}


Kết quả:
Ha Noi


Ở đây:
- nv: Nút nhân viên.
- SelectSingleNode("diachi"): Tìm thẻ địa chỉ bên trong nhân viên.
- InnerText: Lấy nội dung của thẻ.
Cách 2: Dùng Attributes
Lấy mã nhân viên:
string ma = nv.Attributes["manv"].Value;


Kết quả:
NV01


So sánh hai cách:
// Lấy nội dung thẻ
string diaChi = nv.SelectSingleNode("diachi").InnerText;

// Lấy giá trị thuộc tính
string ma = nv.Attributes["manv"].Value;


Đây là hai cách rất hay gặp trong đề thi.

5. Kết hợp XML với DataGridView
Đây là ví dụ thực tế để đưa dữ liệu XML lên bảng.
private void HienThi()
{
    doc.Load(duongDanFile);

    table.Rows.Clear();

    XmlNodeList danhSach = doc.SelectNodes("/ds/nhanvien");

    foreach (XmlNode nv in danhSach)
    {
        string ma = nv.Attributes["manv"].Value;

        string ho = nv.SelectSingleNode("hoten/ho").InnerText;

        string ten = nv.SelectSingleNode("hoten/ten").InnerText;

        string diaChi = nv.SelectSingleNode("diachi").InnerText;

        table.Rows.Add(ma, ho, ten, diaChi);
    }
}


Giải thích luồng chạy:
1. Đọc file XML bằng Load().
2. Xóa dữ liệu cũ trên DataGridView bằng Rows.Clear().
3. Lấy danh sách nhân viên bằng SelectNodes().
4. Dùng foreach duyệt từng nhân viên.
5. Lấy mã, họ, tên và địa chỉ.
6. Dùng Rows.Add() đưa dữ liệu lên bảng.
Kết quả hiển thị:
Danh sách nhân viên
Mã NV	Họ	Tên	Địa chỉ
NV01	Nguyen	An	Ha Noi
NV02	Tran	Binh	Da Nang


Lưu ý: Ví dụ trên giả sử XML có đầy đủ các thẻ và thuộc tính cần thiết. Nếu dữ liệu có thể thiếu, cần kiểm tra null trước khi gọi .InnerText hoặc .Value.