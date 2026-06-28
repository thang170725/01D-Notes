- [CI/CD (cách tự động hóa việc test + build + deploy code mỗi khi bạn push code lên Git)](#cicd-cách-tự-động-hóa-việc-test--build--deploy-code-mỗi-khi-bạn-push-code-lên-git)
---
# CI/CD (cách tự động hóa việc test + build + deploy code mỗi khi bạn push code lên Git)
```bash
CI – Continuous Integration (Tích hợp liên tục)
   👉 Lập trình viên code xong là đẩy lên repo (Git) → hệ thống tự động làm tiếp.

   CI thường sẽ:
      ✅ Build code
      ✅ Chạy test tự động (unit test, lint…)
      ✅ Kiểm tra lỗi sớm

   🎯 Mục tiêu:
      - Phát hiện bug càng sớm càng tốt
      - Tránh cảnh “code chạy máy anh, không chạy máy em”

   Ví dụ:
      Mỗi lần bạn git push, GitHub Actions/Jenkins tự động chạy test.

CD – Continuous Delivery / Continuous Deployment
   - Continuous Delivery: 
      + Code luôn sẵn sàng để deploy
      + Deploy lên production có thể cần bấm nút xác nhận
   - Continuous Deployment: 
      + Code pass hết test → tự động deploy thẳng lên production
      + Không cần con người can thiệp

   🎯 Mục tiêu:
      - Ra feature nhanh
      - Giảm lỗi khi deploy thủ công
```
**Công cụ CI/CD phổ biến**
```bash
🔧 GitHub Actions
🔧 GitLab CI/CD
🔧 Jenkins
🔧 CircleCI
🔧 Azure DevOps
```
**Vì sao CI/CD quan trọng?**
```bash
🚀 Deploy nhanh, đều, ít lỗi
🧪 Test tự động → code chất lượng hơn
👥 Team làm việc mượt hơn
😌 Đỡ stress mỗi lần release
```
**CI/CD hoạt động như thế nào? (Luồng cơ bản)**
```bash
Dev push code
   ↓
CI: build + test
   ↓
CD: deploy (staging / production)
```
**CI/CD trong Python**
```bash
✔ 1. Chạy test tự động
   Ví dụ:
      - pytest
      - unittest

✔ 2. Kiểm tra code style
   - flake8
   - black
   - isort

✔ 3. Build package
   - pip package
   - wheel (.whl)

✔ 4. Deploy app
   - FastAPI / Flask → server
   - Docker → production
   - AWS / VPS / Kubernetes
```
**🧠 Kiến trúc CI/CD production chuẩn**
```bash
GitHub
  ↓ (push / pull request)
GitHub Actions (CI)
  - test
  - lint
  - build Docker image
  ↓ (main branch)
Docker Registry (GHCR / Docker Hub)
  ↓
Server (VPS / EC2)
  - pull image
  - restart container
📦 Stack mình setup mẫu
Python 3.11
FastAPI (hoặc Flask đều tương tự)
Docker
GitHub Actions (CI/CD)
VPS (Ubuntu)
Nginx (reverse proxy)
🏗 1. Project structure chuẩn
app/
  main.py
  routes/
  services/
tests/
  test_main.py
Dockerfile
docker-compose.yml
requirements.txt
.github/workflows/cicd.yml
🧪 2. Python app sample (FastAPI)
# app/main.py
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def home():
    return {"status": "ok"}
🧪 3. Test (CI bắt buộc phải có)
# tests/test_main.py
from fastapi.testclient import TestClient
from app.main import app

client = TestClient(app)

def test_home():
    res = client.get("/")
    assert res.status_code == 200
    assert res.json()["status"] == "ok"
📦 4. requirements.txt
fastapi
uvicorn
pytest
httpx
🐳 5. Dockerfile (production-ready)
FROM python:3.11-slim

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

EXPOSE 8000

CMD ["uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "8000"]
🧱 6. docker-compose (server chạy ổn định)
version: "3.9"

services:
  app:
    build: .
    container_name: python_app
    ports:
      - "8000:8000"
    restart: always
⚙️ 7. CI/CD GitHub Actions (quan trọng nhất)
# .github/workflows/cicd.yml

name: CI/CD Pipeline

on:
  push:
    branches: ["main"]

jobs:
  test-build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Setup Python
        uses: actions/setup-python@v5
        with:
          python-version: "3.11"

      - name: Install dependencies
        run: |
          pip install -r requirements.txt
          pip install pytest

      - name: Run tests
        run: pytest

      - name: Build Docker image
        run: |
          docker build -t my-python-app:latest .
🚀 8. Deploy stage (SSH VPS)

Thêm job deploy:

  deploy:
    needs: test-build
    runs-on: ubuntu-latest

    steps:
      - name: Deploy to VPS via SSH
        uses: appleboy/ssh-action@v1.0.3
        with:
          host: ${{ secrets.VPS_HOST }}
          username: ${{ secrets.VPS_USER }}
          key: ${{ secrets.VPS_SSH_KEY }}
          script: |
            cd /var/www/myapp

            git pull origin main

            docker-compose down
            docker-compose up -d --build
🔐 9. GitHub Secrets cần setup

Trong GitHub repo:

VPS_HOST = IP server
VPS_USER = ubuntu
VPS_SSH_KEY = private key SSH
🖥 10. Setup VPS (Ubuntu)
Cài Docker
sudo apt update
sudo apt install docker.io docker-compose -y
sudo systemctl enable docker
Clone project
cd /var/www
git clone https://github.com/your-repo/myapp.git
cd myapp
Run lần đầu
docker-compose up -d --build
🌐 11. Nginx (production reverse proxy)
server {
    listen 80;
    server_name your-domain.com;

    location / {
        proxy_pass http://localhost:8000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}
🔁 Flow hoàn chỉnh
Dev push code
   ↓
GitHub Actions chạy CI:
   - install deps
   - run tests
   - build Docker
   ↓
Nếu OK:
   ↓
SSH VPS
   ↓
pull code
   ↓
docker-compose restart
   ↓
Production updated 🚀
⚡ Best practices (rất quan trọng)
1. Không deploy nếu test fail

→ luôn dùng needs: test-build

2. Luôn dùng Docker

→ tránh “works on my machine”

3. Tách dev / prod config
.env.dev
.env.prod
4. Không chạy app trực tiếp bằng python

❌ python main.py
✅ uvicorn + docker

5. Restart tự động
restart: always
🔥 Nâng cấp nếu bạn muốn (level production thật)

Mình có thể hướng dẫn tiếp:

1. Blue-Green deployment (zero downtime)
2. CI/CD với Docker Registry (GHCR)
3. Kubernetes deploy (HPA, autoscale)
4. Redis + Celery pipeline CI/CD
5. ML CI/CD (train → validate → deploy model)

Nếu bạn muốn đi “level thực chiến công ty”, nói:
👉 “
setup CI/CD zero downtime + Docker registry”
```