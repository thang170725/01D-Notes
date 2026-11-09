- [Android](#android)
  - [Tạo nút bấm khi nhấn cho phép ẩn hiện thông tin](#tạo-nút-bấm-khi-nhấn-cho-phép-ẩn-hiện-thông-tin)
  - [Ứng dụng tính tổng 2 số](#ứng-dụng-tính-tổng-2-số)
  - [Máy tính cơ bản cộng trừ nhân chia](#máy-tính-cơ-bản-cộng-trừ-nhân-chia)
  - [ListView quản lý nhân viên (Bài 4.8)](#listview-quản-lý-nhân-viên-bài-48)
- [ListView thêm suử xoó quaả ly nhan vien](#listview-thêm-suử-xoó-quaả-ly-nhan-vien)
- [Ôn tập kiểm tra thường xuyên 2](#ôn-tập-kiểm-tra-thường-xuyên-2)
---
# Android
## Tạo nút bấm khi nhấn cho phép ẩn hiện thông tin
**res/layout/activity_main.xml**
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
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Hiện / Ẩn" />

    <TextView
        android:id="@+id/content"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:gravity="center"
        android:text="lê đức thắng"
        android:textSize="24sp"
        android:visibility="gone" />

</LinearLayout>
```
```java
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;

import androidx.appcompat.app.AppCompatActivity;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        // Lấy Button và TextView từ file XML
        Button button = findViewById(R.id.button);
        TextView content = findViewById(R.id.content);

        // Xử lý khi người dùng bấm nút
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
    }
}
```
## Ứng dụng tính tổng 2 số
**activity_main.xml**
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="16dp">

    <TextView
        android:id="@+id/tvTitle"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="TÍNH TỔNG HAO SỐ"
        android:textSize="22sp"
        android:textStyle="bold"
        android:gravity="center"
        android:layout_marginBottom="20dp" />

    <EditText
        android:id="@+id/edtSoA"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Nhập số A"
        android:inputType="numberSigned|numberDecimal" />

    <EditText
        android:id="@+id/edtSoB"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Nhập số B"
        android:inputType="numberSigned|numberDecimal" />

    <Button
        android:id="@+id/btnTong"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="TÍNH TỔNG"
        android:layout_marginTop="10dp" />

    <TextView
        android:id="@+id/tvKetQua"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Kết quả: "
        android:textSize="18sp"
        android:textStyle="bold"
        android:textColor="#FF0000"
        android:layout_marginTop="20dp" />

</LinearLayout>
```
**MainActivity.java**
```java
package com.example.test1;

import android.os.Bundle;
import android.view.View;
import android.widget.EditText;
import android.widget.TextView;
import android.widget.Button;
import android.widget.Toast;

import androidx.appcompat.app.AppCompatActivity;

public class MainActivity extends AppCompatActivity {
    EditText a;
    EditText b;
    TextView kq;
    Button btn;

    @override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main)

        // 1. ánh xạ id
        a = findViewById(R.id.edtSoA);
        b = findViewById(R.id.edtSoB);
        kq = findViewById(R.id.tvKetQua);
        btn = findViewById(R.id.btnTong);

        // 2. xử lý sự kiện
        btn.setOnClickListener(new View.OnClickListener(){
            @override
            void onClick() {
                String strA = a.getText().toString().trim();
                String strB = B.getText().toString().trim();
                
                if (strA.isEmpty() || strB.isEmpty()) {
                    Toast.makeText(
                        MainActivity.this,
                        "Vui lòng nhập đầy đủ 2 số!",
                        Toast.LENGTH_SHORT,
                    ).show();
                    return;
                }

                float numA = Float.parseFloat(strA);
                float numB = Float.parseFloat(strB);
                float sum = numA + numB;

                kq.setText("Kết quả: " + sum);
            }
        });
    }
}
```
## Máy tính cơ bản cộng trừ nhân chia
**activity_main.xml**
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="16dp">

    <TextView
        android:id="@+id/tvTitle"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="MÁY TÍNH CƠ BẢN"
        android:textSize="22sp"
        android:textStyle="bold"
        android:gravity="center"
        android:layout_marginBottom="16dp" />

    <EditText
        android:id="@+id/edtSo1"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Nhập số thứ nhất"
        android:inputType="numberDecimal|numberSigned" />

    <EditText
        android:id="@+id/edtSo2"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Nhập số thứ hai"
        android:inputType="numberDecimal|numberSigned" />

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Chọn phép tính:"
        android:textStyle="bold"
        android:layout_marginTop="10dp" />

    <RadioGroup
        android:id="@+id/rgPhepTinh"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal">

        <RadioButton
            android:id="@+id/radCong"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Cộng (+)"
            android:checked="true" />

        <RadioButton
            android:id="@+id/radTru"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Trừ (-)" />

        <RadioButton
            android:id="@+id/radNhan"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Nhân (*)" />

        <RadioButton
            android:id="@+id/radChia"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Chia (/)" />
    </RadioGroup>

    <Button
        android:id="@+id/btnTinh"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="TÍNH KẾT QUẢ"
        android:layout_marginTop="10dp" />

    <TextView
        android:id="@+id/tvKetQua"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Kết quả: "
        android:textSize="20sp"
        android:textStyle="bold"
        android:textColor="#0000FF"
        android:layout_marginTop="20dp" />

</LinearLayout>
```
**MainActivity.java**
```java
package com.example.test1;

import android.view.View;
import android.os.Bundle;
import android.widget.Button;
import android.widget.TextView;
import android.widget.EditText;
import android.widget.RadioGroup;
import android.widget.RadioButton;
import android.widget.Toast;

import androidx.appcompat.app.AppCompatActivity;

public class MainActivity extends AppCompatActivity{
    EditText edtSo1;
    EditText edtSo2;
    RadioGroup rgPhepTinh;
    Button btn;
    TextView kq;
    RadioButton radCong, radTru, radNhan, radChia;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        // 1. ánh xạ
        btn = findViewById(R.id.btnTinh);
        edtSo1 = findViewById(R.id.edtSo1);
        edtSo2 = findViewById(R.id.edtSo2);
        radCong = findViewById(R.id.radCong);
        radTru = findViewById(R.id.radTru);
        radNhan = findViewById(R.id.radNhan);
        radChia = findViewById(R.id.radChia);
        kq = findViewById(R.id.tvKetQua);

        // 2. xử lý sự kiện
        btn.setOnClickListener(new View.onClickListener() {
            @Override
            void onClick(){
                String str1 = edtSo1.getText().toString().trim();
                String str2 = edtSo2.getText().toString().trim();

                if (str1.isEmpty() || str2.isEmpty()) {
                    Toast.makeText(
                        MainActivity.this,
                        "Vui lòng nhập đủ 2 số!",
                        Toast.LENGTH_SHORT,
                    ).show();
                    return;
                }

                float num1 = Float.parseFloat(str1);
                float num2 = Float.parseFloat(str2);
                
                if (radCong.isChecked()) {
                   kq.setText("Kết quả: " + (num1 + num2));
                }
                else if (radTru.isChecked()) {
                    kq.setText("Kết quả: " + (num1 - num2));
                }
                else if (radNhan.isChecked()) {
                    kq.setText("Kết quả: " + (num1 * num2));
                }
                else {
                    if (num2 == 0) {
                        Toast.makeText(
                            MainActivity.this,
                            "Không thể chia cho 0!",
                            Toast.LENGTH_SHORT,
                        );
                        return;
                    }
                    kq.setText("Kết quả: " + (num1 / num2));
                }
            }
        });
    }
}
```
## ListView quản lý nhân viên (Bài 4.8)
**activity_main.xml**
```bash
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="6dp">

    <!-- Tiêu đề -->
    <TextView android:id="@+id/textView"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:background="#00BCD4"
        android:gravity="center"
        android:paddingVertical="4dp"
        android:text="Quản lý nhân viên"
        android:textColor="#0D0D0D"
        android:textSize="20sp" />

    <!-- Mã nhân viên -->
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal"
        android:gravity="center_vertical">

        <TextView android:layout_width="100dp"
            android:layout_height="wrap_content"
            android:text="Mã NV:"
            android:textSize="20sp"
            android:textStyle="bold" />

        <EditText
            android:id="@+id/maNV"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:hint="Mã nhân viên"
            android:inputType="text" />
    </LinearLayout>

    <!-- Tên nhân viên -->
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal"
        android:gravity="center_vertical">
        <TextView android:layout_width="100dp"
            android:layout_height="wrap_content"
            android:text="Tên NV:"
            android:textSize="20sp"
            android:textStyle="bold" />
        <EditText android:id="@+id/tenNV"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:hint="Tên nhân viên"
            android:inputType="text" />
    </LinearLayout>
    <!-- Loại nhân viên -->
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal"
        android:gravity="center_vertical">
        <TextView
            android:layout_width="100dp"
            android:layout_height="wrap_content"
            android:text="Loại NV:"
            android:textSize="20sp"
            android:textStyle="bold" />

        <RadioGroup
            android:id="@+id/loaiNVG"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:orientation="horizontal">

            <RadioButton
                android:id="@+id/CT"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:text="Chính thức" />

            <RadioButton
                android:id="@+id/TV"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:layout_marginStart="10dp"
                android:text="Thời vụ" />
        </RadioGroup>
    </LinearLayout>
    <!-- Nút Nhập nhân viên -->
    <Button
        android:id="@+id/nhapNV"
        android:layout_width="270dp"
        android:layout_height="wrap_content"
        android:layout_gravity="center_horizontal"
        android:layout_marginLeft="50dp"
        android:layout_marginTop="10dp"
        android:backgroundTint="#B38D8D"
        android:text="Nhập NV"
        android:textColor="#000000" />

    <!-- Nút Danh sách -->
    <Button
        android:id="@+id/danhSach"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_gravity="center_horizontal"
        android:layout_marginTop="5dp"
        android:backgroundTint="#4CAF50"
        android:text="Danh sách"
        android:textColor="#000000" />

    <ListView
        android:id="@+id/list"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:visibility="gone" />

</LinearLayout>
```
**NhanVien.java**
```java
package com.example.test1;

public class NhanVien {
    String maNV;
    String tenNV;
    String typeNV;

    NhanVien(String maNV, String tenNV, String typeNV) {
        this.maNV = maNV;
        this.tenNV = tenNV;
        this.typeNV = typeNV;
    }

    public String getMaNV() {
        return maNV;
    }
    public String getTenNV(){
        return tenNV;
    }
    public String getTypeNV(){
        return typeNV;
    }
}
```
**MyItemList.java**
```java
package com.example.test1;

import android.os.Bundle;
import android.view.View;
import android.widget.ArrayAdapter;
import android.widget.Button;
import android.widget.EditText;
import android.widget.ListView;
import android.widget.RadioGroup;
import android.widget.Toast;

import androidx.appcompat.app.AppCompatActivity;

import java.util.ArrayList;
import java.util.List;

public class MainActivity extends AppCompatActivity {
    EditText maNV, tenNV;
    RadioGroup loaiNVG;
    String typeNV;
    Button nhapNV, danhSach;
    ListView listView;

    List<NhanVien> listNV;
    List<String> listStringDisplay; // Danh sách chuỗi để hiển thị lên ListView
    ArrayAdapter<String> adapter;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        // 1. Ánh xạ View
        maNV = findViewById(R.id.maNV);
        tenNV = findViewById(R.id.tenNV);
        loaiNVG = findViewById(R.id.loaiNVG);
        nhapNV = findViewById(R.id.nhapNV);
        danhSach = findViewById(R.id.danhSach);
        listView = findViewById(R.id.list);

        // 2. Khởi tạo List & Adapter cho ListView
        listNV = new ArrayList<>();
        listStringDisplay = new ArrayList<>();
        adapter = new ArrayAdapter<>(
                this,
                android.R.layout.simple_list_item_1,
                listStringDisplay
        );
        listView.setAdapter(adapter);

        // 3. Sự kiện bấm nút "Nhập NV"
        nhapNV.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                String ma = maNV.getText().toString().trim();
                String ten = tenNV.getText().toString().trim();

                if (ma.isEmpty() || ten.isEmpty()) {
                    Toast.makeText(MainActivity.this, "Vui lòng nhập đầy đủ thông tin!", Toast.LENGTH_SHORT).show();
                    return;
                }

                int checkId = loaiNVG.getCheckedRadioButtonId();
                if (checkId == R.id.CT) {
                    typeNV = "Chính thức";
                } else {
                    typeNV = "Thời vụ";
                }

                // Tạo đối tượng nhân viên và thêm vào list dữ liệu
                NhanVien nv = new NhanVien(ma, ten, typeNV);
                listNV.add(nv);

                // Thêm chuỗi định dạng vào list hiển thị
                listStringDisplay.add(ma + " - " + ten + " - " + typeNV);
                adapter.notifyDataSetChanged(); // Cập nhật lại Adapter

                // Xóa dữ liệu cũ trên ô nhập liệu
                maNV.setText("");
                tenNV.setText("");
                maNV.requestFocus();

                Toast.makeText(MainActivity.this, "Đã thêm nhân viên!", Toast.LENGTH_SHORT).show();
            }
        });

        // 4. Sự kiện bấm nút "Danh sách"
        danhSach.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                // Hiện ListView nếu đang bị ẩn (visibility = gone)
                if (listView.getVisibility() == View.GONE) {
                    listView.setVisibility(View.VISIBLE);
                } else {
                    listView.setVisibility(View.GONE);
                }
            }
        });
    }
}
```
```java
// Package của ứng dụng.
// Nếu project của bạn có package khác thì thay dòng này bằng package của bạn.
package com.example.test1;


