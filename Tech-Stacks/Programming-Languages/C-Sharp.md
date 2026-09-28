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
  - [var](#var)
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
  - [if / else](#if--else)
  - [else if](#else-if)
  - [switch](#switch)
- [Loop (vòng lặp)](#loop-vòng-lặp)
  - [for](#for)
  - [while](#while)
  - [foreach](#foreach)
- [Function](#function)
  - [int](#int)
  - [void](#void)
- [Class](#class)
  - [Constructor](#constructor)
- [Exception](#exception)
  - [finally](#finally)
- [Array](#array)
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
## if / else
**Syn**
```bash
if (condition)
{
    // code
}
else
{
    // code
}
```
**Ex**
```csharp
int age = 20;

if (age >= 18)
{
    Console.WriteLine("Adult");
}
else
{
    Console.WriteLine("Under 18");
}
// Adult
```
## else if
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
## switch
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
## for
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
## foreach
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