# Apache Spark Introduction (framework xử lý dữ liệu lớn, có thể phân chia công việc thành nhiều task và thực thi song song trên nhiều CPU hoặc nhiều máy tính)
```bash
Lưu ý: 
   - Spark không tự động nhanh hơn Python trong mọi trường hợp. Với file nhỏ, Python thuần hoặc pandas thường đơn giản và nhanh hơn do Spark có chi phí khởi tạo và điều phối công việc
```
**Ex: Ví dụ bạn có 10 triệu email dạng JSONL và muốn**
```bash
- Loại bỏ email rỗng.
- Lọc email không phải tiếng Việt.
- Loại bỏ bản ghi trùng lặp.
- Thống kê số lượng email theo loại.
- Ghi dữ liệu đã làm sạch ra file.

-> Với Python thông thường, bạn có thể tự viết vòng lặp hoặc dùng pandas. 
   Khi dữ liệu vượt quá khả năng bộ nhớ hoặc cần xử lý song song trên một cụm máy, Spark cung cấp mô hình thực thi phù hợp hơn.
```
# PySpark Introduction (là Python API của Spark)
```bash
Spark ban đầu được xây dựng chủ yếu bằng Scala/Java. PySpark cho phép bạn dùng Python để điều khiển Spark.
```
# Installation
```bash
pip install pyspark
```
# sql
## SparkSession (điểm khởi đầu để tạo DataFrame, đọc file và chạy Spark SQL)
**Ex**
```python
from pyspark.sql import SparkSession

spark = (
    SparkSession.builder
    .appName("SparkLearning") # đặt tên cho ứng dụng
    .master("local[*]") # chạy Spark ngay trên máy runtime của Colab, sử dụng các CPU khả dụng
    .getOrCreate() # lấy session hiện có hoặc tạo mới
)

print("Spark version:", spark.version) # Spark version: 4.0.4
print("Application name:", spark.sparkContext.appName) # Application name: SparkLearning
print("Master:", spark.sparkContext.master) # Master: local[*]
```
## .createDataFrame()
**Ex**
```python
data = [
    (1, "Xin chào, tôi cần hỗ trợ tài khoản", "vi", "support"),
    (2, "Đơn hàng của tôi đã được giao", "vi", "order"),
    (3, "Your account has been suspended", "en", "security"),
    (4, "", "vi", "unknown"),
    (5, "Khuyến mãi đặc biệt hôm nay", "vi", "marketing"),
    (6, "Your invoice is ready", "en", "billing"),
    (7, "Tôi cần kiểm tra hóa đơn", "vi", "billing"),
    (8, None, "vi", "unknown"),
]

columns = ["id", "content", "language", "category"]

df = spark.createDataFrame(data, schema=columns)

df.show(truncate=False)
# +---+----------------------------------+--------+---------+
# |id |content                           |language|category |
# +---+----------------------------------+--------+---------+
# |1  |Xin chào, tôi cần hỗ trợ tài khoản|vi      |support  |
# |2  |Đơn hàng của tôi đã được giao     |vi      |order    |
# |3  |Your account has been suspended   |en      |security |
# |4  |                                  |vi      |unknown  |
# |5  |Khuyến mãi đặc biệt hôm nay       |vi      |marketing|
# |6  |Your invoice is ready             |en      |billing  |
# |7  |Tôi cần kiểm tra hóa đơn          |vi      |billing  |
# |8  |NULL                              |vi      |unknown  |
# +---+----------------------------------+--------+---------+
```
### .printSchema()
**Ex**
```python
df.printSchema()

root
 |-- id: long (nullable = true)
 |-- content: string (nullable = true)
 |-- language: string (nullable = true)
 |-- category: string (nullable = true)
```
## .filter()
**Ex**
```python
from pyspark.sql import functions as F

clean_df = df.filter(
    F.col("content").isNotNull()
    & (F.trim(F.col("content")) != "")
)

clean_df.show(truncate=False)
# +---+----------------------------------+--------+---------+
# |id |content                           |language|category |
# +---+----------------------------------+--------+---------+
# |1  |Xin chào, tôi cần hỗ trợ tài khoản|vi      |support  |
# |2  |Đơn hàng của tôi đã được giao     |vi      |order    |
# |3  |Your account has been suspended   |en      |security |
# |5  |Khuyến mãi đặc biệt hôm nay       |vi      |marketing|
# |6  |Your invoice is ready             |en      |billing  |
# |7  |Tôi cần kiểm tra hóa đơn          |vi      |billing  |
# +---+----------------------------------+--------+---------+
```