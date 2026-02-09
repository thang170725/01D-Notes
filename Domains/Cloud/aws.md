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
REGION & AVAILABILITY ZONE (AZ) – VÌ SAO KHÔNG ĐẶT 1 CHỖ?

Step này giúp bạn hiểu:

AWS đặt server ở đâu

Vì sao cloud ít sập hơn server thường

Vì sao VN hay chọn Singapore

1️⃣ Region là gì?

👉 Region = khu vực địa lý

Ví dụ:

Singapore

Tokyo

Seoul

Sydney

Frankfurt

US East (Virginia)

📌 Mỗi Region là một khu riêng biệt, cách xa nhau hàng trăm – hàng nghìn km.

2️⃣ Availability Zone (AZ) là gì?

👉 AZ = 1 data center (hoặc 1 cụm data center) trong cùng 1 Region

Ví dụ:

Singapore có:

ap-southeast-1a

ap-southeast-1b

ap-southeast-1c

📌 Các AZ:

Cách nhau vài km – vài chục km

Điện, mạng độc lập

Cháy 1 AZ → AZ khác vẫn sống

3️⃣ Vì sao AWS làm phức tạp vậy?

Để giải quyết nỗi đau kinh điển:

❌ Server truyền thống:

Đặt 1 chỗ

Mất điện → sập

Cháy phòng máy → bye

✅ AWS:

Chạy server ở nhiều AZ

1 AZ chết → AZ khác gánh

👉 Đây gọi là High Availability

4️⃣ Ví dụ cực dễ hiểu

Giả sử:

Bạn có 3 EC2

Đặt ở:

AZ A

AZ B

AZ C

Phía trước là Load Balancer

Kết quả:

1 AZ sập → chỉ mất 1/3 server

Người dùng không biết gì xảy ra

5️⃣ Vì sao VN hay chọn Singapore?

Rất thực tế:

Ping thấp (nhanh)

Ổn định

Rẻ hơn Tokyo

Nhiều dịch vụ hơn VN (hiện tại)

📌 VN chưa có AWS Region chính thức (hiện giờ)

6️⃣ Hiểu sai rất hay gặp ❌

❌ “Tạo 2 EC2 là đủ HA”

❌ “Cùng AZ cũng an toàn”

👉 Sai
Phải:

Nhiều EC2

Nhiều AZ

Có Load Balancer

7️⃣ Tóm tắt 3 câu

🔹 Region = khu vực
🔹 AZ = data center độc lập trong Region
🔹 Muốn không sập → chạy đa AZ
STEP 7: EC2 & SSH – KẾT NỐI VÀO SERVER LẦN ĐẦU

Mục tiêu step này:

Hiểu EC2 là gì (thực tế hơn step trước)

Hiểu SSH là gì

Biết mình đang làm gì, dù chưa tạo account

1️⃣ EC2 thực chất là gì?

👉 EC2 = 1 máy tính ảo chạy trong AWS

Nó có:

CPU

RAM

Ổ cứng

Hệ điều hành (Linux / Windows)

IP riêng / IP public

📌 Khác laptop của bạn ở chỗ:

Không có màn hình

Không có chuột

Điều khiển từ xa qua Internet

2️⃣ “Không màn hình thì dùng kiểu gì?” 🤔

👉 Dùng SSH

3️⃣ SSH là gì? (nói cực đời)

👉 SSH = mở cửa bước vào server bằng dòng lệnh

Ví dụ đời thường:

Bạn đứng trước nhà

Có chìa khóa

Mở cửa → vào nhà

Trong cloud:

Server = ngôi nhà

SSH key = chìa khóa

SSH = hành động mở cửa

📌 KHÔNG có mật khẩu như Facebook
📌 Dùng key file → bảo mật hơn

4️⃣ Khi SSH vào EC2, bạn sẽ thấy gì?

Bạn sẽ thấy màn hình kiểu:

ubuntu@ip-172-31-xx-xx:~$


👉 Nghĩa là:

Bạn đang ngồi trong server

Gõ lệnh → server chạy

Không phải máy bạn nữa

5️⃣ EC2 thường dùng để làm gì?

Chạy backend

Chạy website

Chạy API

Chạy cron job

Test hệ thống

📌 EC2 = “con trâu kéo cày” của AWS

6️⃣ Điều người mới hay sợ (nhưng không cần)

❌ “Tôi không biết Linux”
❌ “Dòng lệnh khó quá”

👉 Yên tâm:

10–15 lệnh là đủ dùng

Cloud không đòi hỏi bạn là sysadmin

7️⃣ Một hiểu nhầm rất phổ biến ❌

“Tạo EC2 là xong hệ thống”

👉 Sai.

EC2 chỉ là 1 máy
Muốn làm cloud đúng cần:

Load Balancer

Auto Scaling

RDS / DB

Security

📌 Nhưng bắt đầu phải từ EC2, không tránh được.

8️⃣ Tóm tắt step này

