- [Cloud](#cloud)
- [IaaS \& PaaS \& SaaS](#iaas--paas--saas)
- [SERVER](#server)
- [CLOUD HOẠT ĐỘNG THẾ NÀO?](#cloud-hoạt-động-thế-nào)
- [KIẾN TRÚC ĐÚNG CHO HỆ THỐNG ĐĂNG KÝ TÍN CHỈ (TRÊN AWS)](#kiến-trúc-đúng-cho-hệ-thống-đăng-ký-tín-chỉ-trên-aws)
---
# Cloud
```bash
Cách sử dụng máy tính, lưu trữ, phần mềm… thông qua Internet, mà bạn không cần sở hữu máy thật
```
**Trước khi có cloud thì sao?**
```bash
- Giả sử bạn mở một quán cà phê và muốn:
    + Quản lý bán hàng
    + Lưu dữ liệu khách
    + Chạy website
- Cách cũ:
    + Mua máy tính mạnh
    + Đặt trong quán (hoặc phòng riêng)
    + Tự lo: điện, mạng, hỏng hóc, nâng cấp
    -> Cái máy đó gọi là server (máy chủ).
```
**Cloud xuất hiện để làm gì?**
```bash
- Cloud = thuê máy tính của người khác qua Internet
- Thay vì mua máy:
    + Bạn thuê server của Amazon / Google / Microsoft
    + Dùng qua Internet
    + Trả tiền theo giờ / theo tháng
- Ví dụ quen thuộc:
    + Gmail → chạy trên cloud của Google
    + Facebook → chạy trên cloud
    + Google Drive → cloud lưu trữ
    + Netflix → cloud để xem phim
    -> Máy tính không nằm trong nhà bạn, mà nằm ở data center (trung tâm dữ liệu) khắp thế giới.
```
# IaaS & PaaS & SaaS
**Ex: MỞ QUÁN ĂN**
```bash
- SaaS (Software as a Service)          : Bạn chỉ việc ăn
    + Ví dụ: Gmail, Google Drive, Facebook
    + Bạn chỉ dùng
    + Không quan tâm:
        + Máy chủ ở đâu
        + Cài đặt gì
        + Bảo trì ra sao
    + Cloud lo hết cho bạn
- PaaS (Platform as a Service)          : Có bếp sẵn, bạn nấu
    + Ví dụ: Heroku, Firebase
    + Có sẵn: Bếp, Gas, Nồi
    + Bạn chỉ: Viết code, Chạy app
    + Không cần quan tâm server bên dưới
- IaaS (Infrastructure as a Service)    : Thuê mặt bằng trống
    + Ví dụ: AWS EC2, Google Compute Engine
    + Bạn thuê: Máy tính (CPU, RAM, ổ cứng)
    + Bạn tự: Cài Windows / Linux, Cài phần mềm, Bảo mật, Quản lý server
```
# SERVER
```bash
- Server = một cái máy tính
- Nhưng:
    + Chạy 24/7
    + Kết nối Internet liên tục
    + Để phục vụ người khác, không phải để bạn dùng cá nhân
- Laptop của bạn cũng có thể là server, nếu:
    + Mở 24/7
    + Người khác truy cập vào nó
```
**Ex**
```bash
- Server giống như nhà hàng
- Bạn = khách
- Website = món ăn
- Server = bếp
```
**Server làm những việc gì?**
```bash
1. Lưu dữ liệu (ảnh, video, tài khoản)
2. Chạy chương trình (website, app)
3. Nhận & trả dữ liệu qua Internet
4. Server ≠ Cloud (rất nhiều người nhầm)
```
# CLOUD HOẠT ĐỘNG THẾ NÀO?
**Ex: Bạn mở trình duyệt và vào một website (ví dụ: xem tin tức)**
```bash
Bạn → Internet → Cloud → Server → Cloud → Internet → Bạn
```
**Bên trong “Cloud” có gì?**
```bash
- Cloud không phải 1 máy, mà gồm:
    + Data Center (Trung tâm dữ liệu). Một toà nhà rất lớn
    + Hàng nghìn server
    + Máy lạnh công suất cực mạnh
    + Nguồn điện dự phòng
    + Amazon / Google / Microsoft sở hữu rất nhiều data center khắp thế giới.
- Khi bạn truy cập website
    + Yêu cầu của bạn đi tới data center gần nhất
    + Một server trống nhận việc
    + Server xử lý → trả kết quả
    + Bạn không biết server nào xử lý
    + Cloud tự chọn cho bạn
```
**Điều “ảo diệu” của cloud: TỰ ĐỘNG MỞ RỘNG**
```bash
- Bình thường: 100 người dùng
- Bỗng nhiên: 100.000 người vào cùng lúc
- Không cloud:
    + Server quá tải
    + Website sập
    + Có cloud:
    + Cloud tự tạo thêm server
    + Chia tải ra nhiều máy
    + Hết đông → tắt bớt → tiết kiệm tiền
```
# KIẾN TRÚC ĐÚNG CHO HỆ THỐNG ĐĂNG KÝ TÍN CHỈ (TRÊN AWS)
```bash
🎯 Mục tiêu: 20.000 sinh viên vào cùng lúc
    - Không sập
    - Không tranh chấp dữ liệu
    - Không cần sinh viên F5 điên cuồng

1️⃣ Lớp ngoài cùng: CỔNG VÀO 🚪
    ✅ Load Balancer (ELB)
        - Nhận toàn bộ request sinh viên
        - Phân phối đều cho nhiều server phía sau
    👉 Không có cái này = 1 cửa → tắc
    
    📌 Trường bạn lag 99% là thiếu hoặc cấu hình kém cái này

2️⃣ Lớp xử lý: SERVER ỨNG DỤNG ⚙️
    ✅ NHIỀU server (EC2 / container)
        Không phải 1 server. Có thể:
            - 5 cái
            - 10 cái
            - 50 cái (khi cao điểm)

    ✅ Auto Scaling
        - Đông → tự tạo server mới
        - Vắng → tắt bớt

    ⚠️ Điều kiện:
        - App không được nhớ dữ liệu trong RAM
        - Mỗi request xử lý độc lập
    👉 Rất nhiều phần mềm trường viết sai chỗ này

3️⃣ Lớp “sống còn”: DATABASE 🧠
    💥 80% hệ thống chết ở đây

    ❌ Sai lầm phổ biến
        1 database duy nhất
            Bị:
                - Lock bảng
                - Deadlock
                - Query chậm

    ✅ Cách làm đúng
        Database riêng cho đăng ký
            Tối ưu:
                - Index
                - Transaction ngắn

            Có thể:
                - Read replica
                - Tách đọc / ghi

4️⃣ VẤN ĐỀ ĐẶC BIỆT: AI CŨNG KHÓ – TRANH CHẤP SUẤT 🥊
    100 sinh viên cùng đăng ký 1 lớp còn 1 chỗ 👉 Ai thắng?

    ❌ Cách ngu (rất hay gặp)
        - Ai gửi request trước thì thắng
        - Database lock → lag toàn hệ thống

    ✅ Cách làm đúng (cloud chuẩn)
        - Queue (hàng chờ)
        - Mỗi click đăng ký → vào hàng chờ
        - Xử lý từng cái một
        - Random / theo slot

    Ví dụ:
        - Mỗi 10 giây chọn ngẫu nhiên
        - Hoặc chia theo khoa / năm
    👉 Không công bằng tuyệt đối, nhưng không sập

5️⃣ Cache – giảm tải cực mạnh 🚀
    - Môn học, thời khóa biểu → cache
    - 90% request không cần chạm database

    📌 Trường thường bỏ qua vì: “Chạy được rồi mà”
        Đến lúc cao điểm → chết
```