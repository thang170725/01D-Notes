- [AndroidX Introduction (xây dựng Android app hiện đại, được phân phối dưới dạng dependencies của project)](#androidx-introduction-xây-dựng-android-app-hiện-đại-được-phân-phối-dưới-dạng-dependencies-của-project)
  - [Ask](#ask)
    - [Tại sao AndroidX phải cài bằng Gradle?](#tại-sao-androidx-phải-cài-bằng-gradle)
    - [Tại sao Android Studio vừa tạo project đã dùng được AndroidX?](#tại-sao-android-studio-vừa-tạo-project-đã-dùng-được-androidx)
- [appcompat](#appcompat)
  - [app](#app)
    - [AppCompatActivity](#appcompatactivity)
      - [onCreate()](#oncreate)
- [findViewById (Lấy các thành phần từ XML)](#findviewbyid-lấy-các-thành-phần-từ-xml)
  - [.setText() (dùng để gán nội dung cho TextView, EditText, ...)](#settext-dùng-để-gán-nội-dung-cho-textview-edittext-)
  - [getText() (Dùng để lấy nội dung hiện tại của TextView hoặc EditView)](#gettext-dùng-để-lấy-nội-dung-hiện-tại-của-textview-hoặc-editview)
  - [setTextSize() (dùng để thay đổi kích thước chữ)](#settextsize-dùng-để-thay-đổi-kích-thước-chữ)
  - [.setVisibility() (Thay đổi trạng thái hiển thị View)](#setvisibility-thay-đổi-trạng-thái-hiển-thị-view)
  - [.getVisibility() (Lấy trạng thái hiển thị hiện tại của TextView)](#getvisibility-lấy-trạng-thái-hiển-thị-hiện-tại-của-textview)
---
# AndroidX Introduction (xây dựng Android app hiện đại, được phân phối dưới dạng dependencies của project)
## Ask
### Tại sao AndroidX phải cài bằng Gradle?
```bash
Trong project của bạn có file: build.gradle.kts hoặc build.gradle
    Android Studio sẽ có dependencies kiểu:
        dependencies {
            implementation(libs.androidx.appcompat)
        }

    Hoặc project cũ có thể thấy:
        implementation 'androidx.appcompat:appcompat:...'
Gradle sẽ tải thư viện đó về. Bạn không cần tự download file .jar hoặc .aar. Android Studio + Gradle quản lý việc này.
```
### Tại sao Android Studio vừa tạo project đã dùng được AndroidX?
```bash
Vì template project của Android Studio đã cấu hình sẵn.

Khi bạn tạo: New Project -> Empty Activity
    Android Studio tạo cho bạn một project có sẵn:
        - Gradle
        - Android SDK
        - AndroidX dependencies

    Sau đó Gradle tải dependencies cần thiết.
        Cho nên bạn chỉ việc: import androidx.appcompat.app.AppCompatActivity; mà không cần tự đi tìm thư viện trên Google.
```
# appcompat
## app 
### AppCompatActivity
**Ex**
```java
import androidx.appcompat.app.AppCompatActivity;

public class MainActivity extends AppCompatActivity {
    
}

// AppCompatActivity là một Activity thuộc AndroidX.
// Có thể hình dung: Activity <- AppCompatActivity <- MainActivity
```

#### onCreate()
```bash
Đây là hàm khởi động cốt lõi (lifecycle method) của một màn hình (Activity) trong Android. Ngay khi bạn mở ứng dụng lên, hàm này sẽ chạy đầu tiên.
```
**Syn**
```bash
@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);
}

- setContentView(R.layout.activity_main): Nạp giao diện XML (activity_main.xml) lên màn hình điện thoại để người dùng nhìn thấy và tương tác. Nơi đây cũng là chỗ lý tưởng để viết các mã ánh xạ (findViewById) và xử lý sự kiện nút bấm.
```
annotation.NonNull
# findViewById (Lấy các thành phần từ XML)
```bash
Hàm findViewById là phương thức có sẵn nằm trong lớp android.app.Activity (và được kế thừa qua androidx.appcompat.app.AppCompatActivity) cũng như lớp android.view.View.
    Lưu ý quan trọng cho bài kiểm tra: Vì đây là hàm cốt lõi của một Activity, KHÔNG CẦN phải gõ lệnh import nào cả khi sử dụng trực tiếp trong Activity của mình (Android Studio tự động hiểu). Em chỉ cần gọi trực tiếp: Button btn = findViewById(R.id.btn_id); là được!
```
**Ex**
```java
Button button = findViewById(R.id.button); // Button: kiểu dữ liệu, cho biết biến này đại diện cho một nút bấm
TextView content = findViewById(R.id.content);
```
## .setText() (dùng để gán nội dung cho TextView, EditText, ...)
**Syn**
```bash
txt.setText("Hello");

- Input:
    + txt: biến đại diện cho TextView
    + setText(...): hàm thay đổi nội dung
    + "Hello": nội dung muốn hiển thị
```
**Ex**
```java
TextView txt = findViewById(R.id.txt);

txt.setText("Hello Android");

// Màn hình sẽ hiển thị:
// Hello Android
```
## getText() (Dùng để lấy nội dung hiện tại của TextView hoặc EditView)
**Ex**
```java
String text = txt.getText().toString();
```
## setTextSize() (dùng để thay đổi kích thước chữ)
**Syn**
```bash
txt.setTextSize(20);
```
**Ex**
```java
TextView txt = findViewById(R.id.txt);

txt.setText("Hello Android");
txt.setTextSize(20);
```
## .setVisibility() (Thay đổi trạng thái hiển thị View)
**Syn**
```bash
txt.setVisibility(View.VISIBLE);

- Input:
    + View.VISIBLE: Hiển thị View
    + View.INVISIBLE:  Ẩn View nhưng vẫn giữ chỗ trên giao diện
    + View.GONE: Ẩn View và xóa luôn khoảng trống không gian mà View chiếm
```
## .getVisibility() (Lấy trạng thái hiển thị hiện tại của TextView)
