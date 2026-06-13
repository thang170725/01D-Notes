- [Directory Structure](#directory-structure)
- [Introduction](#introduction)
- [Installation](#installation)
- [Component (Thành phần)](#component-thành-phần)
  - [Docker Engine](#docker-engine)
    - [Docker Client (CLI)](#docker-client-cli)
    - [Docker Daemon (dockerd) (bộ não điều khiển của Docker)](#docker-daemon-dockerd-bộ-não-điều-khiển-của-docker)
  - [Image (Một “khuôn mẫu” để tạo container)](#image-một-khuôn-mẫu-để-tạo-container)
  - [Container (Image + đang chạy → Giống như process)](#container-image--đang-chạy--giống-như-process)
  - [Dockerfile (file mô tả cách build image)](#dockerfile-file-mô-tả-cách-build-image)
  - [Docker Registry (Nơi lưu images)](#docker-registry-nơi-lưu-images)
  - [Volume](#volume)
  - [Network](#network)
---
# Directory Structure
```bash
Docker/             # mình dùng thư mục này để xem kiến thức về Docker
├── Base.md         # mình dùng file này để xem kiến thức và tiện ích
├── Practices.md    # mình dùng file này để xem lệnh mẫu và bài tập
└── Process.md      # mình dùng file này để thao tác với docker
```
# Introduction
```bash
Giả sử em viết một app:
- Trước khi có Docker.
    + Máy em chạy được 
    + Lên máy người khác → lỗi 
    + Lên server → thiếu lib, sai version 
    + Nguyên nhân: mỗi máy có môi trường khác nhau
- Docker cho phép:
    + Đóng gói app + môi trường + thư viện + cấu hình
    + Thành một gói duy nhất gọi là container
    + Chạy giống hệt nhau ở mọi nơi
```
# Installation
```bash
1. gỡ bản docker cũ nếu có
    1. sudo apt remove docker docker-engine docker.io containerd runc   
2. cập nhật hệ thống & cài tool cần thiết
    1. sudo apt update
    2. sudo apt install -y ca-certificates curl gnupg
3. thêm docker GPG key
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | \
sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg
4. thêm docker repository
echo \
"deb [arch=$(dpkg --print-architecture) \
signed-by=/etc/apt/keyrings/docker.gpg] \
https://download.docker.com/linux/ubuntu \
$(lsb_release -cs) stable" | \
sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
5. cài docker engine
    1. sudo apt update
    2. sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
6. kiểm tra docker đã chạy chưa
    1. sudo docker version
    2. docker --version
7. test container đầu tiên
    1. sudo docker run hello-world
```
# Component (Thành phần)
## Docker Engine
```bash
- Bao gồm:
    + Docker Client + Docker Daemon + REST API
    + Đây là platform hoàn chỉnh
```
### Docker Client (CLI)
```bash
Client không chạy container trực tiếp mà nó gửi request tới Docker Daemon 
```
### Docker Daemon (dockerd) (bộ não điều khiển của Docker)
```bash
- Đây là process chạy nền
- Nhiệm vụ:
    + build image
    + start/stop container
    + quản lý network
    + quản lý volume
```
## Image (Một “khuôn mẫu” để tạo container)
```bash
Không chạy, chỉ là file

Image chứa:
    - OS filesystem
    - libraries
    - app code
    - dependencies
```
## Container (Image + đang chạy → Giống như process)
```bash
Ví dụ: 
    - Image giống Class
    - Container gống Object
```
## Dockerfile (file mô tả cách build image)
**Ex**
```bash
FROM python:3.11

WORKDIR /app

COPY . .

RUN pip install -r requirements.txt

CMD ["python", "main.py"]
```
## Docker Registry (Nơi lưu images)
```bash
Ví dụ:
    - Docker Hub
    - Github Container Registry
    - AWS ECR
```
## Volume
## Network