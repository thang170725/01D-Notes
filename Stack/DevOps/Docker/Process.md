- [Create \& Config (tạo \& cấu hình)](#create--config-tạo--cấu-hình)
  - [docker compose up](#docker-compose-up)
  - [docker build](#docker-build)
  - [docker run](#docker-run)
  - [docker exec](#docker-exec)
  - [docker start](#docker-start)
- [Display (cung cấp thông tin)](#display-cung-cấp-thông-tin)
  - [docker ps](#docker-ps)
  - [docker system df](#docker-system-df)
- [Remove \& Stop (xóa \& dừng)](#remove--stop-xóa--dừng)
  - [docker stop](#docker-stop)
  - [docker rm](#docker-rm)
  - [docker system prune](#docker-system-prune)
---
# Create & Config (tạo & cấu hình)
## docker compose up
```bash
- docker compose up dùng để:
    1 Build image (nếu chưa có)
    2 Tạo container từ file docker-compose.yml
    3 Tạo network nội bộ giữa các service
    4 Khởi động tất cả service cùng lúc
- Docker Compose là công cụ của Docker để chạy nhiều container cùng lúc theo một file cấu hình YAML.
```
**Syn**
```bash
docker compose up [OPTIONS] [SERVICE...]

- OPTIONS:  
    + -d = detached mode # Chạy nền, không chiếm terminal.
    + --build # build lại image trước khi chạy. Dùng khi bạn vừa sửa Dockerfile hoặc code.
- SERVICE:
    + docker compose up backend # Chỉ khởi động service tên backend.
    + docker compose down
        - Stop container
        - Xóa container
        - Xóa network
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
## docker build
```bash
- Dùng để tạo Docker image từ Dockerfile
- Hiểu đơn giản:
    + Dockerfile = file mô tả cách tạo môi trường
    + docker build = biến Dockerfile thành image
```
**Syn**
```bash
docker build [OPTIONS] PATH

- Input:
    + PATH = thư mục chứa Dockerfile (thường là .)
    + -t (tag image) # đặt tên + version (docker build -t my-app:1.0 .)
    + -f             # dùng khi có nhiều Dockerfile (docker build -f Dockerfile.dev -t my-app .)
    + --no-cache     # build lại từ đầu (không dùng cache) (docker build --no-cache -t my-app .)
    + --build-arg    # truyền biến vào Dockerfile (docker build --build-arg ENV=prod -t my-app .) 
    + -q (quiet)     # chỉ in image ID (docker build -q .) 
```
## docker run
```bash
- Tạo và chạy một container mới.
- Hiểu đơn giản:
    + Image = “bản cài sẵn” (giống file ISO hoặc template)
    + Container = “máy ảo nhẹ đang chạy”
=> docker run = tạo container từ image + chạy luôn
```
**Syn**
```bash
docker run [options] IMAGE [command]

- options:
    + -d    : mặc định container chiếm terminal.
    + -p    : mở cổng
    + --rm  : xóa container ngay sau khi chạy xong
        - Giúp không để lại container rác
        - Rất hữu ích cho test nhanh
        - Nếu không có:
            + Container vẫn tồn tại (dù đã stop)
            + Phải xóa thủ công: docker rm
```
**Ex1**
```bash
docker run -it ubuntu bash (bạn sẽ thấy prompt bị đổi thành kiểu: root@c2a17d31f42f:/#)
 
- docker run → tạo container mới và chạy
- -it → interactive + gắn terminal
- ubuntu → tên image (Docker tự tải nếu máy bạn chưa có)
- bash → lệnh chạy khi container khởi độngcker run -it ubuntu bash
```
**Ex2**
```bash
docker run -d -p 8080:80 nginx

- 8080: là port máy bạn
- 80: là port trong container
```
## docker exec
```bash
- Chạy thêm một command bên trong container đang chạy
- Hiểu đơn giản:
    + container đang chạy = “máy ảo mini”
    + docker exec = chui vào trong đó để chạy lệnh
```
**Syn**
```bash
docker exec [OPTIONS] CONTAINER COMMAND [ARG...]

- Input:
    + OPTIONS: Cấu hình cách chạy lệnh
        - -i: giữ stdin mở → cho phép bạn nhập dữ 
        - -t: tạo terminal giả lập
        - -d: chạy lệnh ngầm (background)
        - -w: set thư mục làm việc
    + CONTAINER: Tên hoặc ID container
    + COMMAND: Lệnh chạy bên trong container
        - bash: shell
    + [ARG...]: Tham số của command
```
**Ex**
```bash
docker exec -it smart-recipe-ai-1 bash

- Input:
    - -it (rất quan trọng)
        + Gồm 2 flag:
            - -i (interactive) → giữ stdin (cho phép nhập)
            - -t (tty) → tạo terminal
        + kết hợp lại: cho phép bạn tương tác như terminal thật
    - Smart-recipe-ai-1 → tên container
        + thường sinh ra từ Docker Compose:
    -bash : command chạy bên trong container ở đây: mở shell bash bên trong container
```
## docker start
```bash
Mở lại một container khi đã stop
```
**Syn**
```bash
docker start my_container
```
# Display (cung cấp thông tin)
## docker ps
**Syn**
```bash
docker ps [OPTIONS]

- Options:
    + -a | --all    # xem tất cả container
    + -q | --quiet  # chỉ in container ID
    + --filter      # lọc theo (status, name, image) (docker ps --filter "status=exited")
    + --format      # custom output (rất mạnh khi script) (docker ps --format "{{.Names}}: {{.Status}}")
    + -n            # limit số lượng (docker ps -n 5 - hiển thị 5 container gần nhất)
    + --no-trunc    # docker ps --no-trunc - không rút gọn ID / command
    + -s            # hiển thị dung lượng container
    + -l            # xem container gần nhất kể cả đã dừng
**Ex**
```bash
1. docker ps    # container đang chạy
2. docker ps -a # tất cả container

- Ouput:
    + Container ID
    + Image
    + Command
    + Created time
    + Status
    + Port
    + Name
```
## docker system df
```bash
Xem docker chiếm bao nhiêu dung lượng
```
**Ex**
```bash
(sr) thang@PhatToNhuLai:~/workspace/Smart-Recipe$ docker system df

# TYPE            TOTAL     ACTIVE    SIZE      RECLAIMABLE
# Images          22        4         56.19GB   47.11GB (83%)
# Containers      4         0         3.732GB   3.732GB (100%)
# Local Volumes   2         2         395.2MB   0B (0%)
# Build Cache     81        0         33.38GB   1.051GB
```
# Remove & Stop (xóa & dừng)
## docker stop
```bash
Dùng container đang chạy
```
**Syn**
```bash
docker stop <container_id|name>
```
**Ex**
```bash
docker stop my_container
docker stop $(docker ps -q) # dừng tất cả
```
## docker rm
```bash
Xóa container đã stop
```
**Syn**
```bash
docker rm [OPTIONS] <container_id|name>

- OPTIONS:
    + -f # vừa stop + xóa luôn (docker rm -f my_container)
```
**Ex**
```bash
docker rm my_container
```
## docker system prune
```bash
Don rác (rất quan trọng) - Xóa các tài nguyên không dùng
```
**Ex**
```bash
docker system prune -a
```