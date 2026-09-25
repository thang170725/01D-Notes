- [Android Studio Introduction](#android-studio-introduction)
- [Jetpack Compose](#jetpack-compose)
- [Android View Mode (chế độ android)](#android-view-mode-chế-độ-android)
  - [Ask](#ask)
    - [Cách xử lý khi cây thư mục không có file MainActivity.java](#cách-xử-lý-khi-cây-thư-mục-không-có-file-mainactivityjava)
- [Ask](#ask-1)
  - [workflow xây dựng mobile app trên android studio](#workflow-xây-dựng-mobile-app-trên-android-studio)
  - [Các bước để test chương trình đầu tiên bằng android studio và java](#các-bước-để-test-chương-trình-đầu-tiên-bằng-android-studio-và-java)
  - [lỗi báo error running 'app' default activity not found](#lỗi-báo-error-running-app-default-activity-not-found)
  - [Lỗi error running app the application could be installed: INSTALL\_FAILED\_OLDER\_SDK, ...](#lỗi-error-running-app-the-application-could-be-installed-install_failed_older_sdk-)
---
# Android Studio Introduction
**Cách xây dựng app android trong android studio**
```bash
Android Studio có 2 hướng chính:
    Android Views
    ├── XML → giao diện
    └── Java/Kotlin → logic

    Jetpack Compose
    └── Kotlin → giao diện + logic
```
# Jetpack Compose
```bash
Android hiện nay còn có Jetpack Compose, cho phép viết UI trực tiếp bằng Kotlin, không cần XML:
```
# Android View Mode (chế độ android)
```bash
nên để cây thư mục ở chế độ Android view khi:
    - mới học
    - cần đơn giản hơn và Android Studio tổ chức sẵn cho bạn.
```
**Architechture**
```bash
# cấu trúc thông thường sẽ là
app
├── manifests # manifests → chứa AndroidManifest.xml
├── kotlin+java # kotlin+java → chứa code Java/Kotlin của app
├── res # res → chứa resource như XML layout, ảnh, string...
└── keepRules # keepRules → các rule cho R8/ProGuard
```
## Ask
### Cách xử lý khi cây thư mục không có file MainActivity.java
```bash
Việc không có Activity. Có thể bạn đã chọn một template kiểu No Activity hoặc template hiện tại của Android Studio tạo project theo cấu hình khác.
```
**tạo Activity**
```bash
1.  Chuột phải vào:
    app
    └── kotlin+java
        └── com.example.myfirstapp
2. Chọn: New → Activity → Empty Views Activity
    - Trong cửa sổ hiện ra, đặt: Activity Name: MainActivity
    - Nếu có mục Language, chọn: Java
    - Nếu có Layout Name, để: activity_main
    - Sau đó bấm Finish.
    - Kết quả chúng ta muốn là:
        kotlin+java
        └── com.example.myfirstapp
            └── MainActivity.java

    - và trong:
        res
        └── layout
            └── activity_main.xml
```
# Ask
## workflow xây dựng mobile app trên android studio
```bash
Workflow Java + XML truyền thống:
    Thiết kế giao diện -> Kéo thả trong Android Studio -> Android Studio tạo/chỉnh sửa XML -> XML định nghĩa giao diện -> Java xử lý logic -> Ứng dụng chạy
```
**Ex: Tạo Button**
**Ví dụ bạn kéo một Button vào màn hình.**
```html
<!-- Android Studio sẽ tạo XML kiểu: -->

<Button
    android:id="@+id/btnLogin"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:text="Đăng nhập" 
/>
<!-- XML này nói: Màn hình có một Button, ID là btnLogin, chữ hiển thị là Đăng nhập..." -->
```
**Sau đó Java lấy Button đó ra**
```java
Button btnLogin = findViewById(R.id.btnLogin);

btnLogin.setOnClickListener(v -> {
    // xử lý khi người dùng bấm nút
});
// Java nói: "Khi người dùng bấm Button này thì phải làm gì?"
```
## Các bước để test chương trình đầu tiên bằng android studio và java
**Bước 1: Tạo project Android đầu tiên**
```bash
1. Mở Android Studio. Ở màn hình đầu tiên:
    1.1. Chọn New Project.
    1.2. Chọn template Empty Views Activity. # Lưu ý: chọn Empty Views Activity, không chọn Empty Activity nếu Android Studio của bạn đang phân biệt hai template này Empty Activity thường là Jetpack Compose.
    1.3. Bấm Next.

2. Thiết lập:
    2.1. Name: MyFirstApp
    2.2. Package name: com.example.myfirstapp
    2.3. Save location: để mặc định
    2.4. Language: Java
    2.5. Minimum SDK: API 24 hoặc cao hơn
    2.6. Finish
    2.7. Ở bên trái bạn sẽ thấy đại loại:
        app
        └── src
            └── main
                ├── java
                │   └── com.example.myfirstapp
                │       └── MainActivity.java
                │
                └── res
                    └── layout
                        └── activity_main.xml
```
**Bước 2: Tạo máy Android ảo**
```bash
1. Trên thanh công cụ Android Studio, tìm biểu tượng Device Manager. Hoặc vào:
    Tools → Device Manager
2. Trong Device Manager
    2.1. Chọn: + → Create Virtual Device
    2.2. Chọn một điện thoại, ví dụ: Pixel 6 → Next
3. Chọn Android version
    - Chọn một system image đã có sẵn. Ví dụ: Android 15
    - Nếu có nút Download thì bấm Download và chờ tải xong.
    - Sau đó: Next → Finish
4. Chạy Emulator
    - Trong Device Manager, bạn sẽ thấy: Pixel 6 ▶
    - Bấm nút ▶ để khởi động điện thoại ảo.
    - Chờ Android khởi động hoàn toàn.
5. Chạy project
    Quay lại Android Studio.
    Trên thanh trên cùng, chọn thiết bị vừa tạo, ví dụ:
    Pixel 6 sau đó bấm: ▶ Run
    Android Studio sẽ build project rồi cài app vào Emulator. Nếu thành công, trên điện thoại ảo sẽ xuất hiện app của bạn với giao diện mặc định.
```
**Bước 2 — chạy trên điện thoại thật**
```bash
Nếu bạn dùng điện thoại Android, làm như sau:

1. Bật Developer Options
    Trên điện thoại: Settings → About phone → Build number # Bấm Build number khoảng 7 lần.
        - Bạn sẽ thấy thông báo kiểu: You are now a developer!
        - Tên menu có thể hơi khác tùy Samsung/Xiaomi/OPPO/Pixel...

2. Bật USB Debugging
    Vào: Settings → Developer options → USB debugging → ON

3. Cắm điện thoại vào máy tính
    Dùng cáp USB kết nối điện thoại với máy tính.
    Nếu điện thoại hỏi: Allow USB debugging? Chọn: Allow
    Có thể tích thêm: Always allow from this computer

4. Quay lại Android Studio
    Ở thanh trên cùng, chỗ chọn thiết bị chạy app, thay vì Emulator, bạn sẽ thấy tên điện thoại của bạn.
    Ví dụ:
        - Pixel 7
        - Samsung Galaxy...
        - Xiaomi...
    Chọn điện thoại → bấm ▶ Run.
        Android Studio sẽ: Build app -> ADB kết nối điện thoại -> Cài APK -> Mở app trên điện thoại # Không cần Emulator nữa.
```
**Bước 3 — Tạo giao diện bằng XML**
```bash
1. Mở file XML trong Android Studio:
    app
    └── res
        └── layout
            └── activity_main.xml

    Bấm vào activity_main.xml.

    Ở phía trên editor có thể có: Code | Split | Design -> Chọn Code. # Bạn sẽ thấy XML của giao diện.

2. Xóa nội dung hiện tại
    Xóa toàn bộ nội dung trong activity_main.xml.
    Sau đó dán đoạn này:
        <?xml version="1.0" encoding="utf-8"?>
        <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:orientation="vertical"
            android:gravity="center">

            <TextView
                android:id="@+id/textHello"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:text="Hello World"
                android:textSize="24sp" />

            <Button
                android:id="@+id/btnClick"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:text="Bấm vào đây" />

        </LinearLayout>
4. Chạy lại app
    Bấm Run ▶.
```
**Bước 4: Java bắt sự kiện Button**
```bash
1. Mở MainActivity.java Vào:
    app
    └── kotlin+java
        └── com.example.test1
            └── MainActivity.java

2. Sửa code thành
    package com.example.test1;

    import android.os.Bundle;
    import android.widget.Button;
    import android.widget.TextView;

    import androidx.appcompat.app.AppCompatActivity;

    public class MainActivity extends AppCompatActivity {

        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);

            TextView textHello = findViewById(R.id.textHello);
            Button btnClick = findViewById(R.id.btnClick);

            btnClick.setOnClickListener(v -> {
                textHello.setText("Xin chào Android!");
            });
        }
    }
3. Chạy app
    Bấm Run ▶.
```
## lỗi báo error running 'app' default activity not found 
```bash
Lỗi: Error running 'app': Default Activity not found
    nghĩa đơn giản là: Android Studio không biết phải mở màn hình nào đầu tiên khi bạn bấm Run.

1: kiểm tra AndroidManifest.xml
    Trong Android Studio, mở:
        app
        └── manifests
            └── AndroidManifest.xml
```
## Lỗi error running app the application could be installed: INSTALL_FAILED_OLDER_SDK, ... 
```bash
Khả năng rất cao là do minSdk của project cao hơn Android 9 trên điện thoại của bạn.

Lỗi: INSTALL_FAILED_OLDER_SDK
    nghĩa là: App yêu cầu Android tối thiểu cao hơn phiên bản Android đang có trên điện thoại.
        Ví dụ:
            Điện thoại: 
                - Android 9
                - API 28
            App:
                - minSdk = 36
    -> thì Android 9 không cài được app, vì app yêu cầu API 36 trở lên.

1. Bạn chỉ cần đổi: minSdk = 37 -> minSdk = 28
```