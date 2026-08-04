- [Kiểm tra xem cổng có bị ai chiếm không](#kiểm-tra-xem-cổng-có-bị-ai-chiếm-không)
- [Xem PID đó là chương trình gì](#xem-pid-đó-là-chương-trình-gì)
- [Kiểm tra các dịch vụ](#kiểm-tra-các-dịch-vụ)
---
# Kiểm tra xem cổng có bị ai chiếm không
```bash
netstat -ano | findstr :3306
```
**Ex**
```bash
PS D:\workspace\dev-note> netstat -ano | findstr :3306
  TCP    0.0.0.0:3306           0.0.0.0:0              LISTENING       10360
  TCP    0.0.0.0:33060          0.0.0.0:0              LISTENING       10360
  TCP    [::]:3306              [::]:0                 LISTENING       10360
  TCP    [::]:33060             [::]:0                 LISTENING       10360
```
# Xem PID đó là chương trình gì
```bash
tasklist /FI "PID eq 1234"
```
# Kiểm tra các dịch vụ
```bash
Get-Service *mysql* | sc query type= service | findstr /I mysql
```
Bước 4. Dừng dịch vụ đang chạy

Nếu dịch vụ là MySQL80

Stop-Service MySQL80

hoặc

net stop MySQL80

Kiểm tra lại

netstat -ano | findstr :3306

Nếu không còn dòng nào thì cổng đã được giải phóng.

Bước 5. Nếu không phải dịch vụ mà là tiến trình

Ví dụ PID là 1234

taskkill /PID 1234 /F

Kiểm tra lại

netstat -ano | findstr :3306
Bước 6. Kiểm tra file cấu hình MySQL

Mở file

my.ini

Tùy nơi cài:

C:\ProgramData\MySQL\MySQL Server 8.0\my.ini

hoặc

C:\xampp\mysql\bin\my.ini

Tìm

[mysqld]
port=3306

Nếu đang là

port=3307

thì sửa thành

port=3306

Lưu file.

Bước 7. Khởi động lại MySQL

Nếu là service

Start-Service MySQL80

hoặc

net start MySQL80
Bước 8. Kiểm tra đã chạy trên 3306 chưa
netstat -ano | findstr :3306

Nếu thấy

TCP    0.0.0.0:3306      LISTENING

thì thành công.

Bước 9. Kiểm tra kết nối
mysql -u root -p

hoặc trong Python

conn = mysql.connector.connect(
    host="localhost",
    port=3306,
    user="root",
    password="170725"
)
Nếu MySQL không khởi động được

Kiểm tra lỗi:

Get-Service MySQL80

hoặc

sc query MySQL80
Tôi cần biết chính xác máy bạn đang dùng MySQL nào

Chạy 3 lệnh sau rồi gửi toàn bộ kết quả cho tôi:

netstat -ano | findstr :3306
tasklist /FI "IMAGENAME eq mysqld.exe"
Get-Service *mysql*

Từ kết quả đó, mình sẽ chỉ chính xác dịch vụ nào cần dừng hoặc cấu hình để đưa MySQL về cổng 3306.