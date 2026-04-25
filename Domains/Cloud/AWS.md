- [AWS (Amazon Web Services)](#aws-amazon-web-services)
  - [Region](#region)
  - [Availability Zone (AZ)](#availability-zone-az)
  - [EC2](#ec2)
  - [DATABASE TRÊN AWS (RDS)](#database-trên-aws-rds)
  - [IAM](#iam)
  - [MFA](#mfa)
  - [Truy cập từ máy tính cá nhân lên AWS cloud](#truy-cập-từ-máy-tính-cá-nhân-lên-aws-cloud)
- [Command line](#command-line)
  - [aws s3 mb s3://cloudemindawsconfiguredemo](#aws-s3-mb-s3cloudemindawsconfiguredemo)
  - [aws s3 ls](#aws-s3-ls)
---
# AWS (Amazon Web Services)
```bash
- Một “siêu chợ cloud”
- Bạn cần gì về máy tính → AWS có
- AWS không phải:
    + 1 server
    + 1 phần mềm
    + AWS là rất nhiều dịch vụ cloud ghép lại.
- AWS giống như:
    + Thuê: Nhà (EC2), Kho (S3), Tủ hồ sơ (RDS), Lễ tân (ELB)
    + Bạn muốn thuê cái nào → chọn cái đó.
```
**4 dịch vụ AWS cốt lõi**
```bash
1. EC2 – Máy tính ảo
    + Thuê 1 máy tính qua Internet
    + Cài Linux / Windows
    + Chạy web, app
2. RDS – Database
    + Database có người trông
    + AWS lo: Backup, Update, Hỏng ổ cứng. RDS = DB nhưng đỡ cực
3. S3 – Ổ cứng trên cloud
    + Lưu: Ảnh, File, Video, Rẻ, Bền
    + S3 ≠ server
    + S3 ≠ database
4. ELB – Cửa phân luồng
    + Nhận request
    + Chia cho nhiều EC2
    + Không có ELB → scale rất khó
```
**Điều QUAN TRỌNG nhất cần nhớ**
```bash
- AWS KHÔNG tự động scale nếu bạn không cấu hình
- AWS cho bạn:
    + Gạch
    + Xi măng
    + Thép
- Nhà có chắc hay không là do bạn xây
```
## Region
```bash
- Region = khu vực địa lý
- Ví dụ:
    + Singapore
    + Tokyo
    + Seoul
    + Sydney
    + Frankfurt
    + US East (Virginia)
    => Mỗi Region là một khu riêng biệt, cách xa nhau hàng trăm – hàng nghìn km.
```
## Availability Zone (AZ)
```bash
- AZ = 1 data center (hoặc 1 cụm data center) trong cùng 1 Region
- Ví dụ: Singapore có:
    + ap-southeast-1a
    + ap-southeast-1b
    + ap-southeast-1c
- Các AZ:
    + Cách nhau vài km – vài chục km
    + Điện, mạng độc lập
    + Cháy 1 AZ → AZ khác vẫn sống
```
**Vì sao AWS làm phức tạp vậy?**
```bash
- Để giải quyết nỗi đau kinh điển:
    + Server truyền thống:
        - Đặt 1 chỗ
        - Mất điện → sập
        - Cháy phòng máy → bye
    + AWS:
        - Chạy server ở nhiều AZ
        - 1 AZ chết → AZ khác gánh
        - Đây gọi là High Availability
- Ví dụ cực dễ hiểu:
    + Bạn có 3 EC2 Đặt ở:
        - AZ A
        - AZ B
        - AZ C
    + Phía trước là Load Balancer. Kết quả: 1 AZ sập → chỉ mất 1/3 server. Người dùng không biết gì xảy ra
```
**Vì sao VN hay chọn Singapore?**
```bash
- Rất thực tế:
    + Ping thấp (nhanh)
    + Ổn định
    + Rẻ hơn Tokyo
    + Nhiều dịch vụ hơn VN (hiện tại)
```
## EC2
```bash
- EC2 = 1 máy tính ảo chạy trong AWS
- Nó có:
    + CPU
    + RAM
    + Ổ cứng
    + Hệ điều hành (Linux / Windows)
    + IP riêng / IP public
- Khác laptop của bạn ở chỗ:
    + Không có màn hình
    + Không có chuột
    + Điều khiển từ xa qua Internet
```
**Không màn hình thì dùng kiểu gì**
```bash
- Dùng SSH. SSH = mở cửa bước vào server bằng dòng lệnh
- Ví dụ đời thường:
    + Bạn đứng trước nhà
    + Có chìa khóa
    + Mở cửa → vào nhà
- Trong cloud:
    + Server = ngôi nhà
    + SSH key = chìa khóa
    + SSH = hành động mở cửa
- KHÔNG có mật khẩu như Facebook. Dùng key file → bảo mật hơn
- Khi SSH vào EC2. Bạn sẽ thấy màn hình kiểu: ubuntu@ip-172-31-xx-xx:~$
    + Nghĩa là: Bạn đang ngồi trong server
    + Gõ lệnh → server chạy
    + Không phải máy bạn nữa
- EC2 thường dùng để làm gì?
    + Chạy backend
    + Chạy website
    + Chạy API
    + Chạy cron job
    + Test hệ thống
```
**Điều người mới hay sợ (nhưng không cần)**
```bash
- “Tôi không biết Linux”
- “Dòng lệnh khó quá”
- Yên tâm:
    + 10–15 lệnh là đủ dùng
    + Cloud không đòi hỏi bạn là sysadmin
```
**Một hiểu nhầm rất phổ biến**
```bash
- “Tạo EC2 là xong hệ thống” -> Sai.
- EC2 chỉ là 1 máy. Muốn làm cloud đúng cần:
    + Load Balancer
    + Auto Scaling
    + RDS / DB
    + Security
```
## DATABASE TRÊN AWS (RDS)
```bash
- RDS = Database có người trông
- AWS lo cho bạn:
    + Backup tự động
    + Update OS
    + Thay ổ cứng khi hỏng
    + Monitoring
- Bạn chỉ:
    + Tạo DB
    + Kết nối
    + Viết query
- RDS hỗ trợ:
    + MySQL
    + PostgreSQL
    + MariaDB
    + SQL Server
    + Oracle
```
**Cài DB lên EC2 thì sao?**
```bash
- Được, nhưng bạn phải tự:
    + Backup
    + Restore
    + Update
    + Scale
    + Fix khi ổ cứng chết
- Hệ thống nghiêm túc dùng RDS?
    + Không mất dữ liệu
    + Ổ cứng chết → AWS thay
    + Snapshot vẫn còn
    + High Availability Chạy Multi-AZ. 1 AZ chết → DB tự chuyển
    + Scale dễ hơn
    + Nâng RAM / CPU vài click
```
## IAM
```bash
- Thường để tạo alias (định danh duy nhất). Chuyên quản lý về đăng nhập, quản lý tài khoản
```
## MFA
```bash
- Tăng thêm lớp bảo mật để bảo vệ tài khoản
```
## Truy cập từ máy tính cá nhân lên AWS cloud
```bash
1. Tạo access key
2. Cài đặt aws cli
3. run terminal: aws configure
```
# Command line
## aws s3 mb s3://cloudemindawsconfiguredemo
## aws s3 ls
```bash
Xem các package trong s3
```