// Import các class cần sử dụng.
import android.app.Activity;
import android.os.Bundle;
import android.view.View;
import android.view.ViewGroup;
import android.widget.ArrayAdapter;
import android.widget.ListView;
import android.widget.TextView;


public class MainActivity extends Activity {

    /*
     * ============================================================
     * 1. CLASS PERSON
     * ============================================================
     *
     * Một Person đại diện cho MỘT người.
     *
     * Thay vì chỉ có một String như:
     *
     *      "Nguyễn Văn A"
     *
     * chúng ta muốn một người có nhiều thông tin:
     *
     *      name
     *      age
     *      address
     *      gender
     *
     * Vì vậy chúng ta tạo class Person.
     */
    static class Person {

        // Tên người
        String name;

        // Tuổi
        int age;

        // Địa chỉ
        String address;

        // Giới tính
        String gender;


        /*
         * Constructor của Person.
         *
         * Khi tạo một Person:
         *
         * new Person(
         *      "Nguyễn Văn A",
         *      25,
         *      "Hà Nội",
         *      "Nam"
         * );
         *
         * thì các giá trị sẽ được đưa vào constructor này.
         */
        Person(String name, int age, String address, String gender) {

            // this.name = name
            //
            // "name" bên phải:
            //      là tham số truyền vào constructor
            //
            // "this.name" bên trái:
            //      là biến name của object Person
            this.name = name;

            this.age = age;

            this.address = address;

            this.gender = gender;
        }
    }


