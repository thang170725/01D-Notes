- [Cấu trúc](#cấu-trúc)
---
# Cấu trúc
```bash
Jose/
├── 01_jwt_operations.md     # Thao tác JWT: encode, decode, get_unverified_claims
├── 02_jws_signing.md        # Chữ ký số (Signing): sign, verify, algorithms (HS256, RS256)
├── 03_jwe_encryption.md     # Mã hóa (Encryption): encrypt, decrypt (Dành cho dữ liệu nhạy cảm)
├── 04_jwk_keys.md           # Quản lý khóa: JWK, construct, public/private keys
└── 05_exceptions_errors.md  # Xử lý lỗi: ExpiredSignatureError, JWTError, v.v.
```
**Chi tiết**
```bash
1.  jwt_operations.md (Thao tác chính)
    + Đây là file bạn sẽ mở ra nhiều nhất khi làm Web API.
    + Hàm: jwt.encode(), jwt.decode(), jwt.get_unverified_claims().
    + Mô tả: Cách tạo ra một token từ payload và cách giải mã nó để lấy thông tin user.
    + Mẹo: Ghi chú về các tham số quan trọng như exp (expiration), sub (subject), iat (issued at).
02. jws_signing.md (Chữ ký)
Hàm: jws.sign(), jws.verify().

Mô tả: Tập trung vào các thuật toán ký. Bạn nên ghi chú sự khác biệt giữa Symmetric (HS256 - dùng 1 secret key) và Asymmetric (RS256 - dùng cặp khóa Public/Private).

03. jwe_encryption.md (Mã hóa nội dung)
Hàm: jwe.encrypt(), jwe.decrypt().

Lý do tách riêng: JWS (ở file 01, 02) chỉ giúp xác thực dữ liệu không bị sửa đổi, nhưng ai cũng đọc được nội dung. JWE giúp che giấu hoàn toàn dữ liệu. File này dùng cho các trường hợp cực kỳ bảo mật.

04. jwk_keys.md (Cấu trúc khóa)
Hàm: jwk.construct(), jwk.get_key().

Mô tả: Cách biến một chuỗi JSON thành một đối tượng "Key" để đưa vào hàm sign/verify. Thường dùng khi bạn làm việc với các hệ thống Auth bên thứ ba như Google, Firebase (họ cung cấp khóa qua URL dạng .well-known/jwks.json).

05. exceptions_errors.md (Bắt lỗi)
Các lớp lỗi: ExpiredSignatureError (hết hạn), JWTClaimsError (sai thông tin), JWTError (lỗi chung).

Mục đích: Để bạn biết cần try...except cái gì trong FastAPI nhằm trả về mã lỗi 401 (Unauthorized) chuẩn nhất.

Tại sao chia thế này lại "nét"?
Tách biệt mục đích: Bạn muốn tạo token? Mở 01. Bạn muốn xử lý khóa phức tạp? Mở 04.

Logic bảo mật: Giúp bạn phân biệt rõ giữa Sign (Ký - File 02) và Encrypt (Mã hóa - File 03). Đây là hai khái niệm người mới hay nhầm lẫn nhất.

Hỗ trợ Debug: Khi token bị hết hạn, bạn chỉ cần nhảy vào file 05 để xem tên chính xác của Exception để bắt lỗi cho đúng.
```
# Installation
```bash
pip install python-jose
hoặc
pip install python-jose[cryptography]
```