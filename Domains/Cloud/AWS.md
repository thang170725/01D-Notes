- [AWS (Amazon Web Services)](#aws-amazon-web-services)
  - [Region (khu vực địa lý)](#region-khu-vực-địa-lý)
  - [Availability Zone (AZ) (1 data center hoặc 1 cụm data center trong cùng 1 Region)](#availability-zone-az-1-data-center-hoặc-1-cụm-data-center-trong-cùng-1-region)
  - [EC2](#ec2)
  - [DATABASE TRÊN AWS (RDS)](#database-trên-aws-rds)
  - [MFA (Tăng thêm lớp bảo mật để bảo vệ tài khoản)](#mfa-tăng-thêm-lớp-bảo-mật-để-bảo-vệ-tài-khoản)
  - [Truy cập từ máy tính cá nhân lên AWS cloud](#truy-cập-từ-máy-tính-cá-nhân-lên-aws-cloud)
- [Command line](#command-line)
  - [aws s3 mb s3://cloudemindawsconfiguredemo](#aws-s3-mb-s3cloudemindawsconfiguredemo)
  - [aws s3 ls](#aws-s3-ls)
- [VPC (Mạng ảo cloud)](#vpc-mạng-ảo-cloud)
- [NAT Gateway (đường một chiều)](#nat-gateway-đường-một-chiều)
- [Load Balancer (Bộ cân bằng tải)](#load-balancer-bộ-cân-bằng-tải)
- [Auto Scaling Group (ASG)](#auto-scaling-group-asg)
- [Storage (Lưu trữ)](#storage-lưu-trữ)
  - [Elastic Block Store (EBS) (Giống như ổ cứng SSD gắn trong máy tính của bạn)](#elastic-block-store-ebs-giống-như-ổ-cứng-ssd-gắn-trong-máy-tính-của-bạn)
  - [Simple Storage Service (S3) (Giống như một kho lưu trữ đám mây khổng lồ )](#simple-storage-service-s3-giống-như-một-kho-lưu-trữ-đám-mây-khổng-lồ-)
  - [Log (Nhật ký hệ thống)](#log-nhật-ký-hệ-thống)
  - [Identity and Access Management (IAM) (Quyền truy cập)](#identity-and-access-management-iam-quyền-truy-cập)
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
## Region (khu vực địa lý)
```bash
Ví dụ:
    - Singapore
    - Tokyo
    - Seoul
    - Sydney
    - Frankfurt
    - US East (Virginia)
    => Mỗi Region là một khu riêng biệt, cách xa nhau hàng trăm – hàng nghìn km.
```
## Availability Zone (AZ) (1 data center hoặc 1 cụm data center trong cùng 1 Region)
```bash
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
## MFA (Tăng thêm lớp bảo mật để bảo vệ tài khoản)
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
# VPC (Mạng ảo cloud)
```bash
- VPC là lớp mạng riêng trên cloud dùng để:
    + Cô lập tài nguyên khỏi Internet.
    + Chia mạng thành các subnet.
    + Kiểm soát lưu lượng bằng firewall/routing.
    + Kết nối cloud với mạng nội bộ doanh nghiệp.
    + Xây dựng kiến trúc bảo mật và mở rộng cho ứng dụng.
- Có thể hình dung đơn giản: Cloud là một tòa nhà lớn, còn VPC là văn phòng riêng của bạn trong tòa nhà đó. Bạn tự quyết định ai được vào, các phòng ban được kết nối thế nào và dữ liệu đi theo đường nào.
- VPC (Virtual Private Cloud) là một mạng riêng ảo được tạo bên trong hạ tầng của nhà cung cấp cloud. Nó cho phép bạn xây dựng một môi trường mạng gần giống như một mạng nội bộ (on-premise) nhưng chạy trên cloud.
- Các nhà cung cấp lớn đều có dịch vụ này, ví dụ:
    + Amazon Web Services → VPC
    + Google Cloud → VPC Network
    + Microsoft Azure → Virtual Network (VNet)
- VPC dùng để làm gì?
    1. Cô lập hệ thống khỏi Internet công cộng
        - Bạn có thể tạo các máy chủ (VM, container, database) chỉ giao tiếp trong mạng nội bộ.
        - Ví dụ:
            + Web Server: có IP public
            + Database Server: không có IP public
            + Chỉ Web Server mới truy cập được Database
                Internet
                    |
                Web Server (Public Subnet)
                    |
                Database (Private Subnet)

                Điều này giúp tăng bảo mật đáng kể. 
    2. Chia mạng thành nhiều subnet
        - Trong VPC bạn có thể tạo:
            + Public Subnet
            + Private Subnet
            + Subnet cho Database
            + Subnet cho Backend Service
        - Ví dụ: VPC 10.0.0.0/16
            ├── Public Subnet
            │   └── Web Server
            │
            ├── App Subnet
            │   └── API Server
            │
            └── DB Subnet
                └── MySQL/PostgreSQL
        - Giúp quản lý và kiểm soát truy cập dễ dàng.
    3. Kiểm soát traffic bằng firewall
        - Bạn có thể định nghĩa:
            + Ai được truy cập vào server
            + Cổng nào được mở
            + Server nào được nói chuyện với server nào
        - Ví dụ:
            Allow:
            Internet -> Web : 80,443

            Allow:
            Web -> App : 8080

            Allow:
            App -> DB : 3306

            Deny:
            Internet -> DB
    4. Kết nối cloud với mạng công ty
        - VPC có thể kết nối với datacenter hoặc văn phòng thông qua:
            + VPN Site-to-Site
            + Dedicated Connection (Direct Connect, ExpressRoute...)
        - Kết quả:
            Office Network
                  |
                 VPN
                  |
                 VPC
                  |
            Cloud Resources
        - Người dùng có cảm giác như tài nguyên cloud đang nằm trong mạng nội bộ công ty.
    5. Kết nối nhiều hệ thống với nhau
        - Bạn có thể kết nối:
            + Nhiều VPC
            + Nhiều region
            + Nhiều tài khoản cloud
        - Ví dụ một công ty có:
            + Production VPC
            + Development VPC
            + Testing VPC
            + và vẫn cho phép chúng giao tiếp theo các quy tắc nhất định.
```
**Ex: Ví dụ thực tế**
```bash
Một ứng dụng thương mại điện tử có thể được triển khai như sau:

VPC
│
├── Public Subnet
│   ├── Load Balancer
│   └── Bastion Host
│
├── Private Subnet
│   ├── Backend Service
│   └── Redis
│
└── Database Subnet
    └── PostgreSQL
Người dùng chỉ thấy Load Balancer.
Backend không truy cập trực tiếp từ Internet.
Database hoàn toàn nằm trong mạng riêng.
```
# NAT Gateway (đường một chiều)
```bash
NAT Gateway (Network Address Translation) dùng để giải quyết bài toán "đường một chiều" này (trong đi ra được, ngoài không đi vào được).

Hãy tưởng tượng NAT Gateway giống như một ông bảo vệ đứng ở cửa chung cư:
    - Khi máy chủ Database từ vùng Private muốn ra ngoài internet tải bản vá, nó sẽ gửi gói tin đến ông bảo vệ NAT Gateway.
    - Ông bảo vệ sẽ ghi nhận: "À, máy Database nhờ mình ra ngoài internet lấy gói cập nhật hộ". Sau đó, ông bảo vệ dùng danh nghĩa của chính mình để đi ra internet lấy dữ liệu về, rồi đưa lại cho máy Database.
    - Ngược lại, nếu một hacker từ internet muốn tấn công vào máy Database, họ chỉ nhìn thấy ông bảo vệ (NAT Gateway) chứ không hề biết máy Database nằm ở đâu để mò vào. Ông bảo vệ cũng sẽ từ chối thẳng thừng mọi yêu cầu kết nối tự phát từ bên ngoài.

Lưu ý kiến trúc: NAT Gateway bắt buộc phải được đặt ở Public Subnet (vì nó cần tiếp xúc với internet) thì mới làm trung gian cho các máy ở Private Subnet đi ra ngoài được.
```
# Load Balancer (Bộ cân bằng tải)
```bash
Hãy tưởng tượng Load Balancer giống như một anh lễ tân điều phối khách hàng tại một ngân hàng lớn:
    - Khi người dùng gõ myshop.com, tất cả các yêu cầu truy cập đều phải đi qua "anh lễ tân" Load Balancer này trước tiên.
    - Anh lễ tân sẽ đứng ở ngoài cùng, chia đều khách hàng ra: Khách số 1 vào quầy số 1 (Máy chủ Web 1 ở AZ-A), khách số 2 vào quầy số 2 (Máy chủ Web 2 ở AZ-B). Việc này giúp không máy chủ nào bị quá tải.

Cơ chế tự động xử lý sự cố (Health Check)
    - Điểm "vi diệu" của Load Balancer để giúp bạn không phải thức dậy lúc nửa đêm chính là tính năng Health Check (Kiểm tra sức khỏe).
    - Cứ mỗi 5-10 giây, Load Balancer sẽ tự động gửi một tín hiệu nhỏ (như một tiếng "Alo, bạn còn sống không?") đến cả 2 máy chủ Web.
    - Nếu Máy chủ Web 1 bị sập và không phản hồi, Load Balancer sẽ ngay lập tức đánh dấu: "Máy chủ 1 đã ngỏm".
    - Ngay sau đó, nếu có khách hàng mới truy cập vào website, Load Balancer sẽ tự động gạt máy chủ 1 ra và chuyển hướng 100% khách hàng sang Máy chủ Web 2 vẫn đang khỏe mạnh ở AZ-B. Người dùng bên ngoài sẽ không hề nhận ra hệ thống vừa có sự cố.
```
# Auto Scaling Group (ASG)
```bash
Nó hoạt động dựa trên cơ chế thiết lập hạn mức và theo dõi các chỉ số sức khỏe của máy chủ.

Hãy tưởng tượng bạn cài đặt một hệ thống cảnh báo tự động như sau:
    1. Hệ thống dựa vào "chỉ số" nào để quyết định?
        - Giống như cơ thể người khi chạy mệt thì tim đập nhanh và thở dốc, máy chủ khi chịu tải lớn sẽ lộ ra qua các chỉ số phần cứng. AWS sẽ theo dõi 2 chỉ số phổ biến nhất:
            + CPU Utilization (Tỷ lệ sử dụng chip xử lý): Ngày thường máy chỉ dùng 10-20% CPU. Khi khách vào đông, CPU sẽ tăng lên 80-90%.
            + Memory Utilization (Tỷ lệ sử dụng RAM): Khi lượng dữ liệu cần xử lý cùng một lúc quá lớn, RAM sẽ bị đầy.
    2. Quy trình "Co" và "Giãn" tự động (Scale-out & Scale-in)
        - Bạn (Cloud Engineer) sẽ vào hệ thống và thiết lập một bộ quy tắc (Policy) như sau:
            + Quy tắc Giãn (Scale-out - Tự động tăng): "Nếu trung bình CPU của các máy chủ Web vượt quá 70% và kéo dài trong 3 phút => Hãy lập tức khởi tạo (đẻ) thêm 1 máy chủ mới và gắn nó vào sau Load Balancer để chia lửa."
            + Vào đêm Black Friday, khi 100.000 khách ùa vào, CPU vọt lên 90%, hệ thống tự động đẻ thêm máy thứ 3, thứ 4, thứ 5... cho đến khi CPU hạ xuống dưới mức 70% thì dừng lại. Website của bạn vẫn chạy mượt mà.
            + Quy tắc Co (Scale-in - Tự động giảm): "Nếu qua giờ cao điểm, CPU trung bình giảm xuống dưới 30% và kéo dài trong 10 phút => Hãy tự động xóa (khai tử) bớt các máy chủ thừa đi.
            + Đến 3h sáng, khách đi ngủ hết, CPU giảm sâu. Hệ thống sẽ tự động xóa các máy chủ vừa đẻ thêm, chỉ giữ lại 2 máy chủ gốc ban đầu. Nhờ vậy, công ty của bạn chỉ phải trả tiền cho những máy chủ chạy trong vài tiếng cao điểm, chứ không phải trả tiền cho cả tháng.
```
# Storage (Lưu trữ)
## Elastic Block Store (EBS) (Giống như ổ cứng SSD gắn trong máy tính của bạn)
```bash
Dùng để lưu trữ dữ liệu. Nó chạy rất nhanh nhưng chỉ gắn được vào một máy chủ duy nhất tại một thời điểm. Nếu máy chủ đó bị xóa, dữ liệu trên ổ cứng này cũng có rủi ro bị mất nếu không cấu hình lưu lại.
```
## Simple Storage Service (S3) (Giống như một kho lưu trữ đám mây khổng lồ )
```bash
Nó như Google Drive nhưng quy mô lớn hơn. Nó có thể chứa dung lượng vô hạn, không gắn vào máy chủ nào cả, và có thể truy cập từ bất kỳ đâu qua internet nếu được cấp quyền.
```
## Log (Nhật ký hệ thống)
```bash
Hãy tưởng tượng Log giống như hộp đen của máy bay. Mỗi khi máy chủ hoặc ứng dụng thực hiện một hành động (nhập hàng, xuất hàng, hoặc gặp lỗi), nó đều ghi lại một dòng nhật ký.
    - Để điều tra trận chiến giữa Khả năng A và Khả năng B, bạn sẽ vào AWS CloudWatch Logs để kiểm tra:
        + Nếu bạn thấy dòng chữ kiểu như: Exception in thread "main" java.lang.NullPointerException hoặc SyntaxError: unexpected token => Bạn kết luận ngay: Lỗi Khả năng A (Lỗi code). Bạn sẽ chụp ảnh màn hình dòng này gửi cho đội Developer và bảo: "Code các ông bị lỗi cú pháp/logic rồi, sửa đi nhé!"
        + Nếu bạn thấy dòng chữ kiểu như: AccessDenied: User ... is not authorized to perform: s3:PutObject => Bạn kết luận ngay: Lỗi Khả năng B (Lỗi quyền truy cập). Lúc này lỗi thuộc về bạn (Cloud Engineer), bạn phải vào dịch vụ quản lý tài khoản của AWS (gọi là IAM) để cấp thêm quyền cho máy chủ được phép tải file lên S3.
```
## Identity and Access Management (IAM) (Quyền truy cập)
**Sự khác biệt của IAM User và IAM Role**
```bash
Rủi ro chết người của Cách 1 (Dùng IAM User):
Khi bạn dùng IAM User, AWS sẽ cấp cho bạn một cặp mã gọi là Access Key ID và Secret Access Key (nó tương đương với Username/Password nhưng dành cho code đọc). Để Máy chủ Web có thể gửi ảnh lên S3, lập trình viên buộc phải lưu cặp mã này vào một file cấu hình nằm trên ổ cứng (EBS) của máy chủ, hoặc nhét thẳng vào trong mã nguồn.

Kịch bản bị hack: Nếu hacker tấn công vào Máy chủ Web và chiếm được quyền điều khiển, việc đầu tiên chúng làm là lục lọi các file cấu hình. Chúng sẽ lấy cắp được cặp Access Key này.

Hậu quả: Vì Access Key này có giá trị vĩnh viễn (trừ khi bạn chủ động xóa), hacker có thể mang cặp mã này về máy tính cá nhân của chúng ở Nga, Mỹ... và dùng nó để xóa sạch dữ liệu S3 của công ty bạn từ xa mà bạn không hề hay biết.

Sự an toàn tuyệt đối của Cách 2 (Dùng IAM Role):
Khi bạn gán một IAM Role cho Máy chủ Web, bạn hoàn toàn không phải lưu bất kỳ mật khẩu hay Access Key nào trên máy chủ cả.

Cơ chế hoạt động: AWS có một dịch vụ ngầm tự động phát cho máy chủ một "tấm thẻ quyền hạn tạm thời" (Temporary Credentials). Tấm thẻ này chỉ có hiệu lực trong vòng 1 đến vài tiếng rồi tự động hủy và đổi thẻ mới.

Kịch bản bị hack: Nếu hacker chiếm được Máy chủ Web, chúng cũng không tìm thấy bất kỳ mật khẩu vĩnh viễn nào lưu trên ổ cứng. Chúng chỉ có thể dùng quyền hạn đó ngay tại bên trong con máy chủ đó để ghi file lên S3.

Cách xử lý sự cố: Bạn (Cloud Engineer) chỉ cần lên bảng điều khiển AWS, nhấn nút Gỡ Role ra khỏi máy chủ (hoặc xóa máy chủ đó đi). Lập tức mọi quyền hạn của hacker bị cắt đứt hoàn toàn chỉ trong 1 giây. Khóa Access Key tạm thời cũ cũng tự động vô hiệu hóa.

Tư duy Cloud cốt lõi: "Con người thì dễ làm lộ mật khẩu (quên đổi, đặt mật khẩu yếu, bị lừa đảo), còn Máy móc (Role) thì tuân thủ tuyệt đối quy trình cấp khóa tạm thời và không bao giờ biết mệt mỏi."
```