    /*
     * ============================================================
     * 2. onCreate()
     * ============================================================
     *
     * onCreate() là hàm được Android gọi khi Activity được tạo.
     *
     * Đây thường là nơi chúng ta:
     *
     * - Load giao diện XML
     * - Tìm View
     * - Tạo dữ liệu
     * - Tạo Adapter
     * - Gắn Adapter vào ListView
     */
    @Override
    protected void onCreate(Bundle savedInstanceState) {

        // Gọi onCreate() của Activity cha.
        super.onCreate(savedInstanceState);


        /*
         * ========================================================
         * 3. GẮN FILE activity_main.xml
         * ========================================================
         *
         * setContentView() nói với Android:
         *
         * "Hãy sử dụng activity_main.xml làm giao diện
         *  cho Activity này."
         *
         * Trong activity_main.xml của chúng ta có:
         *
         *      <ListView
         *          android:id="@+id/listView"
         *          ...
         *      />
         */
        setContentView(R.layout.activity_main);


        /*
         * ========================================================
         * 4. LẤY LISTVIEW TỪ XML
         * ========================================================
         *
         * findViewById() tìm View dựa vào ID.
         *
         * Trong XML:
         *
         *      android:id="@+id/listView"
         *
         * thì Java có thể lấy nó bằng:
         *
         *      findViewById(R.id.listView)
         *
         * Sau dòng này:
         *
         *      listView
         *
         * chính là đối tượng ListView trong activity_main.xml.
         */
        ListView listView = findViewById(R.id.listView);


        /*
         * ========================================================
         * 5. TẠO DỮ LIỆU
         * ========================================================
         *
         * Chúng ta tạo một mảng Person.
         *
         * Person[] có nghĩa:
         *
         *      Đây là một mảng chứa các object Person.
         */
        Person[] people = {


                /*
                 * Person thứ nhất
                 *
                 * name    = Nguyễn Văn A
                 * age     = 25
                 * address = Hà Nội
                 * gender  = Nam
                 */
                new Person(
                        "Nguyễn Văn A",
                        25,
                        "Hà Nội",
                        "Nam"
                ),


                /*
                 * Person thứ hai
                 */
                new Person(
                        "Trần Văn B",
                        30,
                        "Hải Phòng",
                        "Nữ"
                ),


                /*
                 * Person thứ ba
                 */
                new Person(
                        "Lê Đức Thắng",
                        28,
                        "Đà Nẵng",
                        "Nam"
                )
        };


        /*
         * ========================================================
         * 6. TẠO ARRAYADAPTER
         * ========================================================
         *
         * Đây là phần quan trọng nhất.
         *
         * ArrayAdapter<Person>
         *
         * có nghĩa:
         *
         * "Adapter này quản lý dữ liệu kiểu Person."
         *
         * Vì dữ liệu của chúng ta là:
         *
         *      Person[]
         *
         * nên Adapter cũng sử dụng:
         *
         *      Person
         */
        ArrayAdapter<Person> adapter = new ArrayAdapter<Person>(


                /*
                 * ------------------------------------------------
                 * THAM SỐ 1: this
                 * ------------------------------------------------
                 *
                 * "this" ở đây là MainActivity hiện tại.
                 *
                 * Activity chính là một Context.
                 *
                 * Adapter cần Context để biết:
                 *
                 * - đang hoạt động trong Activity nào
                 * - lấy resource ở đâu
                 * - tạo View như thế nào
                 */
                this,


                /*
                 * ------------------------------------------------
                 * THAM SỐ 2: R.layout.item_person
                 * ------------------------------------------------
                 *
                 * Đây là layout của MỘT ITEM.
                 *
                 * File:
                 *
                 *      res/layout/item_person.xml
                 *
                 * Trong file đó chúng ta có:
                 *
                 *      txtName
                 *      txtGender
                 *      txtAddress
                 *      txtAge
                 *
                 * Adapter sẽ sử dụng layout này làm "khuôn"
                 * cho từng người.
                 */
                R.layout.item_person,


                /*
                 * ------------------------------------------------
                 * THAM SỐ 3: R.id.txtName
                 * ------------------------------------------------
                 *
                 * ArrayAdapter mặc định cần biết TextView nào
                 * dùng để hiển thị dữ liệu chính.
                 *
                 * Trong item_person.xml chúng ta có:
                 *
                 *      <TextView
                 *          android:id="@+id/txtName"
                 *          ...
                 *      />
                 *
                 * nên truyền:
                 *
                 *      R.id.txtName
                 *
                 * Tuy nhiên vì chúng ta override getView()
                 * bên dưới nên cuối cùng chúng ta tự đưa dữ liệu
                 * vào cả 4 TextView.
                 */
                R.id.txtName,


                /*
                 * ------------------------------------------------
                 * THAM SỐ 4: people
                 * ------------------------------------------------
                 *
                 * Đây chính là dữ liệu mà Adapter quản lý.
                 *
                 * people chứa:
                 *
                 *      Person 1
                 *      Person 2
                 *      Person 3
                 *
                 */
                people
        ) {


            /*
             * ====================================================
             * 7. OVERRIDE getView()
             * ====================================================
             *
             * Đây là phần quan trọng nhất của Custom Adapter.
             *
             * ListView sẽ gọi getView() khi nó cần tạo
             * hoặc hiển thị một item.
             *
             * Ví dụ:
             *
             * position = 0
             * → hiển thị Nguyễn Văn A
             *
             * position = 1
             * → hiển thị Trần Văn B
             *
             * position = 2
             * → hiển thị Lê Đức Thắng
             */
            @Override
            public View getView(
                    int position,
                    View convertView,
                    ViewGroup parent
            ) {


                /*
                 * =================================================
                 * 8. TẠO/LẤY VIEW CỦA ITEM
                 * =================================================
                 *
                 * super.getView() sẽ sử dụng:
                 *
                 *      R.layout.item_person
                 *
                 * để tạo ra giao diện của một item.
                 *
                 * Kết quả trả về là một View.
                 *
                 * View này chính là:
                 *
                 *      item_person.xml
                 */
                View view = super.getView(
                        position,
                        convertView,
                        parent
                );


                /*
                 * =================================================
                 * 9. LẤY PERSON HIỆN TẠI
                 * =================================================
                 *
                 * position cho biết chúng ta đang xử lý
                 * người thứ mấy.
                 *
                 * Ví dụ:
                 *
                 * position = 0
                 * → people[0]
                 * → Nguyễn Văn A
                 *
                 * position = 1
                 * → people[1]
                 * → Trần Văn B
                 */
                Person person = getItem(position);


                /*
                 * =================================================
                 * 10. TÌM CÁC TEXTVIEW TRONG ITEM
                 * =================================================
                 *
                 * view chính là item_person.xml.
                 *
                 * findViewById() tìm các TextView bên trong
                 * item đó.
                 *
                 * Ví dụ:
                 *
                 *      R.id.txtName
                 *
                 * chính là:
                 *
                 *      <TextView
                 *          android:id="@+id/txtName"
                 *          ...
                 *      />
                 */


                // Tìm TextView hiển thị tên
                TextView txtName =
                        view.findViewById(R.id.txtName);


                // Tìm TextView hiển thị giới tính
                TextView txtGender =
                        view.findViewById(R.id.txtGender);


                // Tìm TextView hiển thị địa chỉ
                TextView txtAddress =
                        view.findViewById(R.id.txtAddress);


                // Tìm TextView hiển thị tuổi
                TextView txtAge =
                        view.findViewById(R.id.txtAge);


                /*
                 * =================================================
                 * 11. ĐƯA DỮ LIỆU VÀO TEXTVIEW
                 * =================================================
                 *
                 * Đây chính là lúc dữ liệu Person được đưa
                 * vào giao diện XML.
                 */


                // Lấy tên từ Person rồi đưa vào txtName
                //
                // person.name:
                //      "Nguyễn Văn A"
                //
                // txtName.setText():
                //      hiển thị "Nguyễn Văn A"
                txtName.setText(person.name);


                // Lấy giới tính
                //
                // Ví dụ:
                //      "Nam"
                txtGender.setText(person.gender);


                // Lấy địa chỉ
                //
                // Ví dụ:
                //      "Hà Nội"
                txtAddress.setText(person.address);


                // Lấy tuổi.
                //
                // person.age là int.
                //
                // Chúng ta nối với String " tuổi"
                // để tạo thành:
                //
                //      "25 tuổi"
                //
                // Ví dụ:
                //
                // person.age = 25
                //
                // 25 + " tuổi"
                //
                // → "25 tuổi"
                txtAge.setText(person.age + " tuổi");


                /*
                 * =================================================
                 * 12. TRẢ VỀ VIEW
                 * =================================================
                 *
                 * Sau khi đã đưa dữ liệu vào:
                 *
                 *      txtName
                 *      txtGender
                 *      txtAddress
                 *      txtAge
                 *
                 * chúng ta trả item View này về cho ListView.
                 *
                 * ListView sau đó sẽ hiển thị nó.
                 */
                return view;
            }
        };


        /*
         * ========================================================
         * 13. GẮN ADAPTER VÀO LISTVIEW
         * ========================================================
         *
         * Trước dòng này:
         *
         *      ListView
         *
         * chỉ là một danh sách rỗng.
         *
         * Sau dòng này:
         *
         *      listView.setAdapter(adapter);
         *
         * ListView biết:
         *
         *      "Dữ liệu của tôi nằm trong adapter."
         *
         * Adapter sẽ lấy từng Person
         * rồi tạo item tương ứng.
         */
        listView.setAdapter(adapter);
    }
}
```
# ListView thêm suử xoó quaả ly nhan vien
**MainActivity.java**
```java
package com.example.test1;

