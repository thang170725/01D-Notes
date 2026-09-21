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
**1: Kiểm tra Docker**
```bash
1. docker --version
2. docker compose version

Nếu chưa có Docker, cài:
    1. sudo apt update
    2. sudo apt install -y docker.io docker-compose-v2
    3. sudo usermod -aG docker $USER # Cho user hiện tại dùng Docker không cần sudo
    4. newgrp docker # Sau đó logout/login lại hoặc chạy

Kiểm tra:
1. docker run hello-world
```
**2: Cài LocalStack CLI**
```bash
1. 
docker run --rm -it \
  -p 4566:4566 \
  -e SERVICES=s3,sqs,dynamodb,lambda \
  localstack/localstack:4.3.0

2. Mở terminal thứ 2 và chạy: curl http://localhost:4566/_localstack/health
```