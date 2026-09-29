- [findViewById (Lấy các thành phần từ XML)](#findviewbyid-lấy-các-thành-phần-từ-xml)
- [setOnClickListener (Lắng nghe sự kiện bấm nút)](#setonclicklistener-lắng-nghe-sự-kiện-bấm-nút)
- [TextView](#textview)
---
# findViewById (Lấy các thành phần từ XML)
```bash
findViewById(...) là hàm tìm một thành phần giao diện trong XML thông qua ID.
```
**Ex**
```java
Button button = findViewById(R.id.button); // Button: kiểu dữ liệu, cho biết biến này đại diện cho một nút bấm
TextView content = findViewById(R.id.content);
```
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
# TextView
## .getVisibility() (Lấy trạng thái hiển thị hiện tại của TextView)
## .setVisibility() (Thay đổi trạng thái hiển thị của TextView)

tại sao chỗ này lại là view mà không phải TextView "button.setOnClickListener(new View.OnClickListener() {
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
});"

Vì View ở đây không phải là cái Button, mà là kiểu dữ liệu cha (class cha) của rất nhiều thành phần giao diện Android, trong đó có Button và TextView.

Đây là một khái niệm Java/Android rất quan trọng. Bạn mới học Java thì có thể hiểu theo từng bước.

1. Button thực chất cũng là một View

Trong Android, có quan hệ kiểu:

View
├── TextView
│   └── Button
├── EditText
├── ImageView
├── CheckBox
└── ...

Tức là:

Button

là một loại:

View

Vì vậy Android có thể dùng View để đại diện cho các thành phần giao diện nói chung.

2. Vậy View v là gì?

Trong:

@Override
public void onClick(View v) {

}

v là đối tượng View vừa được click.

Ví dụ bạn có:

Button button = findViewById(R.id.button);

sau đó:

button.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View v) {

    }
});

Khi bạn bấm button, Android sẽ tự gọi:

onClick(...)

và truyền Button vừa được bấm vào biến v.

Mặc dù v có kiểu:

View

nhưng đối tượng thực tế mà nó đang tham chiếu có thể là:

Button
3. Tại sao không viết Button v?

Về mặt ý tưởng, bạn có thể nghĩ:

public void onClick(Button v)

nhưng Android thiết kế OnClickListener để có thể dùng cho mọi loại View, không chỉ Button.

Ví dụ:

TextView
ImageView
Button
EditText
CheckBox

đều có thể nhận sự kiện click.

Do đó Android quy định:

public void onClick(View v)

Thay vì:

public void onClick(Button v)

Nhờ vậy cùng một OnClickListener có thể dùng cho nhiều loại thành phần.

4. Ví dụ rất dễ hiểu

Giả sử:

Button button = findViewById(R.id.button);

button.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View v) {

    }
});

Có thể hình dung Android làm gần giống:

Bạn bấm Button
      ↓
Android phát hiện Button được click
      ↓
Android gọi onClick()
      ↓
Android đưa Button vào biến v
      ↓
onClick(View v)

Nên trong trường hợp này:

v

thực tế đang chứa Button được click.

5. Còn content tại sao lại là TextView?

Đây lại là một chuyện khác:

TextView content = findViewById(R.id.content);

Chúng ta khai báo:

TextView content

vì content trong XML là:

<TextView
    android:id="@+id/content"
    ...
/>

Và chúng ta muốn sử dụng những chức năng riêng của TextView.

Ví dụ:

content.setText("Xin chào");

Đây là chức năng của TextView.

Trong khi đó:

content.setVisibility(View.VISIBLE);

setVisibility() là chức năng mà View cung cấp và TextView được thừa hưởng.

6. Đây chính là tính kế thừa trong Java

Bạn đang bắt đầu gặp một phần rất quan trọng của Java:

View
  ↑
TextView
  ↑
Button

Nếu class con kế thừa class cha:

class TextView extends View

thì TextView có thể sử dụng những thứ mà View có.

Tương tự:

class Button extends TextView

nên Button cũng kế thừa những thứ từ TextView, và cuối cùng từ View.

Vì vậy:

View v

có thể chứa một Button.

Đây là lý do bạn sẽ thấy Android code sử dụng View rất nhiều, ngay cả khi thành phần bạn đang làm việc thực tế là Button, TextView, ImageView...

Bạn nên nhớ câu này:

View là lớp cơ sở cho các thành phần giao diện Android. Button, TextView, ImageView... đều là những loại View.

Nếu bạn muốn, bước tiếp theo mình có thể giải thích 
new View.OnClickListener() { ... } thực chất là cái gì, vì đây chính là phần Java hơi khó hiểu nhất trong đoạn code trên.

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

## 4.8 