import android.os.Bundle;
import android.view.View;
import android.view.ViewGroup;
import android.widget.AdapterView;
import android.widget.ArrayAdapter;
import android.widget.Button;
import android.widget.EditText;
import android.widget.ListView;
import android.widget.RadioButton;
import android.widget.RadioGroup;
import android.widget.TextView;
import android.widget.Toast;

import androidx.appcompat.app.AppCompatActivity;

import java.util.ArrayList;
import java.util.List;

public class MainActivity extends AppCompatActivity {

    // Model Person
    static class Person {
        String id;
        String name;
        String type;
        float salary;

        Person(String id, String name, String type, float salary) {
            this.id = id;
            this.name = name;
            this.type = type;
            this.salary = salary;
        }
    }

    // Khai báo các biến toàn cục
    EditText maNV, tenNV;
    RadioGroup typeGroup;
    RadioButton radCt, radTv;
    Button nhapNV, btnSua, btnXoa;
    ListView listView;

    List<Person> list = new ArrayList<>();
    ArrayAdapter<Person> adapterPerson;

    // Biến lưu vị trí đang được chọn trong ListView (-1 là chưa chọn)
    int selectedIndex = -1;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        // 1. Ánh xạ View
        maNV = findViewById(R.id.maNV);
        tenNV = findViewById(R.id.tenNV);
        typeGroup = findViewById(R.id.typeGroup);
        radCt = findViewById(R.id.ct);
        radTv = findViewById(R.id.tv);
        nhapNV = findViewById(R.id.nhapNV);
        btnSua = findViewById(R.id.btnSua);
        btnXoa = findViewById(R.id.btnXoa);
        listView = findViewById(R.id.listView);

