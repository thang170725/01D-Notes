- [Android Introduction (dùng để lập trình ứng dụng android)](#android-introduction-dùng-để-lập-trình-ứng-dụng-android)
- [onCreate()](#oncreate)
- [app (chứa các class liên quan đến ứng dụng Android và các thành phần cấp ứng dụng)](#app-chứa-các-class-liên-quan-đến-ứng-dụng-android-và-các-thành-phần-cấp-ứng-dụng)
  - [Activity (Một màn hình Android truyền thống thường là một Activity)](#activity-một-màn-hình-android-truyền-thống-thường-là-một-activity)
  - [DatePickerDialog (Hộp thoại chọn ngày)](#datepickerdialog-hộp-thoại-chọn-ngày)
  - [TimePickerDialog (Hộp thoại chọn giờ)](#timepickerdialog-hộp-thoại-chọn-giờ)
- [os (các API liên quan đến hệ thống Android / operating system)](#os-các-api-liên-quan-đến-hệ-thống-android--operating-system)
  - [Bundle (một class của Android dùng để chứa dữ liệu dạng key-value)](#bundle-một-class-của-android-dùng-để-chứa-dữ-liệu-dạng-key-value)
- [view (dùng khi làm giao diện Android)](#view-dùng-khi-làm-giao-diện-android)
  - [View (class cơ bản đại diện cho một thành phần giao diện)](#view-class-cơ-bản-đại-diện-cho-một-thành-phần-giao-diện)
    - [View.OnClickListener](#viewonclicklistener)
- [widget](#widget)
  - [TextView](#textview)
  - [EditText](#edittext)
  - [RadioGroup](#radiogroup)
  - [RadioButton](#radiobutton)
    - [isChecked()](#ischecked)
  - [Toast](#toast)
    - [.makeText()](#maketext)
      - [.show()](#show)
  - [ArrayAdapter (là cầu nối giữa một List dữ liệu Java và một ListView trên giao diện)](#arrayadapter-là-cầu-nối-giữa-một-list-dữ-liệu-java-và-một-listview-trên-giao-diện)
    - [setAdapter](#setadapter)
    - [getCount() (có bao nhiêu phần tử)](#getcount-có-bao-nhiêu-phần-tử)
    - [getItem() (lấy phần tử)](#getitem-lấy-phần-tử)
    - [getItemId(position)](#getitemidposition)
    - [add() (thêm một phần tử)](#add-thêm-một-phần-tử)
- [content (Thông tin môi trường của ứng dụng hiện tại để Android biết bạn đang thao tác trong app nào)](#content-thông-tin-môi-trường-của-ứng-dụng-hiện-tại-để-android-biết-bạn-đang-thao-tác-trong-app-nào)
  - [Context](#context)
- [graphics (Liên quan đến đồ họa, hình ảnh, vẽ)](#graphics-liên-quan-đến-đồ-họa-hình-ảnh-vẽ)
- [net (Liên quan đến network URI Internet)](#net-liên-quan-đến-network-uri-internet)
  - [Uri](#uri)
- [database (Liên quan đến database và dữ liệu dạng bảng)](#database-liên-quan-đến-database-và-dữ-liệu-dạng-bảng)
- [findViewById (Lấy các thành phần từ XML)](#findviewbyid-lấy-các-thành-phần-từ-xml)
  - [.setText() (dùng để gán nội dung cho TextView, EditText, ...)](#settext-dùng-để-gán-nội-dung-cho-textview-edittext-)
  - [getText() (Dùng để lấy nội dung hiện tại của TextView hoặc EditView)](#gettext-dùng-để-lấy-nội-dung-hiện-tại-của-textview-hoặc-editview)
  - [setTextSize() (dùng để thay đổi kích thước chữ)](#settextsize-dùng-để-thay-đổi-kích-thước-chữ)
  - [.setVisibility() (Thay đổi trạng thái hiển thị View)](#setvisibility-thay-đổi-trạng-thái-hiển-thị-view)
  - [.getVisibility() (Lấy trạng thái hiển thị hiện tại của TextView)](#getvisibility-lấy-trạng-thái-hiển-thị-hiện-tại-của-textview)
- [setOnClickListener (Lắng nghe sự kiện bấm nút)](#setonclicklistener-lắng-nghe-sự-kiện-bấm-nút)
  - [Ask](#ask)
    - [tại sao chỗ này lại là view mà không phải TextView](#tại-sao-chỗ-này-lại-là-view-mà-không-phải-textview)
- [Practices](#practices)
  - [4.9](#49)
- [onClick()](#onclick)
- [setText()](#settext)
---
# Android Introduction (dùng để lập trình ứng dụng android)
```bash
android.* là Android Framework API. Android cung cấp sẵn rất nhiều class để lập trình ứng dụng.
    - android.app
    - android.os
    - android.view
    - android.widget
    - android.content
    - android.graphics
    - android.database
    - android.net
    - android.provider
    - ...

Bạn có thể hình dung Android SDK như một hộp công cụ khổng lồ:
    Android SDK
    │
    ├── android.app
    ├── android.os
    ├── android.view
    ├── android.widget
    ├── android.content
    ├── android.graphics
    ├── android.database
    ├── android.net
    ├── android.provider
    └── ...
-> Mỗi package chứa các class phục vụ một nhóm chức năng.
```
# onCreate()
# app (chứa các class liên quan đến ứng dụng Android và các thành phần cấp ứng dụng)
## Activity (Một màn hình Android truyền thống thường là một Activity)
**Ex: Activity**
```java
public class MainActivity extends Activity {
}
```
## DatePickerDialog (Hộp thoại chọn ngày)
```java
DatePickerDialog dialog = new DatePickerDialog(...);

// Nó sẽ hiện kiểu:
// ┌─────────────────────┐
// │     Select date     │
// │                     │
// │    30 / 09 / 2026   │
// │                     │
// │       CANCEL  OK    │
// └─────────────────────┘
```
## TimePickerDialog (Hộp thoại chọn giờ)
# os (các API liên quan đến hệ thống Android / operating system)
## Bundle (một class của Android dùng để chứa dữ liệu dạng key-value)
```bash
Có thể hình dung nó như một cái hộp:
    Bundle
    ┌───────────────────────┐
    │ "name" → "Thắng"      │
    │ "age"  → 25           │
    │ "score" → 100         │
    └───────────────────────┘
-> Android có thể sử dụng Bundle để lưu/khôi phục một số trạng thái của Activity khi cần.
```
**Ex**
```java
@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
}


Bundle data = new Bundle();

data.putString("name", "Thang");
data.putInt("age", 20);

String name = data.getString("name");
int age = data.getInt("age");
```
# view (dùng khi làm giao diện Android)
## View (class cơ bản đại diện cho một thành phần giao diện)
### View.OnClickListener
# widget 
```bash
Nó chứa các widget UI như:
    - import android.widget.Button;
    - import android.widget.TextView;
    - import android.widget.EditText;
    - import android.widget.ImageView;
    - import android.widget.DatePicker;
    - import android.widget.CheckBox;
```
## TextView
## EditText
## RadioGroup
## RadioButton
### isChecked()
## Toast
### .makeText()
**Syn**
```bash
Toast.makeText(context, text, duration)

- Input:
    + context: Hiển thị ở màn hình nào?
    + text: Nội dung thông báo
    + duration: Hiển thị trong bao lâu?
```
**Ex**
```java
Toast.makeText(MainActivity.this, "Vui lòng nhập đầy đủ 2 số!", Toast.LENGTH_SHORT).show();
```
#### .show()
## ArrayAdapter (là cầu nối giữa một List dữ liệu Java và một ListView trên giao diện)
**Ex: Ví dụ bạn có**
```java
List<String> names = Arrays.asList(
    "Nguyễn Văn A",
    "Trần Văn B",
    "Lê Đức Thắng"
);

// Bạn muốn biến nó thành:
// ┌─────────────────────┐
// │ Nguyễn Văn A        │
// ├─────────────────────┤
// │ Trần Văn B          │
// ├─────────────────────┤
// │ Lê Đức Thắng        │
// └─────────────────────┘
// -> thì ArrayAdapter giúp làm việc đó.
```
**Ex2**
*xml*
```xml
<ListView
    android:id="@+id/listView"
    android:layout_width="match_parent"
    android:layout_height="match_parent"/>
```
*java*
```java
ListView listView = findViewById(R.id.listView);

String[] names = {
    "Nguyễn Văn A",
    "Trần Văn B",
    "Lê Đức Thắng"
};

ArrayAdapter<String> adapter = new ArrayAdapter<>(
        this,
        android.R.layout.simple_list_item_1,
        names
);

listView.setAdapter(adapter);
```
### setAdapter
### getCount() (có bao nhiêu phần tử)
Một method thường gặp:

adapter.getCount();

Ví dụ:

String[] names = {
    "Nguyễn Văn A",
    "Trần Văn B",
    "Lê Đức Thắng"
};

thì:

int count = adapter.getCount();

Kết quả:

count = 3

Có thể dùng:

if (adapter.getCount() == 0) {
    // Không có dữ liệu
}
### getItem() (lấy phần tử)
Cú pháp:

adapter.getItem(position);

Ví dụ:

String name = adapter.getItem(0);

Kết quả:

name = "Nguyễn Văn A"

Tiếp:

String name = adapter.getItem(2);

Kết quả:

name = "Lê Đức Thắng"

Nếu:

position
   ↓
    0 → Nguyễn Văn A
    1 → Trần Văn B
    2 → Lê Đức Thắng

thì:

adapter.getItem(1);

→ "Trần Văn B".

### getItemId(position)

Method:

adapter.getItemId(position);

Dùng để lấy ID của item tại vị trí đó.

Ví dụ:

long id = adapter.getItemId(1);

Với ArrayAdapter thông thường, giá trị thường liên quan đến vị trí item.

Ví dụ có thể nhận:

id = 1

Trong phần lớn ứng dụng đơn giản, bạn không cần tự gọi method này.

### add() (thêm một phần tử)

Đây là method rất hữu ích.

Ví dụ:

adapter.add("Phạm Văn C");

Ban đầu:

Nguyễn Văn A
Trần Văn B
Lê Đức Thắng

Sau:

adapter.add("Phạm Văn C");

thành:

Nguyễn Văn A
Trần Văn B
Lê Đức Thắng
Phạm Văn C
Lưu ý

Adapter phải cho phép thay đổi dữ liệu. Với dữ liệu tạo từ Arrays.asList() đôi khi add() sẽ gây lỗi vì danh sách không hỗ trợ thay đổi kích thước.

An toàn hơn:

ArrayList<String> names = new ArrayList<>();

names.add("Nguyễn Văn A");
names.add("Trần Văn B");
names.add("Lê Đức Thắng");

remove() — xóa phần tử

Cú pháp:

adapter.remove("Trần Văn B");

Ban đầu:

Nguyễn Văn A
Trần Văn B
Lê Đức Thắng

Sau:

adapter.remove("Trần Văn B");

Kết quả:

Nguyễn Văn A
Lê Đức Thắng
10. clear() — xóa toàn bộ
adapter.clear();

Trước:

Nguyễn Văn A
Trần Văn B
Lê Đức Thắng

Sau:

adapter.clear();

→ danh sách rỗng:

ListView
┌───────────────────────┐
│                       │
│       Không có gì     │
│                       │
└───────────────────────┘
11. notifyDataSetChanged() — báo cho ListView cập nhật

Đây là method rất quan trọng.

Ví dụ:

adapter.add("Phạm Văn C");

thường Adapter sẽ xử lý cập nhật, nhưng khi bạn thay đổi dữ liệu gốc theo cách khác, bạn thường cần:

adapter.notifyDataSetChanged();

Ví dụ:

names.add("Phạm Văn C");

adapter.notifyDataSetChanged();

Ý nghĩa:

"Dữ liệu của tôi vừa thay đổi, hãy vẽ lại ListView."

Có thể hình dung:

Dữ liệu thay đổi
      ↓
notifyDataSetChanged()
      ↓
Adapter thông báo
      ↓
ListView cập nhật
      ↓
Màn hình thay đổi
12. insert()

Thêm một phần tử vào vị trí cụ thể:

adapter.insert("Lê Văn D", 1);

Ví dụ ban đầu:

0 Nguyễn Văn A
1 Trần Văn B
2 Lê Đức Thắng

Sau:

adapter.insert("Lê Văn D", 1);

Kết quả:

0 Nguyễn Văn A
1 Lê Văn D
2 Trần Văn B
3 Lê Đức Thắng
13. getView() — method quan trọng nhất khi custom Adapter

Đây chính là method bạn vừa hỏi ở MyItemList.

ArrayAdapter có:

public View getView(
    int position,
    View convertView,
    ViewGroup parent
)

Nhiệm vụ:

Tạo/trả về giao diện của một dòng trong ListView.

Ví dụ:

position = 0
    ↓
giao diện dòng 0

position = 1
    ↓
giao diện dòng 1

position = 2
    ↓
giao diện dòng 2

Đây là lý do MyItemList của bạn viết:

@Override
public View getView(
        int position,
        View convertView,
        ViewGroup parent
) {

Bạn đang override getView() của ArrayAdapter để tự quyết định mỗi dòng phải hiển thị như thế nào.

14. Đây là điểm quan trọng nhất của ArrayAdapter

Nếu dùng:

ArrayAdapter<String>

mặc định:

ArrayAdapter<String> adapter =
        new ArrayAdapter<>(
                this,
                android.R.layout.simple_list_item_1,
                names
        );

thì Android tự xử lý việc tạo dòng.

Bạn chỉ cần:

Dữ liệu
  ↓
ArrayAdapter
  ↓
ListView

Nhưng nếu muốn mỗi dòng phức tạp:

┌─────────────────────────────┐
│ ID: 103                     │
│ Họ tên: Lê Đức Thắng        │
│ Nhân viên chính thức        │
│ Mức lương: 12000k           │
└─────────────────────────────┘

thì bạn có thể tạo class:

public class MyItemList extends ArrayAdapter<NhanVien>

và override:

@Override
public View getView(...) {
    ...
}

Khi đó:

NhanVien
    ↓
MyItemList
    ↓
getView()
    ↓
item_nhanvien.xml
    ↓
View
    ↓
ListView
15. ArrayAdapter<NhanVien> nghĩa là gì?

Trong code của bạn:

public class MyItemList extends ArrayAdapter<NhanVien>

ArrayAdapter có dạng tổng quát:

ArrayAdapter<T>

T là kiểu dữ liệu.

Ví dụ:

ArrayAdapter<String>

→ quản lý:

String
ArrayAdapter<Integer>

→ quản lý:

Integer
ArrayAdapter<NhanVien>

→ quản lý:

NhanVien

Vì vậy:

NhanVien nv = list.get(position);

rất hợp lý.
# content (Thông tin môi trường của ứng dụng hiện tại để Android biết bạn đang thao tác trong app nào)
## Context
**Ex**
*xml*
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:gravity="center"
    android:orientation="vertical">

    <Button
        android:id="@+id/button"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Bấm vào đây" />

</LinearLayout>
```
```java
package com.example.test1;

import android.os.Bundle;
import android.widget.Button;
import android.widget.Toast;

import androidx.appcompat.app.AppCompatActivity;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        setContentView(R.layout.activity_main);

        Button button = findViewById(R.id.button);

        button.setOnClickListener(v -> {

            Toast.makeText(
                    MainActivity.this,
                    "Xin chào Lê Đức Thắng!",
                    Toast.LENGTH_SHORT
            ).show();

        });
    }
}
```
*Kết quả*
```bash
┌──────────────────────────┐
│                          │
│      [ Bấm vào đây ]     │
│                          │
└──────────────────────────┘

          ↓ bấm

┌──────────────────────────┐
│                          │
│      [ Bấm vào đây ]     │
│                          │
│  ┌────────────────────┐  │
│  │ Xin chào Lê Đức... │  │
│  └────────────────────┘  │
└──────────────────────────┘
```
# graphics (Liên quan đến đồ họa, hình ảnh, vẽ)
```bash
Bạn sẽ dùng khi cần:
    - xử lý Bitmap
    - vẽ
    - màu sắc
    - Canvas
    - Paint
    - hình học
```
# net (Liên quan đến network URI Internet)
## Uri
```bash
Uri xuất hiện rất nhiều khi làm:
    - URL
    - file
    - content provider
    - mở trình duyệt
    - chọn file
```
# database (Liên quan đến database và dữ liệu dạng bảng)
# findViewById (Lấy các thành phần từ XML)
```bash
findViewById(...) là hàm tìm một thành phần giao diện trong XML thông qua ID.
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
# setOnClickListener (Lắng nghe sự kiện bấm nút)
```java
button.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View v) {

    }
});

// button: nút bấm mà chúng ta muốn theo dõi.
// setOnClickListener(...): đăng ký một bộ lắng nghe sự kiện bấm nút.
// new View.OnClickListener(): tạo một đối tượng thực hiện nhiệm vụ lắng nghe sự kiện.
// onClick(View v): hàm được Android gọi tự động khi người dùng bấm nút.
// @Override: cho biết chúng ta đang viết lại hàm onClick() được quy định trong View.OnClickListener.
```
## Ask
### tại sao chỗ này lại là view mà không phải TextView 
```java
button.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View v) {

        if (content.getVisibility() == View.GONE) {
            // Nếu chữ đang ẩn thì hiện chữ
            content.setVisibility(View.VISIBLE);
        } else {
            // Nếu chữ đang hiện thì ẩn chữ
            content.setVisibility(View.GONE);
        }

    }
});
```
```bash
Vì View ở đây không phải là cái Button, mà là kiểu dữ liệu cha (class cha) của rất nhiều thành phần giao diện Android, trong đó có Button và TextView.
    - Button thực chất cũng là một View
```
# Practices
## 4.9
package com.example.test1;

import android.app.DatePickerDialog;
import android.app.TimePickerDialog;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.DatePicker;
import android.widget.TextView;
import android.widget.TimePicker;

import androidx.appcompat.app.AppCompatActivity;

import java.util.Calendar;

public class MainActivity extends AppCompatActivity {

    TextView txtHienThi;
    Button btnDate, btnTime;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        // Ánh xạ view
        txtHienThi = findViewById(R.id.txtHienThi);
        btnDate = findViewById(R.id.btnDate);
        btnTime = findViewById(R.id.btnTime);

        // Sự kiện nút chọn ngày
        btnDate.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                showDatePicker();
            }
        });

        // Sự kiện nút chọn giờ
        btnTime.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                showTimePicker();
            }
        });
    }

    private void showDatePicker() {
        Calendar c = Calendar.getInstance();   // lấy ngày hiện tại
        int year = c.get(Calendar.YEAR);
        int month = c.get(Calendar.MONTH);
        int day = c.get(Calendar.DAY_OF_MONTH);

        DatePickerDialog dialog = new DatePickerDialog(this,
                new DatePickerDialog.OnDateSetListener() {
                    @Override
                    public void onDateSet(DatePicker view, int y, int m, int d) {
                        // month tính từ 0 nên phải + 1
                        txtHienThi.setText("Ngày đã chọn: " + d + "/" + (m + 1) + "/" + y);
                    }
                }, year, month, day);
        dialog.show();
    }

    private void showTimePicker() {
        Calendar c = Calendar.getInstance();   // lấy giờ hiện tại
        int hour = c.get(Calendar.HOUR_OF_DAY);
        int minute = c.get(Calendar.MINUTE);

        TimePickerDialog dialog = new TimePickerDialog(this,
                new TimePickerDialog.OnTimeSetListener() {
                    @Override
                    public void onTimeSet(TimePicker view, int h, int min) {
                        txtHienThi.setText(String.format("Giờ đã chọn: %02d:%02d", h, min));
                    }
                }, hour, minute, true);   // true = định dạng 24h
        dialog.show();
    }
}

<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="8dp">

    <TextView
        android:id="@+id/txtHienThi"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="HienThi"
        android:textSize="18sp" />

    <Button
        android:id="@+id/btnDate"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Show Date Picker" />

    <Button
        android:id="@+id/btnTime"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Show Time Picker" />

</LinearLayout>


# onClick()
# setText()
