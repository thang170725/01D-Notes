1. Cookie là gì? 🍪
Hiểu đơn giản:

Cookie = tờ giấy ghi chú mà website gửi cho trình duyệt giữ hộ

Website dùng cookie để nhớ bạn là ai, bạn đã làm gì trước đó.

Ví dụ đời thường (quán cà phê)

Bạn vào quán cà phê ☕

Lần đầu: nhân viên hỏi tên → ghi vào phiếu

Lần sau bạn quay lại, đưa phiếu → họ biết bạn là khách quen

📌 Tờ phiếu = cookie

Ví dụ trên website

Bạn đăng nhập Facebook

Bạn đóng trình duyệt

Mở lại vẫn đăng nhập

👉 Vì:

Facebook đã lưu cookie đăng nhập trong trình duyệt

Cookie dùng để làm gì?
Dùng cho	Ví dụ
Nhớ đăng nhập	Facebook, Gmail
Nhớ giỏ hàng	Shopee, Lazada
Nhớ ngôn ngữ	Tiếng Việt / English
Tracking	Quảng cáo bạn từng xem
Cookie trông như thế nào (không cần nhớ kỹ)
user_id=12345
session_token=abcxyz

2. Session là gì? (không phải section) 🧠

⚠️ Bạn đang hỏi session, không phải section
(Section = mục, chương → khác hoàn toàn)

Session là gì?
Hiểu đơn giản:

Session = hồ sơ tạm thời của bạn trên server

Cookie: nằm ở trình duyệt

Session: nằm ở server

Ví dụ đời thường (quán cà phê tiếp)

Bạn vào quán

Nhân viên tạo 1 hồ sơ cho bạn:

Khách A

Gọi cà phê sữa

Đang ngồi bàn số 3

📌 Hồ sơ đó = session

Nhân viên đưa bạn 1 thẻ số
📌 Thẻ số = session_id (được lưu trong cookie)

Khi bạn gọi thêm nước?

Bạn đưa thẻ số

Nhân viên nhìn hồ sơ → biết bạn là ai

➡️ Cookie chỉ chứa mã
➡️ Session chứa thông tin thật

3. Cookie & Session hoạt động cùng nhau thế nào?
Trình duyệt ----(cookie: session_id)---> Server
Server ----(dựa vào session_id tìm session)---> Biết bạn là ai

Ví dụ web thực tế

Bạn login

Server tạo session:

user = thang
role = admin


Server gửi cookie:

session_id = xyz123


Mỗi request sau:

Trình duyệt gửi cookie

Server tìm session → OK

4. So sánh dễ nhớ
Tiêu chí	Cookie	Session
Lưu ở đâu	Trình duyệt	Server
Ai tạo	Server	Server
Dung lượng	Nhỏ	Lớn
Bảo mật	Thấp hơn	Cao hơn
Mất khi	Xóa cookie	Server restart / timeout
5. Ví dụ cực dễ nhớ
❌ Không có cookie

Mỗi lần refresh → web hỏi: “Bạn là ai?”

❌ Có cookie nhưng không có session

Có thẻ số nhưng không có hồ sơ

✅ Có cả 2

Web chạy mượt

Nhớ trạng thái người dùng

6. Liên hệ với Playwright (cho bạn dễ hình dung)

Context ≈ trình duyệt ẩn danh

Cookie ≈ thông tin đăng nhập

Session ≈ trạng thái user trên server

context = await browser.new_context()
# context mới → cookie trống → chưa login

Tóm lại 1 câu cho dễ nhớ

🍪 Cookie = thẻ gửi xe
🧠 Session = hồ sơ trong bãi x