        // 2. Khởi tạo Custom Adapter một lần duy nhất
        adapterPerson = new ArrayAdapter<Person>(
                MainActivity.this,
                R.layout.item_person,
                R.id.id,
                list
        ) {
            @Override
            public View getView(int position, View convertView, ViewGroup parent) {
                View view = super.getView(position, convertView, parent);
                Person person = getItem(position);

                TextView id = view.findViewById(R.id.id);
                TextView name = view.findViewById(R.id.name);
                TextView type = view.findViewById(R.id.type);
                TextView salary = view.findViewById(R.id.salary);

                if (person != null) {
                    id.setText(person.id);
                    name.setText(person.name);
                    type.setText(person.type);
                    salary.setText(String.valueOf(person.salary));
                }

                return view;
            }
        };

        // Gắn adapter vào ListView ngay từ đầu
        listView.setAdapter(adapterPerson);

        // -------------------------------------------------------------
        // 3. THÊM NHÂN VIÊN (CREATE)
        // -------------------------------------------------------------
        nhapNV.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                String ma = maNV.getText().toString().trim();
                String ten = tenNV.getText().toString().trim();

                if (ma.isEmpty() || ten.isEmpty()) {
                    Toast.makeText(MainActivity.this, "Vui lòng nhập đầy đủ thông tin!", Toast.LENGTH_SHORT).show();
                    return;
                }

                String type = "chính thức";
                float salary = 500;

                int checked = typeGroup.getCheckedRadioButtonId();
                if (checked == R.id.tv) {
                    type = "thời vụ";
                    salary = 100;
                }

                // Thêm vào mảng
                Person p = new Person(ma, ten, type, salary);
                list.add(p);

                // Cập nhật giao diện
                adapterPerson.notifyDataSetChanged();
                clearForm();
                Toast.makeText(MainActivity.this, "Thêm thành công!", Toast.LENGTH_SHORT).show();
            }
        });

        // -------------------------------------------------------------
        // 4. CHỌN DÒNG TRONG LISTVIEW ĐỂ XEM/SỬA/XÓA (READ / SELECT)
        // -------------------------------------------------------------
        listView.setOnItemClickListener(new AdapterView.OnItemClickListener() {
            @Override
            public void onItemClick(AdapterView<?> parent, View view, int position, long id) {
                selectedIndex = position; // Lưu lại vị trí chọn
                Person p = list.get(position);

                // Đẩy thông tin lên form nhập
                maNV.setText(p.id);
                tenNV.setText(p.name);
                if (p.type.equals("thời vụ")) {
                    radTv.setChecked(true);
                } else {
                    radCt.setChecked(true);
                }
            }
        });

        // -------------------------------------------------------------
        // 5. SỬA THÔNG TIN NHÂN VIÊN (UPDATE)
        // -------------------------------------------------------------
        btnSua.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                if (selectedIndex == -1) {
                    Toast.makeText(MainActivity.this, "Vui lòng chọn nhân viên cần sửa từ danh sách!", Toast.LENGTH_SHORT).show();
                    return;
                }

                String ma = maNV.getText().toString().trim();
                String ten = tenNV.getText().toString().trim();

                if (ma.isEmpty() || ten.isEmpty()) {
                    Toast.makeText(MainActivity.this, "Không được để trống thông tin!", Toast.LENGTH_SHORT).show();
                    return;
                }

                String type = "chính thức";
                float salary = 500;

                int checked = typeGroup.getCheckedRadioButtonId();
                if (checked == R.id.tv) {
                    type = "thời vụ";
                    salary = 100;
                }

                // Cập nhật thông tin phần tử tại vị trí selectedIndex
                Person p = list.get(selectedIndex);
                p.id = ma;
                p.name = ten;
                p.type = type;
                p.salary = salary;

                // Cập nhật ListView
                adapterPerson.notifyDataSetChanged();
                clearForm();
                Toast.makeText(MainActivity.this, "Cập nhật thành công!", Toast.LENGTH_SHORT).show();
            }
        });

        // -------------------------------------------------------------
        // 6. XÓA NHÂN VIÊN (DELETE)
        // -------------------------------------------------------------
        btnXoa.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                if (selectedIndex == -1) {
                    Toast.makeText(MainActivity.this, "Vui lòng chọn nhân viên cần xóa từ danh sách!", Toast.LENGTH_SHORT).show();
                    return;
                }

                // Xóa khỏi danh sách theo vị trí
                list.remove(selectedIndex);

                // Cập nhật ListView
                adapterPerson.notifyDataSetChanged();
                clearForm();
                Toast.makeText(MainActivity.this, "Xóa thành công!", Toast.LENGTH_SHORT).show();
            }
        });
    }

    // Hàm xóa trắng form và đưa trạng thái vị trí chọn về mặc định
    private void clearForm() {
        maNV.setText("");
        tenNV.setText("");
        radCt.setChecked(true);
        maNV.requestFocus();
        selectedIndex = -1; // Reset vị trí chọn
    }
}
```
**item_person**
```xml
<?xml version="1.0" encoding="utf-8"?>

