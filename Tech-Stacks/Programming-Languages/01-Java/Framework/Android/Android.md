- [Android Introduction (dùng để lập trình ứng dụng android)](#android-introduction-dùng-để-lập-trình-ứng-dụng-android)
- [app (chứa các class liên quan đến ứng dụng Android và các thành phần cấp ứng dụng)](#app-chứa-các-class-liên-quan-đến-ứng-dụng-android-và-các-thành-phần-cấp-ứng-dụng)
  - [Activity (Một màn hình Android truyền thống thường là một Activity)](#activity-một-màn-hình-android-truyền-thống-thường-là-một-activity)
    - [registerForContextMenu (dùng để đăng ký một thành phần giao diện)](#registerforcontextmenu-dùng-để-đăng-ký-một-thành-phần-giao-diện)
  - [DatePickerDialog (Hộp thoại chọn ngày)](#datepickerdialog-hộp-thoại-chọn-ngày)
  - [TimePickerDialog (Hộp thoại chọn giờ)](#timepickerdialog-hộp-thoại-chọn-giờ)
- [os (các API liên quan đến hệ thống Android / operating system)](#os-các-api-liên-quan-đến-hệ-thống-android--operating-system)
  - [Bundle (một class của Android dùng để chứa dữ liệu dạng key-value)](#bundle-một-class-của-android-dùng-để-chứa-dữ-liệu-dạng-key-value)
    - [putSerializable() (Đưa một đối tượng đã implements Serializable vào gói Bundle để chuẩn bị mang lên xe Intent đi truyền dữ liệu)](#putserializable-đưa-một-đối-tượng-đã-implements-serializable-vào-gói-bundle-để-chuẩn-bị-mang-lên-xe-intent-đi-truyền-dữ-liệu)
- [graphics (Liên quan đến đồ họa, hình ảnh, vẽ)](#graphics-liên-quan-đến-đồ-họa-hình-ảnh-vẽ)
- [net (Liên quan đến network URI Internet)](#net-liên-quan-đến-network-uri-internet)
  - [Uri](#uri)
- [database (Liên quan đến database và dữ liệu dạng bảng)](#database-liên-quan-đến-database-và-dữ-liệu-dạng-bảng)
- [setOnClickListener (Lắng nghe sự kiện bấm nút)](#setonclicklistener-lắng-nghe-sự-kiện-bấm-nút)
  - [Ask](#ask)
    - [tại sao chỗ này lại là view mà không phải TextView](#tại-sao-chỗ-này-lại-là-view-mà-không-phải-textview)
- [onClick()](#onclick)
- [setText()](#settext)
- [setOnCheckedChangeListener()](#setoncheckedchangelistener)
- [startActivityForResult (Mở màn hình phụ để nhập liệu và yêu cầu màn hình đó phải trả kết quả ngược về cho màn hình chính khi đóng)](#startactivityforresult-mở-màn-hình-phụ-để-nhập-liệu-và-yêu-cầu-màn-hình-đó-phải-trả-kết-quả-ngược-về-cho-màn-hình-chính-khi-đóng)
- [setOnItemLongClickListener() (Gắn bộ lắng nghe sự kiện nhấn và giữ lâu vào một dòng bất kỳ trong danh sách để biết người dùng đang chọn dòng nào)](#setonitemlongclicklistener-gắn-bộ-lắng-nghe-sự-kiện-nhấn-và-giữ-lâu-vào-một-dòng-bất-kỳ-trong-danh-sách-để-biết-người-dùng-đang-chọn-dòng-nào)
- [OnItemLongClickListener() (Là Interface quy định cấu trúc hàm callback onItemLongClick để xử lý sự kiện nhấn giữ)](#onitemlongclicklistener-là-interface-quy-định-cấu-trúc-hàm-callback-onitemlongclick-để-xử-lý-sự-kiện-nhấn-giữ)
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
### registerForContextMenu (dùng để đăng ký một thành phần giao diện)
```bash
Với hệ thống Android, ra lệnh rằng: 
    "Hãy theo dõi thành phần này, nếu người dùng nhấn giữ (Long Click) vào nó, hãy kích hoạt Context Menu".
```
**Ex**
```java
ListView lvPhongBan = findViewById(R.id.lvPhongBan);
registerForContextMenu(lvPhongBan);

System.out.println(lvPhongBan); // androidx.appcompat.widget.AppCompatListView{4f3a2b1 VFED..CL. .......... 0,0-1080,1542 #7f0800be app:id/lvPhongBan}
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
### putSerializable() (Đưa một đối tượng đã implements Serializable vào gói Bundle để chuẩn bị mang lên xe Intent đi truyền dữ liệu)
**Syn**
```bash
bundle.putSerializable("KEY", doiTuong);
```
**Ex**
```java
Bundle bundle = new Bundle();
PhongBan pb = new PhongBan("PB01", "Phong Ky Thuat");
bundle.putSerializable("KEY_PB", pb);
System.out.println(bundle.get("KEY_PB")); // PB01 - Phong Ky Thuat
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
# startActivityForResult (Mở màn hình phụ để nhập liệu và yêu cầu màn hình đó phải trả kết quả ngược về cho màn hình chính khi đóng)
**Syn**
```java
startActivityForResult(intent, requestCode); // Ma yeu cau cho form nhap la: 100
```
# setOnItemLongClickListener() (Gắn bộ lắng nghe sự kiện nhấn và giữ lâu vào một dòng bất kỳ trong danh sách để biết người dùng đang chọn dòng nào)
**Syn**
```bash
listView.setOnItemLongClickListener(listener);
```
**Ex**
```java
lv.setOnItemLongClickListener(new AdapterView.OnItemLongClickListener() {
    @Override
    public boolean onItemLongClick(AdapterView<?> parent, View view, int position, long id) {
        System.out.println("Nguoi dung dang giu tai dong so: " + position);
        return false;
    }
});
```
# OnItemLongClickListener() (Là Interface quy định cấu trúc hàm callback onItemLongClick để xử lý sự kiện nhấn giữ)
**Syn**
```bash
AdapterView.OnItemLongClickListener
```
**Ex**
```java
AdapterView.OnItemLongClickListener listener = (parent, view, position, id) -> false;
System.out.println("Ten class interface: " + listener.getClass().getName()); // com.example.helloproject.MainActivity$$Lambda$1
```
