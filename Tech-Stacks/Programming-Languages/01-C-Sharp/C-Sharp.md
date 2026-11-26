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
- [DataGridView](#datagridview)
  - [.Rows (Truy cập danh sách các dòng trong DataGridView)](#rows-truy-cập-danh-sách-các-dòng-trong-datagridview)
    - [.Cells() (Lấy dữ liệu của một ô cụ thể)](#cells-lấy-dữ-liệu-của-một-ô-cụ-thể)
      - [.Value (Lấy hoặc gán nội dung cho một ô trong DataGridView)](#value-lấy-hoặc-gán-nội-dung-cho-một-ô-trong-datagridview)
    - [.Add() (Thêm dữ liệu mới vào DataGridView)](#add-thêm-dữ-liệu-mới-vào-datagridview)
    - [RemoveAt() (Xóa dòng dựa vào chỉ số dòng)](#removeat-xóa-dòng-dựa-vào-chỉ-số-dòng)
  - [DataGridViewCellEventArgs](#datagridviewcelleventargs)
    - [RowIndex (Xác định người dùng vừa click vào dòng nào)](#rowindex-xác-định-người-dùng-vừa-click-vào-dòng-nào)
    - [SelectedRows (Lấy dòng đang được chọn)](#selectedrows-lấy-dòng-đang-được-chọn)
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
# DataGridView
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
**Syn**
```bash
table.Rows[chỉ_số_dòng].Cells[chỉ_số_cột].Value
```
**Ex: bảng**
```bash
Chỉ số cột	0	1	2	3
Tên cột	Mã NV	Họ	Tên	Địa chỉ
```
```c#
string maNV = table.Rows[0].Cells[0].Value.ToString(); // "NV01"
string ten = table.Rows[0].Cells[2].Value.ToString(); // An
```
#### .Value (Lấy hoặc gán nội dung cho một ô trong DataGridView)
**Syn**
```bash
table.Rows[0].Cells[0].Value
```
**Ex: lấy dữ liệu**
```c#
string maNV = table.Rows[0].Cells[0].Value.ToString();
```
### .Add() (Thêm dữ liệu mới vào DataGridView)
**Syn**
```bash
table.Rows.Add(giá_trị_cột_1, giá_trị_cột_2, ...);
```
**Ex**
```c#
table.Rows.Add("NV04", "Phạm", "Nam", "Hà Nội");
// Mã NV	Họ	Tên	Địa chỉ
// NV01	Nguyễn	An	Hà Nội
// NV02	Trần	Bình	Đà Nẵng
// NV03	Lê	Minh	TP.HCM
// NV04	Phạm	Nam	Hà Nội
```
### RemoveAt() (Xóa dòng dựa vào chỉ số dòng)
**Syn**
```bash
table.Rows.RemoveAt(chỉ_số_dòng);
```
**Syn**
```c#
table.Rows.RemoveAt(0);
// Ban đầu:
// Mã NV	Tên
// NV01	An
// NV02	Bình
// NV03	Minh

// Kết quả:
// Mã NV	Tên
// NV02	Bình
// NV03	Minh
```
## DataGridViewCellEventArgs 
### RowIndex (Xác định người dùng vừa click vào dòng nào)
**Syn: Cú pháp thường dùng trong sự kiện CellClick**
```bash
private void table_CellClick(
    object sender,
    DataGridViewCellEventArgs e)
{
    int dongChon = e.RowIndex;
}

- table_CellClick	Sự kiện click vào ô trong bảng
- DataGridViewCellEventArgs e	Thông tin về ô được click
- e.RowIndex	Chỉ số dòng được click
- e.ColumnIndex	Chỉ số cột được click
```
**Ex**
```c#
private void table_CellClick(object sender, DataGridViewCellEventArgs e)
{
    int dongChon = e.RowIndex;

    MessageBox.Show(dongChon.ToString());
}

// Nếu bạn click vào dòng nhân viên NV02 (dòng thứ 2), kết quả là:
// 1
```
### SelectedRows (Lấy dòng đang được chọn)
**Syn**
```bash
table.SelectedRows
```
**Ex**
```c#
if (table.SelectedRows.Count > 0)
{
    string maNV = table.SelectedRows[0].Cells[0].Value.ToString();

    MessageBox.Show(maNV);
}
```
Trong C# WinForms (Visual Studio), nếu bạn thiết kế giao diện trong file Form1.cs [Design] thì có thể lấy giá trị của RadioButton và ComboBox (Dropdown) trong file Form1.cs như sau.
1. Lấy giá trị RadioButton
Giả sử bạn có 2 RadioButton:
- radioButtonNam
- radioButtonNu
Kiểm tra RadioButton nào được chọn:
if (radioButtonNam.Checked)
{
    string gioiTinh = "Nam";
}
else if (radioButtonNu.Checked)
{
    string gioiTinh = "Nữ";
}


Thuộc tính quan trọng:
- .Checked: Kiểm tra có được chọn hay không.
- .Text: Lấy nội dung hiển thị trên RadioButton.
Ví dụ:
string gioiTinh = "";

if (radioButtonNam.Checked)
    gioiTinh = radioButtonNam.Text;
else if (radioButtonNu.Checked)
    gioiTinh = radioButtonNu.Text;


2. Lấy giá trị Dropdown (ComboBox)
Giả sử ComboBox có tên comboBoxKhoa.

Lấy giá trị đang được chọn:
string khoa = comboBoxKhoa.SelectedItem?.ToString();


Hoặc:
string khoa = comboBoxKhoa.Text;


Hai cách khác nhau một chút:
Cách	Ý nghĩa
SelectedItem	Lấy item đang được chọn
SelectedValue	Lấy giá trị tương ứng với ValueMember
Text	Lấy nội dung văn bản đang hiển thị

Kiểm tra người dùng đã chọn chưa:
if (comboBoxKhoa.SelectedIndex != -1)
{
    string khoa = comboBoxKhoa.SelectedItem.ToString();
    MessageBox.Show(khoa);
}
else
{
    MessageBox.Show("Vui lòng chọn khoa!");
}


3. Ví dụ kết hợp trong nút Button
Giả sử form có:
- RadioButton: radioButtonNam, radioButtonNu
- ComboBox: comboBoxKhoa
- Button: btnLuu
Code sự kiện Click:
private void btnLuu_Click(object sender, EventArgs e)
{
    // Lấy giới tính
    string gioiTinh = "";

    if (radioButtonNam.Checked)
        gioiTinh = "Nam";
    else if (radioButtonNu.Checked)
        gioiTinh = "Nữ";

    // Lấy khoa
    string khoa = comboBoxKhoa.SelectedItem?.ToString();

    // Kiểm tra dữ liệu
    if (string.IsNullOrEmpty(gioiTinh))
    {
        MessageBox.Show("Vui lòng chọn giới tính!");
        return;
    }

    if (string.IsNullOrEmpty(khoa))
    {
        MessageBox.Show("Vui lòng chọn khoa!");
        return;
    }

    MessageBox.Show($"Giới tính: {gioiTinh}\nKhoa: {khoa}");
}


Lưu ý: Nếu bạn có nhiều RadioButton nhưng muốn chúng chỉ chọn được một giá trị tại một thời điểm, hãy đặt chúng trong cùng một GroupBox hoặc Panel.

Bạn đang sử dụng Windows Forms (WinForms) đúng không? Nếu đúng, mình có thể hướng dẫn thêm cách lấy dữ liệu từ TextBox, RadioButton, ComboBox và lưu tất cả vào SQL Server.