<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:orientation="horizontal"
    android:padding="16dp">

    <!-- CỘT TRÁI -->
    <LinearLayout
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:layout_weight="1"
        android:orientation="vertical">

        <!-- TÊN -->
        <TextView
            android:id="@+id/id"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:textSize="20sp"
            android:textStyle="bold" />

        <!-- GIỚI TÍNH -->
        <TextView
            android:id="@+id/type"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_marginTop="4dp"
            android:textSize="16sp" />

    </LinearLayout>


    <!-- CỘT PHẢI -->
    <LinearLayout
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:layout_weight="1"
        android:orientation="vertical">

        <!-- ĐỊA CHỈ -->
        <TextView
            android:id="@+id/name"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:textSize="20sp"
            android:textStyle="bold" />

        <!-- TUỔI -->
        <TextView
            android:id="@+id/salary"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_marginTop="4dp"
            android:textSize="16sp" />

    </LinearLayout>

</LinearLayout>
```
**activity_main**
```bash
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="10dp">

    <TextView
        android:id="@+id/textView"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:background="#4CAF50"
        android:gravity="center"
        android:padding="8dp"
        android:text="Quản lý nhân viên (CRUD)"
        android:textColor="#FFFFFF"
        android:textSize="20sp"
        android:textStyle="bold" />

    <!-- MÃ NV -->
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginTop="8dp"
        android:orientation="horizontal">

        <TextView
            android:layout_width="100dp"
            android:layout_height="wrap_content"
            android:text="Mã NV:" />

        <EditText
            android:id="@+id/maNV"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:hint="Mã nhân viên"
            android:inputType="text" />
    </LinearLayout>

    <!-- TÊN NV -->
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal">

        <TextView
            android:layout_width="100dp"
            android:layout_height="wrap_content"
            android:text="Tên NV:" />

        <EditText
            android:id="@+id/tenNV"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:hint="Tên nhân viên"
            android:inputType="text" />
    </LinearLayout>

    <!-- LOẠI NV -->
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal">

        <TextView
            android:layout_width="100dp"
            android:layout_height="wrap_content"
            android:text="Loại NV:" />

        <RadioGroup
            android:id="@+id/typeGroup"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:orientation="horizontal">

            <RadioButton
                android:id="@+id/ct"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:layout_weight="1"
                android:checked="true"
                android:text="Chính thức" />

            <RadioButton
                android:id="@+id/tv"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:layout_weight="1"
                android:text="Thời vụ" />
        </RadioGroup>
    </LinearLayout>

    <!-- HÀNG NÚT CHỨC NĂNG: THÊM - SỬA - XÓA -->
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginTop="10dp"
        android:orientation="horizontal">

        <Button
            android:id="@+id/nhapNV"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:backgroundTint="#4CAF50"
            android:text="Thêm" />

        <Button
            android:id="@+id/btnSua"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:backgroundTint="#FF9800"
            android:text="Sửa" />

        <Button
            android:id="@+id/btnXoa"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:backgroundTint="#F44336"
            android:text="Xóa" />
    </LinearLayout>

    <!-- DANH SÁCH -->
    <ListView
        android:id="@+id/listView"
        android:layout_width="match_parent"
        android:layout_height="0dp"
        android:layout_marginTop="10dp"
        android:layout_weight="1" />

</LinearLayout>
```
**NhanVien.java**
```java
package com.example.test1;

public class NhanVien {
    String maNV;
    String tenNV;
    String typeNV;

    NhanVien(String maNV, String tenNV, String typeNV) {
        this.maNV = maNV;
        this.tenNV = tenNV;
        this.typeNV = typeNV;
    }

    public String getMaNV() {
        return maNV;
    }
    public String getTenNV(){
        return tenNV;
    }
    public String getTypeNV(){
        return typeNV;
    }
}
```
# Ôn tập kiểm tra thường xuyên 2
*Product.java*
```java
public class Product{
    public String maSP, tenSP, loaiSP, ngayTao;

