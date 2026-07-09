Để lấy được chuỗi kết nối (DATABASE_URL) khi bạn đang dùng MySQL kết hợp với công cụ quản lý MySQL Workbench, cấu trúc tổng quát của chuỗi sẽ có dạng như sau:

Plaintext


mysql+pymysql://<username>:<password>@<host>:<port>/<database_name>
Bạn có thể tìm các thông số này ngay trong MySQL Workbench bằng cách kiểm tra các vị trí sau:

1. Cách lấy các thông số từ MySQL Workbench
Host & Port: Nhìn ngay ở màn hình Welcome (Home) của Workbench, phần MySQL Connections. Bạn sẽ thấy các block kết nối. Dưới tên kết nối thường ghi rõ dạng localhost:3306 hoặc 127.0.0.1:3306.

localhost hoặc 127.0.0.1 chính là Host.

3306 (mặc định của MySQL) chính là Port.

Username: Cũng tại block đó, bạn sẽ thấy chữ user: root hoặc một tên user cụ thể. root là tài khoản tối cao mặc định của MySQL.

Password: Là mật khẩu bạn nhập mỗi khi click vào để mở kết nối trong Workbench. (Nếu lúc cài đặt bạn để trống thì phần password sẽ bỏ qua).

Database Name (Schema): Khi đã bấm vào bên trong kết nối, nhìn sang cột Navigator bên trái, chọn tab Schemas. Những cái tên hiển thị ở đây (ví dụ: sakila, sys, hoặc database do bạn tự tạo bằng lệnh CREATE DATABASE my_db;) chính là Database Name.

2. Ráp thành chuỗi kết nối hoàn chỉnh cho SQLAlchemy & Alembic
Dựa vào các thông số tìm được ở trên, bạn ráp vào một trong các trường hợp phổ biến sau:

Trường hợp 1: Sử dụng tài khoản root mặc định, có mật khẩu
Giả sử mật khẩu MySQL của bạn là 123456, và database bạn đã tạo sẵn tên là test_db:

Python


DATABASE_URL = "mysql+pymysql://root:123456@localhost:3306/test_db"
Trường hợp 2: Sử dụng tài khoản root nhưng KHÔNG để mật khẩu (để trống)
Nếu bạn không đặt mật khẩu cho root, hãy xóa phần password đi nhưng giữ lại dấu @:

Python


DATABASE_URL = "mysql+pymysql://root@localhost:3306/test_db"
Trường hợp 3: Mật khẩu của bạn có chứa ký tự đặc biệt (Ví dụ: @, :, /,...)
Nếu mật khẩu của bạn phức tạp (chẳng hạn: P@ss:word), việc viết trực tiếp vào chuỗi sẽ làm Alembic hiểu nhầm cấu trúc URL. Bạn cần dùng thư viện urllib.parse để mã hóa nó:

Python


import urllib.parse

password = urllib.parse.quote_plus("P@ss:word")
DATABASE_URL = f"mysql+pymysql://root:{password}@localhost:3306/test_db"
3. Lưu ý bắt buộc khi chạy code
Để SQLAlchemy kết nối được với MySQL qua chuỗi dạng mysql+pymysql://, dự án của bạn cần phải cài đặt thêm driver pymysql.

Hãy đảm bảo bạn đã chạy lệnh này ở terminal:

Bash


pip install pymysql
Sau khi có chuỗi này, bạn chỉ cần ném nó vào biến DATABASE_URL trong file src/database.py và dòng sqlalchemy.url trong file alembic.ini như workflow ở bước trước là hệ thống sẽ tự động chạy trơn tru.
Chuỗi kết nối (Connection String) có định dạng dạng URL như trên không phải chỉ dành riêng cho SQLAlchemy, nhưng nó cũng không hoàn toàn giống nhau cho tất cả các thư viện Python.

Mỗi thư viện kết nối cơ sở dữ liệu sẽ có một quy định riêng về định dạng chuỗi. Việc phân loại dưới đây giúp bạn dễ hình dung:

1. Thành phần cố định (Tất cả các thư viện/công cụ đều cần)
Dù bạn dùng bất kỳ ngôn ngữ (Python, Node.js, Java) hay thư viện nào, bạn vẫn bắt buộc phải cung cấp đủ 5 thông số cốt lõi thu thập từ MySQL Workbench:

User (Ví dụ: root)

Password (Ví dụ: 123456)

Host (Ví dụ: localhost hoặc 127.0.0.1)

Port (Ví dụ: 3306)

Database Name (Ví dụ: test_db)

2. Sự khác biệt về định dạng giữa các thư viện Python
Nhóm 1: Nhóm dùng chuỗi URL (SQLAlchemy, Alembic, Tortoise ORM, Prisma)
Các thư viện ORM cao cấp thường sử dụng cấu trúc URL. Tuy nhiên, phần đầu của chuỗi (gọi là Prefix/Dialect) sẽ chỉ định chính xác driver mà thư viện đó sử dụng.

SQLAlchemy / Alembic: Yêu cầu chỉ rõ driver (ví dụ: pymysql hoặc mysqlconnector).

Plaintext


mysql+pymysql://root:123456@localhost:3306/test_db
Tortoise ORM (Một ORM async phổ biến): Thường chỉ cần ghi mysql://.

Plaintext


mysql://root:123456@localhost:3306/test_db
Nhóm 2: Nhóm Driver thuần/Thấp cấp (PyMySQL, mysql-connector-python)
Nếu bạn không dùng SQLAlchemy mà muốn viết câu lệnh SQL thuần (SELECT * FROM ...) bằng các thư viện kết nối trực tiếp, các thư viện này không nhận chuỗi URL mà nhận các thông số dưới dạng các đối tượng (Arguments) độc lập hoặc Từ điển (Dictionary).

Ví dụ với pymysql:

Python


import pymysql

# Không truyền cả link, mà truyền từng góc cấu thành
connection = pymysql.connect(
    host="localhost",
    user="root",
    password="your_password",
    database="test_db",
    port=3306,
)

*   **Ví dụ với `mysql-connector-python` (Thư viện chính chủ của MySQL):**
    ```python
    import mysql.connector

    connection = mysql.connector.connect(
        host="localhost",
        user="root",
        password="your_password",
        database="test_db",
    )
Kết luận nhanh cho bạn
Chuỗi mysql+pymysql://... mà bạn vừa tạo cấu trúc chung phục vụ cho hệ sinh thái của SQLAlchemy và Alembic.

Nếu sau này bạn chuyển sang làm một dự án khác không dùng SQLAlchemy mà viết SQL thuần bằng driver pymysql, bạn sẽ rã chuỗi URL đó ra thành các biến host, user, password riêng biệt để truyền vào hàm kết nối.