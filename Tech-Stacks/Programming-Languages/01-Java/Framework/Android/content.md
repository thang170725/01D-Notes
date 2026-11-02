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
## Intent (khởi tạo intent để chuyển từ activity này sang activity khác)
**Syn**
```bash
Intent intent = new Intent(ContextHienTai.this, TargetActivity.class);
```
**Ex**
```java
// 1. Ánh xạ nút bấm từ XML sang Java
Button btnToPage2 = findViewById(R.id.btnToPage2);

// 2. Bắt sự kiện click
btnToPage2.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View v) {
        // 3. Khởi tạo Intent để chuyển từ MainActivity sang SecondActivity
        Intent intent = new Intent(MainActivity.this, SecondActivity.class);
        
        // (Mở rộng nếu cần truyền dữ liệu sang trang 2):
        // intent.putExtra("key_data", "Xin chào trang 2");

        // 4. Lệnh thực thi chuyển trang
        startActivity(intent);
    }
});
```
### startActivity()
**Ex**
```java
// 1. Ánh xạ nút bấm từ XML sang Java
Button btnToPage2 = findViewById(R.id.btnToPage2);

// 2. Bắt sự kiện click
btnToPage2.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View v) {
        // 3. Khởi tạo Intent để chuyển từ MainActivity sang SecondActivity
        Intent intent = new Intent(MainActivity.this, SecondActivity.class);
        
        // (Mở rộng nếu cần truyền dữ liệu sang trang 2):
        // intent.putExtra("key_data", "Xin chào trang 2");

        // 4. Lệnh thực thi chuyển trang
        startActivity(intent);
    }
});
```
### .putExtra()  (Đính kèm dữ liệu trực tiếp vào Intent để chuyển cho activity khác)
**Syn**
```bash
intent.putExtra("KEY", giaTri);
```
**Ex**
```java
Button btnToPage2 = findViewById(R.id.btnToPage2);
final EditText edtInput = findViewById(R.id.edtInput); // Ô nhập dữ liệu

btnToPage2.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View v) {
        // 1. Lấy dữ liệu người dùng nhập vào
        String dataToSend = edtInput.getText().toString();

        // 2. Khởi tạo Intent chuyển trang
        Intent intent = new Intent(MainActivity.this, SecondActivity.class);

        // 3. Đính kèm dữ liệu vào Intent (theo cặp Key - Value)
        // Key ở đây thầy đặt là "MY_KEY", Value chính là biến dataToSend
        intent.putExtra("MY_KEY", dataToSend);

        // 4. Thực hiện chuyển trang
        startActivity(intent);
    }
});
```
## getIntent() (nhận intent)
**Ex**
```java
Intent intent = new Intent(MainActivity.this, DetailActivity.class);
intent.putExtra("maNhanVien", "NV01"); // Đính kèm dữ liệu (Key - Value)
startActivity(intent);
```
```java
Intent intent = getIntent(); // Nhận intent gửi sang
String ma = intent.getStringExtra("maNhanVien"); // Lấy dữ liệu ra theo Key
```
### .getStringExtra()
PHẦN 1: Gửi dữ liệu đi từ Trang 1 (MainActivity.java)
Giả sử ở giao diện trang 1 (activity_main.xml), em có một ô nhập văn bản (EditText) có id là edtInput và một nút bấm btnToPage2.

Trong file MainActivity.java, em viết code như sau:

Java
Button btnToPage2 = findViewById(R.id.btnToPage2);
final EditText edtInput = findViewById(R.id.edtInput); // Ô nhập dữ liệu

btnToPage2.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View v) {
        // 1. Lấy dữ liệu người dùng nhập vào
        String dataToSend = edtInput.getText().toString();

        // 2. Khởi tạo Intent chuyển trang
        Intent intent = new Intent(MainActivity.this, SecondActivity.class);

        // 3. Đính kèm dữ liệu vào Intent (theo cặp Key - Value)
        // Key ở đây thầy đặt là "MY_KEY", Value chính là biến dataToSend
        intent.putExtra("MY_KEY", dataToSend);

        // 4. Thực hiện chuyển trang
        startActivity(intent);
    }
});
PHẦN 2: Nhận và hiển thị dữ liệu ở Trang 2 (SecondActivity.java)
Giả sử ở giao diện trang 2 (activity_second.xml), em đã kéo sẵn một cái nhãn (TextView) để hiển thị dữ liệu nhận được, và gán id cho nó là tvDisplay.

Trong file SecondActivity.java (bên trong hàm onCreate), em viết code nhận dữ liệu như sau:

Java
// 1. Ánh xạ TextView từ XML sang Java
TextView tvDisplay = findViewById(R.id.tvDisplay);

// 2. Lấy Intent đã gọi activity này
Intent intent = getIntent();

// 3. Lấy dữ liệu ra bằng đúng cái Key lúc nãy đã gửi ("MY_KEY")
// Vì dữ liệu gửi là kiểu String nên ta dùng getStringExtra()
String receivedData = intent.getStringExtra("MY_KEY");

// 4. Hiển thị dữ liệu lên TextView
if (receivedData != null) {
    tvDisplay.setText("Dữ liệu nhận được: " + receivedData);
}
Lưu ý nhỏ: putExtra hỗ trợ rất nhiều kiểu dữ liệu khác nhau, tùy theo loại dữ liệu em gửi mà lúc nhận em dùng hàm tương ứng:

Gửi chuỗi: intent.putExtra("key", "chuỗi"); 
→ Nhận: intent.getStringExtra("key");

Gửi số nguyên: intent.putExtra("key", 123); 
→ Nhận: intent.getIntExtra("key", giá_trị_mặc_định);

Em đã hình dung được cách truyền dữ liệu qua lại giữa các Activity này chưa? Khi nào em đã hiểu và muốn chuyển sang phần tiếp theo (ví dụ: Tạo Menu hoặc Lưu file Internal/External), hãy gõ "next step" nhé!
