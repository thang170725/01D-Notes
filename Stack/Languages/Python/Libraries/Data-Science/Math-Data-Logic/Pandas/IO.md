- [File (Nhóm xử lý file)](#file-nhóm-xử-lý-file)
  - [Read (Nhóm lấy dữ liệu)](#read-nhóm-lấy-dữ-liệu)
    - [.read\_csv() (lấy dữ liệu từ file)](#read_csv-lấy-dữ-liệu-từ-file)
  - [Write (Nhóm ghi dữ liệu)](#write-nhóm-ghi-dữ-liệu)
    - [.to\_csv()](#to_csv)
- [SQL (Nhóm xử lý sql)](#sql-nhóm-xử-lý-sql)
  - [Read (Nhóm đọc, lấy thông tin)](#read-nhóm-đọc-lấy-thông-tin)
    - [pd.read\_sql()](#pdread_sql)
  - [Write (Nhóm ghi dữ liệu)](#write-nhóm-ghi-dữ-liệu-1)
    - [DataFrame.to\_sql()](#dataframeto_sql)
---
# File (Nhóm xử lý file)
## Read (Nhóm lấy dữ liệu)
### .read_csv() (lấy dữ liệu từ file)
```bash
- Nó đọc delimited text files (file văn bản có cột ngăn cách bằng ký tự phân tách)
- ví dụ:
    + .csv → phân tách bởi dấu phẩy ,
    + .tsv → phân tách bởi tab \t
    + .txt → có thể phân tách bởi ;, |, tab,... miễn là chỉ rõ sep=...
```
**Syn**
```bash
import pandas as pd

li = pd.read_csv(
    "danhSach.csv", 
    header=0,
    name['id', 'fullname']
    sep=',',
    decimal=','
    index=[], 
    encoding=’utf-8’,
    dtype=str,
    na_values=["", "NULL", "None"],
    parse_dates=[0]
) # dữ liệu hiển thị dưới dạng dataframe

- Input:
    + header=           : chỉ định dòng nào trong file được dùng làm tiêu đề cột. 0 là mặc định
    + name=             : cho phép tự định nghĩa tên cột
    + sep=';'           : Phân cách
    + decimal=','       : Nói cho Pandas dấu "," là dấu thập phân
    + parse_dates=[0]   : Bảo Pandas cột số 0 (cột đầu tiên) hãy chuyển thành kiểu ngày giờ.
```
## Write (Nhóm ghi dữ liệu)
### .to_csv()
```bash
Ghi dữ liệu vào file csv.
```
**Syn**
```bash
df.to_csv(
    "file.csv",
    index=True
)

- Input:
    + index: Có ghi cột index của DataFrame ra file CSV hay không.
```
# SQL (Nhóm xử lý sql)
## Read (Nhóm đọc, lấy thông tin)
### pd.read_sql()
```bash
- pandas.read_sql dùng để chạy SQL và trả kết quả về DataFrame.
- Nó là cầu nối giữa:
    + SQL (MariaDB / MySQL / PostgreSQL…)
    + Pandas (DataFrame)
- Rất hay dùng cho:
    + Data analysis
    + Report
    + ETL
    + Export CSV / Excel
    + Test nhanh DB
- read_sql:
    + Mở connection
    + Execute
    + Fetch all
    + Build DataFrame
```
**Khi nào NÊN dùng read_sql?**
```bash
- NÊN:
    + Làm data analysis
    + Tool admin
    + Export dữ liệu
    + Notebook / script
    + Báo cáo
KHÔNG NÊN:
    + API backend realtime
    + CRUD business logic
    + Query lớn streaming (vì load hết vào RAM)
```
**So sánh read_sql vs SQLAlchemy Core**
```bash
Tiêu chí	    read_sql	Core
Output	        DataFrame	Row / Mapping
Hiệu năng	    Trung bình	Cao
Memory	        Load all	Có thể stream
Dùng cho API	❌	        ✅
Dùng cho report	✅	        ⚠️
```
**Syn**
```bash
pandas.read_sql(
    sql,
    con,
    params=None,
    index_col=None,
    parse_dates=None
)

- sql	        : Câu SQL string hoặc SQLAlchemy Select
- con	        : DB connection / engine
- params	    : Bind parameter
- index_col	    : Cột làm index
- parse_dates	: Parse cột ngày
```
**Ex1: Dùng SQL STRING (đơn giản nhất)**
```python
import pandas as pd

query = """
SELECT id, name, city
FROM districts
LIMIT 10
"""

df = pd.read_sql(query, con=engine)

print(df)

#    id        name      city
# 0   1     District A   Hanoi
# 1   2     District B   Hanoi
...

```
**Ex2: Bind parameter (RẤT QUAN TRỌNG)**
```python
query = """
SELECT id, name
FROM districts
WHERE city = %(city)s
LIMIT %(limit)s
"""

df = pd.read_sql(
    query,
    con=engine,
    params={
        "city": "Hanoi",
        "limit": 5
    }
)

# An toàn
```
**Ex3: Dùng SQLAlchemy Table + select (chuẩn hơn)**
```python
from sqlalchemy import select
import pandas as pd

districts = table_factory.get("districts")

stmt = (
    select(
        districts.c.id,
        districts.c.name,
        districts.c.city
    )
    .limit(10)
)

df = pd.read_sql(stmt, con=engine)

print(df.head())


# read_sql nhận trực tiếp Select object
# Không cần convert sang string
```
## Write (Nhóm ghi dữ liệu)
### DataFrame.to_sql()
```bash
- to_sql dùng để:
    + Tạo bảng mới trong database từ DataFrame
    + Hoặc ghi thêm / ghi đè dữ liệu vào bảng đã có
    + Tự động ánh xạ kiểu dữ liệu Pandas → SQL
    + Thường dùng trong:
ETL (Extract – Transform – Load)
    + Data analysis
    + Machine learning pipeline
    + Báo cáo, dashboard
```
**Syn**
```bash
DataFrame.to_sql(
    name,
    con,
    if_exists='fail',
    index=True,
    index_label=None
)

- name	    : Tên bảng SQL
- con	    : Kết nối database (SQLAlchemy engine hoặc connection)
- if_exists	: Cách xử lý nếu bảng đã tồn tại. if_exists có 3 giá trị:
    + 'fail' → báo lỗi (mặc định)
    + 'replace' → xóa bảng cũ, tạo lại
    + 'append' → ghi thêm dữ liệu
- index 	: Có ghi index của DataFrame vào DB không
```
**Ex1: SQLite – đơn giản nhất**
```python
# Bước 1: Tạo DataFrame
import pandas as pd

df = pd.DataFrame({
    "id": [1, 2, 3],
    "name": ["An", "Bình", "Chi"],
    "age": [20, 21, 22]
})

# Bước 2: Kết nối database (SQLite)
from sqlalchemy import create_engine

engine = create_engine("sqlite:///students.db") # File students.db sẽ được tạo nếu chưa tồn tại.

# Bước 3: Ghi DataFrame vào SQL bằng to_sql
df.to_sql(
    name="students",
    con=engine,
    if_exists="replace",
    index=False
)

# Bảng students được tạo: SELECT * FROM students;
```