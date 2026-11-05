- [AndroidX Introduction (xây dựng Android app hiện đại, được phân phối dưới dạng dependencies của project)](#androidx-introduction-xây-dựng-android-app-hiện-đại-được-phân-phối-dưới-dạng-dependencies-của-project)
  - [Ask](#ask)
    - [Tại sao AndroidX phải cài bằng Gradle?](#tại-sao-androidx-phải-cài-bằng-gradle)
    - [Tại sao Android Studio vừa tạo project đã dùng được AndroidX?](#tại-sao-android-studio-vừa-tạo-project-đã-dùng-được-androidx)
- [appcompat](#appcompat)
  - [app](#app)
    - [AppCompatActivity](#appcompatactivity)
      - [onCreate()](#oncreate)
      - [getLayoutInflater()](#getlayoutinflater)
      - [inflate() (dùng để đọc file XML và chuyển nó thành một đối tượng View trong Java)](#inflate-dùng-để-đọc-file-xml-và-chuyển-nó-thành-một-đối-tượng-view-trong-java)
      - [addHeaderView() (dùng để thêm một View vào vị trí đầu tiên của ListView đóng vai trò là phần tiêu đề)](#addheaderview-dùng-để-thêm-một-view-vào-vị-trí-đầu-tiên-của-listview-đóng-vai-trò-là-phần-tiêu-đề)
      - [registerForContextMenu (hàm dùng để đăng ký một view khi người dùng nhấn giữ vào view đó thì android hiển thị context menu)](#registerforcontextmenu-hàm-dùng-để-đăng-ký-một-view-khi-người-dùng-nhấn-giữ-vào-view-đó-thì-android-hiển-thị-context-menu)
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
#### getLayoutInflater()
Công dụng
Dùng để lấy đối tượng LayoutInflater, có nhiệm vụ chuyển file giao diện XML thành đối tượng View trong Java.

Ví dụ: Bạn có file table_header.xml mô tả giao diện tiêu đề bảng. Android chưa thể trực tiếp sử dụng file XML đó như một View trong Java. Vì vậy, cần LayoutInflater để chuyển đổi.
Cú pháp
LayoutInflater inflater = getLayoutInflater();


Hoặc:
LayoutInflater inflater =
        (LayoutInflater) getSystemService(
                Context.LAYOUT_INFLATER_SERVICE
        );


Ví dụ dễ hiểu
Giả sử bạn có file table_header.xml:
<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="50dp"
    android:orientation="horizontal">

    <TextView
        android:layout_width="0dp"
        android:layout_height="match_parent"
        android:layout_weight="1"
        android:text="Mã NV"/>

    <TextView
        android:layout_width="0dp"
        android:layout_height="match_parent"
        android:layout_weight="2"
        android:text="Họ tên"/>

</LinearLayout>


Trong Activity:
LayoutInflater inflater = getLayoutInflater();


Kết quả giả định:

Bạn nhận được một đối tượng LayoutInflater có khả năng đọc và chuyển XML thành các đối tượng View.

Lưu ý: Dòng code trên chưa tạo ra giao diện tiêu đề. Nó chỉ lấy công cụ để tạo giao diện.

#### inflate() (dùng để đọc file XML và chuyển nó thành một đối tượng View trong Java)
```bash
Nói đơn giản:
- getLayoutInflater() lấy công cụ.
- inflate() sử dụng công cụ đó để tạo giao diện từ XML.
```
**Syn**
```bash
View header = inflater.inflate(
        R.layout.table_header,
        null
);

- Input:
    + inflater:	Đối tượng LayoutInflater
    + R.layout.table_header: File XML cần chuyển thành View
    + null: Chưa chỉ định View cha (parent)
```
**Ex**
```bash
Giả sử file table_header.xml có hai TextView:
- Mã NV
- Họ tên
```
```java
LayoutInflater inflater = getLayoutInflater();

View header = inflater.inflate(
        R.layout.table_header,
        null
);


TextView txtMaNV = header.findViewById(R.id.txtMaNV);
TextView txtHoTen = header.findViewById(R.id.txtHoTen);
// Lưu ý: inflate() mới chỉ tạo View, chưa tự động hiển thị nó trên màn hình.
```
#### addHeaderView() (dùng để thêm một View vào vị trí đầu tiên của ListView đóng vai trò là phần tiêu đề)
**Syn**
```bash
listView.addHeaderView(header);

- Input:
    + listView: ListView cần thêm tiêu đề.
    + header: View tiêu đề đã được tạo bằng inflate().
```
**Ex: Bạn có danh sách nhân viên gồm mã nhân viên, họ tên và tuổi**
```bash
Bạn muốn phía trên danh sách có một hàng tiêu đề:
Mã NV	Họ tên	Tuổi
NV01	Nguyễn Văn A	22
NV02	Trần Văn B	23
NV03	Lê Văn C	21

Thay vì tạo tiêu đề như một nhân viên trong Adapter, bạn có thể sử dụng addHeaderView()
```
```java
ListView lvNhanVien = findViewById(R.id.lvNhanVien);

LayoutInflater inflater = getLayoutInflater();

View header = inflater.inflate(
        R.layout.table_header,
        null
);

lvNhanVien.addHeaderView(header);

Kết quả giả định:
Danh sách nhân viên
Mã NV       Họ tên          Tuổi
NV01        Nguyễn Văn A    22
NV02        Trần Văn B      23
NV03        Lê Văn C        21
```
**Ex2: Mô phỏng ListView sau khi thêm Header và dữ liệu Adapter**
```xml
<ListView
    android:id="@+id/lvNhanVien"
    android:layout_width="match_parent"
    android:layout_height="match_parent"/>
```
*Trong MainActivity.java*
```java
public class MainActivity extends AppCompatActivity {

    ListView lvNhanVien;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        lvNhanVien = findViewById(R.id.lvNhanVien);

        // Bước 1: Lấy công cụ LayoutInflater
        LayoutInflater inflater = getLayoutInflater();

        // Bước 2: Tạo View từ file XML
        View header = inflater.inflate(
                R.layout.table_header,
                null
        );

        // Bước 3: Thêm View vào đầu ListView
        lvNhanVien.addHeaderView(header);

        // Bước 4: Tạo dữ liệu
        String[] dsNhanVien = {
                "Nguyễn Văn A",
                "Trần Văn B",
                "Lê Văn C"
        };

        // Bước 5: Tạo Adapter
        ArrayAdapter<String> adapter =
                new ArrayAdapter<>(
                        this,
                        android.R.layout.simple_list_item_1,
                        dsNhanVien
                );

        // Bước 6: Gắn Adapter vào ListView
        lvNhanVien.setAdapter(adapter);
    }
}
```
#### registerForContextMenu (hàm dùng để đăng ký một view khi người dùng nhấn giữ vào view đó thì android hiển thị context menu)
```bash
Với hệ thống Android, ra lệnh rằng: 
    "Hãy theo dõi thành phần này, nếu người dùng nhấn giữ (Long Click) vào nó, hãy kích hoạt Context Menu".
```
**Syn**
```bash
registerForContextMenu(view);

- Input:
    + registerForContextMenu(): Hàm đăng ký Context Menu.
    + view: View mà bạn muốn đăng ký sự kiện nhấn giữ.
```
**Ex: Giả sử có một ListView hiển thị danh sách**
```bash
Danh sách nhân viên
Nguyễn Văn A
Nhấn giữ

Trần Văn B
Nhấn giữ

Lê Văn C
Nhấn giữ

Context Menu khi nhấn giữ
Sửa nhân viên
Xóa nhân viên
Xem thông tin
```
*Bước 1: Đăng ký Context Menu*
```java
Trong onCreate():
registerForContextMenu(lvNhanVien);
```
*Bước 2: Tạo nội dung Context Menu*
```java
@Override
public void onCreateContextMenu(
        ContextMenu menu,
        View v,
        ContextMenu.ContextMenuInfo menuInfo) {

    super.onCreateContextMenu(menu, v, menuInfo);

    menu.setHeaderTitle("Chọn chức năng");

    menu.add(0, 1, 0, "Sửa nhân viên");
    menu.add(0, 2, 1, "Xóa nhân viên");
    menu.add(0, 3, 2, "Xem thông tin");
}


Giải thích:
Thành phần	Ý nghĩa
menu	Đối tượng quản lý Context Menu
v	View được nhấn giữ
menuInfo	Thông tin về phần tử được nhấn giữ
setHeaderTitle()	Đặt tiêu đề menu
add()	Thêm một lựa chọn vào menu

Cú pháp menu.add():
menu.add(groupId, itemId, order, title);


Ví dụ:
menu.add(0, 1, 0, "Sửa nhân viên");


- 0: Group ID.
- 1: ID của mục menu.
- 0: Thứ tự hiển thị.
- "Sửa nhân viên": Nội dung hiển thị.
```
Bước 3: Xử lý khi người dùng chọn menu

Override onContextItemSelected():
@Override
public boolean onContextItemSelected(MenuItem item) {

    switch (item.getItemId()) {

        case 1:
            Toast.makeText(this,
                    "Bạn chọn Sửa nhân viên",
                    Toast.LENGTH_SHORT).show();
            return true;

        case 2:
            Toast.makeText(this,
                    "Bạn chọn Xóa nhân viên",
                    Toast.LENGTH_SHORT).show();
            return true;

        case 3:
            Toast.makeText(this,
                    "Bạn chọn Xem thông tin",
                    Toast.LENGTH_SHORT).show();
            return true;
    }

    return super.onContextItemSelected(item);
}


4. Ví dụ hoàn chỉnh với ListView
public class MainActivity extends AppCompatActivity {

    ListView lvNhanVien;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        lvNhanVien = findViewById(R.id.lvNhanVien);

        String[] dsNhanVien = {
                "Nguyễn Văn A",
                "Trần Văn B",
                "Lê Văn C"
        };

        ArrayAdapter<String> adapter =
                new ArrayAdapter<>(
                        this,
                        android.R.layout.simple_list_item_1,
                        dsNhanVien
                );

        lvNhanVien.setAdapter(adapter);

        // Đăng ký Context Menu cho ListView
        registerForContextMenu(lvNhanVien);
    }

    // Tạo Context Menu
    @Override
    public void onCreateContextMenu(
            ContextMenu menu,
            View v,
            ContextMenu.ContextMenuInfo menuInfo) {

        super.onCreateContextMenu(menu, v, menuInfo);

        menu.setHeaderTitle("Chọn chức năng");

        menu.add(0, 1, 0, "Sửa nhân viên");
        menu.add(0, 2, 1, "Xóa nhân viên");
        menu.add(0, 3, 2, "Xem thông tin");
    }

    // Xử lý khi chọn Context Menu
    @Override
    public boolean onContextItemSelected(MenuItem item) {

        switch (item.getItemId()) {

            case 1:
                Toast.makeText(this, "Sửa nhân viên",
                        Toast.LENGTH_SHORT).show();
                return true;

            case 2:
                Toast.makeText(this, "Xóa nhân viên",
                        Toast.LENGTH_SHORT).show();
                return true;

            case 3:
                Toast.makeText(this, "Xem thông tin",
                        Toast.LENGTH_SHORT).show();
                return true;
        }

        return super.onContextItemSelected(item);
    }
}


5. Một điểm rất quan trọng: Lấy vị trí dòng được nhấn giữ
Khi sử dụng Context Menu với ListView, bạn có thể lấy vị trí dòng mà người dùng nhấn giữ thông qua menuInfo.

Ví dụ:
@Override
public void onContextMenuClosed(Menu menu) {
    super.onContextMenuClosed(menu);
}


Để lấy vị trí dòng, ta sử dụng trong onContextItemSelected():
@Override
public boolean onContextItemSelected(MenuItem item) {

    AdapterView.AdapterContextMenuInfo info =
            (AdapterView.AdapterContextMenuInfo) item.getMenuInfo();

    int position = info.position;

    Toast.makeText(this,
            "Bạn đang chọn dòng: " + position,
            Toast.LENGTH_SHORT).show();

    return true;
}


Ví dụ kết quả:
Vị trí	Nhân viên
0	Nguyễn Văn A
1	Trần Văn B
2	Lê Văn C

Nếu nhấn giữ Nguyễn Văn A thì position = 0.

Nếu nhấn giữ Trần Văn B thì position = 1.

Lưu ý: Nếu ListView có Header bằng addHeaderView(), vị trí info.position bao gồm cả Header. Ví dụ Header ở vị trí 0 thì nhân viên đầu tiên ở vị trí 1.

6. Phân biệt các hàm bạn đã học
Hàm	Công dụng
getLayoutInflater()	Lấy công cụ tạo giao diện
inflate()	Chuyển XML thành View
addHeaderView()	Thêm tiêu đề vào đầu ListView
registerForContextMenu()	Đăng ký menu khi nhấn giữ View
onCreateContextMenu()	Tạo nội dung menu
onContextItemSelected()	Xử lý lựa chọn menu

Mẹo nhớ khi đi thi thực hành Android:
- registerForContextMenu() → Đăng ký.
- onCreateContextMenu() → Tạo menu.
- onContextItemSelected() → Xử lý khi chọn menu.
Đây là 3 thành phần thường đi cùng nhau khi tạo chức năng Sửa/Xóa một phần tử trong ListView.
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