🔹 EC2 = máy tính ảo
🔹 SSH = cách đăng nhập vào máy
🔹 Bạn điều khiển server từ xa bằng dòng lệnh
IP PUBLIC – IP PRIVATE – SECURITY GROUP

Mục tiêu step này:

Biết server có mấy loại IP

Hiểu Security Group là gì

Hiểu vì sao EC2 không mở toang ra Internet

1️⃣ IP là gì? (1 câu)

👉 IP = địa chỉ của máy trên mạng

Giống như:

Nhà có địa chỉ

Máy trên Internet có IP

2️⃣ IP Public vs IP Private
🔹 IP Public

Địa chỉ ngoài Internet

Ai cũng có thể gửi request tới

Ví dụ:

54.xxx.xxx.xxx


👉 Website bạn truy cập = IP public

🔹 IP Private

Địa chỉ nội bộ trong AWS

Chỉ máy trong cùng mạng nhìn thấy

Ví dụ:

172.31.x.x


👉 Internet không truy cập được

3️⃣ EC2 thường có IP nào?

EC2 có cả 2

Nhưng:

App thường chạy trên private IP

Load Balancer dùng public IP

📌 EC2 không nên public trực tiếp nếu là hệ thống nghiêm túc.

4️⃣ Security Group là gì?

👉 Security Group = tường lửa (firewall)

Nó quyết định:

Ai được vào

Vào bằng cổng nào (port)

Ví dụ:

Port 22 → SSH

Port 80 → HTTP

Port 443 → HTTPS

5️⃣ Mặc định EC2 có mở không?

❌ KHÔNG

Mặc định:

Không ai vào được

Bạn phải mở cổng thủ công

Ví dụ:

Cho phép:

SSH (22) từ IP của bạn

HTTP (80) từ Internet

👉 Mở sai = toang
👉 Không mở = an toàn

6️⃣ Vì sao server không bị hack hàng loạt?

Vì:

Không mở cổng → không vào được

Mở đúng cổng → giới hạn IP

Dùng SSH key → không đoán được

📌 Hacker không “thần thánh”, họ cần cửa mở

7️⃣ Một hiểu nhầm phổ biến ❌

“Có IP public là nguy hiểm”

👉 Sai.

Nguy hiểm hay không là:

Security Group

Port mở

8️⃣ Tóm tắt cực gọn

🔹 Public IP: Internet vào được
🔹 Private IP: nội bộ
🔹 Security Group: cửa + khóa
STEP 9: DATABASE TRÊN AWS (RDS) – VÌ SAO KHÔNG CÀI DB LÊN EC2?

Mục tiêu:

Hiểu RDS là gì

Biết khi nào nên / không nên cài DB trên EC2

Hiểu cách cloud “chăm DB thay bạn”

1️⃣ RDS là gì?

👉 RDS = Database có người trông

AWS lo cho bạn:

Backup tự động

Update OS

Thay ổ cứng khi hỏng

Monitoring

Bạn chỉ:

Tạo DB

Kết nối

Viết query

📌 RDS hỗ trợ:

MySQL

PostgreSQL

MariaDB

SQL Server

Oracle

2️⃣ Cài DB lên EC2 thì sao?

👉 Được, nhưng:

❌ Bạn phải tự:

Backup

Restore

Update

Scale

Fix khi ổ cứng chết

📌 Người mới rất dễ toang ở đây.

3️⃣ Vì sao hệ thống nghiêm túc dùng RDS?
🔹 1. Không mất dữ liệu

Ổ cứng chết → AWS thay

Snapshot vẫn còn

🔹 2. High Availability

Chạy Multi-AZ

1 AZ chết → DB tự chuyển

🔹 3. Scale dễ hơn

Nâng RAM / CPU vài click

4️⃣ RDS có phải “thần thánh” không?

❌ Không.

RDS KHÔNG:

Tự sửa query chậm

Tự thiết kế schema

Tự chống logic lock

👉 RDS chỉ giúp hạ tầng ổn định

5️⃣ Vậy khi nào cài DB lên EC2?

Chỉ nên khi:

Học tập

Test

DB đặc biệt (custom)

Muốn tiết kiệm cực độ

📌 Production → RDS

6️⃣ Một hiểu nhầm lớn ❌

“EC2 mạnh thì DB cũng mạnh”

👉 Sai.

DB chết thường vì:

Lock

Query

Thiết kế

Transaction dài

Không phải vì thiếu CPU.

7️⃣ Tóm tắt 3 câu

🔹 RDS = DB được AWS quản
🔹 Production nên dùng RDS
🔹 RDS không cứu logic DB kém

❓ Check nhanh

RDS giúp bạn làm những việc gì?

Vì sao không nên cài DB lên EC2 cho hệ thống thật?

RDS có tự tối ưu query cho bạn không?

👉 Nếu hiểu rồi, nói: “Hiểu rồi”

👉 Step tiếp theo:
STEP 10 – S3 & vì sao không lưu ảnh/file trong database 📦