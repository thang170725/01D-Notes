- [Directory Structure](#directory-structure)
- [Installation](#installation)
---
# Directory Structure
```bash
Jose/                   # mình dùng thư mục này để xem kiến thức cơ bản về Jose
├── Create.md           # mình dùng file này đê tạo, cấu hình
├── 02_jws_signing.md        # Chữ ký số (Signing): sign, verify, algorithms (HS256, RS256)
├── 03_jwe_encryption.md     # Mã hóa (Encryption): encrypt, decrypt (Dành cho dữ liệu nhạy cảm)
├── 04_jwk_keys.md           # Quản lý khóa: JWK, construct, public/private keys
└── 05_exceptions_errors.md  # Xử lý lỗi: ExpiredSignatureError, JWTError, v.v.
```
# Installation
```bash
pip install python-jose
hoặc
pip install python-jose[cryptography]
```