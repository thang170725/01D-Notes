- [aws s3](#aws-s3)
  - [aws s3 ls (các đơn giản để liệt kê bucket)](#aws-s3-ls-các-đơn-giản-để-liệt-kê-bucket)
- [aws s3api (nhóm lệnh AWS CLI dùng để gọi trực tiếp các API của Amazon S3)](#aws-s3api-nhóm-lệnh-aws-cli-dùng-để-gọi-trực-tiếp-các-api-của-amazon-s3)
  - [Ask](#ask)
    - [s3 và s3api khác nhau thế nào?](#s3-và-s3api-khác-nhau-thế-nào)
  - [aws s3api list-buckets (Liệt kê tất cả bucket hiện đang tồn tại)](#aws-s3api-list-buckets-liệt-kê-tất-cả-bucket-hiện-đang-tồn-tại)
  - [aws s3api delete-buckets (xóa bucket khỏi S3)](#aws-s3api-delete-buckets-xóa-bucket-khỏi-s3)
  - [create-bucket (Tạo bucket)](#create-bucket-tạo-bucket)
  - [list-buckets (Liệt kê bucket)](#list-buckets-liệt-kê-bucket)
  - [head-bucket (Kiểm tra bucket)](#head-bucket-kiểm-tra-bucket)
  - [get-bucket-location (Xem region của bucket)](#get-bucket-location-xem-region-của-bucket)
  - [put-object (Upload object)](#put-object-upload-object)
  - [get-object (Download object)](#get-object-download-object)
  - [delete-object (Xóa object)](#delete-object-xóa-object)
  - [list-objects-v2 (Liệt kê object)](#list-objects-v2-liệt-kê-object)
  - [head-object (Xem metadata của object)](#head-object-xem-metadata-của-object)
  - [get-bucket-policy (Lấy bucket policy)](#get-bucket-policy-lấy-bucket-policy)
  - [put-bucket-policy (Thiết lập bucket policy)](#put-bucket-policy-thiết-lập-bucket-policy)
- [aws sqs (Tạo một SQS queue)](#aws-sqs-tạo-một-sqs-queue)
- [aws dynamodb](#aws-dynamodb)
- [aws lambda](#aws-lambda)
- [aws ec2](#aws-ec2)
---
# aws s3
Xóa object và bucket
6.1. Xóa file trên S3
aws --endpoint-url=http://localhost:4566 \
    s3 rm s3://my-first-bucket/hello.txt

Kiểm tra:

aws --endpoint-url=http://localhost:4566 \
    s3 ls s3://my-first-bucket/

Không còn hello.txt là đúng.

6.2. Xóa bucket
aws --endpoint-url=http://localhost:4566 \
    s3 rb s3://my-first-bucket
6.3. Kiểm tra
aws --endpoint-url=http://localhost:4566 s3 ls

Không còn bucket là đúng.

Làm xong → next step.
Download file từ S3

Bây giờ luyện chiều ngược lại.

5.1. Xóa file local
rm hello.txt

Kiểm tra:

ls hello.txt

Phải báo:

No such file or directory
5.2. Download từ S3
aws --endpoint-url=http://localhost:4566 \
    s3 cp s3://my-first-bucket/hello.txt .
5.3. Kiểm tra
cat hello.txt

Kết quả:

Hello LocalStack S3

👉 Đây chính là thao tác tương đương khi làm việc với S3 thật.

Làm xong nói next step.
## aws s3 ls (các đơn giản để liệt kê bucket)
# aws s3api (nhóm lệnh AWS CLI dùng để gọi trực tiếp các API của Amazon S3)
**Kiến thức cần học trước**
[Bucket trong AWS](../../Domains/Cloud/AWS.md#bucket-thùng-chứa-để-lưu-trữ-dữ-liệu)
```bash
Có thể hiểu đơn giản: aws s3 -> Các lệnh đơn giản, dễ dùng -> aws s3api -> Các API S3 chi tiết, nhiều tùy chọn hơn
```
**Syn**
```bash
aws [options] s3api [API-command] [parameters]
```
## Ask
### s3 và s3api khác nhau thế nào?

Ví dụ bạn muốn liệt kê bucket.

Cách 1: s3
aws --endpoint-url=http://localhost:4566 s3 ls

Kết quả có thể là:

2026-09-21 12:30:10 my-first-bucket
2026-09-21 12:31:20 api-bucket

Đây là cách ngắn và dễ sử dụng.

Cách 2: s3api
aws --endpoint-url=http://localhost:4566 \
    s3api list-buckets

Kết quả:

{
    "Buckets": [
        {
            "Name": "my-first-bucket",
            "CreationDate": "2026-09-21T05:30:10+00:00"
        },
        {
            "Name": "api-bucket",
            "CreationDate": "2026-09-21T05:31:20+00:00"
        }
    ],
    "Owner": {
        "DisplayName": "webfile",
        "ID": "..."
    }
}

S3 API trả về JSON chứa nhiều thông tin chi tiết hơn.
## aws s3api list-buckets (Liệt kê tất cả bucket hiện đang tồn tại)
```bash
Nó gọi trực tiếp API ListBuckets của S3
```
Kiểm tra bucket đã bị xóa chưa

Đây chính là lệnh bạn đưa:

aws --endpoint-url=http://localhost:4566 \
    s3api list-buckets

Nó có nghĩa:

Liệt kê tất cả bucket hiện đang tồn tại.

Ví dụ trước khi xóa:

{
    "Buckets": [
        {
            "Name": "my-first-bucket"
        },
        {
            "Name": "api-bucket"
        }
    ]
}

Sau khi:

delete-bucket --bucket api-bucket

chạy:

s3api list-buckets

có thể nhận:

{
    "Buckets": [
        {
            "Name": "my-first-bucket"
        }
    ]
}

Ta thấy:

api-bucket       ❌
my-first-bucket  ✅

→ api-bucket đã được xóa.
## aws s3api delete-buckets (xóa bucket khỏi S3)
## create-bucket (Tạo bucket)
Sửa lệnh

Chạy:

aws --endpoint-url=http://localhost:4566 \
    s3api create-bucket \
    --bucket api-bucket \
    --create-bucket-configuration LocationConstraint=ap-southeast-1

Nếu thành công sẽ có:

{
    "Location": "/api-bucket"
}

Sau đó:

aws --endpoint-url=http://localhost:4566 \
    s3api list-buckets

Gửi kết quả list-buckets.
## list-buckets (Liệt kê bucket)
## head-bucket (Kiểm tra bucket)
## get-bucket-location (Xem region của bucket)
## put-object (Upload object)
S3 Object bằng s3api

Tạo lại file:

echo "Hello S3 API" > api.txt

Upload bằng API:

aws --endpoint-url=http://localhost:4566 \
    s3api put-object \
    --bucket api-bucket \
    --key api.txt \
    --body api.txt

Kiểm tra object:

aws --endpoint-url=http://localhost:4566 \
    s3api list-objects-v2 \
    --bucket api-bucket
## get-object (Download object)
Đọc object bằng s3api
1. Download object về máy
aws --endpoint-url=http://localhost:4566 \
    s3api get-object \
    --bucket api-bucket \
    --key api.txt \
    downloaded.txt
2. Kiểm tra
cat downloaded.txt

Kết quả:

Hello S3 API

👉 Đây là tương đương low-level API của thao tác s3 cp mà ta đã làm trước đó.
## delete-object (Xóa object)
## list-objects-v2 (Liệt kê object)
## head-object (Xem metadata của object)
## get-bucket-policy (Lấy bucket policy)
## put-bucket-policy (Thiết lập bucket policy)
# aws sqs (Tạo một SQS queue)
**Syn**
```bash
aws [endpoint] sqs create-queue --queue-name [QUEUE_NAME]
```
**Ex: tạp một SQS queue có tên my-first-queue trên LocalStack**
```bash
aws --endpoint-url=http://localhost:4566 \
    sqs create-queue \
    --queue-name my-first-queue

Phần 1
aws

Đây là AWS CLI.

Bạn đang nói với terminal:

"Tôi muốn sử dụng AWS CLI."

Phần 2
--endpoint-url=http://localhost:4566

Đây là phần rất quan trọng khi bạn học LocalStack.

AWS thật thường sử dụng endpoint của AWS.

Ví dụ:

https://sqs.ap-southeast-1.amazonaws.com

Nhưng bạn đang dùng LocalStack nên không muốn gửi request lên AWS thật.

LocalStack chạy trên máy bạn:

http://localhost:4566

Do đó:

--endpoint-url=http://localhost:4566

có nghĩa:

"AWS CLI, đừng gọi AWS thật. Hãy gửi request tới LocalStack đang chạy ở localhost:4566."

Phần 3
sqs

Cho AWS CLI biết:

"Tôi muốn làm việc với dịch vụ SQS."

AWS CLI có rất nhiều service:

aws s3
aws sqs
aws dynamodb
aws lambda
aws ec2

Ví dụ:

aws s3 ...

→ làm việc với S3.

aws sqs ...

→ làm việc với SQS.

Phần 4
create-queue

Đây là command/action của SQS.

Nó có nghĩa:

Tạo một queue mới.

SQS có nhiều command khác nhau:

create-queue
list-queues
send-message
receive-message
delete-message
delete-queue
get-queue-url

Ví dụ:

create-queue
     ↓
Tạo queue

send-message
     ↓
Gửi message

receive-message
     ↓
Lấy message

delete-message
     ↓
Xóa message
Phần 5
--queue-name my-first-queue

Đây là parameter/option.

--queue-name

→ chỉ định tên queue.

my-first-queue

→ tên mà bạn muốn đặt cho queue.

Vì vậy:

--queue-name my-first-queue

có nghĩa:

Tạo queue với tên my-first-queue.
Kết quả giả định

Bạn chạy:

aws --endpoint-url=http://localhost:4566 \
    sqs create-queue \
    --queue-name my-first-queue

LocalStack có thể trả về:

{
    "QueueUrl": "http://localhost:4566/000000000000/my-first-queue"
}

Điều này có nghĩa là:

Queue đã được tạo thành công
          │
          ▼
my-first-queue
          │
          ▼
http://localhost:4566/000000000000/my-first-queue

QueueUrl chính là địa chỉ để AWS CLI xác định queue đó.

8. Kiểm tra queue đã tạo

Sau khi tạo, bạn có thể chạy:

aws --endpoint-url=http://localhost:4566 \
    sqs list-queues

Kết quả giả định:

{
    "QueueUrls": [
        "http://localhost:4566/000000000000/my-first-queue"
    ]
}

Có nghĩa là LocalStack hiện đang có queue:

my-first-queue
9. Sau đó gửi một message vào queue

Ví dụ:

aws --endpoint-url=http://localhost:4566 \
    sqs send-message \
    --queue-url http://localhost:4566/000000000000/my-first-queue \
    --message-body "Hello SQS"

Kết quả giả định:

{
    "MD5OfMessageBody": "f7ff9e8b7bb2e09b70935a5d785e0cc5",
    "MessageId": "abc12345-6789-..."
}

Lúc này:

my-first-queue

┌─────────────────────────┐
│                         │
│ "Hello SQS"             │
│                         │
└─────────────────────────┘
10. Lấy message ra

Bạn có thể dùng:

aws --endpoint-url=http://localhost:4566 \
    sqs receive-message \
    --queue-url http://localhost:4566/000000000000/my-first-queue

Kết quả giả định:

{
    "Messages": [
        {
            "MessageId": "abc12345-6789-...",
            "ReceiptHandle": "AQEB...",
            "MD5OfBody": "f7ff9e8b7bb2e09b70935a5d785e0cc5",
            "Body": "Hello SQS"
        }
    ]
}

Bạn thấy:

Body: "Hello SQS"

Đó chính là message mà lúc trước bạn gửi vào queue.

11. Toàn bộ quy trình

Bạn nên nhớ SQS theo chuỗi này:

1. CREATE
      │
      ▼
   Tạo Queue
      │
      ▼
2. SEND
      │
      ▼
   Gửi Message
      │
      ▼
3. RECEIVE
      │
      ▼
   Lấy Message
      │
      ▼
4. DELETE
      │
      ▼
   Xóa Message

Các lệnh tương ứng:

# 1. Tạo queue
aws --endpoint-url=http://localhost:4566 \
    sqs create-queue \
    --queue-name my-first-queue
# 2. Gửi message
aws --endpoint-url=http://localhost:4566 \
    sqs send-message \
    --queue-url http://localhost:4566/000000000000/my-first-queue \
    --message-body "Hello SQS"
# 3. Lấy message
aws --endpoint-url=http://localhost:4566 \
    sqs receive-message \
    --queue-url http://localhost:4566/000000000000/my-first-queue

Sau khi hiểu ReceiptHandle, bạn sẽ có thể:

# 4. Xóa message
aws --endpoint-url=http://localhost:4566 \
    sqs delete-message \
    --queue-url http://localhost:4566/000000000000/my-first-queue \
    --receipt-handle "..."
12. Một ví dụ thực tế rất dễ hình dung

Giả sử bạn xây dựng website bán hàng.

Khách đặt hàng:

User
 │
 │ "Tôi muốn mua iPhone"
 ▼
Backend
 │
 │ send-message
 ▼
SQS: order-queue
 │
 │
 │ "Đơn hàng #1001"
 │
 ▼
Worker
 │
 ▼
Xử lý đơn hàng
 │
 ├── Lưu Database
 ├── Trừ tồn kho
 └── Gửi email

Điểm hay là Backend và Worker không cần phải chạy cùng một lúc.

Backend chỉ cần:

Nhận đơn
  ↓
Đưa vào SQS
  ↓
Trả response cho user

Worker có thể lấy đơn từ SQS và xử lý sau.

Đây chính là lý do SQS rất phổ biến trong các hệ thống AWS.

Bạn chỉ cần nhớ 4 lệnh SQS đầu tiên
Lệnh	Ý nghĩa
create-queue	Tạo queue
send-message	Gửi message
receive-message	Nhận message
delete-message	Xóa message

Với LocalStack, gần như tất cả lệnh đều có thêm:

--endpoint-url=http://localhost:4566

Ở bước tiếp theo, hợp lý nhất là thực hành luôn send-message → receive-message → delete-message trên chính my-first-queue, vì đây là cách dễ hiểu nhất để nắm SQS.s
```
# aws dynamodb
# aws lambda
# aws ec2