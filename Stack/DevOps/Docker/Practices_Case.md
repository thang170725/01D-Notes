    • Docker tạo container (tức gói ứng dụng cùng môi trường (code, thư viện, runtime) vào một đơn vị nhẹ, có thể chạy trên bất kỳ máy nào có Docker. Container nhẹ hơn máy ảo, khởi động nhanh và dễ tái tạo môi trường.
    • Tại sao dùng: tránh “works on my machine”, dễ đóng gói app + dependency, deploy, test, chia sẻ với đồng đội, CI/CD, scale.
    • Rất phổ biến trong devops, backend, data science, ML engineering. Công ty/startup đều dùng rộng rãi. Với intern AI / trình độ hiện tại: RẤT NÊN học. Kiến thức cơ bản Docker giúp bạn:
    • Chạy service phức tạp (MQTT, DB, backend, frontend) trên máy dev chỉ bằng vài lệnh.
    • Đóng gói model/serving để deploy. Giảm thời gian setup môi trường khi chia sẻ project với bạn bè/đồng nghiệp.
Cách cài đặt
Ubuntu:
# 1. Cập nhật và cài phụ thuộc
sudo apt update
sudo apt install -y ca-certificates curl gnupg lsb-release

# 2. Thêm khoá GPG của Docker
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

# 3. Thêm repository chính thức (Ubuntu 24.04 -> 'lunar' hoặc apt will auto-resolve; chung cấu hình)
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] \
  https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" \
  | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# 4. Cập nhật và cài Docker Engine + CLI + containerd + compose plugin
sudo apt update
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

# 5. Kích hoạt và khởi động docker
sudo systemctl enable --now docker

# 6. (Tùy chọn) cho phép user hiện tại chạy docker không cần sudo
sudo usermod -aG docker $USER

# Đăng xuất / đăng nhập lại hoặc chạy `newgrp docker` để thay đổi nhóm có hiệu lực.
newgrp docker
```text
tạo DockerFile và chạy thử Docker container
```



# 2. Tạo thư mục dự án
Tạo một thư mục mới, ví dụ mydockerapp:
```bash
mkdir mydockerapp
cd mydockerapp
```

# 3. Tạo file Python đơn giản
Tạo app.py:
```python
# app.py
print("Hello from Docker!")
```

# 4. Tạo Dockerfile
Tạo một file tên Dockerfile (không có đuôi):
```Dockerfile
# Dockerfile
# Sử dụng image Python chính thức
FROM python:3.12-slim

# Thiết lập thư mục làm việc trong container
WORKDIR /app

# Copy file Python vào container
COPY app.py .

# Lệnh để chạy khi container start
CMD ["python", "app.py"]

Giải thích nhanh:

FROM python:3.12-slim → dùng image Python 3.12 nhẹ.

WORKDIR /app → thư mục làm việc trong container.

COPY app.py . → copy file app.py vào container.

CMD ["python", "app.py"] → chạy lệnh khi container khởi động.
```

# 5. Build Docker image
Chạy lệnh này trong thư mục chứa Dockerfile:

docker build -t mypythonapp .


-t mypythonapp → đặt tên cho image là mypythonapp.

. → Dockerfile ở thư mục hiện tại.

Docker sẽ đọc Dockerfile và tạo image.

# 6. Chạy Docker container
docker run --name testapp mypythonapp


Kết quả bạn sẽ thấy:

Hello from Docker!


Nếu muốn container chạy trong background:

docker run -d --name testapp mypythonapp


-d → detached mode (chạy ngầm).

# 7. Kiểm tra container
docker ps -a   # liệt kê tất cả container
docker logs testapp  # xem log của container

# 8. Xóa container & image
docker stop testapp
docker rm testapp
docker rmi mypythonapp