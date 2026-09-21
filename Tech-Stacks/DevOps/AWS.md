- [aws s3](#aws-s3)
- [aws sqs (Tạo một SQS queue)](#aws-sqs-tạo-một-sqs-queue)
- [aws dynamodb](#aws-dynamodb)
- [aws lambda](#aws-lambda)
- [aws ec2](#aws-ec2)
---
# aws s3
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