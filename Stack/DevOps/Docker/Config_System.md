- [NVIDIA Container Toolkit (Docker)](#nvidia-container-toolkit-docker)
  - [Installation (cài đặt)](#installation-cài-đặt)
- [docker-compose.yml \& compose.yaml (cấu hình file .yml)](#docker-composeyml--composeyaml-cấu-hình-file-yml)
  - [Những thứ thường có trong docker-compose.yml](#những-thứ-thường-có-trong-docker-composeyml)
    - [Volume (Cho container nhìn thấy thư mục trên máy)](#volume-cho-container-nhìn-thấy-thư-mục-trên-máy)
- [Dockerfile (cấu hình Dockerfile)](#dockerfile-cấu-hình-dockerfile)
- [systemctl is-enabled docker (kiểm tra tại sao bật máy Docker tự chạy?)](#systemctl-is-enabled-docker-kiểm-tra-tại-sao-bật-máy-docker-tự-chạy)
- [.dockerignore](#dockerignore)
---
# NVIDIA Container Toolkit (Docker)
```bash
- Docker là một thế giới cô lập, nó không tự ý "thò tay" ra ngoài máy thật để lấy CUDA Toolkit của bạn được vì lý do bảo mật và đồng 
- Nó không phải là CUDA. Nó là một cái "driver phụ" dành riêng cho Docker. Nhiệm vụ của nó là mở một cái "đường ống" để GPU từ máy thật có thể chui vào trong Docker.
- Khi bạn cài NVIDIA Container Toolkit, bạn sẽ đạt được cảnh giới:
    + Máy thật: Cứ để CUDA 12.8 (hoặc xóa luôn CUDA Toolkit trên máy thật đi cho nhẹ, chỉ giữ lại Driver thôi).
    + Dự án A (Docker): Chạy CUDA 11.8.
    + Dự án B (Docker): Chạy CUDA 10.2.
    => Cả hai chạy cùng lúc trên 1 máy, không thằng nào đụng chạm thằng nào.
```
## Installation (cài đặt)
```bash
1. Thêm nguồn:
    curl -fsSL https://nvidia.github.io/libnvidia-container/gpgkey | sudo gpg --dearmor -o /usr/share/keyrings/nvidia-container-toolkit-keyring.gpg \
  && curl -s -L https://nvidia.github.io/libnvidia-container/stable/deb/nvidia-container-toolkit.list | \
    sed 's#deb https://#deb [signed-by=/usr/share/keyrings/nvidia-container-toolkit-keyring.gpg] https://#g' | \
    sudo tee /etc/apt/sources.list.d/nvidia-container-toolkit.list
2. Cài đặt đường ống:
    sudo apt-get update && sudo apt-get install -y nvidia-container-toolkit
3. Kích hoạt:
    sudo nvidia-container-toolkit runtime configure --runtime=docker
    sudo systemctl restart docker
4. Kiểm tra:
    docker run --rm --gpus all nvidia/cuda:11.8.0-base-ubuntu22.04 nvidia-smi
        + docker run = tạo + chạy container
        + --rm = chạy xong xóa luôn
        + --gpus all = bật GPU
        + image = môi trường CUDA
        + nvidia-smi = lệnh kiểm tra GPU

Output:
thang@PhatToNhuLai:~$ docker run --rm --gpus all nvidia/cuda:11.8.0-base-ubuntu22.04 nvidia-smi
Sun Mar 22 10:45:29 2026       
+-----------------------------------------------------------------------------------------+
| NVIDIA-SMI 570.211.01             Driver Version: 570.211.01     CUDA Version: 12.8     |
|-----------------------------------------+------------------------+----------------------+
| GPU  Name                 Persistence-M | Bus-Id          Disp.A | Volatile Uncorr. ECC |
| Fan  Temp   Perf          Pwr:Usage/Cap |           Memory-Usage | GPU-Util  Compute M. |
|                                         |                        |               MIG M. |
|=========================================+========================+======================|
|   0  NVIDIA GeForce RTX 3050 ...    Off |   00000000:01:00.0 Off |                  N/A |
| N/A   65C    P3             16W /   60W |     343MiB /   4096MiB |     35%      Default |
|                                         |                        |                  N/A |
+-----------------------------------------+------------------------+----------------------+
                                                                                         
+-----------------------------------------------------------------------------------------+
| Processes:                                                                              |
|  GPU   GI   CI              PID   Type   Process name                        GPU Memory |
|        ID   ID                                                               Usage      |
|=========================================================================================|
+-----------------------------------------------------------------------------------------+
thang@PhatToNhuLai:~$ 

```
# docker-compose.yml & compose.yaml (cấu hình file .yml)
```bash
docker-compose.yml (hiện nay thường gọi là compose.yaml) là file dùng để khai báo và chạy nhiều container Docker cùng lúc.

Thay vì phải gõ từng lệnh Docker dài dòng:
  docker run ...
  docker run ...
  docker run ...
Bạn mô tả toàn bộ hệ thống trong một file YAML, sau đó chỉ cần: docker compose up
  Docker sẽ tự tạo và kết nối các container.

Tóm lại:
  - Dockerfile = cách tạo 1 image
  - docker-compose.yml = cách chạy nhiều container/service cùng nhau
Trong đồ án AI/FastAPI/React, file này thường dùng để chạy đồng thời:
  Frontend
  Backend
  Database (PostgreSQL/MySQL)
  Redis (nếu có)
  Nginx (nếu có)
chỉ với một lệnh:
  docker compose up
```
**Ex: Ví dụ đơn giản**
```bash
Giả sử project của bạn có:
  - Frontend React
  - Backend FastAPI
  - Database PostgreSQL

Thì docker-compose.yml có thể như:

services:  
  frontend:    
    build: ./frontend    
    ports:      
      - "3000:3000"  

  backend:    
    build: ./backend    
    ports:      
      - "8000:8000"  
  
  postgres:    
    image: postgres:16    
    environment:      
      POSTGRES_USER: admin      
      POSTGRES_PASSWORD: 123456      
      POSTGRES_DB: mydb

Chạy: docker compose up
  - Docker sẽ tạo 3 container:
    frontend
    backend
    postgres

Nếu không dùng docker-compose thì Bạn phải chạy từng lệnh:
  docker run postgres ...
  docker run backend ...
  docker run frontend ...
Ngoài ra còn phải:
  - tạo network
  - map port
  - mount volume
  - truyền biến môi trường
```
## Những thứ thường có trong docker-compose.yml
```bash
1. Service
  Mỗi service = một container
  services:  backend:

2. Build image
  Build từ Dockerfile
    backend:  build: .
    hoặc
    backend:  build: ./backend

3. Image
  Dùng image có sẵn
  redis:  image: redis:7

4. Port Mapping
  ports:  - "8000:8000"
  nghĩa là:
  máy thật:8000   ↓container:8000

5. Environment Variables
  environment:  DB_HOST: postgres  DB_PORT: 5432
  Trong code:
    os.getenv("DB_HOST")
    sẽ nhận:
    postgres
```
### Volume (Cho container nhìn thấy thư mục trên máy)
```bash
  Để lưu dữ liệu
  volumes:  - postgres_data:/var/lib/postgresql/data
  Nếu container bị xoá thì dữ liệu vẫn còn.

  Ví dụ:
    Máy thật:
      project/
      ├── backend/
      ├── frontend/

    Compose:
      volumes:
        - ./backend:/app

    thì:
      Máy thật                  Container
      ./backend    --->         /app
```
**Syn**
```bash
volumes:
  - host_path:container_path
```
**Ex**
```bash
volumes:
  - ./backend:/app

Ví dụ dataset
backend:
  volumes:
    - ./dataset:/app/dataset

Máy:

dataset/train.csv

Container:

/app/dataset/train.csv
```
```bash
1. restart
2. depends_on
```
**Ví dụ**
```bash
project/
├─ backend/│  
  ├─ main.py│  
  ├─ models/│  
  └─ Dockerfile
├─ frontend/│  
  └─ Dockerfile
└─ docker-compose.yml

File:
services:
  backend:    build: ./backend
    ports:
      - "8000:8000"
  frontend:
    build: ./frontend
    ports:
      - "3000:3000"
Chạy:
  docker compose up --build
  là:
    - Frontend   
    - ↓Backend (FastAPI)
  được chạy cùng lúc.

Các lệnh thường dùng
Khởi động:
  docker compose up
Build lại:
  docker compose up --build
Chạy nền:
  docker compose up -d
Xem log:
  docker compose logs
Dừng:
  docker compose down
Xem container:
  docker compose ps
```
**Syn**
```bash
# Đây là phiên bản của ngôn ngữ Docker Compose.
# Nó giống như việc bạn bảo: "Tôi dùng quy chuẩn xây dựng năm 2024"
version: "3.9"

# Dưới đây là danh sách các "căn hộ" (container) bạn muốn xây. 
# Trong dự án của bạn có 4 căn: ai, db, backend, và frontend.
services:
  ai:
    # Chọn Image có sẵn Python và CUDA (Rất sạch sẽ)
    # thay vì cài Windows hay Ubuntu rồi cài CUDA, bạn bảo Docker: "Lấy cho tôi một cái hộp có sẵn Ubuntu và CUDA 11.8 bên trong"
    build:
        context: ./ai
        dockerfile: Dockerfile

    # Kích hoạt GPU
    # Đây là lệnh "mượn đồ". Bạn bảo Docker: "Này, hãy cho cái hộp này quyền sử dụng 1 cái Card đồ họa NVIDIA trên máy thật của tôi". Nếu thiếu dòng này, code AI sẽ chạy bằng CPU (rất chậm).
    deploy:
      resources:
        reservations:
          devices:
            - driver: nvidia
              count: 1
              capabilities: [gpu]
              
    # Gắn code từ máy thật vào trong Docker
    volumes:
        # Đây là "cái gương". Dấu chấm . là thư mục hiện tại (Smart-Recipe) trên máy thật.
        # /app là thư mục ảo bên trong Docker.
        # Mọi thay đổi bạn gõ code ở máy thật sẽ ngay lập tức hiện ra bên trong Docker
      - .:/app
    # Khi bạn chui vào Docker, nó tự động đưa bạn vào thư mục /app luôn, đỡ phải gõ cd /app
    working_dir: /app
    # Giữ cho cái hộp này luôn mở. Nếu không có nó, Docker thấy không có ai làm gì sẽ tự động đóng hộp lại.
    tty: true
    
  db:
    # Lấy một cái hộp có cài sẵn database MariaDB bản 11.
    image: mariadb:11
    container_name: mariadb_container
    restart: always
    # Đây là các biến môi trường. Thay vì vào database gõ lệnh tạo user/pass, bạn ghi sẵn ở đây, Docker sẽ tự tạo cho bạn lúc khởi động.
    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_DATABASE: SmartRecipe
      MYSQL_USER: ai_user
      MYSQL_PASSWORD: ai123
    # Cổng bên trái là máy thật, bên phải là trong Docker. Bạn mở cổng này để các phần mềm quản lý database (như DBeaver) có thể kết nối vào.
    ports:
      - "3306:3306"
    # Đây là "két sắt". Database rất quan trọng, nếu bạn xóa container mà không có dòng này, dữ liệu sẽ mất sạch. Dòng này giúp giữ dữ liệu lại kể cả khi bạn đập đi xây lại container.
    volumes:
      - db_data:/var/lib/mysql

  backend:
    # Khác với image (lấy đồ có sẵn), build nghĩa là: "Hãy nhìn vào thư mục ./backend, trong đó có file Dockerfile, hãy tự xây cái hộp theo hướng dẫn trong đó cho tôi".
    build: ./backend
    container_name: backend_container
    restart: always
    # Bảo Backend đọc các cấu hình bí mật (như mật khẩu DB) từ file .env mà bạn đã biết cách dùng.
    env_file:
      - ./backend/.env
    ports:
      - "3651:3651"
    # Thứ tự ưu tiên. "Đừng xây Backend nếu Database chưa xây xong".
    depends_on:
      - db

  frontend:
    build: ./frontend
    container_name: frontend_container
    restart: always
    ports:
      - "5173:5173"
    depends_on:
      - backend

# Đây là nơi khai báo cái "két sắt" db_data mà bạn đã dùng ở trên. Docker sẽ tự quản lý một vùng nhớ riêng cho nó.
volumes:
  db_data:
```
# Dockerfile (cấu hình Dockerfile)
```bash
Dockerfile là một file văn bản chứa các chỉ thị (instructions) để Docker tự động tạo ra một Docker image.

Dockerfile dùng để :
  - Tự động tạo môi trường chạy ứng dụng
  - Đóng gói ứng dụng thành image
  - Giúp triển khai (deploy) dễ dàng
    + Chỉ cần:
      docker build -t myapp .
      docker run myapp
  - Là ứng dụng chạy được ngay, không cần cài đặt thủ công.
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
  không phải thư mục trên máy. Là thư mục bên trong container
  
  Ví dụ:
    WORKDIR /app

    Docker tạo:
      (container)
      /app

    Giống như:
      mkdir /app
      cd /app
- COPY      : copy file vào container
- RUN       : CHẠY lệnh khi build
- EXPOSE    : Container này sẽ chạy service ở port 8000.
    + Không mở port ra ngoài máy bạn
    + muốn truy cập được phải chạy docker run -p 8000:8000 image_name
- CMD       : lệnh chạy khi container start
```
# systemctl is-enabled docker (kiểm tra tại sao bật máy Docker tự chạy?)
```bash
Trên Linux thường có service:
  docker.service
  - được bật auto start.

Kiểm tra:
  systemctl is-enabled docker
Nếu ra:
  enabled
thì Docker daemon sẽ tự chạy khi boot máy.

Tắt:
  sudo systemctl disable docker
Dừng ngay:
  sudo systemctl stop docker

Muốn chạy lại:
  sudo systemctl start docker
```
# .dockerignore
```bash
Giống .gitignore
```