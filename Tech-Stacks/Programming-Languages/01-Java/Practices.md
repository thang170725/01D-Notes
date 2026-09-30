- [Android](#android)
  - [Tạo nút bấm khi nhấn cho phép ẩn hiện thông tin](#tạo-nút-bấm-khi-nhấn-cho-phép-ẩn-hiện-thông-tin)
  - [Ứng dụng tính tổng 2 số](#ứng-dụng-tính-tổng-2-số)
  - [Máy tính cơ bản cộng trừ nhân chia](#máy-tính-cơ-bản-cộng-trừ-nhân-chia)
  - [ListView quản lý nhân viên (Bài 4.8)](#listview-quản-lý-nhân-viên-bài-48)
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
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">

    <TextView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:background="#26C6DA"
        android:gravity="center"
        android:padding="8dp"
        android:text="Quản lý nhân viên"
        android:textColor="#FFFFFF"
        android:textSize="20sp" />

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal"
        android:padding="4dp">
        <TextView
            android:layout_width="80dp"
            android:layout_height="wrap_content"
            android:text="Mã NV" />
        <EditText
            android:id="@+id/edtMa"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:inputType="text" />
    </LinearLayout>

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal"
        android:padding="4dp">
        <TextView
            android:layout_width="80dp"
            android:layout_height="wrap_content"
            android:text="Tên NV" />
        <EditText
            android:id="@+id/edtTen"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:inputType="text" />
    </LinearLayout>

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal"
        android:padding="4dp">
        <TextView
            android:layout_width="80dp"
            android:layout_height="wrap_content"
            android:text="Loại NV" />
        <RadioGroup
            android:id="@+id/rgLoai"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:orientation="horizontal">
            <RadioButton
                android:id="@+id/radChinhThuc"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:checked="true"
                android:text="Chính thức" />
            <RadioButton
                android:id="@+id/radThoiVu"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:text="Thời vụ" />
        </RadioGroup>
    </LinearLayout>

    <Button
        android:id="@+id/btnNhap"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_gravity="center"
        android:text="Nhập NV" />

    <TextView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:background="#26C6DA"
        android:gravity="center"
        android:padding="6dp"
        android:text="Danh sách"
        android:textColor="#FFFFFF"
        android:textSize="18sp" />

    <ListView
        android:id="@+id/lvNhanVien"
        android:layout_width="match_parent"
        android:layout_height="match_parent" />

</LinearLayout>
```
**NhanVien.java**
```java
public class NhanVien {
    private String ma;
    private String ten;
    private boolean chinhThuc;

    public NhanVien(String ma, String ten, boolean chinhThuc) {
        this.ma = ma;
        this.ten = ten;
        this.chinhThuc = chinhThuc;
    }

    public String getMa() { return ma; }
    public String getTen() { return ten; }
    public boolean isChinhThuc() { return chinhThuc; }

    // Chính thức: 500k, thời vụ: 150k
    public int getLuong() {
        return chinhThuc ? 500 : 150;
    }
}
```
**MyItemList.java**
```java
import android.content.Context;
import android.graphics.Color;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;
import android.widget.ArrayAdapter;
import android.widget.LinearLayout;
import android.widget.TextView;

import java.util.List;

public class MyItemList extends ArrayAdapter<NhanVien> {

    private Context context; // ứng dụng android hiện tại
    private int resource; // file xml dùng làm giao diện 1 dòng
    private List<NhanVien> list; // danh sách nhân viên

    public MyItemList(Context context, int resource, List<NhanVien> list) {
        super(context, resource, list);
        this.context = context;
        this.resource = resource;
        this.list = list;
    }

    // Android gọi getView() để hỏi Adapter: "Hãy đưa cho tôi giao diện của dòng số X."
    @Override
    public View getView(int position, View convertView, ViewGroup parent) {
        // Nạp layout 1 dòng (tái sử dụng view cũ nếu có)
        if (convertView == null) {
            convertView = LayoutInflater.from(context).inflate(resource, parent, false);
        }

        // Ánh xạ view trong dòng
        LinearLayout layoutRow = convertView.findViewById(R.id.layoutRow);
        TextView txtID = convertView.findViewById(R.id.txtRawID);
        TextView txtName = convertView.findViewById(R.id.txtRawName);
        TextView txtType = convertView.findViewById(R.id.txtRawType);
        TextView txtLuong = convertView.findViewById(R.id.txtRawLuong);

        // Lấy nhân viên tại vị trí position
        NhanVien nv = list.get(position);

        txtID.setText("ID: " + nv.getMa());
        txtName.setText("Họ tên: " + nv.getTen());
        txtLuong.setText("Mức lương: " + nv.getLuong() + "k");

        // Đổi loại + màu nền theo loại nhân viên
        if (nv.isChinhThuc()) {
            txtType.setText("Nhân viên chính thức");
            layoutRow.setBackgroundColor(Color.WHITE);
        } else {
            txtType.setText("Nhân viên thời vụ");
            layoutRow.setBackgroundColor(Color.GREEN);
        }

        return convertView;
    }
}
```