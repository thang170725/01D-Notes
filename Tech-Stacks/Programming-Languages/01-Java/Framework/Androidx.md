- [AndroidX (xây dựng Android app hiện đại, được phân phối dưới dạng dependencies của project)](#androidx-xây-dựng-android-app-hiện-đại-được-phân-phối-dưới-dạng-dependencies-của-project)
- [appcompat](#appcompat)
  - [app](#app)
    - [AppCompatActivity](#appcompatactivity)
---
# AndroidX (xây dựng Android app hiện đại, được phân phối dưới dạng dependencies của project)
Tại sao AndroidX phải cài bằng Gradle?

Trong project của bạn có file:

build.gradle.kts

hoặc:

build.gradle

Android Studio sẽ có dependencies kiểu:

dependencies {
    implementation(libs.androidx.appcompat)
}

Hoặc project cũ có thể thấy:

implementation 'androidx.appcompat:appcompat:...'

Gradle sẽ tải thư viện đó về.

Bạn không cần tự download file .jar hoặc .aar.

Android Studio + Gradle quản lý việc này.

# appcompat
## app 
### AppCompatActivity
**Ex**
```java
import androidx.appcompat.app.AppCompatActivity;

public class MainActivity extends AppCompatActivity {
    
}

// AppCompatActivity là một Activity thuộc AndroidX.
// Có thể hình dung: Activity <- AppCompatActivity <- MainActivity
```
15. Tại sao Android Studio vừa tạo project đã dùng được AndroidX?

Vì template project của Android Studio đã cấu hình sẵn.

Khi bạn tạo:

New Project
    ↓
Empty Activity

Android Studio tạo cho bạn một project có sẵn:

Gradle
Android SDK
AndroidX dependencies

Sau đó Gradle tải dependencies cần thiết.

Cho nên bạn chỉ việc:

import androidx.appcompat.app.AppCompatActivity;

mà không cần tự đi tìm thư viện trên Google.