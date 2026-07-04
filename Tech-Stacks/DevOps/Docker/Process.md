- [docker compose](#docker-compose)
  - [Create \& Config (tạo \& cấu hình)](#create--config-tạo--cấu-hình)
    - [docker compose up (chạy file yaml)](#docker-compose-up-chạy-file-yaml)
      - [--build](#--build)
      - [-d (detached mode, chạy nền không chiếm terminal)](#-d-detached-mode-chạy-nền-không-chiếm-terminal)
  - [Remove (xóa \& dừng)](#remove-xóa--dừng)
    - [docker compose down (dừng và xóa toàn bộ tài nguyên mà Docker Compose đã tạo cho project hiện tại)](#docker-compose-down-dừng-và-xóa-toàn-bộ-tài-nguyên-mà-docker-compose-đã-tạo-cho-project-hiện-tại)
      - [--rmi](#--rmi)
- [docker build (Dùng để tạo Docker image từ Dockerfile)](#docker-build-dùng-để-tạo-docker-image-từ-dockerfile)
  - [--no-cache](#--no-cache)
  - [docker run (Tạo và chạy một container mới)](#docker-run-tạo-và-chạy-một-container-mới)
  - [docker exec (Chạy thêm một command bên trong container đang chạy)](#docker-exec-chạy-thêm-một-command-bên-trong-container-đang-chạy)
- [docker start (Mở lại một container khi đã stop)](#docker-start-mở-lại-một-container-khi-đã-stop)
- [Display (cung cấp thông tin)](#display-cung-cấp-thông-tin)
  - [docker ps](#docker-ps)
  - [docker images \& docker image ls (Xem tất cả image)](#docker-images--docker-image-ls-xem-tất-cả-image)
    - [-a (Xem tất cả image trên máy)](#-a-xem-tất-cả-image-trên-máy)
- [Remove \& Stop (xóa \& dừng)](#remove--stop-xóa--dừng)
  - [docker stop ... (Dừng container đang chạy)](#docker-stop--dừng-container-đang-chạy)
  - [docker rm](#docker-rm)
  - [docker volume rm](#docker-volume-rm)
  - [docker volume ls](#docker-volume-ls)
  - [docker volume inspect smart-recipe\_db\_data](#docker-volume-inspect-smart-recipe_db_data)
- [Resource (Quản lý tài nguyên)](#resource-quản-lý-tài-nguyên)
  - [docker system df (Xem docker chiếm bao nhiêu dung lượng)](#docker-system-df-xem-docker-chiếm-bao-nhiêu-dung-lượng)
    - [docker system df -v](#docker-system-df--v)
  - [docker system prune (Xóa các tài nguyên không dùng)](#docker-system-prune-xóa-các-tài-nguyên-không-dùng)
    - [-a | --all (xóa sạch sành sanh tài nguyên Docker tạp ra)](#-a----all-xóa-sạch-sành-sanh-tài-nguyên-docker-tạp-ra)
---
# docker compose
## Create & Config (tạo & cấu hình)
### docker compose up (chạy file yaml)
```bash
Docker Compose là công cụ của Docker để chạy nhiều container cùng lúc theo một file cấu hình YAML.

docker compose up dùng để:
    1. Build image (nếu chưa có)
    2. Tạo container từ file docker-compose.yml
    3. Tạo network nội bộ giữa các service
    4. Khởi động tất cả service cùng lúc
```
**Syn**
```bash
docker compose up [OPTIONS] [SERVICE...]

- OPTIONS:  
    
    + --build # build lại image trước khi chạy. Dùng khi bạn vừa sửa Dockerfile hoặc code.
- SERVICE:
    + docker compose up backend # Chỉ khởi động service tên backend.
    + docker compose down
        - Stop container
        - Xóa container
        - Xóa network
```
#### --build
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
#### -d (detached mode, chạy nền không chiếm terminal)
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
## Remove (xóa & dừng)
### docker compose down (dừng và xóa toàn bộ tài nguyên mà Docker Compose đã tạo cho project hiện tại)
```bash
khi chạy: docker compose down
    Docker sẽ:
        + Stop tất cả containers
        + Xóa containers
        + Xóa network được Docker Compose tạo tự động
    
    docker compose down chỉ xóa những container, network mà file docker-compose.yml (hoặc compose.yaml) của project đó tạo ra, chứ không xóa toàn bộ container trên máy.
        Ví dụ:
            project-a/
            ├── docker-compose.yml

            project-b/
            ├── docker-compose.yml

        Nếu bạn đang ở project-a và chạy: docker compose down
            thì Docker sẽ:
                ✅ Dừng và xóa các container của project-a
                ✅ Xóa network mà Compose tạo cho project-a
                ❌ Không đụng đến container của project-b
                ❌ Không đụng đến các container bạn tạo bằng docker run
                ❌ Không xóa image mặc định

Ví dụ:
    services:  
        frontend:    ...  
        backend:    ...

    Sau khi chạy: docker compose down

    Các container như:
        - p_lightgbm_frontend_container
        - p_lightgbm_backend_container
    => sẽ bị xóa hoàn toàn.
```
**Khi nào nên dùng?**
```bash
1. Sau khi sửa Dockerfile
    Ví dụ sửa:
        "FROM node:20" thành "FROM node:22"
        
        thì nên:
            1. docker compose down
            2. docker compose up --build
        để build lại sạch.
2. Khi container bị lỗi lặp lại
    Ví dụ log của bạn:
        p_lightgbm_backend_container exited with code 1 (restarting)
        
        Có thể thử:
            1. docker compose down
            2. docker compose up --build
        hoặc
            1. docker compose down -v
            2. docker compose up --build
        để làm sạch hơn.
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
#### --rmi
```bash
Nếu bạn chỉ muốn dọn dẹp duy nhất 1 dự án mà không làm ảnh hưởng đến dự án còn lại, hãy dùng lệnh sau ngay tại thư mục của dự án đó:
```
```bash
docker compose down --rmi all

# Lệnh này sẽ dừng container, xóa mạng, và chỉ xóa các Image được định nghĩa trong file compose.yaml của chính dự án đó. Dự án còn lại của bạn sẽ hoàn toàn bình an vô sự!
```
# docker build (Dùng để tạo Docker image từ Dockerfile)
```bash
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
## --no-cache
**Ex: khi không dùng --no-cache**
```bash
COPY requirements.txt .
RUN pip install -r requirements.txt
COPY . .

Lần build đầu:
    Step 1 chạy
    Step 2 chạy
    Step 3 chạy

Lần sau:
    requirements.txt không đổi
Docker dùng cache:
    Step 1 CACHE
    Step 2 CACHE
    Step 3 chạy
rất nhanh.
```
**Tại sao dùng --no-cache?**
```bash
Nếu dùng:
    docker compose build --no-cache backend

    Docker bỏ toàn bộ cache:
        Step 1 chạy lại
        Step 2 chạy lại
        Step 3 chạy lại

Dùng khi:
    - cache bị lỗi
    - dependency bị lỗi
    - nghi ngờ Docker đang dùng layer cũ
    - Không nên dùng thường xuyên vì rất chậm.
```
## docker run (Tạo và chạy một container mới)
```bash
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
- bash → lệnh chạy khi container khởi động
```
**Ex2**
```bash
docker run -d -p 8080:80 nginx

- 8080: là port máy bạn
- 80: là port trong container
```
## docker exec (Chạy thêm một command bên trong container đang chạy)
```bash
Hiểu đơn giản:
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
# docker start (Mở lại một container khi đã stop)
**Syn**
```bash
docker start id | nanme
```
**Ex**
```bash
CONTAINER ID   IMAGE          NAMES
a1b2c3d4e5f6   postgres:16     postgres_db
f6e5d4c3b2a1   redis:7         redis_cache

Dùng ID:
    - docker start a1b2c3d4e5f6
    - docker start f6e5d4c3b2a1

Hoặc dùng tên (thường dễ nhớ hơn):
    - docker start postgres_db
    - docker start redis_cache

Hoặc khởi động nhiều container cùng lúc:
    docker start postgres_db redis_cache
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
## docker images & docker image ls (Xem tất cả image)
```bash
Docker Compose tự đặt tên image cho bạn nếu bạn không chỉ định. Compose sẽ tự sinh image name theo quy tắc:
    <tên_project>-<tên_service>
    
    Ví dụ:
        ~/workspace/lightgbm
        
        thư mục project là: lightgbm
            service là: 
                - backend:
                - frontend:
            => image được tạo:
                - lightgbm-backend
                - lightgbm-frontend
```
**Ex**
```bash
docker image ls hoặc docker images

REPOSITORY          TAG       IMAGE ID       SIZE
lightgbm-backend    latest    cea53b4c3d2c   1.24GB
lightgbm-frontend   latest    09c3989177e1   2.84GB
python              3.10      abc123...
```
### -a (Xem tất cả image trên máy)
**Syn**
```bash
docker image ls -a
```
# Remove & Stop (xóa & dừng)
## docker stop ... (Dừng container đang chạy)
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
# Resource (Quản lý tài nguyên)
## docker system df (Xem docker chiếm bao nhiêu dung lượng)
**Ex**
```bash
(sr) thang@PhatToNhuLai:~/workspace/Smart-Recipe$ docker system df

# TYPE            TOTAL     ACTIVE    SIZE      RECLAIMABLE
# Images          22        4         56.19GB   47.11GB (83%)
# Containers      4         0         3.732GB   3.732GB (100%)
# Local Volumes   2         2         395.2MB   0B (0%)
# Build Cache     81        0         33.38GB   1.051GB
```
### docker system df -v
## docker system prune (Xóa các tài nguyên không dùng)
### -a | --all (xóa sạch sành sanh tài nguyên Docker tạp ra)
**Syn**
```bash
docker system prune -a

Docker sẽ tiến hành một cuộc "tổng vệ sinh" và xóa bỏ toàn bộ:
    - All stopped containers: Tất cả các container đã bị dừng (stop). Do bạn đã stop cả 2 dự án, toàn bộ container của chúng sẽ bị xóa bỏ.
    - All networks not used...: Tất cả các mạng nội bộ do Docker Compose tạo ra mà không có container nào đang dùng.
    - All build cache: Bộ nhớ đệm lúc bạn chạy lệnh RUN trước đó để build image (lần sau build lại sẽ chậm hơn).
    - All images without at least one container associated with them: Đây chính là lý do vì sao 2 dự án của bạn bị bay màu Image. Khi bạn đã stop và xóa sạch container ở trên, các Docker Image của 2 dự án lúc này trở thành "vô gia cư" (không có container nào đang chạy dựa trên chúng). Docker sẽ coi chúng là đồ dư thừa và xóa sạch.
```