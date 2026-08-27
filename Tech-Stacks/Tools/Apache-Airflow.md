- [Apace Airflow Introduction (là công cụ điều phối workflow)](#apace-airflow-introduction-là-công-cụ-điều-phối-workflow)
- [Apache Spark (là một distributed computing framework dùng để xử lý dữ liệu lớn)](#apache-spark-là-một-distributed-computing-framework-dùng-để-xử-lý-dữ-liệu-lớn)
---
# Apace Airflow Introduction (là công cụ điều phối workflow)
```bash
Nói đơn giản:
    Airflow = quản lý xem công việc nào chạy trước, công việc nào chạy sau, chạy khi nào, lỗi thì retry thế nào.

Nó có thể:
    - chạy job hàng ngày lúc 2h sáng
    - retry nếu job lỗi
    - chạy Task B chỉ khi Task A thành công
    - chạy nhiều task song song
    - theo dõi task nào đang chạy/thất bại
    - lưu log
    - gửi cảnh báo khi pipeline lỗi
    - Airflow không phải công cụ xử lý dữ liệu chính


Airflow không sinh ra để xử lý hàng triệu dòng dữ liệu.
    Nó chủ yếu nói: "Hãy chạy Spark job này." hoặc: "Sau khi Spark job xong, chạy Python job này."
```
**Ex: Ví dụ pipeline AI của bạn:**
```bash
Raw JSON
   ↓
Validate data
   ↓
Transform data
   ↓
Create JSON
   ↓
Create table
   ↓
Train model

Airflow có thể quản lý toàn bộ quy trình này:
    Task A: Load JSON
           ↓
    Task B: Validate
           ↓
    Task C: Transform
           ↓
    Task D: Create table
           ↓
    Task E: Upload
```
# Apache Spark (là một distributed computing framework dùng để xử lý dữ liệu lớn)
**Ex**
```bash
Ví dụ bạn có: 1 file JSON = 10 MB 
    Python/Pandas xử lý rất dễ.

Nhưng nếu:
    - 10 TB dữ liệu
    - 100 triệu records
    - 1 tỷ records
-> thì một máy chạy Python/Pandas có thể không đủ.

Spark cho phép chia dữ liệu ra nhiều máy:
                Spark
                  │
        ┌─────────┼─────────┐
        ↓         ↓         ↓
     Worker 1  Worker 2  Worker 3
        ↓         ↓         ↓
      data A    data B    data C

Các máy xử lý song song rồi Spark tổng hợp kết quả.

Vì vậy:
    Spark = công cụ xử lý dữ liệu lớn phân tán.
```