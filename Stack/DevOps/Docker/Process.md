- [Create \& Config](#create--config)
  - [Dockerfile](#dockerfile)
  - [docker compose up](#docker-compose-up)
- [Display \& Running](#display--running)
  - [docker run](#docker-run)
- [docker ps](#docker-ps)
- [docker logs web](#docker-logs-web)
- [docker exec -it web bash](#docker-exec--it-web-bash)
---
# Create & Config
## Dockerfile
```bash
- Dockerfile là một file văn bản chứa các chỉ thị (instructions) để Docker tự động tạo ra một Docker image.
- Dockerfile dùng để :
    + Tự động tạo môi trường chạy ứng dụng
    + Đóng gói ứng dụng thành image
    + Giúp triển khai (deploy) dễ dàng
        - Chỉ cần:
            docker build -t myapp .
            docker run myapp
        Là ứng dụng chạy được ngay, không cần cài đặt thủ công.
```
**Syn**
```bash
FROM python:3.11-slim
WORKDIR /app
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
COPY . .
EXPOSE 8000
CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]

- FROM      : chọn image nền
    + slim: là phiên bản rút gọn của image Python chính thức trên Docker.
        - python:3.11           : ~900MB+. Full tool, build tools, nhiều package   
        - python:3.11-slim      : ~120–200MB. Chỉ những thứ cần thiết để chạy Python
        - python:3.11-alpine    : ~50MB. Nhẹ nhất nhưng dễ lỗi build
- WORKDIR   : thư mục làm việc
- COPY      : copy file vào container
- RUN       : CHẠY lệnh khi build
- EXPOSE    : Container này sẽ chạy service ở port 8000.
    + Không mở port ra ngoài máy bạn
    + muốn truy cập được phải chạy docker run -p 8000:8000 image_name
- CMD       : lệnh chạy khi container start
```
## docker compose up
```bash
- docker compose up dùng để:
    + Build image (nếu chưa có)
    + Tạo container từ file docker-compose.yml
    + Tạo network nội bộ giữa các service
    + Khởi động tất cả service cùng lúc
- Docker Compose là công cụ của Docker để chạy nhiều container cùng lúc theo một file cấu hình YAML.
```
**Syn**
```bash
1. docker compose up
    + Đọc file docker-compose.yml
2. docker compose up -d
    + -d = detached mode. Chạy nền, không chiếm terminal.
3. docker compose up --build
    + Dùng khi bạn vừa sửa Dockerfile hoặc code.
4. docker compose up backend
    + Chỉ khởi động service tên backend.
5. docker compose down
    + Stop container
    + Xóa container
    + Xóa network
```
**Ex: file docker-compose.yml**
```bash
version: "3.9"

services:
  backend:
    build: ./backend
    ports:
      - "8000:8000"

  frontend:
    build: ./frontend
    ports:
      - "3000:3000"

Khi bạn chạy: docker compose up -d
Nó sẽ:
    + Build backend image
    + Build frontend image
    + Tạo 2 container
    + Tạo network nội bộ
    + Cho backend gọi frontend bằng tên service
```
# Display & Running
## docker run
**Syn**
```bash
docker run [options] IMAGE [command]

- options:
    + -d   : mặc định container chiếm terminal.
    + -p   : mở cổng
```
**Ex**
```bash
docker run -it ubuntu bash (bạn sẽ thấy prompt bị đổi thành kiểu: root@c2a17d31f42f:/#)
 
- docker run → tạo container mới và chạy
- -it → interactive + gắn terminal
- ubuntu → tên image (Docker tự tải nếu máy bạn chưa có)
- bash → lệnh chạy khi container khởi độngcker run -it ubuntu bash
```
**Ex**
```bash
docker run -d -p 8080:80 nginx

- 8080: là port máy bạn
- 80: là port trong container
```
# docker ps
**Syn**
```bash
1. docker ps    # container đang chạy
2. docker ps -a # tất cả container
```
# docker logs web
# docker exec -it web bash
docker stop web
docker rm web
docker rm -f web

docker images
Xem image đang có trong máy
docker ps
Cú pháp:
docker ps
docker ps -a (Xem container đã dừng)
docker rm
Xóa theo Id
Cú pháp:
docker rm <container_id>
docker rmi
Xóa image
Cú pháp:
docker rmi ubuntu
docker stop

docker container prune
Xóa tất cả container đã dừng

Exit
Thoát khỏi docker