    Task(String maSP, String tenSP, String loaiSP, String ngayTao){
        this.maSP = maSP;
        this.tenSP = tenSP;
        this.loaiSP = loaiSP;
        this.ngayTao = ngayTao;
    }
}
```
*activity_main.xml*
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="15dp">

    <!-- Dòng tiêu đề có nút 3 gạch ở góc trái -->
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:background="#FF9800"
        android:gravity="center_vertical"
        android:orientation="horizontal"
        android:padding="5dp">

        <TextView
            android:id="@+id/btnMenu3Gach"
            android:layout_width="48dp"
            android:layout_height="48dp"
            android:background="@color/white"
            android:clickable="true"
            android:focusable="true"
            android:gravity="center"
            android:text="☰"
            android:textColor="#000000"
            android:textSize="22sp"
            android:textStyle="bold" />

        <TextView
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:gravity="center"
            android:paddingEnd="48dp"
            android:text="Quản Lý Công Việc"
            android:textColor="#FFFFFF"
            android:textSize="18sp"
            android:textStyle="bold" />

    </LinearLayout>

    <!-- Form nhập liệu -->
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginTop="15dp"
        android:orientation="vertical">

        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_marginTop="8dp"
            android:gravity="center_vertical"
            android:orientation="horizontal">

            <TextView
                android:layout_width="100dp"
                android:layout_height="wrap_content"
                android:text="Mã SP:"
                android:textSize="16sp" />

            <EditText
                android:id="@+id/editMaSP"
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:hint="Nhập mã công việc"
                android:inputType="text" />
        </LinearLayout>

        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_marginTop="8dp"
            android:gravity="center_vertical"
            android:orientation="horizontal">

            <TextView
                android:layout_width="100dp"
                android:layout_height="wrap_content"
                android:text="Tên SP:"
                android:textSize="16sp" />

            <EditText
                android:id="@+id/editTenSP"
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:hint="Nhập tên công việc"
                android:inputType="text" />
        </LinearLayout>

        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_marginTop="8dp"
            android:gravity="center_vertical"
            android:orientation="horizontal">

            <TextView
                android:layout_width="100dp"
                android:layout_height="wrap_content"
                android:text="Loại SP:"
                android:textSize="16sp" />

            <RadioGroup
                android:id="@+id/rgLoaiSP"
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:orientation="horizontal">

                <RadioButton
                    android:id="@+id/rbRan"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:checked="true"
                    android:text="Rắn" />

                <RadioButton
                    android:id="@+id/rbLong"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:layout_marginStart="15dp"
                    android:text="Lỏng" />
            </RadioGroup>
        </LinearLayout>
    </LinearLayout>

    <Button
        android:id="@+id/btnLuuSP"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginTop="15dp"
        android:backgroundTint="#4CAF50"
        android:text="Lưu sản phẩm"
        android:textColor="#FFFFFF" />

    <TextView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginTop="15dp"
        android:text="Danh sách sản phẩm:"
        android:textSize="16sp"
        android:textStyle="bold" />

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:background="#DDDDDD"
        android:orientation="horizontal"
        android:padding="10dp">

        <TextView
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:text="Mã"
            android:textColor="#000000"
            android:textStyle="bold" />

        <TextView
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:text="Tên"
            android:textColor="#000000"
            android:textStyle="bold" />

        <TextView
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:text="Loại SP"
            android:textColor="#000000"
            android:textStyle="bold" />

        <TextView
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1.2"
            android:text="Ngày tạo"
            android:textColor="#000000"
            android:textStyle="bold" />
    </LinearLayout>

    <ListView
        android:id="@+id/lvSP"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:layout_marginTop="5dp" />

</LinearLayout>
```
*row_product.xml (Đặt trong res/layout/)*
```java
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:orientation="horizontal"
    android:padding="10dp">

    <TextView
        android:id="@+id/tvMa"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:layout_weight="1"
        android:textColor="#000000"
        android:textSize="14sp" />

    <TextView
        android:id="@+id/tvTen"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:layout_weight="1"
        android:textColor="#000000"
        android:textSize="14sp" />

    <TextView
        android:id="@+id/tvTrangThai"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:layout_weight="1"
        android:textColor="#000000"
        android:textSize="14sp" />

    <TextView
        android:id="@+id/tvNgay"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:layout_weight="1.2"
        android:textColor="#000000"
        android:textSize="14sp" />
</LinearLayout>
```
*main_menu.xml*
```xml
<?xml version="1.0" encoding="utf-8"?>
<menu xmlns:android="http://schemas.android.com/apk/res/android">
    <item
        android:id="@+id/menu_tai_khoan"
        android:title="Tài khoản">
        <menu>
            <item
                android:id="@+id/menu_dangnhap"
                android:title="Đăng nhập" />
            <item
                android:id="@+id/menu_dangky"
                android:title="Đăng ký" />
        </menu>
    </item>
    <item
        android:id="@+id/menu_dangxuat"
        android:title="Đăng xuất" />
</menu>
```
**activity_detail.xsml**
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="20dp">

    <TextView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="CHI TIẾT SẢN PHẨM"
        android:textSize="20sp"
        android:textStyle="bold"
        android:textColor="#FF9800"
        android:gravity="center"
        android:layout_marginBottom="20dp"/>

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal"
        android:layout_marginBottom="10dp">
        <TextView android:layout_width="120dp" android:layout_height="wrap_content" android:text="Mã sản phẩm:" android:textStyle="bold" android:textSize="16sp"/>
        <TextView android:id="@+id/tvDetailMa" android:layout_width="match_parent" android:layout_height="wrap_content" android:textSize="16sp"/>
    </LinearLayout>

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal"
        android:layout_marginBottom="10dp">
        <TextView android:layout_width="120dp" android:layout_height="wrap_content" android:text="Tên sản phẩm:" android:textStyle="bold" android:textSize="16sp"/>
        <TextView android:id="@+id/tvDetailTen" android:layout_width="match_parent" android:layout_height="wrap_content" android:textSize="16sp"/>
    </LinearLayout>

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal"
        android:layout_marginBottom="10dp">
        <TextView android:layout_width="120dp" android:layout_height="wrap_content" android:text="Loại sản phẩm:" android:textStyle="bold" android:textSize="16sp"/>
        <TextView android:id="@+id/tvDetailLoai" android:layout_width="match_parent" android:layout_height="wrap_content" android:textSize="16sp"/>
    </LinearLayout>

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal"
        android:layout_marginBottom="20dp">
        <TextView android:layout_width="120dp" android:layout_height="wrap_content" android:text="Ngày tạo:" android:textStyle="bold" android:textSize="16sp"/>
        <TextView android:id="@+id/tvDetailNgay" android:layout_width="match_parent" android:layout_height="wrap_content" android:textSize="16sp"/>
    </LinearLayout>

    <Button
        android:id="@+id/btnBack"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Quay lại"
        android:backgroundTint="#607D8B"
        android:textColor="#FFFFFF"/>

</LinearLayout>
```
*MainActivity.java*
```java
public class MainActivity extends AppCompatActivity {
    public static int NHANVIENCONSTANTS = 5;
    TextView btnMenu3Gach;
    EditText editMaSP, editTenSP; 
    RadioGroup rgLoaiSP;
    RadioButton rbRan, rbLong;

    Button btnLuuSP;

    ListView lvSP;

    ArrayList<Product> dsSP = new ArrayList<>();
    ArrayAdapter<Product> adapterSP;

    Product productSelected = null;
    boolean isSua = false;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContextView(R.layout.activity_main);

