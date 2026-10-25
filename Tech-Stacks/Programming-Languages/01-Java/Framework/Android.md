- [Android Introduction (dùng để lập trình ứng dụng android)](#android-introduction-dùng-để-lập-trình-ứng-dụng-android)
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
    - [getCheckedRadioButtonID (Dùng trên đối tượng RadioGroup để xem người dùng đang tích chọn vào nút RadioButton nào trong nhóm)](#getcheckedradiobuttonid-dùng-trên-đối-tượng-radiogroup-để-xem-người-dùng-đang-tích-chọn-vào-nút-radiobutton-nào-trong-nhóm)
  - [RadioButton](#radiobutton)
    - [isChecked()](#ischecked)
  - [Toast](#toast)
    - [.makeText()](#maketext)
      - [.show()](#show)
  - [ArrayAdapter (là cầu nối giữa một List dữ liệu Java và một ListView trên giao diện)](#arrayadapter-là-cầu-nối-giữa-một-list-dữ-liệu-java-và-một-listview-trên-giao-diện)
    - [Ask](#ask)
      - [simple\_list\_item\_1 ở đâu?](#simple_list_item_1-ở-đâu)
      - [Tại sao phải truyền simple\_list\_item\_1?](#tại-sao-phải-truyền-simple_list_item_1)
    - [setAdapter](#setadapter)
    - [getCount() (có bao nhiêu phần tử)](#getcount-có-bao-nhiêu-phần-tử)
    - [getItem() (lấy phần tử)](#getitem-lấy-phần-tử)
    - [getItemId(position)](#getitemidposition)
    - [add() (thêm một phần tử)](#add-thêm-một-phần-tử)
    - [notifyDataSetChanged() (báo cho ListView cập nhật)](#notifydatasetchanged-báo-cho-listview-cập-nhật)
    - [getView() (tạo và vẽ giao diện cho từng dòng (item) trong danh sách ListView)](#getview-tạo-và-vẽ-giao-diện-cho-từng-dòng-item-trong-danh-sách-listview)
  - [ListView](#listview)
    - [setOnItemClickListener (lắng nghe sự kiện người dùng nhấp (click) vào một dòng bất kỳ trong ListView)](#setonitemclicklistener-lắng-nghe-sự-kiện-người-dùng-nhấp-click-vào-một-dòng-bất-kỳ-trong-listview)
    - [notifyDataSetChanged() (thông báo cho Adapter biết dữ liệu trong nguồn (list) đã thay đổi yêu cầu ListView tự động vẽ lại (refresh) giao diện ngay lập tức để cập nhật danh sách mới)](#notifydatasetchanged-thông-báo-cho-adapter-biết-dữ-liệu-trong-nguồn-list-đã-thay-đổi-yêu-cầu-listview-tự-động-vẽ-lại-refresh-giao-diện-ngay-lập-tức-để-cập-nhật-danh-sách-mới)
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
  - [Ask](#ask-1)
    - [tại sao chỗ này lại là view mà không phải TextView](#tại-sao-chỗ-này-lại-là-view-mà-không-phải-textview)
- [onClick()](#onclick)
- [setText()](#settext)
- [setOnCheckedChangeListener()](#setoncheckedchangelistener)
- [Intent](#intent)
  - [.putExtra()](#putextra)
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
### getCheckedRadioButtonID (Dùng trên đối tượng RadioGroup để xem người dùng đang tích chọn vào nút RadioButton nào trong nhóm)
**Syn**
```bash
- Output: 
    + Trả về một số nguyên (int) chính là ID của RadioButton đang được chọn 
    + Nếu không có nút nào được chọn, nó trả về -1.
```
**Ex**
```java
int checkedId = radioGroup.getCheckedRadioButtonId();

RadioButton radioButton = findViewById(checkedId);

String value = radioButton.getText().toString();

// Ví dụ người dùng chọn Nam:
String value = radioButton.getText().toString(); // value = "Nam"
```
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
**Syn**
```bash
ArrayAdapter<String> adapter = new ArrayAdapter<>(
        this,                              // Context
        android.R.layout.simple_list_item_1, // Layout cho từng item
        names                              // Dữ liệu
);

- Input:
    + this: Context của Activity hiện tại.
    + android.R.layout.simple_list_item_1: layout dùng để hiển thị mỗi dòng.
    + names: mảng dữ liệu cần đưa vào list view.
```
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
### Ask 
#### simple_list_item_1 ở đâu?
```bash
Nó nằm bên trong Android SDK/framework, không nằm trong thư mục:

app/
└── src/
    └── main/
        └── res/
            └── layout/

Bạn sẽ không thấy: res/layout/simple_list_item_1.xml trong project của mình.

Thay vào đó: android.R.layout.simple_list_item_1
    có nghĩa là:
        android
          └── R
              └── layout
                  └── simple_list_item_1
        android.R là class R do Android framework cung cấp.

3. Nó thực chất là một layout

simple_list_item_1 là layout đơn giản của Android dùng để hiển thị một dòng text.

Có thể hình dung gần giống:

<TextView
    ...
/>

Tức là khi bạn có:

String[] names = {
    "Nguyễn Văn A",
    "Trần Văn B",
    "Lê Đức Thắng"
};

thì ArrayAdapter sẽ lấy simple_list_item_1 làm khuôn mẫu cho từng dòng:

┌─────────────────────────┐
│ Nguyễn Văn A             │ ← simple_list_item_1
├─────────────────────────┤
│ Trần Văn B               │ ← simple_list_item_1
├─────────────────────────┤
│ Lê Đức Thắng             │ ← simple_list_item_1
└─────────────────────────┘

Có nghĩa là:

names
  ↓
ArrayAdapter
  ↓
simple_list_item_1
  ↓
ListView
```
#### Tại sao phải truyền simple_list_item_1?
```bash
Vì ArrayAdapter cần biết:

"Tôi phải dùng giao diện nào để vẽ mỗi phần tử trong danh sách?"

Ví dụ:

new ArrayAdapter<>(
    this,
    android.R.layout.simple_list_item_1,
    names
);

nói với Android:

"Lấy từng String trong names, đưa nó vào layout simple_list_item_1, sau đó tạo các dòng trong ListView."

1. Bạn cũng có thể tự tạo layout

Ví dụ bạn muốn mỗi dòng đẹp hơn, có:

┌──────────────────────────────┐
│ Nguyễn Văn A                 │
│ Sinh viên                    │
└──────────────────────────────┘

thì không nhất thiết dùng:

android.R.layout.simple_list_item_1

Bạn có thể tự tạo:

res
└── layout
    └── item_user.xml

Ví dụ:

<TextView
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:id="@+id/txtName"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:textSize="20sp"
    android:padding="16dp" />

Sau đó:

ArrayAdapter<String> adapter = new ArrayAdapter<>(
        this,
        R.layout.item_user,
        R.id.txtName,
        names
);

Ở đây sẽ có thêm:

R.id.txtName

vì Adapter cần biết String sẽ được đặt vào TextView nào trong item_user.xml.

Tóm lại
ArrayAdapter<String> adapter = new ArrayAdapter<>(
        this,
        android.R.layout.simple_list_item_1,
        names
);

có thể đọc thành:

Tạo một Adapter cho dữ liệu kiểu String, dùng Activity hiện tại làm Context, dùng layout simple_list_item_1 của Android làm giao diện cho từng dòng, và lấy dữ liệu từ mảng names.

Còn:

android.R.layout.simple_list_item_1

là layout có sẵn của Android, không phải layout trong project của bạn
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
### notifyDataSetChanged() (báo cho ListView cập nhật)
```bash

Có thể hình dung:
    Dữ liệu thay đổi -> notifyDataSetChanged() -> Adapter thông báo -> ListView cập nhật -> Màn hình thay đổi
```
**Syn**
```bash
adapterPerson.notifyDataSetChanged();
```
### getView() (tạo và vẽ giao diện cho từng dòng (item) trong danh sách ListView)
**Syn**
```bash
@Override
public View getView(int position, View convertView, ViewGroup parent) { ... }

- int position: Vị trí (chỉ số index) của dòng hiện tại trong mảng list (bắt đầu từ 0, 1, 2...).
- View convertView: Ô nhớ chứa giao diện cũ được tái sử dụng (giúp tối ưu bộ nhớ, tránh việc phải tạo mới giao diện liên tục khi người dùng cuộn danh sách lên xuống).
- ViewGroup parent: ViewGroup chứa danh sách này (chính là cái ListView).
```
## ListView
### setOnItemClickListener (lắng nghe sự kiện người dùng nhấp (click) vào một dòng bất kỳ trong ListView)
**syn**
```bash
listView.setOnItemClickListener(new AdapterView.OnItemClickListener() {
    @Override
    public void onItemClick(AdapterView<?> parent, View view, int position, long id) {
        // Xử lý khi click vào dòng
    }
});

- Input:
    + onItemClick: Hàm tự động chạy khi hành động click xảy ra.
    + Input (Các tham số):
    + AdapterView<?> parent: Đại diện cho ListView.
    + View view: Giao diện của dòng cụ thể vừa bị click vào.
    + int position: Vị trí dòng vừa được click (cực kỳ quan trọng để biết người dùng đang chọn phần tử thứ mấy trong list).
    + long id: ID của dòng được chọn.
- Output: Không có (void).
```
radTv.setChecked(true) và radCt.setChecked(true) là gì?
Ý nghĩa: Dùng để lập trình đánh dấu tích chọn (hoặc bỏ chọn) cho một RadioButton.

Truyền vào true: Bật tích chọn (nút tròn sáng lên).

Truyền vào false: Bỏ tích chọn.

Trong ngữ cảnh code của bạn: Khi người dùng bấm vào một dòng nhân viên trong danh sách, ứng dụng sẽ đọc xem nhân viên đó là "thời vụ" hay "chính thức" để tự động tích sáng nút tròn tương ứng trên form.

7. Hàm maNV.requestFocus() là gì?
Ý nghĩa: Lệnh dùng để đưa con trỏ chuột (focus) nhấp nháy tập trung vào ô nhập liệu (EditText) đó.

Ứng dụng: Thường được gọi sau khi bấm Thêm/Sửa/Xóa xong để con trỏ tự động nhảy về ô nhập "Mã NV", giúp người dùng có thể gõ tiếp dữ liệu mới ngay lập tức mà không cần dùng tay bấm vào màn hình điện thoại.

8. Giải thích khối code khi click chọn dòng trong ListView:
Java
listView.setOnItemClickListener(new AdapterView.OnItemClickListener() {
    @Override
    public void onItemClick(AdapterView<?> parent, View view, int position, long id) {
        selectedIndex = position; // 1. Lưu lại vị trí dòng đang chọn
        Person p = list.get(position); // 2. Lấy đối tượng Person tại vị trí đó ra

        // 3. Đẩy thông tin của nhân viên đó ngược lại lên các ô EditText trên form
        maNV.setText(p.id);
        tenNV.setText(p.name);
        
        // 4. Kiểm tra loại nhân viên để tích chọn RadioButton tương ứng
        if (p.type.equals("thời vụ")) {
            radTv.setChecked(true);
        } else {
            radCt.setChecked(true);
        }
    }
});
Giải thích tổng quát: Đoạn code này thực hiện tính năng Read / Select (Xem lại / Chọn). Khi bạn chạm tay vào bất kỳ dòng nào trong danh sách nhân viên, thông tin của nhân viên đó sẽ được điền tự động ngược lại lên các ô nhập liệu phía trên để bạn xem hoặc chuẩn bị bấm nút Sửa / Xóa.

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
### notifyDataSetChanged() (thông báo cho Adapter biết dữ liệu trong nguồn (list) đã thay đổi yêu cầu ListView tự động vẽ lại (refresh) giao diện ngay lập tức để cập nhật danh sách mới)
**Syn**
```bash
adapterPerson.notifyDataSetChanged();.
```
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
**Syn**
```bash
button.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View v) {

    }
});

- Input:
    + button: nút bấm mà chúng ta muốn theo dõi.
    + setOnClickListener(...): đăng ký một bộ lắng nghe sự kiện bấm nút.
    + new View.OnClickListener(): tạo một đối tượng thực hiện nhiệm vụ lắng nghe sự kiện.
    + onClick(View v): hàm được Android gọi tự động khi người dùng bấm nút.
    + @Override: cho biết chúng ta đang viết lại hàm onClick() được quy định trong View.OnClickListener.
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
# onClick()
# setText()
# setOnCheckedChangeListener()
```bash
Nếu bạn có 2 RadioButton trong cùng một RadioGroup, cách đơn giản nhất trong Java là bắt sự kiện bằng setOnCheckedChangeListener() của RadioGroup.
```
**Ex**
*XML*
```xml
<RadioGroup
    android:id="@+id/radioGroup"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content">

    <RadioButton
        android:id="@+id/radioNam"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Nam" />

    <RadioButton
        android:id="@+id/radioNu"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Nữ" />

</RadioGroup>
```
```java
RadioGroup radioGroup = findViewById(R.id.radioGroup);

radioGroup.setOnCheckedChangeListener(new RadioGroup.OnCheckedChangeListener() {
    @Override
    public void onCheckedChanged(RadioGroup group, int checkedId) {

        if (checkedId == R.id.radioNam) {
            // Người dùng chọn Nam
        }
        else if (checkedId == R.id.radioNu) {
            // Người dùng chọn Nữ
        }
    }
});

Điểm quan trọng là:

checkedId

chính là ID của RadioButton đang được chọn.

Ví dụ:

RadioGroup
│
├── radioNam  ← chọn cái này
│
└── radioNu

thì:

checkedId == R.id.radioNam

sẽ là true.


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
```
# Intent
// Viết bên trong sự kiện click nút (ví dụ: nút "Mở trang mới")
Intent intent = new Intent(MainActivity.this, SecondActivity.class);
startActivity(intent);
## .putExtra()
Intent intent = new Intent(MainActivity.this, DetailActivity.class);
intent.putExtra("maNhanVien", "NV01"); // Đính kèm dữ liệu (Key - Value)
startActivity(intent);

Intent intent = getIntent(); // Nhận intent gửi sang
String ma = intent.getStringExtra("maNhanVien"); // Lấy dữ liệu ra theo Key
PHẦN 2: OPTIONS MENU (Menu trên thanh tiêu cao / Toolbar góc phải trên)
Dùng khi: Đề bài yêu cầu tạo thanh menu phía góc trên bên phải (ví dụ: menu gồm các chức năng "Thêm", "Tìm kiếm", "Thoát").

Bước 1: Tạo file XML cho Menu
Tạo file menu_main.xml trong thư mục res/menu (nếu chưa có thư mục menu thì click phải vào res 
→ New 
→ Android Resource Directory 
→ chọn type là menu):

XML
<?xml version="1.0" encoding="utf-8"?>
<menu xmlns:android="http://schemas.android.com/apk/res/android"
      xmlns:app="http://schemas.android.com/apk/res-auto">
    <item
        android:id="@+id/menuThem"
        android:title="Thêm mới"
        app:showAsAction="ifRoom" />
    <item
        android:id="@+id/menuThoat"
        android:title="Thoát"
        app:showAsAction="never" />
</menu>
Bước 2: Viết code trong MainActivity.java
Java
// 1. Nạp menu lên giao diện
@Override
public boolean onCreateOptionsMenu(Menu menu) {
    getMenuInflater().inflate(R.menu.menu_main, menu);
    return true;
}

// 2. Bắt sự kiện khi người dùng bấm vào các mục trong menu
@Override
public boolean onOptionsItemSelected(MenuItem item) {
    int id = item.getItemId();
    if (id == R.id.menuThem) {
        // Xử lý khi bấm nút Thêm
        Toast.makeText(this, "Bạn chọn Thêm mới", Toast.LENGTH_SHORT).show();
        return true;
    } else if (id == R.id.menuThoat) {
        finish(); // Thoát ứng dụng
        return true;
    }
    return super.onOptionsItemSelected(item);
}
PHẦN 3: CONTEXT MENU (Menu nhấn giữ vào ListView - Rất hay ra thi!)
Dùng khi: Đề bài yêu cầu nhấn giữ (long click) vào một dòng nhân viên trong ListView, lập tức hiện ra bảng menu nhỏ có chữ "Sửa" hoặc "Xóa".

Cú pháp chuẩn bị và xử lý (Thêm vào onCreate của MainActivity):
Java
// 1. Đăng ký ListView nhận Context Menu
registerForContextMenu(listView);
Java
// 2. Tạo giao diện menu khi người dùng nhấn giữ
@Override
public void onCreateContextMenu(ContextMenu menu, View v, ContextMenu.ContextMenuInfo menuInfo) {
    super.onCreateContextMenu(menu, v, menuInfo);
    getMenuInflater().inflate(R.menu.context_menu, menu); // Bạn tạo 1 file menu_context.xml tương tự phần trên
    // Hoặc tạo code thuần:
    menu.add(0, 1, 0, "Sửa");
    menu.add(0, 2, 0, "Xóa");
}

// 3. Bắt sự kiện chọn Xóa / Sửa trong bảng menu nhấn giữ
@Override
public boolean onContextItemSelected(MenuItem item) {
    // Lấy vị trí dòng bị nhấn giữ
    AdapterView.AdapterContextMenuInfo info = (AdapterView.AdapterContextMenuInfo) item.getMenuInfo();
    int position = info.position; 

    if (item.getTitle().equals("Xóa")) {
        list.remove(position);
        adapterPerson.notifyDataSetChanged();
        Toast.makeText(this, "Đã xóa!", Toast.LENGTH_SHORT).show();
    } else if (item.getTitle().equals("Sửa")) {
        // Lấy dữ liệu dòng đó đưa lên form để sửa
        Person p = list.get(position);
        nhapMa.setText(p.id);
        nhapTen.setText(p.name);
        selectedIndex = position; // Gán lại để lát bấm nút Sửa cập nhật
    }
    return super.onContextItemSelected(item);
}
PHẦN 4: ADAPTER NÂNG CAO (BaseAdapter)
Khi nào dùng: Nếu đề bài yêu cầu giao diện danh sách phức tạp hơn (ví dụ: trong mỗi dòng của ListView ngoài chữ ra còn có kèm 1 cái nút bấm riêng để xóa nhanh dòng đó ngay trên list), lúc này ArrayAdapter thông thường không làm được mà phải dùng BaseAdapter.

Cú pháp khung của một BaseAdapter tự chế:
Java
BaseAdapter myAdapter = new BaseAdapter() {
    @Override
    public int getCount() {
        return list.size(); // Trả về tổng số phần tử trong mảng
    }

    @Override
    public Object getItem(int position) {
        return list.get(position);
    }

    @Override
    long getItemId(int position) {
        return position;
    }

    @Override
    public View getView(int position, View convertView, ViewGroup parent) {
        // Nạp layout từng dòng (item_person.xml)
        View view = getLayoutInflater().inflate(R.layout.item_person, parent, false);
        
        // Ánh xạ các TextView trong dòng và gán dữ liệu
        TextView tvName = view.findViewById(R.id.name);
        tvName.setText(list.get(position).name);

        // (Nếu có nút xóa riêng trong dòng thì bắt sự kiện ở đây luôn)
        
        return view;
    }
};
listView.setAdapter(myAdapter);
📌 Chiến lược ôn tập cho bạn:
Ưu tiên số 1: Nắm vững phần Intent chuyển trang và Truyền dữ liệu (vì đề thi phân chia các chức năng ra các màn hình rất hay dùng).

Ưu tiên số 2: Xem lại kỹ phần Context Menu (Nhấn giữ ListView) vì các thầy cô cực kỳ thích ra câu lệnh này kết hợp với CRUD.

Bạn có muốn tôi cho một bài tập tổng hợp kết hợp cả Intent + CRUD để luyện tập ngay bây giờ không?