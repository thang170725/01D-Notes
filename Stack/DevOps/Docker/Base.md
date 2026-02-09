- [Directory Structure](#directory-structure)
- [Introduction Docker](#introduction-docker)
  - [Image](#image)
  - [Container](#container)
  - [Docker Engine](#docker-engine)
- [Installation](#installation)
---
# Directory Structure
```bash
Docker/
├── 01_Fundamentals_CLI.md    # Khái niệm & Lệnh: image, container, ps, rm, logs
├── 02_Dockerfile_Mastery.md  # Xây dựng Image: FROM, RUN, COPY, CMD vs ENTRYPOINT
├── 03_Storage_Volumes.md     # Dữ liệu: Bind Mounts, Named Volumes (Giữ data khi xóa container)
├── 04_Networking.md          # Kết nối: Bridge, Host, Docker Network (Cách các container gọi nhau)
├── 05_Docker_Compose.md      # Đa dịch vụ: Cấu hình file yaml, build, up, down
└── 06_Optimization_Security.md # Nâng cao: Multi-stage build, .dockerignore, quét lỗ hổng
```
# Introduction Docker
```bash
Giả sử em viết một app:
- Trước khi có Docker.
    + Máy em chạy được ✅
    + Lên máy người khác → lỗi ❌
    + Lên server → thiếu lib, sai version ❌
    + “Máy em chạy mà 😭”
    + 👉 Nguyên nhân: mỗi máy có môi trường khác nhau
- Docker giải quyết thế nào? Docker cho phép:
    + Đóng gói app + môi trường + thư viện + cấu hình
    + Thành một gói duy nhất gọi là container
    + Chạy giống hệt nhau ở mọi nơi
```
## Image
```bash
→ Một “khuôn mẫu” để tạo container
→ Không chạy, chỉ là file
```
## Container
```bash
→ Image + đang chạy
→ Giống như process
```
## Docker Engine
```bash
→ Phần mềm chạy container
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