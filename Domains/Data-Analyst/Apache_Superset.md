- [Apache Superset Introduction (Công cụ để vẽ biểu đồ, phân tích dữ liệu Open source)](#apache-superset-introduction-công-cụ-để-vẽ-biểu-đồ-phân-tích-dữ-liệu-open-source)
- [Installation](#installation)
- [Run (Chạy \& khởi động apache superset)](#run-chạy--khởi-động-apache-superset)
- [Ask](#ask)
  - [Apache Superset sử dụng công nghệ gì?](#apache-superset-sử-dụng-công-nghệ-gì)
- [Tạo một thư mục trên máy host để lưu code](#tạo-một-thư-mục-trên-máy-host-để-lưu-code)
- [Copy mã nguồn từ container ra thư mục vừa tạo](#copy-mã-nguồn-từ-container-ra-thư-mục-vừa-tạo)
- [Clone source code chính thức](#clone-source-code-chính-thức)
- [Truy cập vào thư mục vừa tải](#truy-cập-vào-thư-mục-vừa-tải)
- [Tạo thư mục đích nếu chưa có](#tạo-thư-mục-đích-nếu-chưa-có)
- [Di chuyển thư mục superset ra ngoài](#di-chuyển-thư-mục-superset-ra-ngoài)
- [Xóa các container cũ đã dừng](#xóa-các-container-cũ-đã-dừng)
- [(Tùy chọn) Nếu bạn dùng docker compose, đứng ở thư mục mới và chạy lại:](#tùy-chọn-nếu-bạn-dùng-docker-compose-đứng-ở-thư-mục-mới-và-chạy-lại)
- [Hoặc nếu là redis-server:](#hoặc-nếu-là-redis-server)
- [(Hoặc lệnh docker compose tương ứng mà bạn đang dùng)](#hoặc-lệnh-docker-compose-tương-ứng-mà-bạn-đang-dùng)
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
# Installation
[Link](https://superset.apache.org/user-docs/quickstart)

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

sao tôi không tìm đấy code project apache ở đâu trong máy ubutu của tôi nhỉ thang@PhatToNhuLai:~$ docker ps -a
CONTAINER ID   IMAGE                                                       COMMAND                  CREATED        STATUS                      PORTS     NAMES
477b67177dea   apachesuperset.docker.scarf.sh/apache/superset:latest-dev   "/app/docker/docker-…"   3 months ago   Exited (137) 3 months ago             superset_worker_beat
382d8a917d76   apachesuperset.docker.scarf.sh/apache/superset:latest-dev   "/app/docker/docker-…"   3 months ago   Exited (137) 3 months ago             superset_worker
1693d7231789   apachesuperset.docker.scarf.sh/apache/superset:latest-dev   "/app/docker/docker-…"   3 months ago   Exited (137) 3 months ago             superset_app
f486969c1c15   apachesuperset.docker.scarf.sh/apache/superset:latest-dev   "/app/docker/docker-…"   3 months ago   Exited (0) 3 months ago               superset_init
2b4fe3e8b1a9   postgres:16                                                 "docker-entrypoint.s…"   3 months ago   Exited (137) 3 months ago             superset_db
5e5652d2c9ca   redis:7                                                     "docker-entrypoint.s…"   3 months ago   Exited (137) 3 months ago             superset_cache
thang@PhatToNhuLai:~$ docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
thang@PhatToNhuLai:~$ 

Nguyên nhân chính khiến bạn không tìm thấy mã nguồn của dự án Apache Superset trên máy Ubuntu của mình là do các container Docker đang chạy dựa trên Docker Image có sẵn (apachesuperset.docker.scarf.sh/apache/superset:latest-dev).

Mã nguồn của ứng dụng nằm bên trong Image/Container (tại thư mục /app), chứ không tự động sinh ra một thư mục source code trên hệ điều hành Ubuntu của máy host nếu trước đó bạn chưa từng clone mã nguồn hoặc cấu hình chia sẻ thư mục (volumes / bind mount).

Dưới đây là các cách để bạn xác định vị trí hoặc lấy mã nguồn ra máy host:

1. Tìm lại thư mục dự án (nếu bạn đã từng tải về máy)
Nếu trước đó bạn đã từng tải mã nguồn hoặc file docker-compose về máy nhưng quên mất nằm ở đâu, hãy thử tìm kiếm bằng các cách sau:

Xem lại lịch sử lệnh (Bash History):

Bash
history | grep superset
history | grep clone
Lệnh này sẽ hiển thị các thư mục bạn đã từng truy cập hoặc gõ lệnh liên quan đến Superset.

Tìm kiếm thư mục trên toàn hệ thống:

Bash
sudo find / -name "superset" -type d 2>/dev/null
2. Copy mã nguồn từ Docker Container ra máy host
Nếu bạn muốn lấy mã nguồn hiện tại đang nằm bên trong container ra ngoài máy Ubuntu để xem hoặc chỉnh sửa, bạn có thể dùng lệnh docker cp.

Vì các container hiện đang ở trạng thái Exited, bạn có thể khởi động tạm thời hoặc copy trực tiếp từ container superset_app:

Bash
# Tạo một thư mục trên máy host để lưu code
mkdir -p ~/superset-source

# Copy mã nguồn từ container ra thư mục vừa tạo
docker cp superset_app:/app ~/superset-source/
Sau khi chạy xong, bạn sẽ thấy toàn bộ mã nguồn nằm ở thư mục ~/superset-source/app.

3. Tải (Clone) trực tiếp mã nguồn chuẩn từ GitHub
Nếu mục đích của bạn là phát triển, đóng góp mã nguồn (contribute) hoặc tùy biến mã nguồn của Apache Superset, cách tốt nhất là clone trực tiếp repository chính thức từ GitHub về máy Ubuntu:

Bash
# Clone source code chính thức
git clone https://github.com/apache/superset.git

# Truy cập vào thư mục vừa tải
cd superset
Lưu ý: Khi làm việc với môi trường phát triển (development) của Superset thông qua Docker trên máy local, thông thường bạn sẽ cần clone mã nguồn từ GitHub, sau đó sử dụng file docker-compose đi kèm trong repo đó để cấu hình volumes trỏ mã nguồn local vào container giúp code thay đổi lập tức được cập nhật mà không cần rebuild image.

nó ra như này thì tôi có thể di chuyển folder superset ra folder khác được không, có ảnhhưởng gì không thang@PhatToNhuLai:~$ docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
thang@PhatToNhuLai:~$ history | grep superset
  503  history | grep superset
thang@PhatToNhuLai:~$ history | grep clone
  504  history | grep clone
thang@PhatToNhuLai:~$ sudo find / -name "superset" -type d 2>/dev/null
[sudo] password for thang: 
/home/thang/workspace/test/test/superset
/home/thang/workspace/test/test/superset/helm/superset
/home/thang/workspace/test/test/superset/superset-frontend/plugins/legacy-preset-chart-nvd3/src/vendor/superset
/home/thang/workspace/test/test/superset/superset
/home/thang/workspace/test/test/superset/superset/templates/superset
/home/thang/.local/share/Trash/expunged/3811229383/superset-frontend/plugins/legacy-preset-chart-nvd3/lib/vendor/superset
/home/thang/.local/share/Trash/expunged/3811229383/superset
/var/lib/containerd/io.containerd.snapshotter.v1.overlayfs/snapshots/1189/fs/app/superset
/var/lib/containerd/io.containerd.snapshotter.v1.overlayfs/snapshots/1182/fs/app/superset
/var/lib/containerd/io.containerd.snapshotter.v1.overlayfs/snapshots/1196/fs/app/superset
/var/lib/containerd/io.containerd.snapshotter.v1.overlayfs/snapshots/1201/fs/app/superset
/var/lib/containerd/io.containerd.snapshotter.v1.overlayfs/snapshots/1184/fs/app/superset
/var/lib/containerd/io.containerd.snapshotter.v1.overlayfs/snapshots/1184/fs/app/superset_home/.cache/uv/archive-v0/IqzA7cMbGK8s9HMw/superset
/var/lib/containerd/io.containerd.snapshotter.v1.overlayfs/snapshots/1184/fs/app/superset_home/.cache/uv/archive-v0/IqzA7cMbGK8s9HMw/superset/templates/superset
/var/lib/containerd/io.containerd.snapshotter.v1.overlayfs/snapshots/1184/fs/app/build/lib/superset
/var/lib/containerd/io.containerd.snapshotter.v1.overlayfs/snapshots/1184/fs/app/build/lib/superset/templates/superset
/var/lib/containerd/io.containerd.snapshotter.v1.overlayfs/snapshots/1184/fs/app/.venv/lib/python3.10/site-packages/superset
/var/lib/containerd/io.containerd.snapshotter.v1.overlayfs/snapshots/1184/fs/app/.venv/lib/python3.10/site-packages/superset/templates/superset
/var/lib/containerd/io.containerd.snapshotter.v1.overlayfs/snapshots/1139/fs/app/superset
/var/lib/containerd/io.containerd.snapshotter.v1.overlayfs/snapshots/1174/fs/app/superset
/var/lib/containerd/io.containerd.snapshotter.v1.overlayfs/snapshots/1142/fs/app/superset
/var/lib/containerd/io.containerd.snapshotter.v1.overlayfs/snapshots/1142/fs/app/superset/templates/superset
/var/lib/containerd/io.containerd.snapshotter.v1.overlayfs/snapshots/1202/fs/app/superset
/var/lib/containerd/io.containerd.snapshotter.v1.overlayfs/snapshots/1116/fs/app/superset
/var/lib/containerd/io.containerd.snapshotter.v1.overlayfs/snapshots/1200/fs/app/superset
/var/lib/containerd/io.containerd.snapshotter.v1.overlayfs/snapshots/1145/fs/app/superset
/var/lib/containerd/io.containerd.snapshotter.v1.overlayfs/snapshots/1149/fs/app/superset
/var/lib/docker/volumes/superset_superset_home/_data/.cache/uv/archive-v0/IqzA7cMbGK8s9HMw/superset
/var/lib/docker/volumes/superset_superset_home/_data/.cache/uv/archive-v0/IqzA7cMbGK8s9HMw/superset/templates/superset
thang@PhatToNhuLai:~$ 

Dựa vào kết quả bạn vừa gửi, thư mục mã nguồn gốc của bạn nằm ở đây:
/home/thang/workspace/test/test/superset

Bạn hoàn toàn có thể di chuyển thư mục này sang một vị trí khác (ví dụ: chuyển ra /home/thang/workspace/superset), nhưng cần lưu ý một số điểm để không làm lỗi cấu hình Docker khi bạn muốn chạy lại dự án sau này.

1. Di chuyển có ảnh hưởng gì không?
Về mặt mã nguồn (Code): Không bị ảnh hưởng gì cả, vì đây là các tệp tin tĩnh (source code, cấu hình, Dockerfile).

Về mặt Docker Containers hiện tại: Các container hiện tại của bạn đang ở trạng thái Exited (đã dừng), nên việc di chuyển thư mục không làm hỏng các container đang chạy.

Về mặt Docker Compose:

Các file docker-compose.yml thường sử dụng đường dẫn tương đối (ví dụ: - .:/app hoặc trỏ tới các file nội bộ trong thư mục).

Nếu bạn di chuyển thư mục đi, cấu trúc bên trong giữ nguyên thì không sao, nhưng khi bạn bật lại Docker, bạn phải đứng ở thư mục mới để chạy lệnh docker compose. Nếu bạn vẫn chạy từ đường dẫn cũ, hệ thống sẽ báo lỗi không tìm thấy file cấu hình.

Hướng dẫn di chuyển an toàn
Nếu bạn muốn dọn dẹp và đưa thư mục superset ra một vị trí gọn gàng hơn (ví dụ: chuyển từ /home/thang/workspace/test/test/superset ra /home/thang/workspace/superset), hãy làm theo các bước sau:

Bước 1: Di chuyển thư mục bằng lệnh mv
Mở terminal và chạy lệnh sau (thay đổi đường dẫn đích theo ý muốn của bạn):

Bash
# Tạo thư mục đích nếu chưa có
mkdir -p /home/thang/workspace

# Di chuyển thư mục superset ra ngoài
mv /home/thang/workspace/test/test/superset /home/thang/workspace/superset
Bước 2: Truy cập vào thư mục mới
Sau khi di chuyển xong, mỗi khi làm việc với dự án, bạn nhớ cd vào đường dẫn mới này:

Bash
cd /home/thang/workspace/superset
Bước 3: Dọn dẹp các container cũ (Khuyên dùng)
Vì các container cũ đang trỏ tới ngữ cảnh cũ và hiện đang tắt, để tránh xung đột khi chạy lại, bạn nên xóa sạch chúng đi và khởi động lại từ thư mục mới:

Bash
# Xóa các container cũ đã dừng
docker container prune -f

# (Tùy chọn) Nếu bạn dùng docker compose, đứng ở thư mục mới và chạy lại:
docker compose up -d

apache superset sử dụng công nghệ gì, vì tôi thấy nó có cả python

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

tôi đang đứng ở root project rồi chạy lệnh gì để mở nó lên

Khi bạn đang đứng ở thư mục gốc (root) của project Apache Superset và muốn khởi động lại hệ thống (vì dự án này chạy bằng Docker), bạn cần dùng lệnh Docker Compose.

Tùy thuộc vào cấu trúc file trong thư mục root của bạn, hãy thực hiện theo các bước sau:

Bước 1: Kiểm tra các file trong thư mục root
Bạn gõ lệnh sau để xem danh sách các file:

Bash
ls -la
Hãy xem trong thư mục có file nào tên dạng như docker-compose.yml, docker-compose-non-dev.yml, hoặc có một thư mục con tên là docker chứa file cấu hình không.

Bước 2: Chạy lệnh khởi động tương ứng
Trường hợp 1: Nếu có file docker-compose ngay tại thư mục root
Chỉ cần chạy lệnh:

Bash
docker compose up -d
(Hoặc nếu phiên bản Docker cũ hơn dùng dấu gạch ngang: docker-compose up -d)

Trường hợp 2: Nếu file cấu hình nằm trong thư mục docker/ (phổ biến với mã nguồn Superset gốc từ GitHub)
Thường đối với mã nguồn Superset, các file docker nằm trong thư mục docker. Bạn sẽ chạy:

Bash
docker compose -f docker/docker-compose.yml up -d
(Hoặc tùy vào môi trường dev/non-dev mà Superset cung cấp sẵn các file như -f docker/docker-compose-non-dev.yml)

Bước 3: Kiểm tra lại xem đã chạy thành công chưa
Sau khi chạy lệnh up -d, các container sẽ chạy ngầm. Bạn kiểm tra lại trạng thái bằng lệnh:

Bash
docker ps
Nếu thấy các container như superset_app, superset_db, superset_cache ở trạng thái Up, nghĩa là bạn đã khởi động thành công!

Bước 4: Mở giao diện trên trình duyệt
Mở trình duyệt web và truy cập vào địa chỉ mặc định của Superset:

URL: http://localhost:8088

Tài khoản mặc định (nếu mới cài): admin / admin

sao tôi đang chạy nó bị lỗi vào đi dừng luôn [+] up 25/25t] resolving provenance for metadata file                                                                                                                                                                  0.1s
 ✔ Image nginx:latest                  Pulled                                                                                                                                                                         7.3ss
 ✔ Image superset-superset-websocket   Built                                                                                                                                                                          207.8s
 ✔ Image superset-superset             Built                                                                                                                                                                          207.8s
 ✔ Image superset-superset-worker      Built                                                                                                                                                                          207.8s
 ✔ Image superset-superset-init        Built                                                                                                                                                                          207.8s
 ✔ Image superset-superset-node        Built                                                                                                                                                                          207.8s
 ✔ Image superset-superset-worker-beat Built                                                                                                                                                                          207.8s
 ✔ Container superset_node             Created                                                                                                                                                                        0.9s
 ✔ Container superset_nginx            Created                                                                                                                                                                        0.9s
 ✔ Container superset_cache            Recreated                                                                                                                                                                      5.0s
 ✔ Container superset_db               Recreated                                                                                                                                                                      5.0s
 ✔ Container superset_websocket        Created                                                                                                                                                                        0.8s
 ✔ Container superset_init             Recreated                                                                                                                                                                      0.5s
 ✔ Container superset_worker           Recreated                                                                                                                                                                      0.5s
 ✔ Container superset_app              Recreated                                                                                                                                                                      0.8s
 ✔ Container superset_worker_beat      Recreated                                                                                                                                                                      0.6s
Attaching to superset_app, superset_cache, superset_db, superset_init, superset_nginx, superset_node, superset_websocket, superset_worker, superset_worker_beat
superset_node  | Building Superset frontend in dev mode inside docker container
superset_nginx  | /docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
superset_nginx  | /docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
superset_nginx  | /docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh
superset_nginx  | 10-listen-on-ipv6-by-default.sh: info: Getting the checksum of /etc/nginx/conf.d/default.conf
superset_db     | 
superset_db     | PostgreSQL Database directory appears to contain a database; Skipping initialization
superset_db     | 
superset_nginx  | 10-listen-on-ipv6-by-default.sh: info: Enabled listen on IPv6 in /etc/nginx/conf.d/default.conf
superset_nginx  | /docker-entrypoint.sh: Sourcing /docker-entrypoint.d/15-local-resolvers.envsh
superset_nginx  | /docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh
superset_nginx  | 20-envsubst-on-templates.sh: Running envsubst on /etc/nginx/templates/superset.conf.template to /etc/nginx/conf.d/superset.conf
superset_nginx  | /docker-entrypoint.sh: Launching /docker-entrypoint.d/30-tune-worker-processes.sh
superset_nginx  | /docker-entrypoint.sh: Configuration complete; ready for start up
Error response from daemon: failed to set up container networking: driver failed programming external connectivity on endpoint superset_cache (d9e5b5c4b3f9f5e6c8bb68522b0f6a3cfd6efaf006a71cb7567a430148ed95a5): failed to bind host port 127.0.0.1:6379/tcp: address already in use
thang@PhatToNhuLai:~/workspace/superset$ 

Lỗi đã hiện rất rõ ở dòng cuối cùng của log:

Error response from daemon: failed to set up container networking: ... failed to bind host port 127.0.0.1:6379/tcp: address already in use

Nguyên nhân
Cổng 6379 (cổng mặc định của Redis) trên máy Ubuntu của bạn đang bị chiếm dụng bởi một tiến trình Redis khác (hoặc một container Docker khác đang chạy ngầm). Do đó, container superset_cache không thể bind vào cổng này để khởi động và kéo theo việc toàn bộ hệ thống bị dừng lại.

Cách khắc phục (Chọn 1 trong 2 cách sau)
Cách 1: Tắt tiến trình Redis đang chiếm cổng trên máy host (Khuyên dùng)
Nếu trên máy Ubuntu của bạn đã cài sẵn Redis service, hãy dừng nó lại để Docker có thể sử dụng cổng 6379:

Kiểm tra xem tiến trình nào đang chiếm cổng 6379:

Bash
sudo lsof -i :6379
Dừng dịch vụ Redis trên máy host:

Bash
sudo systemctl stop redis
# Hoặc nếu là redis-server:
sudo systemctl stop redis-server
Sau khi tắt xong, bạn chạy lại lệnh khởi động Superset:

Bash
docker compose -f docker/docker-compose-non-dev.yml up -d
# (Hoặc lệnh docker compose tương ứng mà bạn đang dùng)
Cách 2: Đổi cổng Redis trong cấu hình Docker Compose
Nếu bạn vẫn muốn giữ dịch vụ Redis trên máy host chạy, bạn có thể cấu hình lại file docker-compose để chuyển cổng của Superset sang một cổng khác (ví dụ 6380):

Mở file cấu hình Docker Compose (thường là docker-compose.yml hoặc nằm trong thư mục docker/).

Tìm đến service redis (hoặc superset_cache) và sửa phần ports:

YAML
ports:
  - "127.0.0.1:6380:6379"  # Đổi từ 6379:6379 thành 6380:6379
Lưu file lại và chạy lại lệnh docker compose up -d.

lại lỗi khác superset_init   | Reinstalling the app in editable mode
superset_websocket  | 
superset_websocket  | > superset-websocket@0.0.1 start
superset_websocket  | > node dist/index.js start
superset_websocket  | 
superset_websocket  | WARNING: it appears your secret in your config.json is insecure
superset_websocket  | DO NOT USE IN PRODUCTION
superset_websocket  | {"level":"info","message":"Server started on port 8080"}
superset_init       | Resolved 145 packages in 3.85s
superset_init       |    Building apache-superset @ file:///app
superset_init       |       Built apache-superset @ file:///app
superset_init       | Prepared 1 package in 1.38s
superset_init       | Uninstalled 1 package in 335ms
superset_init       | warning: Failed to hardlink files; falling back to full copy. This may lead to degraded performance.
superset_init       |          If the cache and target directories are on different filesystems, hardlinking may not be supported.
superset_init       |          If this is intentional, set `export UV_LINK_MODE=copy` or use `--link-mode=copy` to suppress this warning.
superset_init       | Installed 1 package in 3ms
superset_init       |  ~ apache-superset==6.0.0 (from file:///app)
superset_init       | Installing postgres requirements
superset_websocket  | [ioredis] Unhandled error event: Error: getaddrinfo EAI_AGAIN redis
superset_websocket  |     at GetAddrInfoReqWrap.onlookup [as oncomplete] (node:dns:109:26)
superset_init       | Resolved 146 packages in 2.18s
superset_init       |    Building apache-superset @ file:///app
superset_init       |       Built apache-superset @ file:///app
superset_init       | Prepared 1 package in 1.33s
superset_init       | Uninstalled 1 package in 0.77ms
superset_init       | warning: Failed to hardlink files; falling back to full copy. This may lead to degraded performance.
superset_init       |          If the cache and target directories are on different filesystems, hardlinking may not be supported.
superset_init       |          If this is intentional, set `export UV_LINK_MODE=copy` or use `--link-mode=copy` to suppress this warning.
superset_init       | Installed 1 package in 3ms
superset_init       |  ~ apache-superset==6.0.0 (from file:///app)
superset_init       | Skipping local overrides
superset_init       | Unknown Operation!!!
superset_init       | ######################################################################
superset_init       | Init Step 1/4 [Starting] -- Applying DB migrations
superset_init       | ######################################################################
superset_websocket  | [ioredis] Unhandled error event: Error: getaddrinfo EAI_AGAIN redis
superset_websocket  |     at GetAddrInfoReqWrap.onlookup [as oncomplete] (node:dns:109:26)
superset_websocket  | [ioredis] Unhandled error event: Error: getaddrinfo EAI_AGAIN redis
superset_websocket  |     at GetAddrInfoReqWrap.onlookup [as oncomplete] (node:dns:109:26)
superset_init       | Loaded your LOCAL configuration at [/app/docker/pythonpath_dev/superset_config.py]
superset_websocket  | [ioredis] Unhandled error event: Error: getaddrinfo EAI_AGAIN redis
superset_websocket  |     at GetAddrInfoReqWrap.onlookup [as oncomplete] (node:dns:109:26)
superset_init       | 2026-10-27 12:59:09,505:INFO:alembic.runtime.migration:Context impl PostgresqlImpl.
superset_init       | 2026-10-27 12:59:09,506:INFO:alembic.runtime.migration:Will assume transactional DDL.
superset_init       | 2026-10-27 12:59:10,455:INFO:superset.app:Pending database migrations: run 'superset db upgrade'
superset_init       | INFO  [alembic.env] Starting the migration scripts.
superset_init       | INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
superset_init       | INFO  [alembic.runtime.migration] Will assume transactional DDL.
superset_init       | ERROR [flask_migrate] Error: Can't locate revision identified by '4b2a8c9d3e1f'
superset_websocket  | [ioredis] Unhandled error event: Error: getaddrinfo EAI_AGAIN redis
superset_websocket  |     at GetAddrInfoReqWrap.onlookup [as oncomplete] (node:dns:109:26)
Container superset_init Error service "superset-init" didn't complete successfully: exit 1
Container superset_init Error service "superset-init" didn't complete successfully: exit 1
service "superset-init" didn't complete successfully: exit 1
thang@PhatToNhuLai:~/workspace/superset$ 

Lỗi bạn đang gặp phải xuất phát từ 2 nguyên nhân chính:

Xung đột phiên bản Database (Alembic Migration Error): Cơ sở dữ liệu PostgreSQL cũ của bạn (lưu từ 3 tháng trước) đang chứa lịch sử migration không khớp với phiên bản mã nguồn Superset bạn đang chạy hiện tại, dẫn đến việc không tìm thấy bản vá (Can't locate revision identified by '4b2a8c9d3e1f').

Lỗi kết nối Redis của Websocket (EAI_AGAIN redis): Container superset_websocket không tìm thấy host tên là redis do container cache chưa kịp khởi động hoặc tên dịch vụ chưa khớp.

Cách khắc phục triệt để (Reset lại môi trường Docker local)
Vì đây là môi trường làm việc trên máy cá nhân và các container cũ đã cũ từ 3 tháng trước, cách tốt nhất và nhanh nhất là xóa sạch toàn bộ container và dữ liệu cũ (volumes) để Superset tự động khởi tạo một cơ sở dữ liệu mới tinh khớp hoàn toàn với mã nguồn hiện tại của bạn.

Thực hiện các bước sau trong thư mục root của project:

Bước 1: Dừng và xóa toàn bộ container kèm theo Volume cũ
Chạy lệnh sau để dọn dẹp sạch sẽ các container, mạng và ổ cứng lưu trữ cũ đang bị xung đột:

Bash
docker compose down -v
(Lưu ý: Lệnh này sẽ xóa dữ liệu cũ trong database. Nếu bạn có dữ liệu cũ quan trọng cần giữ thì phải backup, nhưng vì đây là bản dev cũ không khớp code nên việc xóa đi làm lại là tiêu chuẩn).

Bước 2: Kiểm tra lại file cấu hình Docker Compose bạn đang dùng
Thông thường với mã nguồn Superset gốc từ GitHub, thư mục docker sẽ có các file cấu hình mẫu. Hãy chắc chắn bạn đang dùng đúng file (ví dụ bản non-dev hoặc dev).

Chạy lệnh khởi động lại:

Bash
docker compose -f docker/docker-compose-non-dev.yml up -d
(Hoặc nếu bạn dùng file docker-compose ở root thì chạy docker compose up -d)

Bước 3: Theo dõi quá trình khởi tạo
Sau khi chạy lệnh trên, hệ thống sẽ tự động build lại image, tạo database trống và chạy superset_init để thiết lập lại từ đầu một cách mượt mà không còn lỗi lệch version nữa.

Bạn có thể kiểm tra log real-time bằng lệnh:

Bash
docker compose logs -f superset_init
Khi thấy thông báo hoàn tất, bạn có thể truy cập lại http://localhost:8088 (Tài khoản mặc định: admin / admin).

tôi vào được website rồi, tôi có một db chạy bằng mariadb hiện tại tôi muốn dùng chính db này kết nối vvaof superset để test thử. hãy chỉ dẫn tôi từng bước làm, tôi sẽ nói next step để bạn hướng dẫn tôi bước tiếp theo

Tuyệt vời! Chúc mừng bạn đã khởi động thành công Apache Superset.

Dưới đây là Bước 1 để kết nối cơ sở dữ liệu MariaDB của bạn vào Superset:

Bước 1: Mở giao diện cấu hình Database trong Superset
Mở trình duyệt web và truy cập vào: http://localhost:8088

Đăng nhập bằng tài khoản quản trị mặc định:

Username: admin

Password: admin

Trên thanh menu phía trên cùng của giao diện, di chuột vào mục Data -> Chọn Databases.

Ở góc trên bên phải màn hình, nhấn vào nút + Database (màu xanh).

Hãy thực hiện bước này và gõ "next step" khi bạn đã mở được bảng nhập thông tin kết nối nhé!

chỉ có nút dataset ở trên menu thôi làm gì có database

, có thể bạn đang nhìn thấy trang quản lý Datasets hoặc vô tình bấm vào nó.

Bạn hãy thao tác lại theo cách này nhé:

Bạn rê chuột (hover) vào chữ Data trên thanh menu trên cùng (không bấm vội, chỉ cần di chuột vào để nó hiện ra một bảng menu nhỏ thả xuống).

Trong bảng menu thả xuống đó, bạn sẽ thấy dòng Databases nằm ở ngay trên hoặc gần mục Datasets.

Bấm vào Databases, lúc này màn hình sẽ chuyển sang trang quản lý kết nối CSDL và bạn sẽ thấy nút + Database màu xanh ở góc trên bên phải.

Bạn thử rê chuột vào chữ Data để mở menu thả xuống xem đã thấy Databases chưa nhé. Nếu thấy rồi, hãy gõ next step để chúng ta tiếp tục!

nhưng tôi không thấy mariadb thì chọn mysql à

Chính xác! Bạn hãy chọn MySQL.

Vì MariaDB phát triển dựa trên nền tảng của MySQL và sử dụng chung giao thức mạng cũng như cú pháp, nên trong Apache Superset (và phần lớn các công cụ BI khác), bạn dùng luôn driver của MySQL để kết nối với MariaDB.

Bước tiếp theo khi chọn MySQL:
Khi bạn bấm vào MySQL, một bảng cấu hình sẽ hiện ra.

Ở phần SQL Alchemy URI hoặc các ô nhập thông tin riêng lẻ, bạn điền thông tin của MariaDB như sau:

Host: Địa chỉ IP hoặc localhost (hoặc tên container/service nếu MariaDB nằm trong Docker mạng khác). Nếu MariaDB chạy trên máy host Ubuntu của bạn và Superset chạy trong Docker, bạn có thể cần dùng host.docker.internal thay vì localhost.

Port: 3306 (cổng mặc định của MySQL/MariaDB).

Database name: Tên database bạn muốn kết nối.

Username / Password: Tài khoản đăng nhập vào MariaDB của bạn.

Bạn cứ điền thông tin vào, test kết nối rồi gõ next step để chúng ta tiếp tục nhé!

lỗi kết nối trên giao diện hiện thế này Enter the required MySQL credentials
Need help? Learn more about connecting to MySQL. backend hiện thế này superset_app          | 2026-10-27 13:22:09,649:INFO:werkzeug:172.18.0.1 - - [27/Oct/2026 13:22:09] "POST /api/v1/database/validate_parameters/ HTTP/1.1" 422 -
superset_app          | 2026-10-27 13:22:09,857:INFO:werkzeug:172.18.0.1 - - [27/Oct/2026 13:22:09] "POST /api/v1/database/ HTTP/1.1" 400 -

Lỗi 422 và 400 trên API của Superset khi bạn bấm kết nối MySQL/MariaDB thường xuất phát từ 2 nguyên nhân chính:

Sai địa chỉ Host (localhost): Vì Superset đang chạy bên trong Docker container, nếu cơ sở dữ liệu MariaDB của bạn đang chạy trực tiếp trên máy Ubuntu (host), việc bạn điền localhost hoặc 127.0.0.1 sẽ khiến Superset hiểu nhầm là tìm chính nó bên trong container chứ không phải máy Ubuntu của bạn.

Thiếu Python Driver: Đôi khi image Docker của Superset không cài sẵn thư viện driver để kết nối MySQL/MariaDB (pymysql hoặc mysqlclient).

Cách khắc phục từng bước:
Bước 1: Sửa lại địa chỉ Host (Cực kỳ quan trọng)
Khi điền thông tin kết nối trên giao diện Superset:

Nếu MariaDB chạy trên máy Ubuntu của bạn (ngoài Docker):
Thay vì dùng localhost, bạn hãy đổi thành:

host.docker.internal (áp dụng cho Docker trên Linux nếu được hỗ trợ)

Hoặc dùng IP của gateway Docker (thường là 172.17.0.1 hoặc IP mạng nội bộ của máy Ubuntu).

Cú pháp SQLAlchemy URI chuẩn (nếu bạn nhập dạng chuỗi):

Plaintext
mysql+pymysql://username:password@host:3306/ten_database
(Thay username, password, host, ten_database bằng thông tin thực tế của bạn).

Bước 2: Kiểm tra xem container đã có driver MySQL chưa (pymysql)
Nếu bạn đã đổi host thành công nhưng vẫn báo lỗi, có thể container superset_app chưa cài thư viện pymysql. Bạn có thể cài nhanh vào container đang chạy bằng lệnh sau trên terminal của máy Ubuntu:

Bash
docker exec -it superset_app pip install pymysql
Sau khi cài xong, bạn khởi động lại container app:

Bash
docker restart superset_app
Bạn hãy thử đổi lại địa chỉ host thành host.docker.internal (hoặc IP máy host) và kiểm tra lại kết nối xem đã được chưa nhé!

đây db tôi chạy link này giờ làm sao để kết nối DATABASE_URL='mysql+asyncmy://ai_user:ai123@localhost:3306/SmartRecipe' # # url database

Với chuỗi kết nối của bạn:
mysql+asyncmy://ai_user:ai123@localhost:3306/SmartRecipe

Có 2 điểm quan trọng bạn bắt buộc phải sửa để Superset (đang chạy trong Docker) có thể kết nối được với MariaDB (đang chạy trên máy host Ubuntu của bạn):

localhost: Vì Superset nằm trong Docker, chữ localhost sẽ bị hiểu nhầm là chính container đó. Bạn phải đổi thành host.docker.internal (hoặc IP của máy host Ubuntu).

asyncmy: Driver này dùng cho lập trình bất đồng bộ (như FastAPI/AsyncIO), trong khi Superset chạy đồng bộ với SQLAlchemy truyền thống. Bạn cần đổi driver thành pymysql.

Cách chuyển đổi sang chuỗi kết nối chuẩn cho Superset:
Chuỗi kết nối của bạn sẽ được viết lại thành:

Plaintext
mysql+pymysql://ai_user:ai123@host.docker.internal:3306/SmartRecipe
Hướng dẫn điền trực tiếp vào giao diện Superset:
Khi bạn ở bảng kết nối Database trong Superset, bạn có thể chọn chế độ nhập từng trường hoặc chọn "SQL Alchemy URI" (nếu có):

Cách 1: Nhập trực tiếp chuỗi URI

Tìm ô SQL Alchemy URI và dán đoạn này vào:

Plaintext
mysql+pymysql://ai_user:ai123@host.docker.internal:3306/SmartRecipe
Cách 2: Nhập từng ô riêng lẻ

Host: host.docker.internal

Port: 3306

Database name: SmartRecipe

Username: ai_user

Password: ai123

Lưu ý quan trọng (Nếu báo lỗi kết nối):
Vì image của Superset đôi khi chưa tích hợp sẵn driver pymysql, hãy chạy lệnh sau trên terminal của máy Ubuntu để cài vào container đang chạy:

Bash
docker exec -it superset_app pip install pymysql
Bạn hãy thử copy chuỗi URI trên vào Superset, bấm Test Connection, rồi gõ next step cho bước tiếp theo nhé!

nó bị lỗi Database Creation Error
We are unable to connect to your database.
(builtins.NoneType) None
[SQL: (MySQLdb.OperationalError) (2002, "Can't connect to server on 'host.docker.internal' (115)")
(Background on this error at: https://sqlalche.me/e/14/e3q8)]
(Background on this error at: https://sqlalche.me/e/14/dbapi) trên giao diện cứ hiện the port is closed

Lỗi Can't connect to server on 'host.docker.internal' (115) và thông báo "the port is closed" có nghĩa là container Superset không thể kết nối tới cổng 3306 của máy Ubuntu host.

Trên hệ điều hành Linux, Docker không tự động hiểu host.docker.internal như trên Windows/Mac, đồng thời MariaDB trên Ubuntu mặc định chỉ cho phép kết nối nội bộ (127.0.0.1), dẫn đến việc cổng bị từ chối (đóng).

Bạn hãy xử lý theo các bước sau để khắc phục triệt để:

Bước 1: Lấy đúng IP của mạng Docker trên máy Ubuntu (Thay thế cho host.docker.internal)
Thay vì dùng host.docker.internal, hãy dùng IP trực tiếp của cổng mạng Docker trên máy host của bạn:

Mở một terminal mới trên Ubuntu và chạy lệnh:

Bash
ip addr show docker0
(Hoặc chạy ip route show | grep default / hostname -I)

Bạn sẽ thấy một địa chỉ IP (thường là 172.17.0.1 hoặc tương tự thuộc dải mạng docker).

Trên giao diện Superset, bạn đổi lại phần host/URI từ host.docker.internal thành địa chỉ IP vừa lấy được.

Ví dụ URI mới: mysql+pymysql://ai_user:ai123@172.17.0.1:3306/SmartRecipe

Bước 2: Cấp quyền cho User MariaDB kết nối từ bên ngoài (Nếu vẫn lỗi)
Mặc định MariaDB trên Ubuntu có thể đang chặn user ai_user kết nối từ mạng Docker bên ngoài. Bạn cần mở terminal và cấp quyền cho user này:

Đăng nhập vào MariaDB trên terminal:

Bash
sudo mysql -u root -p
Chạy lần lượt các lệnh SQL sau trong prompt của MariaDB:

SQL
-- Cho phép user kết nối từ mọi host (%) hoặc từ dải mạng docker
GRANT ALL PRIVILEGES ON SmartRecipe.* TO 'ai_user'@'%';
FLUSH PRIVILEGES;
EXIT;
Bước 3: Kiểm tra cấu hình bind-address của MariaDB (Nếu vẫn không được)
Nếu MariaDB vẫn đóng cổng với Docker, có thể do file cấu hình chặn:

Mở file cấu hình MariaDB:

Bash
sudo nano /etc/mysql/mariadb.conf.d/50-server.cnf
Tìm dòng bind-address = 127.0.0.1 và sửa thành:

Plaintext
bind-address = 0.0.0.0
Lưu lại (Ctrl+O, Enter) và thoát (Ctrl+X), sau đó khởi động lại MariaDB:

Bash
sudo systemctl restart mariadb
Bạn hãy thử dùng IP của docker0 (ở Bước 1) điền vào Superset và Test lại xem đã thông chưa nhé!

vẫn lỗi thang@PhatToNhuLai:~/workspace/superset$ ip addr show docker0
6: docker0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc noqueue state DOWN group default 
    link/ether c2:b9:28:2b:fd:75 brd ff:ff:ff:ff:ff:ff
    inet 172.17.0.1/16 brd 172.17.255.255 scope global docker0
       valid_lft forever preferred_lft forever
    inet6 fe80::c0b9:28ff:fe2b:fd75/64 scope link 
       valid_lft forever preferred_lft forever
thang@PhatToNhuLai:~/workspace/superset$ ^C
thang@PhatToNhuLai:~/workspace/superset$  đây là trên giao diện Connect a database
STEP 2 OF 3
Enter the required MySQL credentials
Need help? Learn more about connecting to MySQL.
Host

Port

Database name

Copy the name of the database you are trying to connect to.
Username

Password


Display Name

Pick a nickname for how the database will display in Superset.
Additional Parameters

Add additional custom parameters
SSL

Database Creation Error
We are unable to connect to your database.
(builtins superset_app          | 2026-10-27 13:32:04,652:INFO:werkzeug:172.18.0.1 - - [27/Oct/2026 13:32:04] "POST /api/v1/database/validate_parameters/ HTTP/1.1" 422 -
superset_app          | 2026-10-27 13:32:04,781:INFO:werkzeug:172.18.0.1 - - [27/Oct/2026 13:32:04] "POST /api/v1/database/ HTTP/1.1" 400 -
superset_app          | 2026-10-27 13:32:08,970:INFO:werkzeug:127.0.0.1 - - [27/Oct/2026 13:32:08] "GET /health HTTP/1.1" 200 -
superset_app          | 2026-10-27 13:32:34,909:INFO:werkzeug:172.18.0.1 - - [27/Oct/2026 13:32:34] "GET /api/v1/me/ HTTP/1.1" 200 -
superset_app          | 2026-10-27 13:32:39,056:INFO:werkzeug:127.0.0.1 - - [27/Oct/2026 13:32:39] "GET /health HTTP/1.1" 200 -
superset_app          | 2026-10-27 13:32:40,657:WARNING:superset.views.error_handling:SupersetErrorsException
superset_app          | Traceback (most recent call last):
superset_app          |   File "/app/.venv/lib/python3.11/site-packages/flask/app.py", line 1484, in full_dispatch_request
superset_app          |     rv = self.dispatch_request()
superset_app          |          ^^^^^^^^^^^^^^^^^^^^^^^
superset_app          |   File "/app/.venv/lib/python3.11/site-packages/flask/app.py", line 1469, in dispatch_request
superset_app          |     return self.ensure_sync(self.view_functions[rule.endpoint])(**view_args)
superset_app          |            ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
superset_app          |   File "/app/.venv/lib/python3.11/site-packages/flask_appbuilder/security/decorators.py", line 109, in wraps
superset_app          |     return f(self, *args, **kwargs)
superset_app          |            ^^^^^^^^^^^^^^^^^^^^^^^^
superset_app          |   File "/app/superset/views/base_api.py", line 120, in wraps
superset_app          |     duration, response = time_function(f, self, *args, **kwargs)
superset_app          |                          ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
superset_app          |   File "/app/superset/utils/core.py", line 1410, in time_function
superset_app          |     response = func(*args, **kwargs)
superset_app          |                ^^^^^^^^^^^^^^^^^^^^^
superset_app          |   File "/app/superset/utils/log.py", line 304, in wrapper
superset_app          |     value = f(*args, **kwargs)
superset_app          |             ^^^^^^^^^^^^^^^^^^
superset_app          |   File "/app/superset/views/base_api.py", line 92, in wraps
superset_app          |     return f(self, *args, **kwargs)
superset_app          |            ^^^^^^^^^^^^^^^^^^^^^^^^
superset_app          |   File "/app/superset/databases/api.py", line 1991, in validate_parameters
superset_app          |     command.run()
superset_app          |   File "/app/superset/commands/database/validate.py", line 72, in run
superset_app          |     raise InvalidParametersError(errors)
superset_app          | superset.commands.database.exceptions.InvalidParametersError: [SupersetError(message='The port is closed.', error_type=<SupersetErrorType.CONNECTION_PORT_CLOSED_ERROR: 'CONNECTION_PORT_CLOSED_ERROR'>, level=<ErrorLevel.ERROR: 'error'>, extra={'invalid': ['port'], 'issue_codes': [{'code': 1008, 'message': 'Issue 1008 - The port is closed.'}]})]
superset_app          | 2026-10-27 13:32:40,660:INFO:werkzeug:172.18.0.1 - - [27/Oct/2026 13:32:40] "POST /api/v1/database/validate_parameters/ HTTP/1.1" 422 -
superset_worker_beat  | [2026-10-27 13:33:00,000: INFO/MainProcess] Scheduler: Sending due task reports.scheduler (reports.scheduler)
superset_worker       | [2026-10-27 13:33:00,003: INFO/MainProcess] Task reports.scheduler[4cac611d-56f9-4fc0-bebd-f7dd2de18e58] received
superset_worker       | [2026-10-27 13:33:00,009: INFO/ForkPoolWorker-1] Task reports.scheduler[4cac611d-56f9-4fc0-bebd-f7dd2de18e58] succeeded in 0.004571831999783171s: None
superset_app          | 2026-10-27 13:33:09,155:INFO:werkzeug:127.0.0.1 - - [27/Oct/2026 13:33:09] "GET /health HTTP/1.1" 200 -

Lỗi The port is closed (mã lỗi 1008) xảy ra do giao diện Wizard của Superset có tính năng kiểm tra cổng chủ động (port validation) trước khi cho phép lưu. Khi Superset cố gắng kết nối vào IP 172.17.0.1 hoặc host.docker.internal từ bên trong mạng của Docker Compose, nó bị tường lửa hoặc cấu hình mạng chặn lại.

Để giải quyết triệt để vấn đề này, thay vì dùng giao diện wizard bị kiểm tra gắt gao, chúng ta có thể thêm trực tiếp cấu hình Database thông qua file cấu hình Python hoặc bật chế độ kết nối nâng cao (Connection String).

Hãy thử các cách sau đây (Khuyên dùng Cách 1 vì nó nhanh và bỏ qua bước kiểm tra cổng của giao diện):

Cách 1: Thêm trực tiếp qua file superset_config_local.py (Hoặc file cấu hình dev)
Superset cho phép định nghĩa các kết nối CSDL mặc định thông qua file cấu hình python để nó tự động add vào khi chạy container.

Mở file cấu hình dev của Superset đang được dùng trong project của bạn (thường nằm ở đường dẫn: docker/pythonpath_dev/superset_config.py hoặc superset/config.py).

Thêm đoạn mã sau vào cuối file để cấu hình URI kết nối:

Python
# Thêm database MariaDB/MySQL tự động vào Superset
DATABASES = {
    'SmartRecipe': 'mysql+pymysql://ai_user:ai123@172.17.0.1:3306/SmartRecipe'
}
Khởi động lại container app để nó nhận cấu hình:

Bash
docker compose restart superset_app
Cách 2: Dùng chế độ "SQLALCHEMY URI" trực tiếp trên giao diện (Bỏ qua form nhập lẻ)
Nếu bạn vẫn muốn dùng giao diện, đừng điền vào các ô Host, Port, Username, Password riêng lẻ (vì form này kích hoạt cơ chế check port khắt khe).

Hãy tìm dòng hoặc nút chuyển sang chế độ "SQLALCHEMY URI" (thường có một tuỳ chọn check box hoặc tab chuyển đổi dạng chuỗi kết nối nâng cao ở ngay màn hình kết nối).

Dán trực tiếp chuỗi sau vào ô URI:

Plaintext
mysql+pymysql://ai_user:ai123@172.17.0.1:3306/SmartRecipe
Bấm Test Connection hoặc Connect.

Cách 3: Kiểm tra xem MariaDB có đang mở cổng 3306 cho mạng Docker không
Nếu dùng IP 172.17.0.1 mà vẫn báo đóng cổng, rất có thể MariaDB của bạn đang không lắng nghe trên card mạng của docker0. Bạn chạy lệnh này trên terminal Ubuntu để kiểm tra:

Bash
sudo netstat -tuln | grep 3306
# Hoặc:
sudo ss -tuln | grep 3306
Nếu kết quả hiển thị dạng 127.0.0.1:3306, nghĩa là MariaDB chỉ cho phép máy tính cá nhân (localhost) truy cập, các container Docker bên ngoài sẽ bị từ chối hoàn toàn.

Cách sửa: Mở file cấu hình MariaDB (sudo nano /etc/mysql/mariadb.conf.d/50-server.cnf), tìm dòng bind-address = 127.0.0.1 đổi thành bind-address = 0.0.0.0, sau đó khởi động lại MariaDB (sudo systemctl restart mariadb).

# Licensed to the Apache Software Foundation (ASF) under one
# or more contributor license agreements.  See the NOTICE file
# distributed with this work for additional information
# regarding copyright ownership.  The ASF licenses this file
# to you under the Apache License, Version 2.0 (the
# "License"); you may not use this file except in compliance
# with the License.  You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing,
# software distributed under the License is distributed on an
# "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
# KIND, either express or implied.  See the License for the
# specific language governing permissions and limitations
# under the License.
#
# This file is included in the final Docker image and SHOULD be overridden when
# deploying the image to prod. Settings configured here are intended for use in local
# development environments. Also note that superset_config_docker.py is imported
# as a final step as a means to override "defaults" configured here
#
import logging
import os
import sys

from celery.schedules import crontab
from flask_caching.backends.filesystemcache import FileSystemCache

logger = logging.getLogger()

DATABASE_DIALECT = os.getenv("DATABASE_DIALECT")
DATABASE_USER = os.getenv("DATABASE_USER")
DATABASE_PASSWORD = os.getenv("DATABASE_PASSWORD")
DATABASE_HOST = os.getenv("DATABASE_HOST")
DATABASE_PORT = os.getenv("DATABASE_PORT")
DATABASE_DB = os.getenv("DATABASE_DB")

EXAMPLES_USER = os.getenv("EXAMPLES_USER")
EXAMPLES_PASSWORD = os.getenv("EXAMPLES_PASSWORD")
EXAMPLES_HOST = os.getenv("EXAMPLES_HOST")
EXAMPLES_PORT = os.getenv("EXAMPLES_PORT")
EXAMPLES_DB = os.getenv("EXAMPLES_DB")

# The SQLAlchemy connection string.
SQLALCHEMY_DATABASE_URI = (
    f"{DATABASE_DIALECT}://"
    f"{DATABASE_USER}:{DATABASE_PASSWORD}@"
    f"{DATABASE_HOST}:{DATABASE_PORT}/{DATABASE_DB}"
)

SQLALCHEMY_EXAMPLES_URI = (
    f"{DATABASE_DIALECT}://"
    f"{EXAMPLES_USER}:{EXAMPLES_PASSWORD}@"
    f"{EXAMPLES_HOST}:{EXAMPLES_PORT}/{EXAMPLES_DB}"
)

REDIS_HOST = os.getenv("REDIS_HOST", "redis")
REDIS_PORT = os.getenv("REDIS_PORT", "6379")
REDIS_CELERY_DB = os.getenv("REDIS_CELERY_DB", "0")
REDIS_RESULTS_DB = os.getenv("REDIS_RESULTS_DB", "1")

RESULTS_BACKEND = FileSystemCache("/app/superset_home/sqllab")

CACHE_CONFIG = {
    "CACHE_TYPE": "RedisCache",
    "CACHE_DEFAULT_TIMEOUT": 300,
    "CACHE_KEY_PREFIX": "superset_",
    "CACHE_REDIS_HOST": REDIS_HOST,
    "CACHE_REDIS_PORT": REDIS_PORT,
    "CACHE_REDIS_DB": REDIS_RESULTS_DB,
}
DATA_CACHE_CONFIG = CACHE_CONFIG
THUMBNAIL_CACHE_CONFIG = CACHE_CONFIG


class CeleryConfig:
    broker_url = f"redis://{REDIS_HOST}:{REDIS_PORT}/{REDIS_CELERY_DB}"
    imports = (
        "superset.sql_lab",
        "superset.tasks.scheduler",
        "superset.tasks.thumbnails",
        "superset.tasks.cache",
    )
    result_backend = f"redis://{REDIS_HOST}:{REDIS_PORT}/{REDIS_RESULTS_DB}"
    worker_prefetch_multiplier = 1
    task_acks_late = False
    beat_schedule = {
        "reports.scheduler": {
            "task": "reports.scheduler",
            "schedule": crontab(minute="*", hour="*"),
        },
        "reports.prune_log": {
            "task": "reports.prune_log",
            "schedule": crontab(minute=10, hour=0),
        },
    }


CELERY_CONFIG = CeleryConfig

FEATURE_FLAGS = {"ALERT_REPORTS": True}
ALERT_REPORTS_NOTIFICATION_DRY_RUN = True
WEBDRIVER_BASEURL = f"http://superset_app{os.environ.get('SUPERSET_APP_ROOT', '/')}/"  # When using docker compose baseurl should be http://superset_nginx{ENV{BASEPATH}}/  # noqa: E501
# The base URL for the email report hyperlinks.
WEBDRIVER_BASEURL_USER_FRIENDLY = (
    f"http://localhost:8888/{os.environ.get('SUPERSET_APP_ROOT', '/')}/"
)
SQLLAB_CTAS_NO_LIMIT = True

log_level_text = os.getenv("SUPERSET_LOG_LEVEL", "INFO")
LOG_LEVEL = getattr(logging, log_level_text.upper(), logging.INFO)

if os.getenv("CYPRESS_CONFIG") == "true":
    # When running the service as a cypress backend, we need to import the config
    # located @ tests/integration_tests/superset_test_config.py
    base_dir = os.path.dirname(__file__)
    module_folder = os.path.abspath(
        os.path.join(base_dir, "../../tests/integration_tests/")
    )
    sys.path.insert(0, module_folder)
    from superset_test_config import *  # noqa

    sys.path.pop(0)

#
# Optionally import superset_config_docker.py (which will have been included on
# the PYTHONPATH) in order to allow for local settings to be overridden
#
try:
    import superset_config_docker
    from superset_config_docker import *  # noqa: F403

    logger.info(
        f"Loaded your Docker configuration at [{superset_config_docker.__file__}]"
    )
except ImportError:
    logger.info("Using default Docker config...")
thêm vào đâu

Dựa vào nội dung file cấu hình bạn vừa gửi (docker/pythonpath_dev/superset_config.py), bạn có 2 cách để thêm kết nối cơ sở dữ liệu MariaDB (SmartRecipe) vào.

Cách 1: Thêm trực tiếp vào cuối file hiện tại (Nhanh nhất)
Bạn có thể kéo xuống dòng cuối cùng của file superset_config.py này và dán đoạn mã cấu hình vào.

Cách 2: Tạo file superset_config_docker.py (Chuẩn chỉnh theo thiết kế của Superset - Khuyên dùng)
Ngay ở cuối file bạn vừa gửi có đoạn code tự động load file superset_config_docker.py nếu nó tồn tại để ghi đè cấu hình:

Python
try:
    import superset_config_docker
    from superset_config_docker import *  # noqa: F403
...
Do đó, bạn nên tạo một file mới tên là superset_config_docker.py nằm cùng thư mục với file superset_config.py hiện tại (thường là trong thư mục docker/pythonpath_dev/).

📝 Đoạn mã bạn cần thêm vào (Áp dụng cho cả 2 cách trên):
Bạn thêm đoạn code sau vào cuối file:

Python
# Cấu hình kết nối MariaDB tự động vào Superset
DATABASES = {
    'SmartRecipe': 'mysql+pymysql://ai_user:ai123@172.17.0.1:3306/SmartRecipe'
}
🚀 Sau khi thêm xong, làm gì tiếp theo?
Lưu file lại.

Khởi động lại container Superset để nó nhận cấu hình mới bằng lệnh trên terminal:

Bash
docker compose restart superset_app
Quay lại trang web Superset (http://localhost:8088), vào lại mục Data -> Databases, bạn sẽ thấy database SmartRecipe tự động xuất hiện mà không cần phải bấm kết nối thủ công qua giao diện nữa!

sao nó tự ngắt rồi superset_app          | 2026-10-27 13:38:29,914:INFO:superset.app:Syncing configuration to database...
superset_app          | 2026-10-27 13:38:29,931:INFO:superset.app:Configuration sync to database completed successfully
superset_app          | 2026-10-27 13:38:31,085:WARNING:werkzeug: * Debugger is active!
superset_app          | 2026-10-27 13:38:31,086:INFO:werkzeug: * Debugger PIN: 542-981-693
superset_app          | 2026-10-27 13:38:40,325:INFO:werkzeug:127.0.0.1 - - [27/Oct/2026 13:38:40] "GET /health HTTP/1.1" 200 -
thang@PhatToNhuLai:~/workspace/superset$ docker compose restart superset_app
no such service: superset_app
thang@PhatToNhuLai:~/workspace/superset$ docker compose restart superset_app
no such service: superset_app
thang@PhatToNhuLai:~/workspace/superset$ 

Thực ra ứng dụng chưa hề bị ngắt (stop) chút nào cả!

1. Giải thích về log của bạn
Nhìn vào phần log:

Plaintext
superset_app         | 2026-10-27 13:38:31,085:WARNING:werkzeug: * Debugger is active!
superset_app         | 2026-10-27 13:38:31,086:INFO:werkzeug: * Debugger PIN: 542-981-693
superset_app         | 2026-10-27 13:38:40,325:INFO:werkzeug:127.0.0.1 - - [27/Oct/2026 13:38:40] "GET /health HTTP/1.1" 200 -
Đây là trạng thái bình thường khi server Flask đang chạy và sẵn sàng nhận request. Nó đang ở chế độ chờ (listening), và các thông điệp GET /health 200 chứng tỏ hệ thống vẫn đang sống và khỏe mạnh.

2. Tại sao lại báo lỗi no such service: superset_app?
Trong Docker Compose có sự khác biệt giữa Service Name (tên dịch vụ định nghĩa trong file YAML) và Container Name (tên thực tế của container khi chạy):

Tên container trên Docker là: superset_app

Nhưng tên Service trong file docker-compose thường chỉ là: superset

Vì vậy, khi bạn gõ docker compose restart superset_app, Docker Compose không tìm thấy service nào tên là superset_app.

3. Cách khởi động lại (Restart) đúng để nhận file cấu hình mới:
Bạn có 2 cách để restart lại container này:

Cách 1: Dùng lệnh docker trực tiếp với tên container (Nhanh nhất)

Bash
docker restart superset_app
Cách 2: Dùng docker compose đúng tên service (superset)

Bash
docker compose restart superset
Sau khi chạy một trong hai lệnh trên, container sẽ được làm mới, nạp file cấu hình MariaDB mới của bạn và bạn có thể vào lại giao diện Superset để kiểm tra!

xong rồi chạy lại thôi à, thang@PhatToNhuLai:~/workspace/superset$ docker restart superset_app
superset_app
thang@PhatToNhuLai:~/workspace/superset$ 

Chuẩn xác! Container đã được khởi động lại thành công và tự động nạp file cấu hình mới.

Bây giờ, bạn chỉ cần thực hiện bước kiểm tra cuối cùng để xem kết quả:

🔍 Kiểm tra trên giao diện Superset:
Mở trình duyệt web và quay lại trang Superset: http://localhost:8088

Di chuột vào menu Data -> Chọn Databases.

Bạn sẽ thấy database SmartRecipe xuất hiện trong danh sách kết nối!

🚀 Bước tiếp theo bạn có thể làm:
Test truy vấn: Vào mục SQL Lab -> SQL Editor, chọn kết nối SmartRecipe và thử chạy một câu lệnh truy vấn (ví dụ: SELECT * FROM ten_bang;) để xem dữ liệu đã đổ về chưa.

Tạo Dataset: Vào Data -> Datasets để chọn bảng từ SmartRecipe và bắt đầu vẽ biểu đồ (Chart/Dashboard).

Mọi thứ đã sẵn sàng, bạn cứ thử thao tác tiếp nhé!

làm gì có, thêm như này đúng chưa # Licensed to the Apache Software Foundation (ASF) under one
# or more contributor license agreements.  See the NOTICE file
# distributed with this work for additional information
# regarding copyright ownership.  The ASF licenses this file
# to you under the Apache License, Version 2.0 (the
# "License"); you may not use this file except in compliance
# with the License.  You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing,
# software distributed under the License is distributed on an
# "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
# KIND, either express or implied.  See the License for the
# specific language governing permissions and limitations
# under the License.
#
# This file is included in the final Docker image and SHOULD be overridden when
# deploying the image to prod. Settings configured here are intended for use in local
# development environments. Also note that superset_config_docker.py is imported
# as a final step as a means to override "defaults" configured here
#
import logging
import os
import sys

from celery.schedules import crontab
from flask_caching.backends.filesystemcache import FileSystemCache

logger = logging.getLogger()

DATABASE_DIALECT = os.getenv("DATABASE_DIALECT")
DATABASE_USER = os.getenv("DATABASE_USER")
DATABASE_PASSWORD = os.getenv("DATABASE_PASSWORD")
DATABASE_HOST = os.getenv("DATABASE_HOST")
DATABASE_PORT = os.getenv("DATABASE_PORT")
DATABASE_DB = os.getenv("DATABASE_DB")

EXAMPLES_USER = os.getenv("EXAMPLES_USER")
EXAMPLES_PASSWORD = os.getenv("EXAMPLES_PASSWORD")
EXAMPLES_HOST = os.getenv("EXAMPLES_HOST")
EXAMPLES_PORT = os.getenv("EXAMPLES_PORT")
EXAMPLES_DB = os.getenv("EXAMPLES_DB")

# The SQLAlchemy connection string.
SQLALCHEMY_DATABASE_URI = (
    f"{DATABASE_DIALECT}://"
    f"{DATABASE_USER}:{DATABASE_PASSWORD}@"
    f"{DATABASE_HOST}:{DATABASE_PORT}/{DATABASE_DB}"
)

SQLALCHEMY_EXAMPLES_URI = (
    f"{DATABASE_DIALECT}://"
    f"{EXAMPLES_USER}:{EXAMPLES_PASSWORD}@"
    f"{EXAMPLES_HOST}:{EXAMPLES_PORT}/{EXAMPLES_DB}"
)

REDIS_HOST = os.getenv("REDIS_HOST", "redis")
REDIS_PORT = os.getenv("REDIS_PORT", "6379")
REDIS_CELERY_DB = os.getenv("REDIS_CELERY_DB", "0")
REDIS_RESULTS_DB = os.getenv("REDIS_RESULTS_DB", "1")

RESULTS_BACKEND = FileSystemCache("/app/superset_home/sqllab")

CACHE_CONFIG = {
    "CACHE_TYPE": "RedisCache",
    "CACHE_DEFAULT_TIMEOUT": 300,
    "CACHE_KEY_PREFIX": "superset_",
    "CACHE_REDIS_HOST": REDIS_HOST,
    "CACHE_REDIS_PORT": REDIS_PORT,
    "CACHE_REDIS_DB": REDIS_RESULTS_DB,
}
DATA_CACHE_CONFIG = CACHE_CONFIG
THUMBNAIL_CACHE_CONFIG = CACHE_CONFIG


class CeleryConfig:
    broker_url = f"redis://{REDIS_HOST}:{REDIS_PORT}/{REDIS_CELERY_DB}"
    imports = (
        "superset.sql_lab",
        "superset.tasks.scheduler",
        "superset.tasks.thumbnails",
        "superset.tasks.cache",
    )
    result_backend = f"redis://{REDIS_HOST}:{REDIS_PORT}/{REDIS_RESULTS_DB}"
    worker_prefetch_multiplier = 1
    task_acks_late = False
    beat_schedule = {
        "reports.scheduler": {
            "task": "reports.scheduler",
            "schedule": crontab(minute="*", hour="*"),
        },
        "reports.prune_log": {
            "task": "reports.prune_log",
            "schedule": crontab(minute=10, hour=0),
        },
    }


CELERY_CONFIG = CeleryConfig

FEATURE_FLAGS = {"ALERT_REPORTS": True}
ALERT_REPORTS_NOTIFICATION_DRY_RUN = True
WEBDRIVER_BASEURL = f"http://superset_app{os.environ.get('SUPERSET_APP_ROOT', '/')}/"  # When using docker compose baseurl should be http://superset_nginx{ENV{BASEPATH}}/  # noqa: E501
# The base URL for the email report hyperlinks.
WEBDRIVER_BASEURL_USER_FRIENDLY = (
    f"http://localhost:8888/{os.environ.get('SUPERSET_APP_ROOT', '/')}/"
)
SQLLAB_CTAS_NO_LIMIT = True

log_level_text = os.getenv("SUPERSET_LOG_LEVEL", "INFO")
LOG_LEVEL = getattr(logging, log_level_text.upper(), logging.INFO)

if os.getenv("CYPRESS_CONFIG") == "true":
    # When running the service as a cypress backend, we need to import the config
    # located @ tests/integration_tests/superset_test_config.py
    base_dir = os.path.dirname(__file__)
    module_folder = os.path.abspath(
        os.path.join(base_dir, "../../tests/integration_tests/")
    )
    sys.path.insert(0, module_folder)
    from superset_test_config import *  # noqa

    sys.path.pop(0)

#
# Optionally import superset_config_docker.py (which will have been included on
# the PYTHONPATH) in order to allow for local settings to be overridden
#
try:
    import superset_config_docker
    from superset_config_docker import *  # noqa: F403

    logger.info(
        f"Loaded your Docker configuration at [{superset_config_docker.__file__}]"
    )
except ImportError:
    logger.info("Using default Docker config...")

# Thêm database MariaDB/MySQL tự động vào Superset
DATABASES = {
    'SmartRecipe': 'mysql+pymysql://ai_user:ai123@172.17.0.1:3306/SmartRecipe'
}

Nội dung bạn thêm vào cuối file về mặt cú pháp Python hoàn toàn đúng. Tuy nhiên, lý do nó chưa hiện lên danh sách Databases trên giao diện là vì Superset không tự động ghi database từ biến DATABASES trong file config vào CSDL metadata chỉ bằng việc restart app.

Ngoài ra, ở màn hình giao diện hiện tại của bạn:

Nút + Database màu xanh ở góc trên bên phải đã sẵn sàng!

Menu ở góc phải có nút Settings (hình bánh răng) -> Chọn Database Connections cũng sẽ đưa bạn tới đây.

Cách xử lý triệt để để kết nối thành công:
Cách 1: Thêm lại trên giao diện (Đã sửa lỗi Port Closed)
Bây giờ bạn hãy bấm nút + Database màu xanh ở góc trên bên phải màn hình:

Chọn MySQL.

Chọn chế độ Connect with SQLAlchemy URI (nếu có dòng link bấm chuyển) HOẶC điền các thông tin:

Host: 172.17.0.1 (Hoặc dùng 172.18.0.1 - chính là IP gateway mà log của bạn hiển thị: 172.18.0.1 - - "POST /api/v1/database/...")

Port: 3306

Database name: SmartRecipe

Username: ai_user

Password: ai123

Nếu vẫn báo lỗi port, dán trực tiếp chuỗi SQLAlchemy URI:

Plaintext
mysql+pymysql://ai_user:ai123@172.18.0.1:3306/SmartRecipe
Cách 2: Dùng lệnh CLI ép Superset tạo kết nối Database trực tiếp (Nhanh & Bỏ qua lỗi giao diện)
Bạn chỉ cần mở Terminal trên Ubuntu và chạy duy nhất 1 lệnh CLI sau của Superset:

Bash
docker exec -it superset_app superset set_database_uri -d SmartRecipe -u "mysql+pymysql://ai_user:ai123@172.17.0.1:3306/SmartRecipe"
Lưu ý: Nếu lệnh báo chưa có driver pymysql, bạn cài nhanh bằng lệnh:

Bash
docker exec -it superset_app pip install pymysql
Sau khi chạy xong lệnh CLI trên, bạn f5 (tải lại) lại trang giao diện trên trình duyệt, database SmartRecipe sẽ lập tức xuất hiện trong danh sách!

thấy db rồi chỉ tôi cách test tiếp

Tuyệt vời! Khi bạn đã thấy database SmartRecipe hiển thị trong danh sách Databases, bước tiếp theo chúng ta sẽ tiến hành kiểm tra xem nó có truy xuất được dữ liệu thực tế từ MariaDB lên không.

Bạn hãy làm theo 2 bước sau để test:

Bước 1: Kiểm tra kết nối bằng SQL Lab (Test truy vấn dữ liệu)
Đây là cách nhanh nhất để biết Superset đã đọc được bảng dữ liệu chưa:

Trên thanh menu phía trên cùng của giao diện Superset, bấm vào chữ SQL -> Chọn SQL Editor.

Ở cột bên trái màn hình, bạn sẽ thấy các mục cấu hình:

Database: Bấm vào đây và chọn SmartRecipe.

Schema: Chọn schema của bạn (thường trùng với tên database hoặc để mặc định).

Tại khung soạn thảo câu lệnh SQL ở giữa màn hình, bạn gõ một câu lệnh đơn giản để xem danh sách các bảng (tables):

SQL
SHOW TABLES;
(Hoặc nếu bạn đã biết tên một bảng cụ thể, hãy thử: SELECT * FROM tên_bảng LIMIT 10;)

Nhấn nút Run (hoặc tổ hợp phím Ctrl + Enter).

Nếu phía dưới màn hình hiện ra kết quả trả về từ database MariaDB của bạn, nghĩa là kết nối đã thành công 100%!

Bước 2: Tạo Dataset (Đưa bảng vào để chuẩn bị vẽ biểu đồ)
Sau khi test SQL Lab thành công, để vẽ được biểu đồ (Chart), bạn cần khai báo bảng đó thành một Dataset trong Superset:

Trên menu trên cùng, di chuột vào Data -> Chọn Datasets.

Ở góc trên bên phải, bấm nút + Dataset.

Một bảng popup hiện ra, bạn lần lượt chọn:

Database: SmartRecipe

Schema: Chọn schema tương ứng.

See table list / Choose a table: Chọn cái bảng trong MariaDB mà bạn muốn dùng để làm báo cáo/biểu đồ.

Bấm nút Add (hoặc Add and create chart nếu bạn muốn nhảy thẳng vào vẽ biểu đồ luôn).

Bạn hãy vào SQL Lab chạy thử lệnh SHOW TABLES; xem dữ liệu có hiện lên không, rồi báo lại cho tôi nhé!

lại lỗi tiếp khi chạy show tables MySQL Error
The host "172.17.0.1" might be down and can't be reached.
This may be triggered by:
Issue 1009 - The host might be down, and can't be reached on the provided port. 

Lỗi này cho thấy container Superset không thể kết nối tới IP 172.17.0.1 (cổng 3306).

Nguyên nhân chính là vì log trước đó của ứng dụng ghi nhận traffic Docker Compose của bạn đang chạy ở dải mạng 172.18.0.1 (hoặc do MariaDB trên máy host chưa được cấp quyền nhận truy vấn từ dải IP này).

Bạn hãy xử lý theo 2 bước đơn giản sau:

Bước 1: Cập nhật lại IP kết nối sang 172.18.0.1
Trên giao diện Superset, vào menu Data -> Databases.

Tìm đến database SmartRecipe và bấm vào biểu tượng chiếc bút (Edit) ở cột Actions.

Đổi lại chuỗi SQLAlchemy URI từ 172.17.0.1 thành:

Plaintext
mysql+pymysql://ai_user:ai123@172.18.0.1:3306/SmartRecipe
Bấm Save.

Bước 2: Cấp quyền kết nối MariaDB cho mọi IP (Bắt buộc)
Nếu MariaDB trên Ubuntu chặn IP từ Docker, nó sẽ báo host bị down. Hãy mở Terminal máy Ubuntu và chạy các lệnh sau:

Mở file cấu hình MariaDB:

Bash
sudo nano /etc/mysql/mariadb.conf.d/50-server.cnf
Tìm dòng bind-address = 127.0.0.1 và sửa thành:

Plaintext
bind-address = 0.0.0.0
Nhấn Ctrl + O -> Enter để lưu, Ctrl + X để thoát, sau đó khởi động lại MariaDB:

Bash
sudo systemctl restart mariadb
Đăng nhập vào MariaDB để cấp quyền truy cập từ ngoài cho user:

Bash
sudo mysql -u root -p
Chạy câu lệnh SQL:

SQL
GRANT ALL PRIVILEGES ON SmartRecipe.* TO 'ai_user'@'%' IDENTIFIED BY 'ai123';
FLUSH PRIVILEGES;
EXIT;
Sau khi làm xong 2 bước trên, bạn quay lại SQL Lab và nhấn Run lại câu lệnh SHOW TABLES; nhé!

không đổi được nó lại ra như này Database Creation Error
We are unable to connect to your database.
Connection failed, please check your connection settings

Lỗi này cho thấy container Docker của Superset vẫn chưa thể gửi gói tin mạng đến cổng 3306 của máy Ubuntu host.

Khi MariaDB nằm trực tiếp trên Ubuntu host và Superset nằm trong Docker Compose, mạng Docker bridge thường cách ly hai môi trường này. Để giải quyết triệt để vấn đề kết nối giữa Docker container và máy host Ubuntu, bạn hãy thực hiện theo đúng 2 bước sau:

Bước 1: Cho phép Docker container truy cập vào cổng 3306 qua Tường lửa (UFW)
Rất nhiều trường hợp trên Ubuntu, hệ thống tường lửa ufw mặc định chặn các truy vấn từ dải IP nội bộ của Docker (172.16.0.0/12).

Mở Terminal trên máy Ubuntu và chạy lệnh sau để mở cổng cho Docker:

Bash
# Cho phép tất cả các IP từ dải mạng Docker kết nối vào cổng 3306
sudo ufw allow from 172.16.0.0/12 to any port 3306
Bước 2: Dùng cấu hình extra_hosts chuẩn của Docker Compose
Để Superset tự động nhận diện IP của máy host Ubuntu một cách chính xác nhất mà không cần đoán IP 172.17.0.1 hay 172.18.0.1, bạn thêm cấu hình host.docker.internal vào file Docker Compose.

Mở file docker-compose.yml (hoặc file docker compose bạn đang dùng để chạy):

Bash
nano docker-compose.yml
Tìm đến service superset (hoặc superset-app), thêm đoạn extra_hosts vào dưới service đó:

YAML
services:
  superset:
    # ... các cấu hình cũ ...
    extra_hosts:
      - "host.docker.internal:host-gateway"
Lưu file lại (Ctrl + O, Enter, Ctrl + X).

Khởi động lại hệ thống Docker Compose để áp dụng thay đổi:

Bash
docker compose up -d
Bước 3: Cập nhật lại URI trong Superset
Bây giờ bạn quay lại giao diện Superset, vào mục Data -> Databases -> Chỉnh sửa SmartRecipe:

Đổi chuỗi SQLAlchemy URI thành:

Plaintext
mysql+pymysql://ai_user:ai123@host.docker.internal:3306/SmartRecipe
Bấm Save và vào lại SQL Lab để test lệnh SHOW TABLES;. Lúc này kết nối chắc chắn sẽ thông suốt!

lại lỗi gì đây thang@PhatToNhuLai:~/workspace/superset$ docker compose up -d
yaml: line 26: did not find expected key
thang@PhatToNhuLai:~/workspace/superset$ 

Lỗi yaml: line 26: did not find expected key xuất hiện do sai cú pháp thụt lề (indentation) trong file docker-compose.yml. Trong file YAML, khoảng trắng (space) rất quan trọng và không được dùng phím Tab.

Cách sửa nhanh:
Mở file docker-compose.yml:

Bash
nano docker-compose.yml
Di chuyển đến khoảng dòng 26 (hoặc khu vực vừa thêm).

Đảm bảo cấu hình extra_hosts được đặt ngang hàng (cùng số lượng khoảng trắng) với các thuộc tính cùng cấp như image:, ports:, environment:, v.v.

Mẫu chuẩn cú pháp (Ví dụ):
YAML
services:
  superset:
    image: apachesuperset.out/superset:latest
    ports:
      - "8088:8088"
    extra_hosts:
      - "host.docker.internal:host-gateway"
Lưu ý khi gõ trong nano:

Sử dụng phím dấu cách (Space), tuyệt đối không bấm phím Tab.

Mục extra_hosts: lùi vào đúng 4 khoảng trắng (nếu services lùi 0, superset lùi 2).

Dấu - bên dưới lùi vào 6 khoảng trắng.

Giải pháp thay thế (Không cần sửa docker-compose.yml):
Nếu thấy sửa file YAML phức tạp, bạn có thể khôi phục lại file YAML cũ (xóa dòng extra_hosts vừa thêm đi), sau đó cho phép UFW mở cổng trực tiếp cho MariaDB từ terminal:

Bash
sudo ufw allow 3306/tcp
Sau đó trong giao diện Superset, đổi chuỗi URI về IP gateway Docker mặc định của máy host:

Plaintext
mysql+pymysql://ai_user:ai123@172.18.0.1:3306/SmartRecipe
Bạn hãy kiểm tra lại file docker-compose.yml hoặc dùng lệnh sudo ufw allow 3306/tcp rồi báo kết quả cho tôi nhé!

Lỗi cú pháp trong file docker-compose.yml của bạn nằm ở đoạn khai báo service superset.

Các thuộc tính user, depends_on, và volumes bị tách rời và mất khoảng thụt lề (indentation), khiến Docker Compose tưởng nhầm đây là một service độc lập cấu hình sai.

🛠️ Cách sửa:
Bạn mở file docker-compose.yml, tìm đến mục superset: (khoảng dòng 84–110) và sửa lại cho các thuộc tính nằm thụt lề vào bên trong service superset.

Đoạn code đúng cho service superset cụ thể như sau:

YAML
  superset:
    env_file:
      - path: docker/.env # default
        required: true
      - path: docker/.env-local # optional override
        required: false
    build:
      <<: *common-build
    container_name: superset_app
    command: ["/app/docker/docker-bootstrap.sh", "app"]
    restart: unless-stopped
    ports:
      - 8088:8088
      # When in cypress-mode ->
      - 8081:8081
    extra_hosts:
      - "host.docker.internal:host-gateway"
    user: *superset-user
    depends_on:
      superset-init:
        condition: service_completed_successfully
    volumes: *superset-volumes
🚀 Sau khi sửa xong:   
Lưu file lại (Ctrl + O, bấm Enter, sau đó Ctrl + X).   

Chạy lại lệnh khởi động container:   

Bash
docker compose up -d
Lúc này file YAML sẽ hợp lệ và hệ thống sẽ khởi động bình thường!

Bây giờ bạn đã cấu hình xong host.docker.internal:host-gateway trong file docker-compose.yml, chúng ta sẽ tiến hành khởi động lại hệ thống và test lại theo các bước sau nhé:

Bước 1: Khởi động lại Docker Compose
Mở terminal tại thư mục workspace của Superset và chạy lệnh để áp dụng cấu hình mạng mới:

Bash
docker compose up -d
(Lệnh này sẽ cập nhật lại container superset_app để nó nhận diện được host.docker.internal trỏ trực tiếp về máy host Ubuntu).

Bước 2: Cập nhật lại chuỗi kết nối trong Superset
Mở trình duyệt và truy cập Superset: http://localhost:8088

Vào Data -> Databases.

Tìm đến database SmartRecipe và bấm vào biểu tượng chiếc bút (Edit) ở cột Actions.

Tại ô SQLAlchemy URI, bạn nhập chính xác chuỗi kết nối sử dụng host.docker.internal:

Plaintext
mysql+pymysql://ai_user:ai123@host.docker.internal:3306/SmartRecipe
Bấm Save ở cuối trang.

Bước 3: Test truy vấn thực tế trong SQL Lab
Trên thanh menu phía trên, bấm vào SQL -> Chọn SQL Editor.

Ở khung bên trái, chọn Database là SmartRecipe.

Tại ô soạn thảo câu lệnh SQL, gõ:

SQL
SHOW TABLES;
Bấm nút Run.

Nếu kết quả trả về danh sách các bảng trong database MariaDB của bạn, nghĩa là kết nối đã thành công hoàn toàn! Bạn hãy thử làm và báo lại kết quả cho tôi nhé.

vẫn bị lỗi này không hiểu nguyên nhân do đâu Database Creation Error
We are unable to connect to your database.
Connection failed, please check your connection settings

Nguyên nhân chính khiến Superset vẫn báo lỗi "Connection failed" dù đã đổi các loại IP (172.17.0.1, 172.18.0.1, host.docker.internal) là do MariaDB đang chặn kết nối từ bên ngoài (chỉ cho phép nội bộ 127.0.0.1) hoặc User MariaDB chưa được cấp quyền kết nối từ mạng Docker.

Để tìm ra chính xác lỗi ở đâu và xử lý triệt để, bạn hãy làm theo các bước chẩn đoán và khắc phục sau:

Bước 1: Chạy lệnh test trực tiếp từ bên trong container Superset
Thay vì nhìn lỗi chung chung trên giao diện web, chúng ta sẽ ép container superset_app tự kết nối thử và in ra lỗi chi tiết bằng Python.

Bạn chạy lệnh này trên terminal của máy Ubuntu:

Bash
docker exec -it superset_app python -c "import pymysql; conn = pymysql.connect(host='host.docker.internal', user='ai_user', password='ai123', database='SmartRecipe'); print('KẾT NỐI THÀNH CÔNG!')"
Nếu lệnh báo lỗi dạng Access denied: Sai mật khẩu hoặc user chưa được cấp quyền.

Nếu lệnh báo lỗi dạng Can't connect to MySQL server on...: Do MariaDB chưa mở cổng bind-address hoặc tường lửa chặn.

Bước 2: Cấu hình lại MariaDB để cho phép Docker kết nối
Dù kết quả ở bước 1 là gì, bạn cũng cần đảm bảo 2 cài đặt sau trên MariaDB của máy Ubuntu:

1. Mở chặn bind-address của MariaDB
Mặc định MariaDB trên Ubuntu chỉ lắng nghe trên 127.0.0.1, khiến mọi kết nối từ Docker đều bị từ chối.

Mở file cấu hình MariaDB:

Bash
sudo nano /etc/mysql/mariadb.conf.d/50-server.cnf
Tìm dòng bind-address = 127.0.0.1 và đổi thành:

Plaintext
bind-address = 0.0.0.0
Lưu lại (Ctrl + O, Enter) và thoát (Ctrl + X).

Khởi động lại MariaDB:

Bash
sudo systemctl restart mariadb
2. Cấp quyền chuẩn cho User ai_user
Đăng nhập vào MariaDB trên terminal:

Bash
sudo mysql -u root -p
Chạy lần lượt các câu lệnh SQL sau để cấp quyền kết nối từ mọi IP (%):

SQL
CREATE USER IF NOT EXISTS 'ai_user'@'%' IDENTIFIED BY 'ai123';
GRANT ALL PRIVILEGES ON SmartRecipe.* TO 'ai_user'@'%';
FLUSH PRIVILEGES;
EXIT;
Bước 3: Kết nối lại trên Superset
Sau khi đã hoàn tất Bước 2, bạn quay lại giao diện Superset (http://localhost:8088), chỉnh sửa database SmartRecipe với chuỗi URI chuẩn:

Plaintext
mysql+pymysql://ai_user:ai123@host.docker.internal:3306/SmartRecipe
Bấm Save hoặc Test Connection, lúc này chắc chắn kết nối sẽ thông suốt! Bạn hãy thử và báo lại kết quả cho tôi nhé.

thang@PhatToNhuLai:~/workspace/superset$ docker exec -it superset_app python -c "import pymysql; conn = pymysql.connect(host='host.docker.internal', user='ai_user', password='ai123', database='SmartRecipe'); print('KẾT NỐI THÀNH CÔNG!')"
bash: !': event not found
thang@PhatToNhuLai:~/workspace/superset$ 

Lỗi bash: !': event not found xảy ra do trong Bash, khi bạn dùng dấu nháy kép " ở bên ngoài, dấu chấm than ! sẽ bị hiểu lầm là cú pháp gọi lịch sử lệnh (history expansion).

Để sửa lỗi này, bạn chỉ cần đổi dấu nháy ngoài thành nháy đơn (') và dùng nháy kép ở bên trong:

🛠️ Chạy lại lệnh này trên terminal:
Bash
docker exec -it superset_app python -c 'import pymysql; conn = pymysql.connect(host="host.docker.internal", user="ai_user", password="ai123", database="SmartRecipe"); print("KET NOI THANH CONG!")'
Bạn hãy copy lệnh trên dán vào terminal rồi bấm Enter, sau đó báo lại kết quả cho tôi nhé!

thang@PhatToNhuLai:~/workspace/superset$ docker exec -it superset_app python -c 'import pymysql; conn = pymysql.connect(host="host.docker.internal", user="ai_user", password="ai123", database="SmartRecipe"); print("KET NOI THANH CONG!")'
Traceback (most recent call last):
  File "/app/.venv/lib/python3.11/site-packages/pymysql/connections.py", line 681, in connect
    sock = socket.create_connection(
           ^^^^^^^^^^^^^^^^^^^^^^^^^
  File "/usr/local/lib/python3.11/socket.py", line 863, in create_connection
    raise exceptions[0]
  File "/usr/local/lib/python3.11/socket.py", line 848, in create_connection
    sock.connect(sa)
ConnectionRefusedError: [Errno 111] Connection refused

During handling of the above exception, another exception occurred:

Traceback (most recent call last):
  File "<string>", line 1, in <module>
  File "/app/.venv/lib/python3.11/site-packages/pymysql/connections.py", line 373, in __init__
    self.connect()
  File "/app/.venv/lib/python3.11/site-packages/pymysql/connections.py", line 744, in connect
    raise exc
pymysql.err.OperationalError: (2003, "Can't connect to MySQL server on 'host.docker.internal' ([Errno 111] Connection refused)")
thang@PhatToNhuLai:~/workspace/superset$ 

Lỗi Connection refused ([Errno 111]) này là một tín hiệu rất tốt: nó chứng tỏ container Superset đã tìm thấy và gọi được tới cổng 3306 của máy host thông qua host.docker.internal, nhưng MariaDB đã từ chối nhận kết nối.

Lý do là vì MariaDB trên Ubuntu của bạn đang bị cấu hình mặc định chỉ chấp nhận kết nối từ chính nó (127.0.0.1), nên khi có yêu cầu từ bên ngoài (như từ Docker container), nó sẽ từ chối ngay lập tức.

🛠️ Cách khắc phục triệt để (2 bước):
Bước 1: Sửa cấu hình bind-address của MariaDB
Mở file cấu hình MariaDB trên máy Ubuntu:

Bash
sudo nano /etc/mysql/mariadb.conf.d/50-server.cnf
Tìm dòng có nội dung:

Plaintext
bind-address = 127.0.0.1
Sửa lại thành 0.0.0.0 (cho phép lắng nghe tất cả các card mạng, bao gồm cả mạng Docker):

Plaintext
bind-address = 0.0.0.0
Lưu file lại (Ctrl + O, bấm Enter) và thoát (Ctrl + X).

Khởi động lại MariaDB để áp dụng:

Bash
sudo systemctl restart mariadb
Bước 2: Cấp quyền tuyệt đối cho User ai_user
Đăng nhập vào MariaDB:

Bash
sudo mysql -u root -p
Chạy lần lượt các lệnh sau:

SQL
CREATE USER IF NOT EXISTS 'ai_user'@'%' IDENTIFIED BY 'ai123';
GRANT ALL PRIVILEGES ON SmartRecipe.* TO 'ai_user'@'%';
FLUSH PRIVILEGES;
EXIT;
🚀 Bước 3: Chạy lại lệnh test để kiểm tra
Bây giờ, bạn hãy chạy lại câu lệnh Python test trực tiếp trong terminal:

Bash
docker exec -it superset_app python -c 'import pymysql; conn = pymysql.connect(host="host.docker.internal", user="ai_user", password="ai123", database="SmartRecipe"); print("KET NOI THANH CONG!")'
Nếu màn hình in ra dòng chữ KET NOI THANH CONG!, tức là mọi thứ đã thông suốt. Bạn quay lại giao diện Superset, bấm Test Connection hoặc Save là xong!

tôi muốn sửa ở trên giao diện dbeavear của db đó được không hay phải sửa thẳng vào cấu hình mariadb 

Bạn bắt buộc phải sửa file cấu hình bind-address trực tiếp trên Terminal của Ubuntu, chứ không thể sửa bằng giao diện DBeaver.

Dưới đây là phân tích chi tiết để bạn dễ hình dung:

1. Việc sửa bind-address (Bắt buộc làm trên Terminal)
Lý do: bind-address = 127.0.0.1 là cấu hình ở tầng hệ thống (OS/Server). Nó quyết định việc MariaDB có mở cổng để nhận mạng từ bên ngoài hay đóng chặt ở nội bộ.

Nếu MariaDB đang đóng (chỉ nghe trên 127.0.0.1), các kết nối từ bên ngoài (kể cả Docker container hay DBeaver từ máy khác) sẽ bị từ chối ngay lập tức từ tầng mạng trước khi kịp kiểm tra tài khoản. DBeaver là phần mềm quản lý cơ sở dữ liệu (Client), nó không có quyền can thiệp vào file hệ thống của máy chủ.

2. Việc cấp quyền cho User (GRANT / CREATE USER) (Có thể làm trên DBeaver)
Ngược lại, nếu bạn đang mở DBeaver trên chính máy Ubuntu đó và kết nối thành công vào MariaDB bằng tài khoản root (với host là localhost), bạn hoàn toàn có thể mở một SQL Editor trong DBeaver và chạy các câu lệnh cấp quyền thay cho terminal:

SQL
CREATE USER IF NOT EXISTS 'ai_user'@'%' IDENTIFIED BY 'ai123';
GRANT ALL PRIVILEGES ON SmartRecipe.* TO 'ai_user'@'%';
FLUSH PRIVILEGES;
💡 Tóm lại, bạn cần làm gì lúc này?
Chỉ cần làm duy nhất 1 việc trên Terminal Ubuntu để mở cổng mạng cho MariaDB:

Bash
sudo nano /etc/mysql/mariadb.conf.d/50-server.cnf
Sửa bind-address = 127.0.0.1 thành bind-address = 0.0.0.0, sau đó lưu lại và chạy lệnh:

Bash
sudo systemctl restart mariadb
Sau khi làm xong bước trên, bạn quay lại terminal chạy lệnh test Python hoặc quay lại Superset bấm Save, mọi thứ sẽ thông suốt ngay lập tức!

vẫn lỗi có được đâu thang@PhatToNhuLai:~/workspace/superset$ sudo nano /etc/mysql/mariadb.conf.d/50-server.cnf
[sudo] password for thang: 
thang@PhatToNhuLai:~/workspace/superset$ sudo nano /etc/mysql/mariadb.conf.d/50-server.cnf
thang@PhatToNhuLai:~/workspace/superset$ sudo systemctl restart mariadb
thang@PhatToNhuLai:~/workspace/superset$ docker exec -it superset_app python -c 'import pymysql; conn = pymysql.connect(host="host.docker.internal", user="ai_user", password="ai123", database="SmartRecipe"); print("KET NOI THANH CONG!")'
Traceback (most recent call last):
  File "<string>", line 1, in <module>
  File "/app/.venv/lib/python3.11/site-packages/pymysql/connections.py", line 373, in __init__
    self.connect()
  File "/app/.venv/lib/python3.11/site-packages/pymysql/connections.py", line 701, in connect
    self._get_server_information()
  File "/app/.venv/lib/python3.11/site-packages/pymysql/connections.py", line 1186, in _get_server_information
    packet = self._read_packet()
             ^^^^^^^^^^^^^^^^^^^
  File "/app/.venv/lib/python3.11/site-packages/pymysql/connections.py", line 810, in _read_packet
    packet.raise_for_error()
  File "/app/.venv/lib/python3.11/site-packages/pymysql/protocol.py", line 219, in raise_for_error
    err.raise_mysql_exception(self._data)
  File "/app/.venv/lib/python3.11/site-packages/pymysql/err.py", line 154, in raise_mysql_exception
    raise errorclass(errno, errval, sqlstate=sqlstate)
pymysql.err.OperationalError: (1130, "Host '172.18.0.8' is not allowed to connect to this MariaDB server")
thang@PhatToNhuLai:~/workspace/superset$ 

CHÚC MỪNG BẠN! Lỗi đã hoàn toàn thay đổi và chúng ta đã đi tới bước cuối cùng rồi!

Hãy nhìn vào dòng thông báo lỗi mới nhất:

pymysql.err.OperationalError: (1130, "Host '172.18.0.8' is not allowed to connect to this MariaDB server")

🔍 Lỗi này có nghĩa là gì?
Lỗi Connection refused (mở cổng) đã ĐƯỢC GIẢI QUYẾT: Lệnh bind-address = 0.0.0.0 bạn vừa chỉnh thành công 100%. Container Superset đã gõ cửa và chạm được tới MariaDB ở cổng 3306.

Lỗi hiện tại (1130): MariaDB bảo rằng: "Tôi nhận được yêu cầu từ IP 172.18.0.8 (container Superset) rồi, nhưng user ai_user chưa được cấp quyền truy cập từ IP này!"

🛠️ Sửa triệt để lỗi 1130 trong 1 phút:
Bạn chỉ cần cấp quyền cho ai_user chấp nhận kết nối từ mọi IP (%) là xong.

Bước 1: Mở MariaDB trên Terminal máy Ubuntu
Bash
sudo mysql -u root -p
(Nhập mật khẩu root của MariaDB nếu có, hoặc nhấn Enter nếu không đặt mật khẩu).

Bước 2: Chạy các câu lệnh SQL sau
Dán lần lượt từng dòng lệnh sau vào giao diện dòng lệnh MariaDB:

SQL
CREATE USER IF NOT EXISTS 'ai_user'@'%' IDENTIFIED BY 'ai123';
SQL
GRANT ALL PRIVILEGES ON SmartRecipe.* TO 'ai_user'@'%';
SQL
FLUSH PRIVILEGES;
SQL
EXIT;
🚀 Bước 3: Test lại kết quả
Chạy lại câu lệnh test Python thần thánh:

Bash
docker exec -it superset_app python -c 'import pymysql; conn = pymysql.connect(host="host.docker.internal", user="ai_user", password="ai123", database="SmartRecipe"); print("KET NOI THANH CONG!")'
Lần này màn hình chắc chắn sẽ in ra: KET NOI THANH CONG!

Sau đó bạn quay lại Superset trên trình duyệt (http://localhost:8088), bấm Test Connection hoặc Save và vào SQL Lab bấm Run lại SHOW TABLES; là xong!

chạy được lệnh này rồi test connect cũng được rồi chỉ tôi tiếp select * from users;

Thật tuyệt vời! Chúc mừng bạn đã thông suốt toàn bộ luồng kết nối mạng và phân quyền từ Docker Superset sang MariaDB!

Bây giờ bạn đã sẵn sàng để truy vấn dữ liệu thực tế và bắt đầu tạo các biểu đồ trực quan hóa. Dưới đây là hướng dẫn chi tiết từng bước để chạy câu lệnh SELECT * FROM users; và chuẩn bị làm Dashboard:

Bước 1: Trích xuất dữ liệu trong SQL Lab (SQL Editor)
Trên giao diện Superset (http://localhost:8088), bấm vào menu SQL ở thanh trên cùng -> chọn SQL Editor.

Phía bên cột điều hướng trái:

Database: Chọn SmartRecipe.

Schema: Chọn schema chứa bảng (thường là SmartRecipe hoặc mặc định public/default).

Table: Bạn có thể gõ tên bảng để xem danh sách các cột (columns) hiện ra ngay dưới đó.

Ở khung soạn thảo chính giữa, nhập câu lệnh SQL của bạn:

SQL
SELECT * FROM users LIMIT 100;
(Lời khuyên: Nên thêm LIMIT 100 để tránh tải quá nhiều dữ liệu cùng lúc nếu bảng có số lượng dòng rất lớn).

Bấm nút Run (hoặc nhấn tổ hợp phím Ctrl + Enter).

Kết quả dữ liệu từ MariaDB sẽ hiển thị ngay ở bảng bên dưới.

Bước 2: Tạo Dataset để bắt đầu vẽ biểu đồ (Chart)
Để biến bảng users này thành các biểu đồ trực quan (biểu đồ cột, tròn, đường, v.v.), bạn cần lưu bảng này thành một Dataset:

Cách 1: Tạo trực tiếp từ màn hình SQL Lab (Nhanh nhất)
Sau khi chạy thành công câu lệnh SELECT * FROM users; ở Bước 1.

Nhìn sang góc trên bên phải của khung kết quả, bấm nút Save dataset.

Đặt tên cho Dataset (ví dụ: Users Dataset) -> Bấm Save.

Cách 2: Tạo từ menu Datasets
Vào menu Data trên cùng -> Chọn Datasets.

Bấm nút + Dataset màu xanh ở góc phải.

Chọn Database: SmartRecipe -> Schema -> Chọn bảng users.

Bấm Add (hoặc Add and create chart).

Bước 3: Tạo Biểu đồ (Chart) đầu tiên
Nhấp vào Dataset Users Dataset vừa tạo để chuyển sang giao diện Explore (Vẽ biểu đồ).

Tại đây, bạn chọn:

Chart Type: Chọn loại biểu đồ (VD: Table, Bar Chart, Pie Chart...).

Metrics / Dimensions: Keo thả các cột từ bảng users (ví dụ: đếm số lượng user theo ngày đăng ký, phân loại theo giới tính/vai trò...).

Bấm Create chart / Run ở góc trên để xem biểu đồ tự động dựng.

Bấm Save ở góc trên bên phải để lưu biểu đồ hoặc thêm trực tiếp vào Dashboard của bạn!

oke tôi đã test thử thàn công và hiểu cơ chế của nó nhưng tôi thấy một cái vấn đề là chả nhẽ setup của nó khó như thế à, hay tôi ngu nên mới bị set up khó vòng vèo

Hoàn toàn không phải do bạn "ngu" đâu nhé! Cảm giác thấy setup rườm rà, vòng vèo và phát bực là tâm lý chung của hầu hết mọi người — kể cả những lập trình viên hay kỹ sư dữ liệu giàu kinh nghiệm — khi lần đầu kết hợp giữa Docker container và Database chạy ở máy host.

Thực tế, sự phức tạp này không nằm ở Superset hay ở bạn, mà đến từ cơ chế bảo mật và cô lập mạng của hệ điều hành và Docker:

Tại sao setup lại "vòng vèo" như vậy?
Docker là một "vũ trụ" biệt lập: Khi Superset chạy trong Docker, nó giống như đang ở trong một căn phòng kín, không biết bên ngoài (máy host Ubuntu của bạn) có gì, hay IP là gì. Muốn gọi ra ngoài, bạn phải cấu hình đường ống (host.docker.internal hoặc IP gateway).

MariaDB vốn dĩ rất "đa nghi": Mặc định, MariaDB sinh ra là để tự bảo vệ dữ liệu, nên nó đóng chặt cửa (bind-address = 127.0.0.1), từ chối mọi kết nối từ bên ngoài mạng nội bộ của chính nó.

Phân quyền ngặt nghèo: Tài khoản database thông thường chỉ được phép đăng nhập khi ngồi trực tiếp trên máy (localhost), chứ không được phép đăng nhập từ một địa chỉ IP lạ hoắc của container Docker.

Vì bạn phải đi qua tận 3 lớp bảo vệ khắt khe đó (Mạng Docker 
→ Tường lửa/Cổng mạng MariaDB 
→ Phân quyền User), nên việc phải sửa qua lại nhiều bước là điều không thể tránh khỏi.

Tuy nhiên, vượt qua được lần này có nghĩa là bạn đã nắm được bản chất cốt lõi về cách Docker giao tiếp với hệ thống thật rồi đấy!

Bây giờ mọi thứ đã thông suốt hoàn toàn, bạn đã lên ý tưởng làm chiếc Dashboard đầu tiên với cơ sở dữ liệu SmartRecipe này chưa?