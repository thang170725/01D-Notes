- [Apache Superset Introduction (Công cụ để vẽ biểu đồ, phân tích dữ liệu Open source)](#apache-superset-introduction-công-cụ-để-vẽ-biểu-đồ-phân-tích-dữ-liệu-open-source)
- [Run (Chạy \& khởi động apache superset)](#run-chạy--khởi-động-apache-superset)
- [Ask](#ask)
  - [Apache Superset sử dụng công nghệ gì?](#apache-superset-sử-dụng-công-nghệ-gì)
---
# Apache Superset Introduction (Công cụ để vẽ biểu đồ, phân tích dữ liệu Open source)
```bash
Là một phần mềm mã nguồn mở. Nó là một hệ thống dashboard hoàn chỉnh:
    - ví dụ bên trong superset đã có sẵn:
        + kết nối database
        + viết sql
        + cache dữ liệu
        + phân quyền
        + dashboard
        + filter
        + export pdf, csv
        + chia sẽ dashboard
        + lưu biểu đồ
        + lịch sử chỉnh sửa
        + quản lý người dùng
```
# Run (Chạy & khởi động apache superset)
**Chạy bằng docker**
*Bước 1: Kiểm tra các file trong thư mục*
```bash
ls -la # Hãy xem trong thư mục có file nào tên dạng như docker-compose.yml, docker-compose-non-dev.yml, hoặc có một thư mục con tên là docker chứa file cấu hình không.
```
*Bước 2: Chạy lệnh khởi động tương ứng*
```bash
Trường hợp 1: Nếu có file docker-compose ngay tại thư mục root
Chỉ cần chạy lệnh: docker compose up -d
(Hoặc nếu phiên bản Docker cũ hơn dùng dấu gạch ngang: docker-compose up -d)

Trường hợp 2: Nếu file cấu hình nằm trong thư mục docker/ (phổ biến với mã nguồn Superset gốc từ GitHub)
Thường đối với mã nguồn Superset, các file docker nằm trong thư mục docker. Bạn sẽ chạy: docker compose -f docker/docker-compose.yml up -d
(Hoặc tùy vào môi trường dev/non-dev mà Superset cung cấp sẵn các file như -f docker/docker-compose-non-dev.yml)
```
*Bước 3: Kiểm tra lại xem đã chạy thành công chưa*
```bash
Sau khi chạy lệnh up -d, các container sẽ chạy ngầm. Bạn kiểm tra lại trạng thái bằng lệnh:

Bash


docker ps
Nếu thấy các container như superset_app, superset_db, superset_cache ở trạng thái Up, nghĩa là bạn đã khởi động thành công!
```
*Bước 4: Mở giao diện trên trình duyệt*
```bash
Mở trình duyệt web và truy cập vào địa chỉ mặc định của Superset:

URL: http://localhost:8088

Tài khoản mặc định (nếu mới cài): admin / 
```
# Ask
## Apache Superset sử dụng công nghệ gì?
Apache Superset là một nền tảng trực quan hóa dữ liệu và Business Intelligence (BI) mã nguồn mở rất mạnh mẽ. Lý do bạn thấy nó sử dụng Python vì Python chính là "trái tim" ở phần Backend của ứng dụng này.

Dưới đây là chi tiết về công nghệ mà Apache Superset sử dụng và lý do tại sao họ lại chọn Python:

Tại sao Apache Superset lại sử dụng Python?
Superset được thiết kế để kết nối với vô số hệ thống cơ sở dữ liệu khác nhau và xử lý dữ liệu lớn. Python được chọn làm ngôn ngữ cốt lõi cho Backend vì những ưu điểm sau:

Thư viện kết nối cơ sở dữ liệu khổng lồ (SQLAlchemy):
Superset có khả năng kết nối với hầu hết mọi loại CSDL trên thị trường (PostgreSQL, MySQL, Snowflake, BigQuery, Presto, Trino, v.v.). Python sử dụng SQLAlchemy làm ORM và lớp trừu tượng để dịch các truy vấn SQL một cách linh hoạt sang các dialect của từng loại database khác nhau.

Xử lý tác vụ nền (Celery):
Việc render biểu đồ nặng, gửi cảnh báo (Alerts & Reports) qua email/Slack cần chạy ngầm. Superset sử dụng Celery (viết bằng Python) phối hợp với Redis (như bạn thấy container superset_cache và superset_worker trong Docker của bạn) để quản lý hàng đợi tác vụ.

Hệ sinh thái Khoa học dữ liệu (Data Science):
Python là ngôn ngữ tiêu chuẩn trong ngành dữ liệu, giúp Superset dễ dàng tích hợp các thư viện xử lý dữ liệu, định dạng thời gian, và các module phân tích nâng cao.

Tổng quan toàn bộ công nghệ của Apache Superset
Công nghệ của Superset được chia rõ ràng thành các tầng (Layers):

Tầng (Layer)	Công nghệ sử dụng	Vai trò chính
Backend (Server)	Python, Flask, Gunicorn	Xây dựng API REST, xử lý logic nghiệp vụ, xác thực người dùng, tương tác với database qua Flask framework.
Task Queue & Cache	Celery, Redis	Xử lý các tác vụ bất đồng bộ (chạy ngầm), lưu trữ cache giúp tăng tốc độ tải biểu đồ.
Metadata Database	PostgreSQL / MySQL / SQLite	Nơi lưu trữ cấu hình của Superset (thông tin user, các dashboard, chart bạn tạo ra, phân quyền). Đây chính là container superset_db trong máy bạn.
Frontend (UI)	React, TypeScript, Redux, Ant Design	Giao diện người dùng đơn trang (SPA) hiện đại, mượt mà và trực quan.
Visualization	Apache ECharts	Thư viện JavaScript mã nguồn mở chuyên vẽ biểu đồ (do ApacheFoundation phát triển) để tạo các loại biểu đồ phong phú trên Superset.
Deployment / DevOps	Docker, Docker Compose, Kubernetes, Helm	Đóng gói ứng dụng để chạy đa nền tảng một cách ổn định (giống cách bạn đang dùng Docker trên Ubuntu).

Mối liên hệ với Docker containers của bạn:
Nhìn lại danh sách Docker của bạn trước đó:

superset_app, superset_worker: Chạy mã nguồn Python/Flask.

superset_db: Chứa PostgreSQL để lưu metadata của Superset.

superset_cache: Chứa Redis để làm cache và queue cho Python xử lý.