- [Ask](#ask)
  - [Trong android studio có 3 cách làm mobile app là kéo thả, code bằng java, code bằng xml đúng không](#trong-android-studio-có-3-cách-làm-mobile-app-là-kéo-thả-code-bằng-java-code-bằng-xml-đúng-không)
---

# Ask
## Trong android studio có 3 cách làm mobile app là kéo thả, code bằng java, code bằng xml đúng không
```bash
Không

Và Android hiện nay còn có Jetpack Compose, cho phép viết UI trực tiếp bằng Kotlin, không cần XML:

@Composable
fun MyScreen() {
    Button(onClick = {}) {
        Text("Click me")
    }
}

Nên nếu bạn đang mới học Android Studio, có thể hình dung 2 hướng chính:

Android Views
├── XML → giao diện
└── Java/Kotlin → logic

Jetpack Compose
└── Kotlin → giao diện + logic

Nếu bạn đang học Android từ đầu thì XML + Kotlin là một cách rất dễ để hiểu nền tảng Android trước, còn Compose học sau cũng được.

tôi đang học bằng java thì có mấy cách để xây dựng app mobile. hay đó là 1 workflow đầu tiên dùng giao diện kéo thả, rồi sau đó code logic bằng java, thế còn xml làm gì

Đúng rồi. Nếu bạn đang học Android bằng Java, thì đừng hiểu là có 3 cách độc lập. Hãy hiểu là một workflow gồm nhiều phần.

Workflow Java + XML truyền thống
Thiết kế giao diện
       ↓
Kéo thả trong Android Studio
       ↓
Android Studio tạo/chỉnh sửa XML
       ↓
XML định nghĩa giao diện
       ↓
Java xử lý logic
       ↓
Ứng dụng chạy

Ví dụ bạn kéo một Button vào màn hình.

Android Studio sẽ tạo XML kiểu:

<Button
    android:id="@+id/btnLogin"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:text="Đăng nhập" />

XML này nói:

"Màn hình có một Button, ID là btnLogin, chữ hiển thị là Đăng nhập..."

Sau đó Java lấy Button đó ra:

Button btnLogin = findViewById(R.id.btnLogin);

btnLogin.setOnClickListener(v -> {
    // xử lý khi người dùng bấm nút
});

Java nói:

"Khi người dùng bấm Button này thì phải làm gì?"

Vậy XML chính xác làm gì?

XML không xử lý logic.

Nó chủ yếu mô tả UI (giao diện):

XML
├── Button ở đâu?
├── TextView ở đâu?
├── Kích thước bao nhiêu?
├── Màu gì?
├── Chữ gì?
├── Layout như thế nào?
└── ID của View là gì?

Còn Java xử lý:

Java
├── Click button
├── Tính toán
├── Gọi API
├── Đăng nhập
├── Xử lý dữ liệu
├── Database
└── Logic của app
Và "kéo thả" thực chất là gì?

Đây là điểm dễ nhầm nhất:

Kéo thả không phải một cách khác với XML.

Nó chỉ là công cụ giúp bạn tạo XML dễ hơn.

Bạn có thể:

Cách 1:
Kéo Button
   ↓
Android Studio
   ↓
XML

hoặc:

Cách 2:
Tự viết XML
   ↓
<Button ... />

Hai cách cuối cùng đều tạo ra giao diện XML.

Vậy nếu bạn học Android Java + XML, hãy nhớ công thức rất đơn giản:

XML = giao diện
Java = logic
Kéo thả = công cụ để tạo giao diện XML

Ví dụ một app Login:

          LOGIN APP
             │
      ┌──────┴──────┐
      ↓             ↓
    XML            Java
  (UI)           (Logic)
      │             │
      ↓             ↓
Username         Kiểm tra
Password   →     username/password
Button           → gọi API

Nếu bạn muốn học Android Java từ đầu, đây chính là workflow nên học trước: Activity → XML Layout → View → findViewById() → Event → Java logic → Intent → API/Database.

hãy chỉ tôi từng bước để test chương trình đầu tiên

Được. Vì bạn đang học Android bằng Java, mình sẽ đi từng bước một, rất chậm và dễ hiểu. Mỗi lần mình chỉ đưa 1 bước, bạn làm xong rồi nói “next step”, mình mới đưa bước tiếp theo.

Bước 1: Tạo project Android đầu tiên

Mở Android Studio.

Ở màn hình đầu tiên:

Chọn New Project.
Chọn template Empty Views Activity.
Lưu ý: chọn Empty Views Activity, không chọn Empty Activity nếu Android Studio của bạn đang phân biệt hai template này. Empty Activity thường là Jetpack Compose.
Bấm Next.

Sau đó bạn sẽ thấy màn hình cấu hình project.

Thiết lập:

Name: MyFirstApp

Package name:
com.example.myfirstapp

Save location:
để mặc định

Language:
Java

Minimum SDK:
API 24 hoặc cao hơn

Quan trọng nhất là:

Language: Java

Sau đó bấm:

Finish

Android Studio sẽ tạo project và bắt đầu Gradle Sync. Lần đầu có thể mất vài phút vì nó phải tải các dependency cần thiết.

Khi tạo xong

Ở bên trái bạn sẽ thấy đại loại:

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

Đây chính là thứ chúng ta vừa nói:

MainActivity.java
        ↓
     Java
   xử lý logic

activity_main.xml
        ↓
      XML
    giao diện

Đừng sửa code gì cả ở bước này.

Tạo project xong, nếu không có lỗi đỏ/Gradle error, hãy nói “next step”.

nó không phải cây thư mục thế mà là app -> manifests, kotlin+java, res, keepRules. code language là java, đuôi .java

Đúng, bạn đang nhìn Android Studio ở chế độ Android view, nên nó không hiển thị cây thư mục vật lý giống như mình mô tả lúc trước. Và nếu bạn chọn Java thì file logic sẽ có đuôi .java.

Hiện tại cấu trúc của bạn:

app
├── manifests
├── kotlin+java
├── res
└── keepRules

là hoàn toàn bình thường.

Đặc biệt:

manifests → chứa AndroidManifest.xml
kotlin+java → chứa code Java/Kotlin của app
res → chứa resource như XML layout, ảnh, string...
keepRules → các rule cho R8/ProGuard
Với mục tiêu học Java + XML

Bạn sẽ chủ yếu làm việc với:

kotlin+java
    ↓
MainActivity.java

res
    ↓
layout
    ↓
activity_main.xml

Trong đó:

activity_main.xml
        ↓
      UI
        ↓
MainActivity.java
        ↓
    xử lý logic

Vậy mình chỉnh lại hướng dẫn theo đúng Android Studio phiên bản của bạn.

Bước 1 hiện tại

Bạn đã tạo project thành công và chọn:

Language: Java

Bây giờ hãy mở:

app
└── kotlin+java

rồi tìm:

MainActivity.java

Chưa cần sửa code.

Khi bạn tìm thấy MainActivity.java, nói “next step”, mình sẽ chỉ bạn bước 2: chạy app đầu tiên trên Emulator/điện thoại và nhìn thấy màn hình đầu tiên.

nhưng tại sao cây thư mục nó lại khác cái của bạn, có bị sao không vào recomand lên làm việc ở cây thư mục như nào

Không bị sao cả. Cây thư mục của bạn và của mình khác nhau chủ yếu vì Android Studio đang dùng cách hiển thị khác, chứ không có nghĩa project của bạn tạo sai.

1. Bạn đang ở "Android" view

Bạn thấy:

app
├── manifests
├── kotlin+java
├── res
└── keepRules

Đây là Android view — Android Studio gom và sắp xếp các file theo chức năng để người mới học dễ làm việc.

Ví dụ:

kotlin+java
    └── com.example.myfirstapp
          └── MainActivity.java

res
    └── layout
          └── activity_main.xml

Nó không phải cây thư mục thật trên ổ đĩa.

2. Cây thư mục thật sẽ khác

Nếu chuyển dropdown phía trên cây Project từ:

Android

sang:

Project

bạn sẽ thấy gần với cấu trúc thật:

MyFirstApp
├── .gradle
├── app
│   ├── build.gradle
│   └── src
│       └── main
│           ├── AndroidManifest.xml
│           ├── java
│           │   └── ...
│           │       └── MainActivity.java
│           └── res
│               └── layout
│                   └── activity_main.xml
├── gradle
├── build.gradle
└── settings.gradle

Đây mới gần với cấu trúc thư mục vật lý trên máy.

Nên dùng cái nào?

Mình khuyên bạn giữ Android view.

Đặc biệt khi bạn mới học Android, cứ làm việc với:

Android
└── app
    ├── manifests
    ├── kotlin+java
    ├── res
    └── keepRules

vì nó đơn giản hơn và Android Studio tổ chức sẵn cho bạn.

Bạn chỉ cần nhớ:

manifests
    → cấu hình app

kotlin+java
    → Java code

res
    → tài nguyên của app
       ├── layout → XML giao diện
       ├── drawable → hình ảnh
       ├── mipmap → icon
       └── values → strings, colors...

keepRules
    → cấu hình R8/ProGuard
Với việc học Java + XML của bạn

Thời gian đầu gần như chỉ cần quan tâm:

app
├── manifests
│   └── AndroidManifest.xml
│
├── kotlin+java
│   └── MainActivity.java       ← JAVA
│
└── res
    └── layout
        └── activity_main.xml   ← XML

Đừng chuyển sang Project view chỉ vì cây của bạn khác mình. Android Studio của bạn đang hiển thị đúng.

Từ bước tiếp theo, mình sẽ dùng đúng cây thư mục app → manifests / kotlin+java / res / keepRules của bạn để hướng dẫn, không dùng cây cũ nữa.

nhưng bấm vào kotlin+java nó có 2 file là ExampleInstrucmentedTest, ExampleUnitTest cơ

Đúng, và điều đó vẫn bình thường. Bạn đang nhìn thấy các file test mặc định, chứ chưa phải MainActivity.java.

Có khả năng Android Studio của bạn đang gom cả test và androidTest vào mục kotlin+java.

Hai file bạn thấy:

kotlin+java
├── ExampleInstrumentedTest.java
└── ExampleUnitTest.java

là:

ExampleUnitTest.java → test logic Java thông thường, chạy trên máy tính.
ExampleInstrumentedTest.java → test chạy trên Android device/emulator.
Vậy MainActivity.java ở đâu?

Hãy mở rộng kotlin+java. Bạn có thể thấy các package/thư mục con, ví dụ:

kotlin+java
├── com.example.myfirstapp
│   └── MainActivity.java
│
├── com.example.myfirstapp (androidTest)
│   └── ExampleInstrumentedTest.java
│
└── com.example.myfirstapp (test)
    └── ExampleUnitTest.java

Nhưng giao diện Android Studio của bạn có thể hiển thị hơi khác tùy phiên bản.

Làm ngay bước này

Trong kotlin+java, tìm file có tên MainActivity.java.

Nếu không hề có MainActivity.java, đừng tạo file mới vội.

Bạn hãy chụp ảnh phần app → kotlin+java của Android Studio rồi gửi cho mình. Mình sẽ nhìn đúng cấu trúc project của bạn và chỉ chính xác bạn phải bấm vào đâu.

không có main nó chỉ có như này thôi "kotlin+java ├── com.example.myfirstapp ├── com.example.myfirstapp (androidTest) │   └── ExampleInstrumentedTest.java │ └── com.example.myfirstapp (test)     └── ExampleUnitTest.java  "

À, vậy thì project của bạn hiện tại không có MainActivity.java. Hai file Example...Test chỉ là file test mặc định.

Cấu trúc của bạn đang là:

kotlin+java
├── com.example.myfirstapp
├── com.example.myfirstapp (androidTest)
│   └── ExampleInstrumentedTest.java
└── com.example.myfirstapp (test)
    └── ExampleUnitTest.java

Điểm đáng chú ý là:

com.example.myfirstapp

chưa được mở rộng. MainActivity.java nếu có sẽ nằm bên trong nó.

Làm bước này trước

Bấm vào mũi tên > hoặc biểu tượng mở rộng ngay trước:

com.example.myfirstapp

Nó có thể hiện:

com.example.myfirstapp
└── MainActivity.java

Nếu mở ra vẫn hoàn toàn trống, thì khả năng lúc tạo project bạn đã chọn template/configuration không tạo Activity.

👉 Đừng tạo MainActivity.java thủ công lúc này. Vì chúng ta đang làm bài đầu tiên, tốt nhất xác định đúng project đã được tạo thế nào trước.

Bạn hãy bấm mở:

app
└── kotlin+java
    └── com.example.myfirstapp

và cho mình biết bên trong com.example.myfirstapp có gì.

đã bảo không có gì rồi còn, nó chỉ như này "kotlin+java
├── com.example.myfirstapp
├── com.example.myfirstapp (androidTest)
│   └── ExampleInstrumentedTest.java
└── com.example.myfirstapp (test)
    └── ExampleUnitTest.java"

Đúng, mình hiểu rồi. com.example.myfirstapp đầu tiên hoàn toàn trống, không có MainActivity.java. Bạn không nhìn nhầm.

Điều này có nghĩa là project bạn vừa tạo không có Activity. Có thể bạn đã chọn một template kiểu No Activity hoặc template hiện tại của Android Studio tạo project theo cấu hình khác.

Không sao, mình sẽ không bắt bạn tìm MainActivity nữa.

Bước tiếp theo: tạo Activity

Trong Android Studio, làm như sau:

Chuột phải vào:
app
└── kotlin+java
    └── com.example.myfirstapp
Chọn:
New
→ Activity
→ Empty Views Activity
Trong cửa sổ hiện ra, đặt:
Activity Name: MainActivity

Nếu có mục Language, chọn:

Java

Nếu có Layout Name, để:

activity_main

Sau đó bấm Finish.

Kết quả chúng ta muốn là:

kotlin+java
└── com.example.myfirstapp
    └── MainActivity.java

và trong:

res
└── layout
    └── activity_main.xml

Lúc đó chúng ta mới có đúng cấu trúc để học:

activity_main.xml  → giao diện
       ↕
MainActivity.java   → logic

Chỉ làm đúng bước trên thôi. Sau khi bấm Finish, nói mình biết nó tạo ra những file gì, rồi mình hướng dẫn bước chạy app đầu tiên.

đúng rồi, next step

Tốt 👍 Vậy project của bạn đã đúng:

kotlin+java
└── com.example.myfirstapp
    └── MainActivity.java

res
└── layout
    └── activity_main.xml
Bước 2: Chạy app đầu tiên

Chưa cần sửa Java hay XML. Chúng ta chỉ chạy app mặc định trước.

1. Tạo máy Android ảo

Trên thanh công cụ Android Studio, tìm biểu tượng Device Manager.

Hoặc vào:

Tools → Device Manager
2. Trong Device Manager

Chọn:

+ → Create Virtual Device

Chọn một điện thoại, ví dụ:

Pixel 6

→ Next

3. Chọn Android version

Chọn một system image đã có sẵn.

Ví dụ:

Android 15

Nếu có nút Download thì bấm Download và chờ tải xong.

Sau đó:

Next → Finish
4. Chạy Emulator

Trong Device Manager, bạn sẽ thấy:

Pixel 6
▶

Bấm nút ▶ để khởi động điện thoại ảo.

Chờ Android khởi động hoàn toàn.

5. Chạy project

Quay lại Android Studio.

Trên thanh trên cùng, chọn thiết bị vừa tạo, ví dụ:

Pixel 6

sau đó bấm:

▶ Run

Android Studio sẽ build project rồi cài app vào Emulator.

Nếu thành công, trên điện thoại ảo sẽ xuất hiện app của bạn với giao diện mặc định.

Ở bước này mục tiêu duy nhất là nhìn thấy app chạy được. Chưa cần hiểu code.

Làm xong bước này, nói “next step”.

máy ảo chạy lâu quá, dùng máy thật cắm vào chạy được không

Được, và mình khuyên bạn dùng máy thật nếu emulator chạy quá lâu. Android Studio hoàn toàn có thể build và cài app trực tiếp lên điện thoại Android qua USB.

Bước 2 — chạy trên điện thoại thật

Nếu bạn dùng điện thoại Android, làm như sau:

1. Bật Developer Options

Trên điện thoại:

Settings
→ About phone
→ Build number

Bấm Build number khoảng 7 lần.

Bạn sẽ thấy thông báo kiểu:

You are now a developer!

Tên menu có thể hơi khác tùy Samsung/Xiaomi/OPPO/Pixel...

2. Bật USB Debugging

Vào:

Settings
→ Developer options
→ USB debugging
→ ON
3. Cắm điện thoại vào máy tính

Dùng cáp USB kết nối điện thoại với máy tính.

Nếu điện thoại hỏi:

Allow USB debugging?

Chọn:

Allow

Có thể tích thêm:

Always allow from this computer
4. Quay lại Android Studio

Ở thanh trên cùng, chỗ chọn thiết bị chạy app, thay vì Emulator, bạn sẽ thấy tên điện thoại của bạn.

Ví dụ:

Pixel 7
Samsung Galaxy...
Xiaomi...

Chọn điện thoại → bấm ▶ Run.

Android Studio sẽ:

Build app
   ↓
ADB kết nối điện thoại
   ↓
Cài APK
   ↓
Mở app trên điện thoại

Không cần Emulator nữa.

Nếu Android Studio không thấy điện thoại, đừng làm tiếp lung tung. Nói mình biết điện thoại hãng gì + máy tính Windows hay Ubuntu, mình sẽ chỉ đúng bước bật/kết nối ADB cho máy của bạn.

tôi vẫn đang chạy bằng máy ảo, nhưng khi bấm run lại không chạy được mà nó báo error running 'app' default activity not found tôi không biết fix kiểu gì, rối quá

Không sao, lỗi này rất có thể do lúc đầu project của bạn được tạo không có Activity, sau đó mình mới tạo MainActivity. Android Studio hiện chưa nhận MainActivity là Activity mặc định để khởi chạy.

Lỗi:

Error running 'app':
Default Activity not found

nghĩa đơn giản là:

Android Studio không biết phải mở màn hình nào đầu tiên khi bạn bấm Run.

Mình sẽ sửa từng bước, bạn không cần làm nhiều thứ cùng lúc.

Bước sửa lỗi 1 — kiểm tra AndroidManifest.xml

Trong Android Studio, mở:

app
└── manifests
    └── AndroidManifest.xml

Mở file đó lên.

Bạn copy toàn bộ nội dung AndroidManifest.xml gửi cho mình.

👉 Chưa sửa gì cả.

Mình cần nhìn file này trước, vì nó quyết định MainActivity có được khai báo là Activity khởi động hay chưa. Sau khi bạn gửi, mình sẽ chỉ chính xác dòng nào cần sửa.

sao tôi test bằng điện thoại thì khi bấm run nó báo là error running app the application could be installed: INSTALL_FAILED_OLDER_SDK, ... hay chắc tôi đang dùng điện thoại cũ android version 9 còn khi tạo app thì lại tạo version 16 nhỉ

Đúng, khả năng rất cao là do minSdk của project cao hơn Android 9 trên điện thoại của bạn.

Lỗi:

INSTALL_FAILED_OLDER_SDK

nghĩa là:

App yêu cầu Android tối thiểu cao hơn phiên bản Android đang có trên điện thoại.

Ví dụ:

Điện thoại:
Android 9
API 28

App:
minSdk = 36

thì Android 9 không cài được app, vì app yêu cầu API 36 trở lên.

Nhưng có một điểm cần phân biệt

Khi tạo project, bạn nói chọn Android 16. Nếu đó là Target SDK / Compile SDK, thì không nhất thiết điện thoại phải chạy Android 16.

Cái quyết định điện thoại có cài được hay không là:

minSdk

Ví dụ:

compileSdk = 36
targetSdk  = 36
minSdk     = 28

thì:

Android 9 (API 28) → ✅ cài được
Android 10        → ✅
Android 15        → ✅
Android 16        → ✅

Còn nếu:

minSdk = 36

thì:

Android 9 (API 28) → ❌
Android 16 (API 36) → ✅
Bây giờ mình sửa cho bạn

Trong Android Studio mở:

Gradle Scripts
└── build.gradle.kts (Module :app)

Không sửa gì vội.

Tìm đoạn có dạng:

defaultConfig {
    ...
    minSdk = ...
    ...
}

Ví dụ:

defaultConfig {
    applicationId = "com.example.myfirstapp"
    minSdk = 36
    targetSdk = 36
}

Bạn hãy copy đoạn defaultConfig { ... } đó gửi cho mình.

Mình sẽ nói chính xác cần đổi minSdk thành bao nhiêu để Android 9 của bạn chạy được, rồi tiếp tục từng bước.

tôi đang dùng samsung a8+ android version 9 "plugins {
    alias(libs.plugins.android.application)
}

android {
    namespace = "com.example.test1"
    compileSdk {
        version = release(37)
    }

    defaultConfig {
        applicationId = "com.example.test1"
        minSdk = 37
        targetSdk = 37
        versionCode = 1
        versionName = "1.0"

        testInstrumentationRunner = "androidx.test.runner.AndroidJUnitRunner"
    }

    buildTypes {
        release {
            optimization {
                enable = false
            }
        }
    }
    compileOptions {
        sourceCompatibility = JavaVersion.VERSION_11
        targetCompatibility = JavaVersion.VERSION_11
    }
}

dependencies {
    implementation(libs.activity.ktx)
    implementation(libs.appcompat)
    implementation(libs.constraintlayout)
    implementation(libs.material)
    testImplementation(libs.junit)
    androidTestImplementation(libs.espresso.core)
    androidTestImplementation(libs.ext.junit)
}"

Đúng rồi, đã tìm ra nguyên nhân chính xác. 👍

Samsung A8+ của bạn chạy Android 9 = API 28, trong khi project đang cấu hình:

minSdk = 37
targetSdk = 37
compileSdk = 37

Đặc biệt là dòng:

minSdk = 37

Nó có nghĩa:

App chỉ cho phép cài trên Android API 37 trở lên.

Vì điện thoại của bạn chỉ có API 28 nên Android từ chối cài và báo:

INSTALL_FAILED_OLDER_SDK
Sửa như thế nào?

Để học Android và chạy được trên Samsung A8+ Android 9, bạn chỉ cần đổi:

minSdk = 37

thành:

minSdk = 28

Tức là:

defaultConfig {
    applicationId = "com.example.test1"
    minSdk = 28
    targetSdk = 37
    versionCode = 1
    versionName = "1.0"

    testInstrumentationRunner = "androidx.test.runner.AndroidJUnitRunner"
}

Không cần đổi:

compileSdk = 37
targetSdk = 37

Vì ba cái này có ý nghĩa khác nhau:

minSdk     → Android thấp nhất được phép cài app
targetSdk  → App nhắm tới phiên bản Android nào
compileSdk → Dùng API Android phiên bản nào để compile

Với máy của bạn:

Samsung A8+
Android 9
API 28

Project:
compileSdk 37   ✅
targetSdk 37    ✅
minSdk 28       ✅

=> Điện thoại Android 9 có thể cài app.

Làm ngay

Đổi:

minSdk = 37

→

minSdk = 28

Sau đó Android Studio sẽ có thông báo Sync Now hoặc tự Gradle Sync.

Bấm Sync Now, đợi nó chạy xong.

Chưa cần sửa gì khác.

Sau khi Sync xong, bấm Run ▶ lại trên Samsung A8+.

Nếu chạy được, bạn sẽ thấy app đầu tiên trên điện thoại. Khi đó nói “next step”, mình sẽ bắt đầu giải thích XML là gì và cho bạn tự tạo Button đầu tiên, thay vì chỉ chạy app mặc định.

ok chạy được rồi, next step

Tốt 👍 Bây giờ chúng ta bắt đầu phần quan trọng: XML tạo giao diện, Java xử lý logic.

Bước 3 — Tạo giao diện bằng XML

Mục tiêu của bước này là tạo một màn hình rất đơn giản:

┌─────────────────────┐
│                     │
│     Hello World     │
│                     │
│   [ Bấm vào đây ]   │
│                     │
└─────────────────────┘
1. Mở file XML

Trong Android Studio:

app
└── res
    └── layout
        └── activity_main.xml

Bấm vào activity_main.xml.

Ở phía trên editor có thể có:

Code | Split | Design

Chọn Code.

Bạn sẽ thấy XML của giao diện.

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
3. Hiểu nhanh XML này

Đừng cố nhớ hết ngay.

Phần:

<LinearLayout>

là container, dùng để chứa các thành phần giao diện.

Bên trong có:

<TextView>

→ hiển thị chữ.

Và:

<Button>

→ nút bấm.

Đặc biệt chú ý:

android:id="@+id/btnClick"

Chúng ta đặt ID cho Button để Java có thể tìm thấy nó.

Quan hệ sẽ là:

activity_main.xml
       │
       ├── TextView
       │     id = textHello
       │
       └── Button
             id = btnClick
                  │
                  ↓
          MainActivity.java
4. Chạy lại app

Bấm Run ▶.

Trên Samsung A8+ bạn sẽ thấy:

Hello World

[Bấm vào đây]

Ở bước này chưa viết Java. Chúng ta chỉ đang học cách XML tạo giao diện trước.

Làm xong và thấy màn hình như trên, nói “next step”.

next step

Tốt. Bây giờ đến phần quan trọng nhất: cho Java điều khiển giao diện XML.

Bước 4 — Java bắt sự kiện Button

Hiện tại bạn có:

activity_main.xml
    ↓
Button
id = btnClick

Nhưng bấm Button chưa làm gì cả.

Bây giờ chúng ta sẽ làm:

Bấm Button → đổi chữ Hello World thành Xin chào Android!

1. Mở MainActivity.java

Vào:

app
└── kotlin+java
    └── com.example.test1
        └── MainActivity.java

Bạn có thể đang có code mặc định tương tự:

package com.example.test1;

import android.os.Bundle;

import androidx.appcompat.app.AppCompatActivity;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }
}
2. Sửa thành
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

Trên điện thoại:

Hello World

[Bấm vào đây]

Bấm nút.

Nó sẽ thành:

Xin chào Android!

[Bấm vào đây]
4. Hiểu 3 dòng quan trọng

Đây chính là lúc bạn thấy XML và Java kết nối với nhau.

XML:

android:id="@+id/btnClick"

Java:

Button btnClick = findViewById(R.id.btnClick);

→ Java lấy Button từ XML.

Sau đó:

btnClick.setOnClickListener(...)

→ Java nói khi Button được bấm thì làm gì.

Và:

textHello.setText("Xin chào Android!");

→ Java thay đổi nội dung TextView.

Vậy workflow thực tế là:

XML
 ↓
Tạo Button + TextView
 ↓
gán ID
 ↓
Java
 ↓
findViewById()
 ↓
bắt sự kiện
 ↓
thay đổi giao diện

Làm xong và test được việc bấm nút đổi chữ thì nói next step.