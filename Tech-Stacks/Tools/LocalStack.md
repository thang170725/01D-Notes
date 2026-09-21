+ [<<Back](Base.md)
- [LocalStack Introduction (là một môi trường giả lập AWS chạy ngay trên máy local của bạn)](#localstack-introduction-là-một-môi-trường-giả-lập-aws-chạy-ngay-trên-máy-local-của-bạn)
- [Installation](#installation)
  - [Linux](#linux)
---
# LocalStack Introduction (là một môi trường giả lập AWS chạy ngay trên máy local của bạn)
```bash
Thay vì ứng dụng của bạn phải kết nối tới AWS thật:
    Backend -> AWS thật (S3 / SQS / Lambda / DynamoDB / ...)

thì khi dùng LocalStack:
    Backend -> LocalStack (S3, SQS, Lambda, DynamoDB, SNS, ...)

Nó đặc biệt hữu ích khi development và testing, vì bạn có thể sử dụng nhiều dịch vụ AWS mà không cần tạo tài nguyên thật trên AWS.
```
**Ex**
```bash
Giả sử backend Python của bạn upload file lên S3.
    Bình thường: Nếu cấu hình AWS thật → file được upload lên S3 thật, có thể phát sinh chi phí và ảnh hưởng dữ liệu thật.

    Với LocalStack, bạn có thể cấu hình: Python Backend -> localhost:4566 -> LocalStack -> Fake S3 (Bạn vẫn dùng SDK như boto3, nhưng request được gửi tới LocalStack thay vì AWS)

LocalStack thường chạy bằng Docker
```
# Installation
## Linux
**1:Kiểm tra Docker**
```bash
docker --version
docker compose version

Nếu chưa có Docker, cài:
sudo apt update
sudo apt install -y docker.io docker-compose-v2

Cho user hiện tại dùng Docker không cần sudo:
sudo usermod -aG docker $USER

Sau đó logout/login lại hoặc chạy:

newgrp docker

Kiểm tra:

docker run hello-world
```
**2: Cài LocalStack CLI**
```bash
1. curl -Lo localstack-cli-4.11.1-linux-amd64-onefile.tar.gz \ 
https://github.com/localstack/localstack-cli/releases/download/v4.11.1/localstack-cli-4.11.1-linux-amd64-onefile.tar.gz

2. Giải nén: sudo tar xvzf localstack-cli-4.11.1-linux-amd64-onefile.tar.gz -C /usr/local/bin

3. Kiểm tra: localstack --version

4. Khởi động LocalStack: localstack start -d

5. Kiểm tra: localstack status

6. Test nhanh AWS API
curl http://localhost:4566/_localstack/health

Bạn sẽ nhận được JSON chứa trạng thái các AWS services.