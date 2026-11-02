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
- [widget.AdapterView Lớp cha chung quản lý tất cả các cấu trúc hiển thị dạng danh sách (ListView, GridView, Spinner...).](#widgetadapterview-lớp-cha-chung-quản-lý-tất-cả-các-cấu-trúc-hiển-thị-dạng-danh-sách-listview-gridview-spinner)
---
# TextView
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
# widget.AdapterView Lớp cha chung quản lý tất cả các cấu trúc hiển thị dạng danh sách (ListView, GridView, Spinner...).

Cú pháp: AdapterView<?> parent

Ví dụ độc lập:

Java
AdapterView<?> parentView = lvPhongBan;
System.out.println("Tong so item hien tai trong danh sach: " + parentView.getCount());
Output / Kết quả giả định khi println:

Plaintext
Tong so item hien tai trong danh sach: 3
11. getMenuInflater
Dùng để làm gì: Lấy ra bộ quản lý MenuInflater chuyên dùng để chuyển đổi file thiết kế XML menu thành đối tượng hiển thị thật.

Cú pháp: MenuInflater inflater = getMenuInflater();

Ví dụ độc lập:

Java
android.view.MenuInflater inflater = getMenuInflater();
System.out.println("Doi tuong MenuInflater: " + inflater);
Output / Kết quả giả định khi println:

Plaintext
Doi tuong MenuInflater: android.view.MenuInflater@7f8a2b1
12. inflate
Dùng để làm gì: Đọc file XML menu và "bơm" (vẽ) các mục menu lên đối tượng Menu hiển thị trên màn hình.

Cú pháp: inflater.inflate(R.menu.ten_file_xml, menu);

Ví dụ độc lập:

Java
// Trong ham onCreateContextMenu:
// getMenuInflater().inflate(R.menu.contextmenu_phongban, menu);
System.out.println("Da nap thanh cong file XML menu vao bo nho");
Output / Kết quả giả định khi println:

Plaintext
Da nap thanh cong file XML menu vao bo nho
13. AdapterContextMenuInfo
Dùng để làm gì: Chứa thông tin chi tiết về item trong Adapter bị nhấn giữ (quan trọng nhất là lấy ra số thứ tự position của dòng đó).

Cú pháp: AdapterView.AdapterContextMenuInfo info = (AdapterView.AdapterContextMenuInfo) item.getMenuInfo();

Ví dụ độc lập:

Java
// Gia su lay duoc info tu dong thu 1 (position = 1)
int position = 1;
System.out.println("Vi tri dong bi nhan giu: " + position);
Output / Kết quả giả định khi println:

Plaintext
Vi tri dong bi nhan giu: 1
14. getMenuInfo
Dùng để làm gì: Phương thức của MenuItem dùng để lấy về đối tượng chứa ngữ cảnh bổ sung của menu (như thông tin dòng bị nhấn giữ).

Cú pháp: item.getMenuInfo()

Ví dụ độc lập:

Java
// Object info = item.getMenuInfo();
System.out.println("Gia tri tra ve cua getMenuInfo la mot doi tuong ContextMenuInfo");
Output / Kết quả giả định khi println:

Plaintext
Gia tri tra ve cua getMenuInfo la mot doi tuong ContextMenuInfo
15. onContextItemSelected
Dùng để làm gì: Hàm hệ thống tự động chạy khi người dùng bấm vào một chức năng cụ thể trong bảng Context Menu.

Cú pháp: public boolean onContextItemSelected(MenuItem item)

Ví dụ độc lập:

Java
@Override
public boolean onContextItemSelected(MenuItem item) {
    System.out.println("ID cua muc menu vua duoc bam: " + item.getItemId());
    return super.onContextItemSelected(item);
}
Output / Kết quả giả định khi bấm nút Xóa phòng ban:

Plaintext
ID cua muc menu vua duoc bam: 2131230803
16. view.MenuItem
Dùng để làm gì: Đại diện cho từng mục/dòng lựa chọn nằm bên trong Menu.

Cú pháp: MenuItem item

Ví dụ độc lập:

Java
// String title = item.getTitle().toString();
String title = "Danh sach nhan vien";
System.out.println("Tieu de cua muc menu: " + title);
Output / Kết quả giả định khi println:

Plaintext
Tieu de menu: Danh sach nhan vien
17. AlertDialog
Dùng để làm gì: Tạo một hộp thoại cảnh báo dạng popup nổi lên giữa màn hình để hỏi xác nhận người dùng trước khi thực hiện việc quan trọng.

Cú pháp: AlertDialog.Builder builder = new AlertDialog.Builder(this);

Ví dụ độc lập:

Java
AlertDialog.Builder builder = new AlertDialog.Builder(null);
System.out.println("Da khoi tao AlertDialog.Builder thanh cong");
Output / Kết quả giả định khi println:

Plaintext
Da khoi tao AlertDialog.Builder thanh cong
18. content.DialogInterface
Dùng để làm gì: Giao diện điều khiển trạng thái của hộp thoại (dùng để ra lệnh tắt/hủy hộp thoại).

Cú pháp: DialogInterface dialog

Ví dụ độc lập:

Java
String action = "dialog.cancel() da tat hop thoại";
System.out.println(action);
Output / Kết quả giả định khi println:

Plaintext
dialog.cancel() da tat hop thoại
19. setNegativeButton
Dùng để làm gì: Tạo nút "Không / Hủy" trong hộp thoại AlertDialog.

Cú pháp: builder.setNegativeButton("Text", listener);

Ví dụ độc lập:

Java
System.out.println("Da tao xong nut tu choi trong AlertDialog");
Output / Kết quả giả định khi println:

Plaintext
Da tao xong nut tu choi trong AlertDialog
20. requestFocus
Dùng để làm gì: Ép bàn phím ảo hiển thị và đưa con trỏ nhấp nháy tập trung vào ô nhập liệu (EditText) chỉ định.

Cú pháp: editText.requestFocus();

Ví dụ độc lập:

Java
boolean kqFocus = true;
System.out.println("Con tro da nhay vao o EditText chua? " + kqFocus);
Output / Kết quả giả định khi println:

Plaintext
Con tro da nhay vao o EditText chua? true
21. Activity trong AndroidManifest.xml (kèm theme Dialog)
Dùng để làm gì: Khai báo màn hình phụ với hệ thống Android để tránh lỗi văng app, và cấu hình android:theme="@style/Theme.AppCompat.Dialog" để biến màn hình đó thành một khung pop-up nhỏ nổi lên trên màn hình chính thay vì che kín màn hình.

Cú pháp:

XML
<activity 
    android:name=".ThemNhanVienActivity"
    android:theme="@style/Theme.AppCompat.Dialog" />
Output / Hành vi thực tế trên máy ảo: Khi Intent gọi Activity này, ứng dụng không chuyển trang toàn màn hình mà hiện ra một khung Dialog nhỏ gọn nằm đè lên giao diện chính.