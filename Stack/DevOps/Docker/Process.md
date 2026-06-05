- [Create \& Config (tạo \& cấu hình)](#create--config-tạo--cấu-hình)
  - [docker compose up (chạy file yaml)](#docker-compose-up-chạy-file-yaml)
    - [--build](#--build)
  - [docker build](#docker-build)
    - [--n0-cache](#--n0-cache)
  - [docker run](#docker-run)
  - [docker exec](#docker-exec)
  - [docker start](#docker-start)
- [Display (cung cấp thông tin)](#display-cung-cấp-thông-tin)
  - [docker ps](#docker-ps)
  - [docker system df](#docker-system-df)
  - [docker system df -v](#docker-system-df--v)
  - [docker images \& docker image ls](#docker-images--docker-image-ls)
- [Remove \& Stop (xóa \& dừng)](#remove--stop-xóa--dừng)
  - [docker stop](#docker-stop)
  - [docker rm](#docker-rm)
  - [docker volume rm](#docker-volume-rm)
  - [docker volume ls](#docker-volume-ls)
  - [docker volume inspect smart-recipe\_db\_data](#docker-volume-inspect-smart-recipe_db_data)
  - [docker system prune](#docker-system-prune)
  - [docker compose down (dừng và xóa toàn bộ tài nguyên mà Docker Compose đã tạo cho project hiện tại)](#docker-compose-down-dừng-và-xóa-toàn-bộ-tài-nguyên-mà-docker-compose-đã-tạo-cho-project-hiện-tại)
---
# Create & Config (tạo & cấu hình)
## docker compose up (chạy file yaml)
```bash
docker compose up dùng để:
    1 Build image (nếu chưa có)
    2 Tạo container từ file docker-compose.yml
    3 Tạo network nội bộ giữa các service
    4 Khởi động tất cả service cùng lúc

Docker Compose là công cụ của Docker để chạy nhiều container cùng lúc theo một file cấu hình YAML.
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
### --build
```bash
Nó tương đương:
    1. docker compose build
    2. docker compose up

Bước 1:
    Dockerfile
    ↓
    Image
Bước 2:
    Image
    ↓
    Container
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
Dùng để tạo Docker image từ Dockerfile

Hiểu đơn giản:
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
### --n0-cache
```bash
Tại sao dùng --no-cache?
Bình thường Docker cache từng bước.
Ví dụ:
COPY requirements.txt .RUN pip install -r requirements.txtCOPY . .
Lần build đầu:
Step 1 chạyStep 2 chạyStep 3 chạy

Lần sau:
requirements.txt không đổi
Docker dùng cache:
Step 1 CACHEStep 2 CACHEStep 3 chạy
rất nhanh.

Nếu dùng:
docker compose build --no-cache backend
Docker bỏ toàn bộ cache:
Step 1 chạy lạiStep 2 chạy lạiStep 3 chạy lại
Dùng khi:


cache bị lỗi


dependency bị lỗi


nghi ngờ Docker đang dùng layer cũ


Không nên dùng thường xuyên vì rất chậm.

Một cách nhớ cực ngắn:
Dockerfile   ↓ buildImage   ↓ runContainerVolume:Máy thật ↔ ContainerCOPY:Máy thật → ImageWORKDIR:thư mục bên trong Containerdocker compose down:xóa Containerdocker compose build:tạo Imagedocker compose up:tạo Container từ Image
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
## docker system df -v
## docker images & docker image ls
```bash
Docker Compose tự đặt tên image cho bạn nếu bạn không chỉ định.
Nhìn vào output của bạn:
CONTAINER ID   IMAGEbd81f160f081   lightgbm-frontend98478be58265   lightgbm-backend
thì:
services:  backend:    build: ./backend  frontend:    build: ./frontend
Compose sẽ tự sinh image name theo quy tắc:
<tên_project>-<tên_service>
Ví dụ:
~/workspace/lightgbm
thư mục project là:
lightgbm
service là:
backend:frontend:
=> image được tạo:
lightgbm-backendlightgbm-frontend

Xem tất cả image
docker image ls
hoặc
docker images
Ví dụ:
REPOSITORY          TAG       IMAGE ID       SIZElightgbm-backend    latest    cea53b4c3d2c   1.24GBlightgbm-frontend   latest    09c3989177e1   2.84GBpython              3.10      abc123...

Xem image của container nào
Container:
docker ps -a
Ví dụ:
CONTAINER ID   IMAGE98478be58265   lightgbm-backend
Muốn xem chi tiết:
docker inspect 98478be58265
hoặc:
docker inspect p_lightgbm_backend_container
Trong đó sẽ có:
"Image": "sha256:...."

Muốn tự đặt tên image
Trong compose:
services:  backend:    build: ./backend    image: my-lightgbm-api  frontend:    build: ./frontend    image: my-lightgbm-ui
Build xong:
docker image ls
sẽ thấy:
my-lightgbm-apimy-lightgbm-ui
thay vì:
lightgbm-backendlightgbm-frontend

Xem image đang chiếm dung lượng bao nhiêu
docker image ls
hoặc chi tiết hơn:
docker system df
hoặc:
docker history lightgbm-backend
Ví dụ:
docker history lightgbm-backend
sẽ cho bạn biết layer nào đang chiếm nhiều GB nhất:
IMAGE          CREATED        SIZECOPY . .       300MBpip install    700MBpython:3.10    120MB...
Lệnh này cực kỳ hữu ích khi tối ưu Dockerfile.

Phân biệt nhanh
Nhiều người mới học Docker hay nhầm:
Image = bản cài đặt
Giống như file ISO Windows.
lightgbm-backend
là image.

Container = máy đang chạy
Giống như:
Windows đã cài từ file ISO
Container được tạo từ image.
Image   ↓Container
Một image có thể tạo nhiều container:
lightgbm-backend├── container A├── container B└── container C

Xem tất cả image trên máy
docker image ls -a
Xem tất cả container
docker ps -a
Xem tất cả volume
docker volume ls
Xem tất cả network
docker network ls
Đó là 4 lệnh gần như dùng hằng ngày khi làm Docker.
```
# Remove & Stop (xóa & dừng)
## docker stop
```bash
Dừng container đang chạy
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
## docker volume rm
## docker volume ls
## docker volume inspect smart-recipe_db_data
## docker system prune
```bash
Don rác (rất quan trọng) - Xóa các tài nguyên không dùng
```
**Ex**
```bash
docker system prune -a
```
## docker compose down (dừng và xóa toàn bộ tài nguyên mà Docker Compose đã tạo cho project hiện tại)
```bash
Khi nào nên dùng?
    1. Sau khi sửa Dockerfile
        Ví dụ sửa:
            FROM node:20
            thành
            FROM node:22
            thì nên:
            docker compose downdocker compose up --build
            để build lại sạch.
    2. Khi container bị lỗi lặp lại
        Ví dụ log của bạn:
        p_lightgbm_backend_container exited with code 1 (restarting)
        Có thể thử:
        docker compose downdocker compose up --build
        hoặc
        docker compose down -vdocker compose up --build
        để làm sạch hơn.
```
```bash
Cụ thể, khi chạy: docker compose down
    - Docker sẽ:
        + Stop tất cả containers
        + Xóa containers
        + Xóa network được Docker Compose tạo tự động

Ví dụ:

services:  
    frontend:    ...  
    backend:    ...

Sau khi chạy: docker compose down
Các container như:
    - p_lightgbm_frontend_container
    - p_lightgbm_backend_container
sẽ bị xóa hoàn toàn.
```
**Khác gì với docker compose stop?**
```bash
docker compose stop
    - Chỉ dừng container
    - Container vẫn còn tồn tại
    - Khi chạy lại:
        + docker compose start
        + nó khởi động lại container cũ.

docker compose down
    - Dừng container
    - Xóa container
    - Xóa network
    - Muốn chạy lại phải:
        + docker compose up
        + Docker sẽ tạo container mới.
```