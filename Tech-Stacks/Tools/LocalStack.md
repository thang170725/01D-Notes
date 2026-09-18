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
Ví dụ:

docker run --rm -it \
  -p 4566:4566 \
  localstack/localstack

Sau đó các AWS service của LocalStack thường được truy cập qua:

http://localhost:4566

Ví dụ cấu hình boto3:

import boto3

s3 = boto3.client(
    "s3",
    endpoint_url="http://localhost:4566",
    region_name="ap-southeast-1",
    aws_access_key_id="test",
    aws_secret_access_key="test",
)
LocalStack khác Docker như thế nào?

Đây là điểm dễ nhầm:

Công cụ	Vai trò
Docker	Chạy container
LocalStack	Giả lập AWS services
AWS	Cloud thật

Nói đơn giản:

Docker là cách chạy LocalStack; LocalStack là AWS giả lập để development.

Ví dụ project của bạn có thể có:

email_automation_project/
│
├── backend/
├── frontend/
├── docker-compose.yml
└── .env

và docker-compose.yml chạy:

Backend
Database
Redis
LocalStack

để toàn bộ hệ thống có thể chạy trên máy local, gần giống môi trường production nhưng không cần phụ thuộc AWS thật.

Nếu bạn đang thấy localstack trong Docker Compose / .env / code Python của project, gửi đoạn đó cho tôi, tôi có thể giải thích chính xác LocalStack đang được dùng để giả lập service AWS nào và luồng request chạy như thế nào.