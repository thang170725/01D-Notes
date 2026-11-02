- [Serializable (giúp biến đối tượng thành một cục dữ liệu để có thể truyền qua lại giữa các Intent)](#serializable-giúp-biến-đối-tượng-thành-một-cục-dữ-liệu-để-có-thể-truyền-qua-lại-giữa-các-intent)
---
# Serializable (giúp biến đối tượng thành một cục dữ liệu để có thể truyền qua lại giữa các Intent)
```bash
Bình thường hàm putExtra của Intent chỉ gửi được các dữ liệu cơ bản như String, int, boolean, float, v.v
    Nhưng nếu trong ứng dụng có một đối tượng tự định nghĩa và muốn truyền đối tượng này sang activity khác trong lệnh putExtra thì class đó bắt buộc phải implements serializable.
```
**Ex: Truyền một đối tượng từ activity này sang activity khác**
*Bước 1: Tạo một Class đối tượng (Ví dụ: User.java) và cho implements Serializable*
```java
import java.io.Serializable; // <--- Thư viện đây nhé em

// Phải có chữ "implements Serializable" ở cuối
public class User implements Serializable {
    private String username;
    private int age;

    // Hàm khởi tạo (Constructor)
    public User(String username, int age) {
        this.username = username;
        this.age = age;
    }

    // Các hàm lấy dữ liệu (Getter)
    public String getUsername() { return username; }
    public int getAge() { return age; }
}
```
*Bước 2: Gói đối tượng gửi đi từ Trang 1 (MainActivity.java)*
```java
import android.content.Intent;
import android.os.Bundle;
import androidx.appcompat.app.AppCompatActivity;

public class MainActivity extends AppCompatActivity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        // 1. Tạo một đối tượng User
        User myUser = new User("Nguyen Van A", 21);

        // 2. Khởi tạo Intent chuyển trang
        Intent intent = new Intent(MainActivity.this, SecondActivity.class);

        // 3. Đưa đối tượng vào Intent (vì User đã implements Serializable nên mới cho bỏ vào đây)
        intent.putExtra("USER_OBJECT", myUser);

        // 4. Chuyển trang
        startActivity(intent);
    }
}
```
*Bước 3: Nhận đối tượng ở Trang 2 (SecondActivity.java)*
```java
import android.content.Intent;
import android.os.Bundle;
import android.widget.TextView;
import androidx.appcompat.app.AppCompatActivity;

public class SecondActivity extends AppCompatActivity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_second);

        TextView tvInfo = findViewById(R.id.tvInfo);

        // 1. Lấy Intent gửi đến
        Intent intent = getIntent();

        // 2. Lấy dữ liệu Serializable ra và Ép kiểu (Casting) về lại kiểu (User)
        User receivedUser = (User) intent.getSerializableExtra("USER_OBJECT");

        // 3. Sử dụng dữ liệu từ đối tượng
        if (receivedUser != null) {
            String info = "Tên: " + receivedUser.getUsername() + " - Tuổi: " + receivedUser.getAge();
            tvInfo.setText(info);
        }
    }
}
```
BƯỚC 4 (Bước cuối): Lưu trữ file (Internal Storage & External Storage)
Trong các bài kiểm tra Android, phần lưu file thường tập trung vào Internal Storage (Bộ nhớ trong) vì nó dễ viết và không cần xin quyền phức tạp. Thầy sẽ hướng dẫn phần này trước, kèm đầy đủ các lệnh import.

PHẦN A: Lưu file vào Bộ nhớ trong (Internal Storage)
File lưu ở đây sẽ nằm kín bên trong thư mục riêng của ứng dụng, người dùng bình thường (không root máy) sẽ không nhìn thấy được, rất an toàn để lưu dữ liệu cấu hình hoặc ghi chú cá nhân.

1. Code ghi file (Write File)
Java
import android.content.Context; // Để dùng chế độ ghi MODE_PRIVATE
import android.widget.Toast;
import java.io.FileOutputStream; // Thư viện xuất dữ liệu ra file

// --- Đoạn code thực hiện ghi file ---
String fileName = "note.txt"; // Tên file muốn lưu
String dataToWrite = "Xin chào, đây là nội dung lưu vào file!";

try {
    // Mở luồng ghi file trong bộ nhớ trong (MODE_PRIVATE: ghi đè nếu trùng tên)
    FileOutputStream fos = openFileOutput(fileName, Context.MODE_PRIVATE);
    
    // Chuyển chuỗi thành mảng byte và ghi vào file
    fos.write(dataToWrite.getBytes());
    
    // Đóng luồng sau khi ghi xong
    fos.close();
    
    Toast.makeText(this, "Lưu file thành công!", Toast.LENGTH_SHORT).show();
} catch (Exception e) {
    e.printStackTrace();
    Toast.makeText(this, "Lỗi khi lưu file!", Toast.LENGTH_SHORT).show();
}
2. Code đọc file (Read File)
Java
import java.io.BufferedReader;
import java.io.FileInputStream; // Thư viện đọc dữ liệu từ file
import java.io.InputStreamReader;

// --- Đoạn code thực hiện đọc file ---
String fileName = "note.txt";
StringBuilder stringBuilder = new StringBuilder();

try {
    // Mở luồng đọc file
    FileInputStream fis = openFileInput(fileName);
    InputStreamReader isr = new InputStreamReader(fis);
    BufferedReader br = new BufferedReader(isr);
    
    String line;
    // Đọc từng dòng cho đến hết file
    while ((line = br.readLine()) != null) {
        stringBuilder.append(line).append("\n");
    }
    
    fis.close();
    
    // Biến `stringBuilder.toString()` chính là toàn bộ nội dung đọc được từ file
    String content = stringBuilder.toString();
    Toast.makeText(this, "Đọc file: " + content, Toast.LENGTH_LONG).show();

} catch (Exception e) {
    e.printStackTrace();
    Toast.makeText(this, "Không tìm thấy file hoặc lỗi đọc!", Toast.LENGTH_SHORT).show();
}
PHẦN B: Lưu file vào Bộ nhớ ngoài (External Storage / Public Directory)
Nếu đề bài yêu cầu lưu ra bộ nhớ chung của thiết bị (như thư mục Downloads hoặc Documents), trên các phiên bản Android hiện đại, giáo viên thường sẽ chấm cách sử dụng getExternalFilesDir() để không cần phải xin quyền phức tạp (Runtime Permission):

Java
import android.os.Environment;
import java.io.File;
import java.io.FileOutputStream;

// Lấy thư mục riêng của app nằm trên bộ nhớ ngoài (External Storage)
File externalDir = getExternalFilesDir(null); // hoặc Environment.DIRECTORY_DOCUMENTS
if (externalDir != null) {
    File myFile = new File(externalDir, "my_external_file.txt");
    
    try {
        FileOutputStream fos = new FileOutputStream(myFile);
        fos.write("Dữ liệu lưu ngoài bộ nhớ".getBytes());
        fos.close();
        // Thành công!
    } catch (Exception e) {
        e.printStackTrace();
    }
}
Đến đây, thầy đã đi qua toàn bộ các phần trọng tâm nhất cho bài kiểm tra thường xuyên số 2 của em:

Chuyển trang (Intent).

Truyền dữ liệu qua lại giữa các Activity (putExtra / getStringExtra).

Tạo và xử lý Menu (Options Menu).

Lưu trữ file (Internal & External Storage).

Em còn phần nào chưa rõ hoặc muốn thầy giải thích sâu hơn về đoạn code nào không? Cứ hỏi thầy nhé, chúc em ôn tập thật tốt và đạt điểm cao!