        // 1. ánh xạ
        btnMenu3Gach = findViewById(R.id.btnMenu3Gach);
        editMaSP = findViewById(R.id.editMaSP);
        editTenSP = findViewById(R.id.editTenSP);
        rgLoaiSP = findViewById(R.id.rgLoaiSP);
        rbRan = findViewById(R.id.rbRan);
        rbLong = findViewById(R.id.rbLong);
        btnLuuSP = findViewById(R.id.btnLuuSP);
        lvSP = findViewById(R.id.lvSP);

        // 2. Gắn Custom Adapter cho ListView
        adapterSP = new ArrayAdapter<Task>(
            this, 
            R.layout.row_product, 
            R.id.tvMa,
            dsSP
        ) {
            @Override
            public View getView(int position, View convertView, ViewGroup parent) {
                View view = super.getView(position, convertView, parent);
                Product p = getItem(position)

                TextView tvMa = convertView.findViewById(R.id.tvMa);
                TextView tvTen = convertView.findViewById(R.id.tvTen);
                TextView tvLoaiSP = convertView.findViewById(R.id.tvLoaiSP);
                TextView tvNgay = convertView.findViewById(R.id.tvNgay);

                if (p != null) {
                    tvMa.setText(p.maSP);
                    tvTen.setText(p.tenSSP);
                    tvLoaiSP.setText(p.loaiSP);
                    tvNgay.setText(p.ngayTao);
                }
                return convertView;
            }
        };
        lvSP.setAdapter(adapterSP);

        // 3. bấm nút lưu sản phẩm
        btnLuuTask.setOnClickListener(v -> {
            String maSP = editMaSP.getText().toString().trim();
            String tenSP = editTenSP.getText().toString().trim();
            String loaiSP = rbRan.isChecked() ? "Rắn" : "Lỏng";
            String ngayTao = new SimpleDateFormat("dd/MM/yyyy HH:mm", Locale.getDefault()).format(new Date());

            if (isSua == false){
                Product sp = new Product(maSP, tenSP, loaiSP, ngayTao);
                dsSP.add(sp);
            } else {
                productSelected.maSP = maSP;
                productSelected.tenSP = tenSP;
                productSelected.loaiSP = loaiSP;
                productSelected.ngayTao = ngayTao;
                isSua = false;
            }
           
            adapterSP.notifyDataSetChanged();
            reset();
        });

        // 4. sử lý menu 3 gạch
        btnMenu3Gach.setOnClickListener(v -> {
            PopupMenu popup = new PopupMenu(MainActivity, this);
            popup.getMenuInflater().inflate(R.menu.main_menu, popup.getmenu());
            popup.setOnMenuItemClickListener(item -> {
                int id = item.getItemId();
                if (id == R.id.menu_dientu) {
                    Toast.makeText(MainActivity.this, "Điện tử", Toast.LENGTH_SHORT).show();
                    return true;
                } else if (id == R.id.menu_thoitrang) {
                    Toast.makeText(MainActivity.this, "Thời trang", Toast.LENGTH_SHORT).show();
                    return true;
                } else if (id == R.id.menu_thoat) {
                    Toast.makeText(MainActivity.this, "Thoát", Toast.LENGTH_SHORT).show();
                    return true;
                }
                return false;
            });
            popup.show();
        });

        // 5. bắt sự kiện click 1 dòng để sửa
        lvSP.setOnItemClickListener((parent, view, position, id) -> {
            productSelected = dsSP.get(position);
            
            Intent i = new Intent(MainActivity.this, DetailActivity.class);
            i.putExtra("ma_sp", productSelected.maSP);
            i.putExtra("ten_sp", productSelected.tenSP);
            i.putExtra("loai_sp", productSelected.loaiSP);
            i.putExtra("ngay_sp", productSelected.ngayTao);

            startActivity(i);
        });

        // 6. bắt sự kiện nhấn giữ
        registerForContextMenu(lvSP);
    }

    @Override
    public void onCreateContextMenu(
        ContextMenu menu,
        View view,
        ContextMenu.ContextMenuInfo menuinfo
    ){
        super.onCreateContextMenu(menu, view, menuinfo);
        AdapterView.AdapterContextMenuInfo info = (AdapterView.AdapterContextMenuInfo) menuinfo;

        productSelected = dsSP.get(info.position);
        getMenuInflater().inflate(R.menu.xoa, menu);
    }

    @Override
    public boolean onContextItemSelected(MenuItem item){
        int id = item.getItemId();
        if (id == R.id.xoa){
            AlertDialog.Builder builder = new AlertDialog.Builder(MainActivity.this);
            builder.setTitle("Xóa sản phẩm");
            builder.setMessage("Bạn có chắc chắn muốn xóa công việc này không");
            builder.setPositiveButton("Có", (dialog, which) -> {
                dsSP.remove(productSelected);
                adapterSP.notifyDataSetChanged();
                productSelected=null;
                reset();
            });
            builder.setNegativeButton("Không", (dialog, which) -> {
                dialog.dimiss();
            });
            builder.show();
            return true;
        }
    }

    public void reset(){
        editMaSP.setText("");
        editTenSP.setText("");
        isSua = false;
        productSelected = null;
    }
}
```
**DetailActivity.java**
```java
public class DetailActivity extends AppCompatActivity {
    TextView tvDetailMa, tvDetailTen, tvDetailLoai, tvDetailNgay;
    Button btnBack;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_detail);

        // Ánh xạ
        tvDetailMa = findViewById(R.id.tvDetailMa);
        tvDetailTen = findViewById(R.id.tvDetailTen);
        tvDetailLoai = findViewById(R.id.tvDetailLoai);
        tvDetailNgay = findViewById(R.id.tvDetailNgay);
        btnBack = findViewById(R.id.btnBack);

        // Nhận Intent được gửi từ MainActivity sang
        Intent intent = getIntent();
        if (intent != null) {
            String ma = intent.getStringExtra("ma_sp");
            String ten = intent.getStringExtra("ten_sp");
            String loai = intent.getStringExtra("loai_sp");
            String ngay = intent.getStringExtra("ngay_sp");

            // Đưa lên TextView để hiển thị
            tvDetailMa.setText(ma);
            tvDetailTen.setText(ten);
            tvDetailLoai.setText(loai);
            tvDetailNgay.setText(ngay);
        }

        // Nút quay lại màn hình chính
        btnBack.setOnClickListener(v -> finish());
    }
}
```