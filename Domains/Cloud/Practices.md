- [Ask (Các câu hỏi về cloud)](#ask-các-câu-hỏi-về-cloud)
  - [Vấn đề các trường đại học có sử dụng cloud không?](#vấn-đề-các-trường-đại-học-có-sử-dụng-cloud-không)
  - [Giải pháp giảm tải cho db khi nhiều request?](#giải-pháp-giảm-tải-cho-db-khi-nhiều-request)
---
# Ask (Các câu hỏi về cloud)
## Vấn đề các trường đại học có sử dụng cloud không?
```bash
Vấn đề: “AWS đã auto scale rồi sao vẫn lag?”
    👉 Vì “chạy trên AWS” ≠ “dùng đúng cách AWS”
    
    Rất nhiều hệ thống nằm trên AWS nhưng vẫn lag sập.
    
    AWS không tự động làm mọi thứ, nếu không cấu hình thì nó ngu như server thường.

1️⃣ Khả năng cao trường bạn đang ở tình huống nào?
    Có server riêng / 1 server duy nhất

    Trường mua:
        - 1 server vật lý hoặc
        - 1 EC2 (AWS) cấu hình cố định
        - Không auto scale

    Đến giờ đăng ký → 10.000 sinh viên cùng click
        👉 Kết quả:
            - CPU 100%
            - RAM full
            - Website đơ toàn tập
=> Dù server đó nằm trong AWS → vẫn lag y như server tự mua

🟠 Kịch bản 2: Có AWS nhưng làm cho “có”
    Có: 1–2 EC2
        - Không Load Balancer
        - Không Auto Scaling
        - Database chung 1 chỗ

    👉 Chỗ chết thường là:
        - Database bị quá tải
        - Backend lock bảng
        - Query quá chậm

    📌 Auto scale không cứu được database kém thiết kế

🟡 Kịch bản 3: Chỉ mua domain + hosting rẻ
    - Mua tên miền (domain)
    - Dùng shared hosting / VPS rẻ tiền
    - Không cloud “xịn” gì cả

    2️⃣ Auto Scaling KHÔNG PHẢI phép màu 🧙‍♂️
```
**Vì sao “đăng ký tín chỉ” đặc biệt dễ sập?**
```bash
Vì: Tất cả sinh viên cùng truy cập 1 thời điểm
    Cùng:
        - Login
        - Query môn học
        - Ghi dữ liệu đăng ký
👉 Đây là bài toán khó nhất của hệ thống web

Netflix:
    - Nhiều người xem
    - Nhưng ít ghi dữ liệu

Đăng ký tín chỉ:
    - Rất nhiều ghi + tranh chấp dữ liệu
    - Khó hơn rất nhiều
```
**Một hệ thống đăng ký tín chỉ làm đúng cloud sẽ có**
```bash
- Load Balancer
- Auto Scaling
- Queue (xếp hàng xử lý)
- Cache
- Database scale / shard
- Thậm chí random thứ tự sinh viên

👉 Nhưng làm cái này:
    - Tốn tiền
    - Tốn công
    - Trường thường… không muốn đầu tư 😅
```
## Giải pháp giảm tải cho db khi nhiều request?
```bash
Tách db nhưng
    ❌ Tách theo “chức năng” là sai
    ✅ Tách theo “điểm nóng ghi dữ liệu”
    ✅ Không FK cross DB
    ✅ App chịu trách nhiệm ràng buộc
```
**tách theo rằng buộc mềm không có khóa ngoài**
```bash
👉 ĐÚNG, và trong hệ thống lớn người ta làm như vậy rất nhiều.
    Tên gọi chính xác:
        ❌ Không dùng foreign key (FK)
        ✅ Dùng logical reference / soft reference
        
        Ràng buộc được kiểm soát bởi application logic

2️⃣ Vì sao KHÔNG dùng khóa ngoài (FK)?
    FK nghe có vẻ “chuẩn”, nhưng trong hệ thống tải lớn:
        ❌ FK gây:
            - Lock lan rộng
            - Transaction kéo dài
            - Scale kém
            - Không shard DB được
            - Không tách DB được

    📌 FK phù hợp:
        - Hệ nhỏ
        - Ít user
        - Ít ghi

    📌 FK không phù hợp:
        - Đăng ký tín chỉ
        - Flash sale
        - Booking vé
        - Thanh toán

3️⃣ “Không FK thì dữ liệu có loạn không?” 🤔
    👉 Không, nếu thiết kế đúng.

    Thực tế: 99.9% thời gian KHÔNG có lỗi
        Lỗi chỉ xảy ra khi:
            - Mất kết nối giữa các service
            - Bug code
            - Retry không đúng
            📌 Và những lỗi này có thể xử lý nghiệp vụ, không phải lỗi hệ thống.

4️⃣ Vì sao chấp nhận “ràng buộc mềm”?
    Vì hệ thống lớn ưu tiên:
        🟢 Không sập
        🟢 Phục vụ được số đông
        🟡 Còn dữ liệu → xử lý sau

    Ví dụ:
        - Thừa 1 bản ghi đăng ký → admin xóa
        - Trùng → reconcile
        - Lệch trạng thái → batch job sửa
        👉 Còn hơn là 20.000 sinh viên không đăng ký được

5️⃣ Cách người ta GIẢM sai sót (rất quan trọng)
    Không phải “buông cho lỗi”, mà là giảm lỗi tới mức rất thấp.

    ✅ 1. Quy ước ID bất biến
        - student_id không bao giờ đổi
        - Không reuse ID

    ✅ 2. Kiểm tra ở tầng app
        - Trước khi ghi:
        - Check student tồn tại
        - Check quyền
        - Sau khi ghi:
            + Log
            + Audit

    ✅ 3. Idempotent request
        Click 10 lần → chỉ tạo 1 đăng ký

    ✅ 4. Job đối soát (reconciliation)
        - Chạy ban đêm
        - So sánh DB core ↔ DB đăng ký
        - Sửa sai

    📌 Ngân hàng làm vậy mỗi ngày.

6️⃣ Một câu nói rất “đời” trong ngành 😄
    “FK là luxury, không phải necessity.” (Khóa ngoại là đồ xa xỉ, không phải bắt buộc)
```