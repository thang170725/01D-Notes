1. PySpark là gì?

PySpark là Python API của Spark.

Spark ban đầu được xây dựng chủ yếu bằng Scala/Java.

PySpark cho phép bạn dùng Python để điều khiển Spark.

Ví dụ:

from pyspark.sql import SparkSession

spark = SparkSession.builder \
    .appName("MyPipeline") \
    .getOrCreate()

df = spark.read.json("data.json")

df.filter(df.age > 18).show()

Nếu dùng Pandas:

import pandas as pd

df = pd.read_json("data.json")

df = df[df["age"] > 18]

Ý tưởng khá giống nhau.

Nhưng Spark có khả năng phân tán dữ liệu trên cluster.

Nếu bạn nói Spark trong Python, thường là Apache Spark, và Python dùng Spark thông qua thư viện PySpark.

Spark dùng để làm gì?

Spark dùng để xử lý dữ liệu lớn (Big Data) phân tán trên nhiều máy.

Ví dụ bạn có:

1 file CSV       → 100 MB
100 file CSV     → 100 GB
100.000 file     → vài TB

Nếu dùng Python/Pandas:

import pandas as pd

df = pd.read_csv("data.csv")
df.groupby("user_id")["amount"].sum()

Khi dữ liệu quá lớn, máy của bạn có thể:

thiếu RAM
xử lý rất chậm
không thể load toàn bộ dataset

Spark giải quyết bằng cách chia dữ liệu ra nhiều partition và xử lý song song.

                 Dataset 1 TB
                      │
          ┌───────────┼───────────┐
          ↓           ↓           ↓
       Worker 1    Worker 2    Worker 3
       300 GB      300 GB      400 GB
          │           │           │
          └───────────┼───────────┘
                      ↓
                   Result
Python + Spark

Cài:

pip install pyspark

Sau đó:

from pyspark.sql import SparkSession

spark = SparkSession.builder \
    .appName("MyApp") \
    .getOrCreate()

df = spark.read.csv(
    "data.csv",
    header=True,
    inferSchema=True
)

df.groupBy("user_id").sum("amount").show()

Điểm hay là API khá giống Pandas:

# Pandas
df.groupby("user_id")["amount"].sum()

so với:

# PySpark
df.groupBy("user_id").sum("amount")
Spark thường được dùng cho

1. ETL / Data Engineering

Database
   ↓
Spark
   ↓
Clean / Transform
   ↓
Data Warehouse / Data Lake

2. Big Data analytics

Ví dụ:

hàng tỷ transaction
log server
dữ liệu click
dữ liệu IoT
dữ liệu người dùng

3. Machine Learning trên dữ liệu lớn

Spark có module:

Spark
 ├── Spark SQL
 ├── Spark Streaming
 ├── MLlib
 └── GraphX

Trong đó MLlib hỗ trợ một số thuật toán ML phân tán.

Spark khác Pandas thế nào?
	Pandas	PySpark
Dữ liệu	Nhỏ → vừa	Rất lớn
Chạy	Chủ yếu 1 máy	Có thể nhiều máy
RAM	Phụ thuộc máy	Có thể phân tán
API	Đơn giản	Phức tạp hơn
Big Data	❌	✅
Distributed processing	❌	✅

Ví dụ:

Pandas

CSV 500 GB
     ↓
RAM máy
     ↓
💥 MemoryError

Trong khi Spark:

CSV 500 GB
     ↓
┌────┬────┬────┬────┐
│ W1 │ W2 │ W3 │ W4 │
└────┴────┴────┴────┘
     ↓
parallel processing
     ↓
   Result

Tóm lại: nếu bạn đang học Python backend/AI thì chưa nhất thiết phải học Spark ngay. Spark đặc biệt quan trọng khi đi vào Data Engineering, Big Data, ETL, Data Platform hoặc ML với dataset rất lớn.